# Encrypt text using self-signed certificate
## Creating the certificate
### Pick a domain name which can be anything and also a friendly name
- $domainName = "me@domain"
- $friendlyName = "Give it a name"
### Create the certificate
- `$cert = New-SelfSignedCertificate -NotAfter (Get-Date).AddYears(2) -DnsName $domainName -CertStoreLocation Cert:\CurrentUser\My -KeyUsage KeyAgreement,KeyEncipherment,DataEncipherment -Type DocumentEncryptionCert -FriendlyName $friendlyName`
### Create a backup
- `$certThumprint=(Get-ChildItem -Path Cert:\CurrentUser\My\ | Where { $_.FriendlyName -eq $friendlyName }).Thumbprint`
- With Password
  - `Export-PfxCertificate -Cert Cert:\CurrentUser\My\$certThumprint -FilePath $env:USERPROFILE\Certificates\MyDocEncCert.pfx -Password (ConvertTo-SecureString -AsPlainText 'password123!' -Force)`
- Without Password
  - `Export-Certificate -Cert $cert -FilePath $env:USERPROFILE\certificates\mycertFilename.cer -Type CERT`

## Encrypt some text using the certificate
- `$outFile=$env:USERPROFILE\encryptedFile.txt`
- `"text to be encrypted" | Protect-CmsMessage -To cn=$domainName | Out-File $outFile`
- `"text to be encrypted" | Protect-CmsMessage -To $cert`
- `"text to be encrypted" | Protect-CmsMessage -To (Get-Item Cert:\CurrentUser\My\$($cert.Thumbprint))`
## Decrypt using the certificate (no need to specify the certificate)
- `Unprotect-CmsMessage -Path $EncryptedFilePath`

# Code Signing
## Create a new personal certificate
- `$certificateName = Read-Host -Prompt 'Enter name of your certificate e.g. MyCert or me@domain.com'`
- `$cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation Cert:\CurrentUser\My\ -Type Codesigning -NotAfter (Get-Date).AddYears(3)`

## Alternatively, get an already-created personal certificate
- `$certThumprint = Read-Host -Prompt 'Enter thumbprint of your certificate'`
- `$cert = Get-ChildItem -Path Cert:\CurrentUser\My\ | Where { $_.Thumbprint -eq $certThumprint }`

## Import the created certificate into *Trusted Publishers* and *Trusted Root Certification Authorities*
**This can be done manually using `certmgr.msc` or using the following commands:**
- Export your certificate into a .cer file
  - `Export-Certificate -Type CERT -Cert $cert -FilePath $env:userprofile\documents\myCert.cer`
  - `Import-Certificate -FilePath $env:userprofile\documents\myCert.cer -CertStoreLocation Cert:\CurrentUser\TrustedPublisher`
  - `Import-Certificate -FilePath $env:userprofile\documents\myCert.cer -CertStoreLocation Cert:\CurrentUser\Root -Confirm`

## Sign your PowerShell script (.ps1) file
- `$pathToPs1File=Read-Host -Prompt 'Enter path to your ps1 script'`
- `Set-AuthenticodeSignature -FilePath $pathToPs1File -Certificate $cert`