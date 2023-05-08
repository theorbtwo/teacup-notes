References
---

ingenic sdk: [https://github.com/HackerHomestead/Ingenic-SDK-T31-1.1.1-20200508].  Will also be referenced as `file:///S:/projects/teacup/Ingenic-SDK-T31-1.1.1-20200508/` when I am being lazy.

`lib{alog,audioProcess,imp,sysutils}.{so,a}`: ingenic sdk/lib-5.4.0/glibc
ingenic

`tx-isp-t31.ko`: ingenic sdk/opensource/drivers/tx-isp-t31/tx-isp-t31.ko

libsysutils.so
----

  crux161 — Yesterday at 8:19 PM
  So far I think you’re the only one offering us any hope on this front. It’s good to hear something on this
  My only hope is that we can understand enough to get basic functions like a graceful shutdown that works as intended.

`SU_Base_Shutdown`:

Equivelent to `sync; kill -17 1` in shell terms.



tx-isp-t31.ko, tiziano_load_parameters()
---

This is where `/etc/sensor/%s-t31.bin` gets loaded.  The path is compiled in to the kernel.  Format as a [https://ide.kaitai.io/] file:

```
meta:
  id: t31_bin
  file-extension: bin
  encoding: ascii
  endian: le
seq:
  - id: version_str
    size: 8
    type: strz
    # must be "2.10.0"
  - id: header_str
    size: 8
    type: strz
    # must be "header0"
  - id: payload_size
    type: u4
  - id: crc
    type: u4
  - id: tparams_day
    type: tparams
  - id: tparams_night
    type: tparams
types:
  tparams:
    seq:
      - id: blob
        size: 0x137f0
```





libimp gISPdev, ISPdev:

* allocated in IMP_ISP_Open
* is 0xb8 bytes long (IMP_ISP_Open)
* 0x00, char[0x12] path, which is "/dev/tx-isp" (hardcoded). (IMP_ISP_Open)
* 0x20, int filehandle (IMP_ISP_Open)
* 0xac, void* NCUAlloc (IMP_ISP_Tuning_GetNCUAlloc)
* associated: 
* * custom_{sharpness,contrast}
* * isp_video_drop_func
* * static_gain.9001


...

IOCTLs
------

| ioctl num | users |
| -         | - |
| `0xc008710a` | libimp `LinuxIpCtrl_WriteRegister` |
| `0xc008710b` | libimp `LinuxIpCtrl_ReadRegister`  |
| `0x20007101` | libimp `LinuxIpCtrl_Destroy` |
| `0x4004505a` | libimp `__ao_dev_set_gain` |
| `0xc008561b` | libimp `IMP_ISP_Tuning_GetISPHflip` |
|   | |

