# Installing Instant Client 11.2 on macOS

## 1. Download the desired Instant Client ZIP files.
All installations require the Basic or Basic Light package [Download](https://www.oracle.com/database/technologies/instant-client/macos-intel-x86-downloads.html#license-lightbox)

## 2. Unzip the packages into a single directory.
Unzip the packages into a single directory such as "~/instantclient_11_2". For example, to use SQL*Plus
```bash
cd ~
unzip instantclient-basic-macos.x64-11.2.0.4.0.zip
unzip instantclient-sqlplus-macos.x64-11.2.0.4.0.zip
```

## 3. Open directory
```bash
cd ~/instantclient_11_2
ln -s libclntsh.dylib.11.1 libclntsh.dylib
```

## 4. Add links to "~/lib" for required Basic package libraries. For example, to use OCI programs
```bash
mkdir ~/lib
ln -s ~/instantclient_11_2/{libclntsh.dylib.11.1,libnnz11.dylib,\
libociei.dylib} ~/lib/
```

## 5. To be able to run SQL*Plus, add its libraries to "~/lib", and update PATH. For example
```bash
ln -s ~/instantclient_11_2/{libsqlplus.dylib,libsqlplusic.dylib} ~/lib/
export PATH=~/instantclient_11_2:$PATH
```

## 6. Run SQL*Plus and connect using your database credentials and connection string
```bash
# sqlplus [username]/[password]@[Database host: localhost]/[service]
sqlplus hr/welcome@localhost/XE
```