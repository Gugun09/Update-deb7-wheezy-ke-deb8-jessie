# Update-deb7-wheezy-ke-deb8-jessie

Langkah pertama mari kita perbarui data repository dan kemudian upgrade paket – paket aplikasinya:

apt-get update && apt-get upgrade
Silahkan cek versi Debian untuk nanti dibandingkan, ada 2 cara:

cat /etc/debian_version
7.9
uname -a
Linux servernesia 3.2.0-4-686-pae #1 SMP Debian 3.2.41-2 i686 GNU/Linux
Kalau sudah selesai maka kita edit daftar repository yang digunakan dalam Debian 7:

nano /etc/apt/sources.list
Semestinya akan mirip seperti ini isinya:

deb http://ftp.us.debian.org/debian/ wheezy main
deb-src http://ftp.us.debian.org/debian/ wheezy main

deb http://security.debian.org/ wheezy/updates main
deb-src http://security.debian.org/ wheezy/updates main

# wheezy-updates, previously known as 'volatile'
deb http://ftp.us.debian.org/debian/ wheezy-updates main
deb-src http://ftp.us.debian.org/debian/ wheezy-updates main
Gantikan dengan yang ini, maksudnya diarahkan memakai repository untuk Debian 8:

deb http://ftp.us.debian.org/debian/ jessie main
deb-src http://ftp.us.debian.org/debian/ jessie main

deb http://security.debian.org/ jessie/updates main
deb-src http://security.debian.org/ jessie/updates main

# jessie-updates
deb http://ftp.us.debian.org/debian/ jessie-updates main
deb-src http://ftp.us.debian.org/debian/ jessie-updates main
Lakukan proses update dan upgrade paket aplikasi lagi:

apt-get update && apt-get upgrade
Setelah persiapannya selesai, akhirnya kita lanjutkan dengan proses upgrade Debian 7 ke Debian 8:

apt-get dist-upgrade
Di tengah – tengah prosesnya akan muncul pertanyaan berikut:

Disable SSH password authentication for root?

<Yes>                            <No>
Ini maksudnya apakah login root dengan password lewat SSH akan dimatikan atau tidak. Saya anjurkan jawab dengan No kalau anda belum mensetting login SSH tanpa kata sandi. Sekarang login root memakai password memang sudah dimatikan secara default di Debian 8 soalnya.

Setelah itu kita bersihkan paket – paket aplikasi yang sudah tidak terpakai:

apt-get autoremove
Dan… langkah penyelesaian adalah restart servernya:

reboot
Tahu darimana kita suskes upgrade? Saya ilustrasikan dengan hasil perintah dibawah:

cat /etc/debian_version
8.3
uname -a
Linux servernesia 3.16.0-4-686-pae #1 SMP Debian 3.16.7-ckt20-1+deb8u3 (2016-01-17) i686 GNU/Linux
Bandingkan dengan hasil cek versi diawal tutorial. Jelas sudah berbeda rilis versi Debiannya dan kernelnya.
