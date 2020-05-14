# BackupSQLAgentJobs.ps1

```powershell
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.ConnectionInfo")
[System.Reflection.Assembly]::LoadWithPartialName("Microsoft.SqlServer.Management.Common.ServerConnection")

$OutputFolder = ".\Test"
$DoesFolderExist = Test-Path $OutputFolder
$null = if (!$DoesFolderExist){New-Item -Path $OutputFolder -Type Directory}

$ServerName = "Server"
$ConnectionString = "Server=$ServerName;database=master;uid={user};pwd={password};persist security info=true"

$ServerConnection = New-Object Microsoft.SqlServer.Management.Common.ServerConnection
$ServerConnection.ConnectionString = $ConnectionString

$srv = New-Object Microsoft.SqlServer.Management.Smo.Server($ServerConnection)

$singleFile = $TRUE
if ($singleFile) {
    $srv.JobServer.Jobs | ForEach-Object {$_.Script() + "GO`r`n"} | Out-File ".\$OutputFolder\jobs.sql"
} else {
    $srv.JobServer.Jobs | ForEach-Object -process {Out-File -filepath $(".\$OutputFolder\" + $($_.Name -replace '\\', '') + ".sql") -inputobject $_.Script() }
}
```
