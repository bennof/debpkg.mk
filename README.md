# debpkg.mk
Debian package makefile (minimal)

## Getting started

### Creating a folder for your packages
The first step is always to create a new folder that will contain your sources for the packages.

```sh
$ mkdir my_debs
$ cd my_debs
```

### Downloading debpkg.mk
The next step is to download `debpkg.mk`. Right now the best way is to use the git repository as 
source. Doing it this way causes a little bit loger url but works best. 

```sh
$ wget https://raw.githubusercontent.com/bennof/debpkg.mk/master/debpkg.mk
```
Or:
```sh
$ curl -O https://raw.githubusercontent.com/bennof/debpkg.mk/master/debpkg.mk
```

### Create your first package
To create your first package just run:

```sh
$ make -f debpkg.mk new NAME=my_package
```

Now you should edit the control file in `my_package/DEBIAN/control`. All fields needed have a preset. The 
Username is set using the `$USER` environment variable. The name ist the package name. For further information 
read https://www.debian.org/doc/debian-policy/ch-controlfields.html

One of the most important fields is `DEPENDS`. Here are all dependency packages listed (comma sperated).
https://www.debian.org/doc/debian-policy/ch-relationships.html

Next you can build the filesystem tree and insert the files to be installed.

### Pack your package
Just run:

```sh
$ make -f debpkg.mk build
```

All packages are in `./.build/`.

### Install to a local repository
*Experimental*
Just run:

```sh
$ sudo make -f debpkg.mk install
$ apt-get update
$ apt-cache search my_package
> my_package - some description 
```


## Create a Makefile / Config

You can create a Makefile after downloading `debpkg.mk`:

```
# My Makefile
BUILD_PATH:=some/path # here are the created deb-files (INFO: this folder should not be detected by SRCS)
REP_NAME:=repository_name
INSTALL_PATH:=/some/path/to/private/repository_name # here will the private repository be build
SRCS:=my_package_1 my_package_2 # your packages 

include debpkg.mk
```

## Further commands

### Help
```sh
$ make -f debpkg.mk help
```

### Test
```sh
$ make -f debpkg.mk test
```

### Update
```sh
$ make -f debpkg.mk update
```
### Init
```sh
$ make -f debpkg.mk init
```
