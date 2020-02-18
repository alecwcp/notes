# How to install PHP from source

These instructions are mostly taken from [Building PHP](http://www.phpinternalsbook.com/php7/build_system/building_php.html).

Clone the PHP source.
```
git clone git@github.com:php/php-src.git
```
Optionally rename the remote from origin to upstream. (I keep my fork of a project called origin, and the source called upstream)
```
git remote rename origin upstream
```
Fetch the tags too (specific releases are available as a tag).
```
git fetch upstream --tags
```
Checkout the release to build. (Release 7.3.14 in this case)
```
git checkout php-7.3.14
```
Before building PHP there are some dependencies that are needed, install any common missing ones with following command (Debian/Ubuntu)
```
sudo apt-get install build-essential autoconf libtool bison re2c
```
Build the configure script. (`force` flag necessary because we're building from source)
```
./buildconf --force
```
Setup the configuration. `--prefix` option is the installation location. Extensions to build are passed with `--enable-NAME` or `--disable-NAME` switches. If an extension or SAPI has external dependencies these are passed with the `--with-NAME` or `--without-NAME` switches. To see a full list of options run `./configure help | less`. This step will throw errors if there are any issues with your setup for building PHP (e.g. missing libraries). Make sure the value chosen for `--prefix` is in `$PATH` so `php` is available globally after installation. (Chosen extensions here are `openssl`, `zlib` and `mbstring`). Make sure that if any dependencies are missing that you install the dev/devel versions of the libraries since the non-dev versions typically do not include the required headers (e.g. install `libxml2-dev` not `libxml2`).
```
./configure --prefix=$HOME/bin/php7.3 --with-openssl --with-zlib --enable-mbstring
```
Build, change the number used for the `-j` option to the number of cores you have available (see `grep "cpu cores" /proc/cpuinfo`). (using 4 cores here)
```
make -j4
```
Optionally run the tests - say yes to the option to send the report to the PHP QA team, help out open source a bit.
```
make test
```
Actually install PHP (to the location given as `--prefix` when running `./configure`).
```
make install
```
Check PHP is now available.
```
php -v
```

**All done!**

