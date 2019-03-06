# Newebe: Distributed Social Network

## Sekilas Tentang

Newebe merupakan aplikasi web bertipe *distributed social network*. Perbedaan Newebe dengan jejaring sosial yang lain adalah Newebe menawarkan solusi yang biasa dihadapkan oleh jejaring sosial pada umumnya, yaitu kita menukar data-data privasi kita sebagai alat untuk berhubungan dengan orang lain. Untuk itu, Newebe menawarkan alat untuk berelasi dengan orang lain yang dapat dihost sendiri oleh pengguna dan proses hubungan dilakukan secara langsung dengan pengguna lain

![alt text](https://camo.githubusercontent.com/56872c8d40995c85182c65122987aee1ed71d96f/687474703a2f2f67656c6e696f722e66696c65732e776f726470726573732e636f6d2f323031302f31322f6e6574776f726b2e676966)

## Instalasi

Langkah instalasi pada *remote server* untuk Debian atau Ubuntu users dari komputer lokal"

1. Install python-setuptools dan python-pip
```
$ apt-get install python python-setuptools python-pip
```
2. Install fabric fabtools menggunakan pip command 
```
$ pip install fabric fabtools
```

3. Get dan install fabfile.py
```
$ wget https://raw.github.com/gelnior/newebe/master/deploy/fabfile.py
```

4. Menjalankan fabric.api pada username@hostname
```
$ fab setup -H myrootuser@myhosturlorip
```
Newebe akan berjalan pada https://localhost:8000/

Kemudian lakukan Update pada remote server
```
$ sudo pip install git+git://github.com/gelnior/newebe.git
$ sudo supervisorctl restart newebe 
```

## Cara Pemakaian

**Sisi Server**

Langkah penggunaan Newebe:

1. Install Dependencies:
* Python > 2.6
* Couchdb >= 0.11.0
* Coucdbkit >= 0.4.8
* Tornado >= 2.0.0
* Pycurl >= 1.0.0
* Daemon >= 1.0.0
* Markdown >= 2.0.0
* PIL >= 1.1.6
* pytz

```
$ sudo apt-get install python python-setuptools python-pip python-pycurl 
                     python-dev python-imaging build-essential couchdb git
                     libxml2-dev libxslt-dev openssl supervisor
```

2. Install Newebe
```
$ sudo pip install git+git://github.com/gelnior/newebe.git
```

3. Jalankan database menggunakan CouchDB
```
$ sudo /etc/init.d/couchdb start
```
untuk memastikan apakah database sudah berjalan atau belum -> muncul lebih dari satu baris
```
$ ps -ef | grep couchdb
```

4. Membuat Newebe user dan membuat Newebe folder
```
$ sudo adduser --disabled-password --shell=/bin/bash newebe
$ sudo su newebe
$ cd
$ mkdir newebe
$ mkdir newebe/certs
```

5. Membuat sertifikasi untuk HTTPS. Ketika dijalankan, akan diberikan beberapa pertanyaan, jawab sesuai yang diinginkan
```
$ sudo su newebe
$ cd ~/newebe/certs
$ openssl genrsa -out ./server.key 1024
$ openssl req -new -x509 -days 3650 -key ./server.key -out ./server.crt
```
6. Membuat root user, set *supervisor configuration* untuk Newebe user.

*  Buat file baru:
```
$ sudo nano /etc/supervisor/conf.d/newebe.conf
```

*  Kemudian salin kode berikut:
```
[program:newebe]
autorestart=false
command=newebe_server.py
redirect_stderr=true
user=newebe
```

7. Jalankan newebe
```
$ sudo supervisorctl update`
```

8. Newebe siap digunakan pada https://localhost:8000

Jika Newebe belum berhasil dijalankan, maka lakukan perintah berikut:
```
$ sudo pip install importlib
$ sudo supervisorctl start newebe
```

**Sisi Client**

Untuk menjalankan Newebe di sisi client, install node.js terlebih dahulu
```
$ git clone https://github.com/ry/node.git
```
```
$ cd node
$ ./configure
$ make
$ make install
```
Kemudian install Brunch the front-end assembler:
```
$ npm install brunch -g
```
Install build dependencies
```
$ cd client
$ npm install
```
Lalu lihat perubahan file pada directory client
```
$ cd client
$ brunch w
```

Run tests (backend)
===================
Aktivasi virtual env, kemudian install dependencies
``` 
$ virtualenv --distribute --no-site-packages virtualenv
$ . virtualenv/bin/activate
$ pip install -r deploy/requirements-dev.txt
```
Jalankan tests untuk setiap module. Untuk melakukan tes, jalankan newebe kedua pada port 8889
```
$ sh launch_tests.sh
```

- Tampilan aplikasi web
![alt text](https://drive.google.com/open?id=15sptLqDsXBzytIz_1iyIbY41ykn5xDfn)
- Fungsi-fungsi utama
- Isi dengan data real/dummy (jangan kosongan) dan sertakan beberapa screenshot


## Pembahasan

- Pendapat anda tentang aplikasi web ini
	- pros:
1. Mudah digunakan
2. Tampilan sederhana
	- cons:
1. Terlalu banyak dependencies
2. Use an embedded database, bukan Couchdb

## Referensi
https://github.com/gelnior/newebe
https://github.com/gelnior/newebe/wiki/Hardware
