# Minimal implementation of git in Python

## Creating a new repository

```bash
$ ./git init
```

## Adding a file to the index

```bash
$ echo 'file 1' > file
$ ./git update-index --add file
```

## Commiting changes

```bash
$ ./git write-tree
tree-sha1-output
$ echo 'Init commit' | ./git commit-tree sha1-output --name "Your name" --email "Your@email"
commit-sha1-output
```

## Updating master branch to point to your new commit

```bash
$ ./git update-ref refs/heads/master commit-sha1-output
```

## Extra commands

### Hashing a file

```bash
$ ./git hash-object file
file-sha-output
```

### Creating an object from a file and adding it to the index

```bash
$ ./git hash-object -w file
file-sha-output
$ ./git update-index --add --cacheinfo 100644,file-sha-output,file
```

### Printing the contents of an object

```bash
$ ./git cat-file -p 1f0d599f4a702177a95f282bca4f3141c481ecde
# Contents of the first version of ./git
$ ./git cat-file -p fe46efb2c730f8cf4d1aa82fb2a775d380fb9c06
100755 git 1f0d599f4a702177a95f282bca4f3141c481ecde
$ ./git cat-file -p 687057a776d350815418972f3f001a25b88a259e
tree fe46efb2c730f8cf4d1aa82fb2a775d380fb9c06
author Erick Hernandez Curiel <Erick.HernandezCuriel@mx.bosch.com> 1581607242 +0000
committer Erick Hernandez Curiel <Erick.HernandezCuriel@mx.bosch.com> 1581607242 +0000

Init commit

```

### Printing the type of an object

```bash
$ ./git cat-file -t 1f0d599f4a702177a95f282bca4f3141c481ecde
blob
$ ./git cat-file -t fe46efb2c730f8cf4d1aa82fb2a775d380fb9c06
tree
$ ./git cat-file -t 687057a776d350815418972f3f001a25b88a259e
commit
```
