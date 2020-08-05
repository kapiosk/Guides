# EntityFramework

Update database first classes

```powershell
Scaffold-DbContext "Server={};Database={};user id={};password={}" Microsoft.EntityFrameworkCore.SqlServer -OutputDir DB -force -startupproject Core -project Core -Context SomeContext -NoOnConfiguring
```
