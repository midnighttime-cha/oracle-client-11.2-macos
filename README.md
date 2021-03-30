# Installing Instant Client 11.2 for php on macOS

## 1. Install Instant Client 11.2

### 1.1. Download the desired Instant Client ZIP files.
All installations require the Basic or Basic Light package [Download](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html#license-lightbox)

1. Dowload: instantclient-basic-macos.x64-11.2.0.4.0.zip
2. Dowload: instantclient-sqlplus-macos.x64-11.2.0.4.0.zip
3. Dowload: instantclient-sdk-macos.x64-11.2.0.4.0.zip 

### 1.2. Unzip the packages into a single directory.
Unzip the packages into a single directory such as "~/instantclient_11_2". For example, to use SQL*Plus
```bash
cd ~
unzip instantclient-basic-macos.x64-11.2.0.4.0.zip
unzip instantclient-sqlplus-macos.x64-11.2.0.4.0.zip
unzip instantclient-sdk-macos.x64-11.2.0.4.0.zip
```

### 1.3. Edit .bash_profile in Home Directory
```bash
sudo nano ~/.bash_profile
```
add code under follow
```bash
export ORACLE_HOME=/Users/[YOUR_USER]/instantclient_11_2
export DYLD_LIBRARY_PATH=/Users/[YOUR_USER]/instantclient_11_2
export PATH=$PATH:$DYLD_LIBRARY_PATH
export SQL_PATH=$ORACLE_HOME
export PATH=$PATH:$ORACLE_HOME
export NLS_LANG="AMERICAN_AMERICA.UTF8"
```

### 1.4. Run .bash_profile
```bash
source ~/.bash_profile
```

### 1.5. Open directory
```bash
cd ~/instantclient_11_2
ln -s libclntsh.dylib.11.1 libclntsh.dylib
```

### 1.6. Add links to "~/lib" for required Basic package libraries. For example, to use OCI programs
```bash
mkdir ~/lib
ln -s ~/instantclient_11_2/{libclntsh.dylib.11.1,libnnz11.dylib,libociei.dylib} ~/lib/
```

### 1.7. To be able to run SQL*Plus, add its libraries to "~/lib", and update PATH. For example
```bash
ln -s ~/instantclient_11_2/{libsqlplus.dylib,libsqlplusic.dylib} ~/lib/
```

### 1.8. Run SQL*Plus and connect using your database credentials and connection string
```bash
# sqlplus [username]/[password]@[Database host: localhost]/[service]
sqlplus hr/welcome@localhost/XE
```

## 2. Install OCI8 with pecl

### 2.1. Install Auto Config
```bash
brew install autoconf
```

### 2.2. Uninstall old OCI8
```bash
pecl uninstall oci8 # for PHP 8.

pecl uninstall oci8-2.2.0 # for PHP 7.

pecl uninstall oci8-2.0.12 # for PHP 5.2 - PHP 5.6.

pecl uninstall oci8-1.4.10 # for PHP 4.3.9 - PHP 5.1.
```

### 2.3. Install oci8 with pecl
```bash
pecl install oci8 # Use 'pecl install oci8' to install for PHP 8.

pecl install oci8-2.2.0 # Use 'pecl install oci8-2.2.0' to install for PHP 7.

pecl install oci8-2.0.12 # Use 'pecl install oci8-2.0.12' to install for PHP 5.2 - PHP 5.6.

pecl install oci8-1.4.10 # Use 'pecl install oci8-1.4.10' to install for PHP 4.3.9 - PHP 5.1.
```

### 2.4. PECL check for ORACLE_HOME
Please provide the path to the ORACLE_HOME directory. Use 'instantclient,/path/to/instant/client/lib' if you're compiling with Oracle Instant Client [autodetect] :

type under follow.
```bash
instantclient,/Users/[YOUR_USER]/instantclient_11_2
```

### 2.5. Edit org.apache.httpd.plist
```bash
<dict>
<key>XPC_SERVICES_UNAVAILABLE</key>
<string>1</string>
....
<key>DYLD_LIBRARY_PATH</key>
<string>/Users/[YOUR_USER]/instantclient_11_2</string>
...
</dict>
```

### 2.6. Edit php.ini
```bash
cd /etc
sudo cp php.ini.default php.ini
```

### 2.7. Add extension=oci8.so in /ect/php.ini and restart apache
```bash
sudo apachectl restart
```

### 2.8. Check OCI8 status
```bash
php --ri oci8
```
....
```bash
OCI8 Support => enabled
OCI8 DTrace Support => disabled
OCI8 Version => 2.0.8
Revision => $Id: f04114d4d62cffes4cdc2ed3b7f22f9c2c3a5016 $
Oracle Run-time Client Library Version => 12.1.0.2.0
Oracle Compile-time Instant Client Version => 12.1

Directive => Local Value => Master Value
oci8.max_persistent => -1 => -1
oci8.persistent_timeout => -1 => -1
oci8.ping_interval => 60 => 60
oci8.privileged_connect => Off => Off
oci8.statement_cache_size => 20 => 20
oci8.default_prefetch => 100 => 100
oci8.old_oci_close_semantics => Off => Off
oci8.connection_class => no value => no value
oci8.events => Off => Off
```