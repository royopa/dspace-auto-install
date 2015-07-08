dspace-auto-install
===================

Automatic install DSpace on Ubuntu like systems.

This project was based in article LiveCD on [Wiki DSpace].

http://royopa.wordpress.com/2014/03/04/instalacao-do-dspace-4-1-em-sistemas-ubuntu-like/

Checking the status in command line
-----------------------------------

http://asciinema.org/a/10778

Download a Linux Image
----------------------

To avoid the install process, we download a imagem with Ubuntu Linux at the site [Virtual Box Images].

Ubuntu Linux Server Edition 14.04 x86
Size (compressed/uncompressed): 430 MB/1.4 GB
MD5SUM of ova image: 7afed719e42e59f870509b6ffe53c442
Link: https://s3-eu-west-1.amazonaws.com/virtualboxes.org/ubuntu-14.04-server-i386.ova.torrent
Active user account(s)(username/password): ubuntu/reverse

Clone the repository
--------------------

Clone the repository to your computer:
```shell
git clone git@github.com:royopa/dspace-auto-install.git
```

or download the package
------------------------
```shell
wget https://github.com/royopa/dspace-auto-install/archive/master.zip
unzip master.zip
cd dspace-auto-install-master
```

Change the parameters
---------------------

Change the parameters in according to your needs:

build-dspace
------------

    VERSION_DSPACE="5.2"
    
build.properties
----------------

    dspace.name = DSpace
    default.language = pt_BR
    
dspace.cfg
----------

    dspace.name = DSpace
    default.language = pt_BR
    mail.server=smtp.gmail.com
    mail.server.username = treinamento.dspace@gmail.com
    mail.server.password = yourPassword
    mail.extraproperties = mail.smtp.socketFactory.port=465, \
    mail.smtp.socketFactory.class=javax.net.ssl.SSLSocketFactory, \
    mail.smtp.socketFactory.fallback=false
    mail.from.address = treinamento.dspace@gmail.com
    feedback.recipient = treinamento.dspace@gmail.com
    mail.admin = treinamento.dspace@gmail.com
    alert.recipient = treinamento.dspace@gmail.com
    registration.notify = treinamento.dspace@gmail.com
    
Install
-------
Execute the install script

```shell
./build-dspace
```

Using with via Vagrant
----------------------
```sh
vagrant up
```

[Virtual Box Images]:"http://www.osboxes.org/ubuntu/#builder-column-542409983f9f0"
[Wiki DSpace]:"https://wiki.duraspace.org/display/DSPACE/LiveCD"
[XUbuntu]:"http://downloads.sourceforge.net/virtualboximage/xubuntu_1204.7z"
