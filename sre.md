References
---

ingenic sdk: [https://github.com/HackerHomestead/Ingenic-SDK-T31-1.1.1-20200508].  Will also be referenced as `file:///S:/projects/teacup/Ingenic-SDK-T31-1.1.1-20200508/` when I am being lazy.

`lib{alog,audioProcess,imp,sysutils}.{so,a}`: ingenic sdk/lib-5.4.0/glibc
ingenic

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
