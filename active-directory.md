# Useful Commands when Using Active Directory

## How to get the current domain info
   ```powershell
   Get-ADDomain
   ```

## How to test connectivity with the AD domain controller
   ```powershell
   Test-Connection <Domain-Controller>
   ```

## How to list all OUs (Organizational Units)
  ```powershell
   Get-ADOrganizationalUnit -Filter # | Select-Object Name, DistinguishedName
   ```

## How to check the groups a user belongs to
   ```powershell
   Get-ADUser -Identity <Username> -Properties MemberOf | Select-Object -ExpandProperty MemberOf
   ```

## How to check the accounts which have been inactive by at least 90 days
   ```powershell
   Search-ADAccount -AccountInactive -UsersOnly -TimeSpan 90.00:00:00
   ```

## How to list computers stored in a container (NOT OU). The list can be exported as csv also:
   ```powershell
   Get-ADComputer -Filter # -Properties # | Select-Object Name, OperatingSystem, DistinguishedName
   Get-ADComputer -Filter # -Properties # | Select-Object Name, OperatingSystem, DistinguishedName | Export-Csv -Path "C:\ADComputers.csv" -NoTypeInformation
   ```



