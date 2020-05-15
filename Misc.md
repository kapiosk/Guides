# Misc

Get Fill TFS History

```powershell
./tf history /collection:"{org-url}" "$/{project}" /recursive /noprompt | Out-File -FilePath "D:\TFS.log"
```
