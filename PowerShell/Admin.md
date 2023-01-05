```PowerShell
# Shorthand commands
Get-ChildItem | ? {} # Where {}
Get-ChildItem | % {} # ForEach {}
```

```PowerShell
# find command
Get-Command -Name '*name*'
```

```PowerShell
# Find which process has a lock on a directory or file
Get-WmiObject Win32_Process | ? {$_.commandLine -like "*file_dir_name*"}
```

```PowerShell
Get-Process | %  { $pr_var = $_; $_.Modules | % { if ($_.filename -like '*file_dir_name*') { "$($pr_var.Name)`tPID: $($pr_var.Id)" } } }
```

```PowerShell
# If folder not exists, create it
if (-Not (Test-Path $dir_path)) { md $dir_path }
```

```PowerShell
# Environment Variable
[Environment]::GetEnvironmentVariable($var_name, $scope)
[Environment]::SetEnvironmentVariable($var_name, $value, $scope)
```

```PowerShell
# Add to PATH Environment Variable
function Add-Path($Path, $Scope) {
    $Path = [Environment]::GetEnvironmentVariable("PATH", $Scope) + [IO.Path]::PathSeparator + $Path
    [Environment]::SetEnvironmentVariable( "PATH", $Path, $Scope )
}
```

```PowerShell
# Unzip a compressed file
Expand-Archive $in_file -DestinationPath $out_dir
```

```PowerShell
# Get timezone code from its id
$tz_code = ((Get-TimeZone).id.split(' ') | % { $_[0] }) -join ''
```

```PowerShell
# Install Winget
Add-AppxPackage ./Microsoft.DesktopAppInstaller_8wekyb3d8bbwe.msixbundle
```

```PowerShell

```

