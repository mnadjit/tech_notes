# Windows Boot Manager
```Windows
bcdedit /enum    # Get Windows Boot Manager and Boot Loader
bcdedit /enum {bootmgr}   # Get Windows Boot Manager only
bcdedit /enum {current}   # Get Windows Boot Loader only

bcdedit /set hypervisorlaunchtype auto    # enable virtualisation
bcdedit /set hypervisorlaunchtype off     # disable virtualisation

bcdedit /copy {current} /d "Windows 11 New Boot Loader"   # copy current bootloader to a new entry; /d means description
```
