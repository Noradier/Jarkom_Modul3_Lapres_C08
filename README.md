# Lapres Praktikum Jarkom Modul 2

Anri adalah seorang mahasiswa tingkat akhir yang sedang mengerjakan TA mengenai DHCP dan Proxy. Bu Meguri sebagai dosen pembimbing Anri memberikan tugas pertamanya, (1) yaitu untuk membuat topologi jaringan demi kelancaran TA-nya. Anri sudah pernah mempelajari teknik Jaringan Komputer sehingga Anri dapat membuat topologi tersebut dengan mudah. Bu Meguri memerintahkan Anri untuk menjadikan SURABAYA sebagai router, MALANG sebagai DNS Server, TUBAN sebagai DHCP server, serta MOJOKERTO sebagai Proxy server, dan UML lainnya sebagai client. Bu Meguri berpesan pada Anri untuk menyusun topologi secara hati-hati dan memperhatikan gambar topologi yang diberikan Bu Meguri.

## Soal 1

### Soal
Membuat topologi jaringan

### Jawaban

## Soal 2

### Soal

### Jawaban

## Soal 3

### Soal

### Jawaban

## Soal 4

### Soal

### Jawaban

## Soal 5

### Soal

### Jawaban

## Soal 6

### Soal

### Jawaban

## Soal 7

### Soal
Pertama, akses ke proxy **hanya bisa dilakukan** oleh Anri sendiri sebagai user TA. User autentikasi milik Anri memiliki format:
- **User** : userta_yyy
- **Password** : inipassw0rdta_yyy

### Jawaban
- Membuat file **passwd** di **MOJOKERTO** pada **/etc/squid/** dengan command:
```
htpasswd -c /etc/squid/passwd userta_c08
```

- Kemudian ubah konfigurasi pada **/etc/squid/squid.conf** menjadi berikut:

```
http_port 8080
visible_hostname mojokerto

auth_param basic program /usr/lib/squid/basic_ncsa_auth /etc/squid/passwd
auth_param basic children 5
auth_param basic realm Proxy
auth_param basic credentialsttl 2 hours
auth_param basic casesensitive on
acl USERS proxy_auth REQUIRED
```

## Soal 8

### Soal
Anri sudah menjadwal pengerjaan TA-nya setiap hari **Selasa-Rabu pukul 13.00-18.00**. Bu Meguri membatasi penggunaan internet Anri hanya pada jadwal yang telah ditentukan itu saja. Maka diluar jam tersebut, Anri tidak dapat mengakses jaringan internet dengan proxy tersebut.

### Jawaban
- Pada **/etc/squid/squid.conf** tambahkan:
```
acl "nama_variabel1" time TW 13:00-18:00

http_access allow USERS "nama_variabel1"
http_access deny all
```

## Soal 9

### Soal
Jadwal bimbingan dengan Bu Meguri adalah setiap hari **Selasa-Kamis pukul 21.00 - 09.00** keesokan harinya (sampai Jumat jam 09.00).

### Jawaban
- Pada **/etc/squid/squid.conf** tambahkan:
```
acl "nama_variabel2" time TWH 21:00-23:59
acl "nama_variabel3" time WHF 00:00-09:00

http_access allow USERS "nama_variabel2"
http_access allow USERS "nama_variabel3"
```

## Soal 10

### Soal
Agar Anri bisa fokus mengerjakan TA, setiap dia **mengakses google.com, maka akan di redirect menuju monta.if.its.ac.id** agar Anri selalu ingat untuk mengerjakan TA.

### Jawaban
- Pada **/etc/squid/squid.conf** tambahkan:
```
acl "nama_vairabel4" dstdomain www.google.com

deny_info http://monta.if.its.ac.id/ "nama_vairabel4"
http_access deny "nama_vairabel4"
```

## Soal 11

### Soal
Untuk menandakan bahwa Proxy Server ini adalah Proxy yang dibuat oleh Anri, Bu Meguri meminta Anri untuk mengubah **error page default squid.**

### Jawaban
- File **ERR_ACCESS_DENIED** pada **/usr/share/squid/errors/en/**, diganti dengan hasil download ***wget 10.151.36.202/error403.tar.gz***

## Soal 12

### Soal
Karena Bu Meguri dan Anri adalah tipe orang pelupa, maka untuk memudahkan mereka, Anri memiliki ide ketika menggunakan proxy cukup dengan mengetikkan domain **janganlupa-ta.yyy.pw** dan memasukkan port **8080**.

### Jawaban
- Di **MALANG**, pada /etc/bind/named.conf.local diisi domain **janganlupa-ta.yyy.pw** (Dalam kasus ini **janganlupa-ta.c08.pw**)

![Gambar 12](12.png)