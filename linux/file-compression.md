# File compression

## zip / unzip

### Creating a zip archive

```sh
zip target.zip file1.txt file2.txt file3.txt
```

### Creating zip from directory

```sh
zip dir.zip -r dir
```

- `-r` as in **r**ecursive.

### Showing zip files' content

```sh
unzip -l dir.zip
```

- `-l` as in **l**ist.

### Unzipping into a specific directory

```sh
unzip dir.zip -d /tmp
```

- `-d` as in target **d**irectory.
