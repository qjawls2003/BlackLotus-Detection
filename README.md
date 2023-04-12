# CVE-2022-21894
Public repo for anything CVE-2022-21894

# Main page
https://www.microsoft.com/en-us/security/blog/2023/04/11/guidance-for-investigating-attacks-using-cve-2022-21894-the-blacklotus-campaign/

## Basic Detection
  > mountvol /s
Mounts the EFI system partition on the specified drive.

  > dir E:\EFI\Microsoft\Boot\*efi
Search for .efi files that have odd timestamps

  > Get-FileHash -Algorithm MD5 -Path (Get-ChildItem "E:\EFI\Microsoft\Boot\*.*" -Recurse)
Get the FileHash of all the bootloader files to see if any generate ERROR_SHARING_VIOLATION

  



## Sysmon
https://github.com/olafhartong/sysmon-modular

## Vulnerability

### Method
https://github.com/Wack0/CVE-2022-21894

1. Local Access required
2. Privileged user required
