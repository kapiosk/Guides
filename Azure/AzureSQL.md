# Misc

## SQLPackage

Install

<https://docs.microsoft.com/en-us/sql/tools/sqlpackage-download?view=sql-server-ver15>

Backup (Linux Example)

```bash
sqlpackage /Action:Export /TargetFile:"{fileName}" /SourceConnectionString:"Server=tcp:{server}.database.windows.net,1433;Initial Catalog={database};Persist Security Info=False;User ID={username};Password={password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"
```

Restore (Powershell Example)

```powershell
.\SqlPackage.exe /a:Import /sf:"{fileName}" /tsn:"{SQLInstance}" /tdn:"{database}" /tu:"{username}" /tp:"{password}"
```

## sqlcmd & bcp

Install

<https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?view=sql-server-ver15>
