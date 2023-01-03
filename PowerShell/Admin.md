```PowerShell
# Shorthand commands
Get-ChildItem | ? {} # Where {}
Get-ChildItem | % {} # ForEach {}

# find command
Get-Command -Name '*name*'

# Find which process has a lock on a directory or file
Get-WmiObject Win32_Process | ? {$_.commandLine -like "*file_dir_name*"}

# If folder not exists create it
if (-Not (Test-Path $dir_path)) { md $dir_path }

# Unzip a compressed file
Expand-Archive $in_file -DestinationPath $out_dir

# Get timezone code from its id
$tz_code = ((Get-TimeZone).id.split(' ') | % { $_[0] }) -join ''

# 

```