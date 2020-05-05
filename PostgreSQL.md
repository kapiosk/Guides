# Backup

```bash
PGPASSWORD="potato" pg_dumpall -U user -h localhost -f=db.sql
PGPASSWORD="potato" pg_dump -U user -h localhost -d database -f database.sql
```
