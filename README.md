# AutomatedActiveDirectoryScript
Automated Active Directory Script For New Users

Import-Module ActiveDirectory

$users = Import-Csv "C:\Scripts\employees.csv"

foreach ($user in $users) {

$fullname = "$($user.FirstName) $($user.LastName)"

New-ADUser `
-Name $fullname `
-GivenName $user.FirstName `
-Surname $user.LastName `
-SamAccountName $user.Username `
-UserPrincipalName "$($user.Username)@homelab.local" `
-Department $user.Department `
-AccountPassword (ConvertTo-SecureString $user.Password -AsPlainText -Force) `
-Enabled $true `
-Path "OU=Employees,DC=homelab,DC=local"
}
