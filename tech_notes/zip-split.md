Zip directory, without compressing and encrypting with a password:

```
zip -0er backup-desktop.zip backup_desktop/
```

> 0: no compression
> e: encrypt it with a password
> r: means whole directory

Split **backup-desktop.zip** in **backup_split** directory with **backup-desktop-** prefix:

```
split -b 1m backup-desktop.zip backup_split/backup-desktop-
```
> -b 1m: 1 Megabyte size of each file

Use md5 to print **checksum** of **backup-desktop.zip** file:

```
md5 -q backup-desktop.zip
```

> -q: print only checksum

Print splitted files' **checksum**

```
cat backup_split/backup-desktop-* | md5 -q
```

> cat backup_split/backup-desktop-* : merge files in backup_split with "backup-desktop-" prefix.
> | md5 -q:  send that merged files to md5 -q and md5 -q will print another text which is splitted files' checksum.


Merge files:

```
cat backup-desktop-* > backup-desktop.zip
```

> cat backup-desktop-* : means merge every file in directory with backup-desktop- prefix.
> > backup-desktop.zip: means save merged files as backup-desktop.zip

Unzip it:

```
unzip backup-desktop.zip
```


