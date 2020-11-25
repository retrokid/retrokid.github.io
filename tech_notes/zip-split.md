# Zip and Split notes

----------------------

**zip directory, without compressing and encrypting with a password:**

```sh
zip -0er backup-desktop.zip backup_desktop/
```

**split backup-desktop.zip to 1megabyte files in backup_split directory with backup-desktop- prefix:**

```sh
split -b 1m backup-desktop.zip backup_split/backup-desktop-
```

**md5 backup-desktop.zip file:**

```sh
md5 -q backup-desktop.zip
```

**md5 splitted files**

```sh
cat backup_split/backup-desktop-* | md5 -q
```

**merge files:**

```sh
cat backup-desktop-* > backup-desktop.zip
```

**unzip files:**

```sh
unzip backup-desktop.zip
```

-------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/zip-split.md)
