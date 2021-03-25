# Installing Instant Client 11.2 for php on macOS

## 1. Install Instant Client 11.2

### 1. Download the desired Instant Client ZIP files.
All installations require the Basic or Basic Light package [Download](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html#license-lightbox)

### 2. Unzip the packages into a single directory.
Unzip the packages into a single directory such as "~/instantclient_11_2". For example, to use SQL*Plus
```bash
cd ~
unzip instantclient-basic-macos.x64-11.2.0.4.0.zip
unzip instantclient-sqlplus-macos.x64-11.2.0.4.0.zip
```

### 3. Open directory
```bash
cd ~/instantclient_11_2
ln -s libclntsh.dylib.11.1 libclntsh.dylib
```

### 4. Add links to "~/lib" for required Basic package libraries. For example, to use OCI programs
```bash
mkdir ~/lib
ln -s ~/instantclient_11_2/{libclntsh.dylib.11.1,libnnz11.dylib,\
libociei.dylib} ~/lib/
```

### 5. To be able to run SQL*Plus, add its libraries to "~/lib", and update PATH. For example
```bash
ln -s ~/instantclient_11_2/{libsqlplus.dylib,libsqlplusic.dylib} ~/lib/
export PATH=~/instantclient_11_2:$PATH
```

### 6. Run SQL*Plus and connect using your database credentials and connection string
```bash
# sqlplus [username]/[password]@[Database host: localhost]/[service]
sqlplus hr/welcome@localhost/XE
```

## 2. Install OCI8 with pecl

### 1. Install oci8 with pecl
```bash
pecl install oci8 # Use 'pecl install oci8' to install for PHP 8.

pecl install oci8-2.2.0 # Use 'pecl install oci8-2.2.0' to install for PHP 7.

pecl install oci8-2.0.12 # Use 'pecl install oci8-2.0.12' to install for PHP 5.2 - PHP 5.6.

pecl install oci8-1.4.10 # Use 'pecl install oci8-1.4.10' to install for PHP 4.3.9 - PHP 5.1.
```

### 2. Install oci8 with pecl
```bash
pecl install oci8 # Use 'pecl install oci8' to install for PHP 8.
```