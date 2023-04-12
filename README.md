# CVE-2022-21894
Public repo for anything CVE-2022-21894

# Main page
https://www.microsoft.com/en-us/security/blog/2023/04/11/guidance-for-investigating-attacks-using-cve-2022-21894-the-blacklotus-campaign/
### Windows Defender now capable of removing this threat "Possible vulnerable EFI bootloader "

## Basic Detection
### Mounts the EFI system partition on the specified drive.
  $ mountvol /s

### Search for .efi files that have odd timestamps

  $ dir E:\EFI\Microsoft\Boot\*efi

### Get the FileHash of all the bootloader files to see if any generate ERROR_SHARING_VIOLATION
  $ Get-FileHash -Algorithm MD5 -Path (Get-ChildItem "E:\EFI\Microsoft\Boot\*.*" -Recurse)

### Staging directory presence
  Check historical presence of deleted files in a custom directory such as ESP:\system32\
  The directory is not deleted after BalckLotus installation.

### Check for HVCI integrity (if it exists)
  $ reg query HKLM\SYSTEM\CurrentControlSet\Control\DeviceGuard\Scenarios\HypervisorEnforcedCodeIntegrity

### Check for specific Windows Defender Events (tampering with Defender)
  $ Get-EventLog -LogName System -InstanceId 3006
  $ Get-EventLog -LogName System -InstanceId 7023

### Check for connection to C2 serve via winlogon.exe port 80
  $ netstat -ano | findstr ":80"
  $ tasklist /V | findstr "winlogon.exe"
#### Use sysmon and add new configuration to the sysmonconfig.xml
  <Image condition="image">winlogon.exe</Image>



## Sysmon
https://github.com/olafhartong/sysmon-modular

## Vulnerability

### Method
https://github.com/Wack0/CVE-2022-21894


