# Misc

## SQLPackage

Install

<https://docs.microsoft.com/en-us/sql/tools/sqlpackage-download?view=sql-server-ver15>

Backup

```bash
sqlpackage /SourceConnectionString:"Server=tcp:{server}.database.windows.net,1433;Initial Catalog={database};Persist Security Info=False;User ID={username};Password={password};MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;" /Action:Export /TargetFile:t.bacpac
```

## sqlcmd & bcp

Install

<https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-setup-tools?view=sql-server-ver15>
