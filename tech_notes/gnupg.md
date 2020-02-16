# GnuPG 2.2.19 notes

------------------------

**generate key**

```sh
gpg --full-generate-key
```

**encrypt with cipher:**

```sh
gpg -c --armor --cipher-algo AES256 --no-symkey-cache --output test.aes test.txt 
```

**decrypt:**

```sh
gpg --decrypt --no-symkey-cache --output test1.txt test.aes
```

### Configuration Files

Create inside `~/.gnupg/`

**gpg.conf:**

```
armor
personal-cipher-preferences AES256
verbose
use-embedded-filename
```

**gpg-agent.conf:**

```
default-cache-ttl 0
max-cache-ttl 0
```

**Kill gpg-agent:**

```sh
gpgconf --kill gpg-agent
```

**Launch gpg-agent:**

```sh
gpgconf --launch gpg-agent
```

**Encrypt with .conf files active:**

```sh
gpg -c test.txt
```

**Decrypt with .conf files active:**

```sh
gpg --decrypt test.txt.asc
```

### Batch

```sh
echo your_password | gpg --batch --yes --passphrase-fd 0 your_file.gpg
```

-------------------

[download this page as .md](https://raw.githubusercontent.com/retrokid/retrokid.github.io/master/tech_notes/gnupg.md)
