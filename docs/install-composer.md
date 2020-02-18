# How to install composer

These instructions are mostly taken from [Composer Download](https://getcomposer.org/download/).

Download the composer installer.
```
php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
```
Optionally verify the installer (get the correct checksum from [Composer Public Keys](https://composer.github.io/pubkeys.html)).
```
php -r "if (hash_file('sha384', 'composer-setup.php') === 'e0012edf3e80b6978849f5eff0d4b4e4c79ff1609dd1e613307e16318854d24ae64f26d17af3ef0bf7cfb710ca74755a') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
```
Install composer to the chosen directory (`--install-dir` option) - make sure this is in `$PATH` - and give it a name if you choose (`--filename` option, default value `composer.phar`).
```
php composer-setup.php --install-dir=$HOME/bin --filename=composer
```
Get rid of the installer.
```
php -r "unlink('composer-setup.php');"
```
Check composer is available.
```
composer -V
```

**All done!**

