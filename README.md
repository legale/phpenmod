# phpenmod
Simple PHP extension enabler/disabler

[![phpenmod](https://github.com/legale/phpenmod/raw/master/screenshot.png)]

## Usage
Just compiled and installed php-src on Arch Linux

### PHP installation 
```
git clone https://github.com/php/php-src
cd php-src

./buildconf

./configure \ 
--disable-all \
--with-config-file-scan-dir=/etc/php/php.d \
--with-config-file-path=/etc/php/php.ini \
--enable-ctype \

make -j4 && sudo make install
```

### Extension installation
```
cd ~/src/php-src/ext/readline
phpize && ./configure && make -j4 && sudo make install
cd ~/src/php-src/ext/mbstring
phpize && ./configure && make -j4 && sudo make install
```

### phpenmod installation
```
wget https://github.com/legale/phpenmod/raw/master/phpenmod -O ~/bin/phpenmod
chmod +x ~/bin/phpenmod
ln -s /home/ru/bin/phpenmod /home/ru/bin/phpdismod
```

### phpenmod usage example
#### Trying to enable installed extensions
```
[ru@ru-manjaro php.d]$ phpenmod readline mbstring
```

Results:
```
phpenmod: Ini file not found. Trying to create new...
phpenmod: Done.
phpenmod: Ini file not found. Trying to create new...
phpenmod: Done.
```

#### Use with a different PHP version
```
[ru@ru-manjaro php.d]$ export PHP_BIN=php81
[ru@ru-manjaro php.d]$ phpenmod readline mbstring
```

#### Listing scan directory
```
ls /etc/php/php.d/
```
Results:
```
10-readline.ini  20-mbstring.ini
```

#### Trying to disable mbstring

```
phpdismod mbstring
cat 20-mbstring.ini
```
Results:
```
phpdismod: Trying to disable PHP extension mbstring...
phpdismod: Done. 
;extension=mbstring
```


#### Listing enabled PHP extensions
```
php -m
```
Results:
```
[PHP Modules]
Core
ctype
date
hash
pcre
readline
Reflection
SPL
standard

[Zend Modules]

```


