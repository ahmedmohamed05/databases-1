# Backup And Restore DBs

## Full backup

Full backup which take a copy from the whole DB and store it

You can backup using the mouse method

Right mouse click on the database select Tasks -> Backup

Select the path you want, and the filename followed by _.bak_ extension

Ex

```
c:\backups\students.bak
```

> It's important to backup on another partition or better to another drive, If The drive of the server destroyed you can always use the backup which stored on another place, Not effected

You can do the same with the script

```sql
backup database [database] to disk = '[path]';
```

EX:

```sql
backup database Students to disk = 'C:\dbs-backups\students.bak';
```

> Make sure that the user have access permissions to the path

## Differential Backup

comparing the difference from the last backup and change it

The syntax is similar to the full backup but with two more keywords

```sql
backup database [database] to disk = '[path]' with differential;
```

EX:

```sql
backup database Students to disk = 'C:\dbs-backups\students.bak' with differential;
```

> Differential backup appends the changes from the last full backup which keeps the file size growing

## Restore DB

You can restore using the mouse method

Right mouse click on the database select Tasks -> Restore

or you can restore using the script

Syntax:

```sql
restore database [database name] from disk = '[path]';
```

EX:

```sql
restore database Students from disk = 'C:\dbs-backups\students.bak';
```

> You must use the same DB name
