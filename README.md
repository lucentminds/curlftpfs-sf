# curlftpfs

## Original owner

Homepage: http://curlftpfs.sourceforge.net/  
Repo: https://sourceforge.net/projects/curlftpfs/

## Description
CurlFtpFS is a filesystem for acessing ftp hosts based on FUSE and
libcurl. It automatically reconnects if the server times out. 

[@galo2099's](https://github.com/galo2099) motivation to start this project was to learn how to program using [Curl](http://curl.haxx.se) and [Fuse](http://fuse.sourceforge.net). He also wanted to maintain his [website](https://golaberto.com.br) using the tools that he was used to, like `cd`, `mv`, `cp` and `vim`.

As the FTP protocol is not very feature rich, this filesystem does not fulfill every constraint of a real filesystem, but it should be usable for simple tasks like copying and editing files.

## Requirements

glib-2.0  
libcurl >= 7.17.0  
fuse >= 2.2

fedora
```shell
dnf install glib2-devel fuse-devel libcurl-devel
```


## Compilation and Installation

```shell
./configure
make
make install
```
## Remove or uninstall

```shell
make uninstall
```

## Usage

```shell
curlftpfs <ftpsite> <mountpoint>
```

ex.:
```shell
curlftpfs ftp://ftp.sunet.se/ sunet/
```


## Debugging

```shell
curlftpfs -f -v -o debug,ftpfs_debug=3 <ftpsite> <mountpoint> 
```

(runs the curlftpfs in foreground and shows libcurl verbose debug output)  


## Known Problems

1) Several GUI application (gedit, leafpad,...) use open(O_RDWR) + seek mode for saving files 
which cannot be supported by the FTP protocol. Therefore saving files might throw an error.
Hopefully future kernels will provide special errno's to make it easier to 
deal with less capable file-systems.

2) There seems to be a bug in libcurl 7.18 which sometimes causes problems reading files. 
Should be fixed in libcurl >= 7.18.2

http://sourceforge.net/tracker/index.php?func=detail&aid=1951588&group_id=976&atid=100976




