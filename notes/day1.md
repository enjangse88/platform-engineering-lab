
Week 1 - Day 1 Summary
Platform Engineering Lab - Linux Foundation

Tanggal: Week 1 - Day 1

Durasi: ±3 jam

Tujuan Hari Ini:
Mengenal Linux sebagai seorang Platform Engineer, bukan sekadar pengguna Linux.

Apa yang Dipelajari
1. Mengenal Identitas Server

Command yang dipelajari:

hostname
hostname -f
hostnamectl
Yang dipahami
Apa itu Hostname.
Perbedaan Hostname dan FQDN.
Mengapa server production memiliki naming convention.
Bagaimana hostname digunakan oleh:
SSH
Monitoring
Logging
Kubernetes
Ansible
Kesimpulan

Hostname adalah nama sebuah server.

Namun hostname bukan identitas permanen karena dapat diubah kapan saja.

2. hostnamectl

Output yang dipelajari

Static hostname
Icon name
Chassis
Machine ID
Boot ID
Operating System
Kernel
Architecture
Hardware Vendor
Hardware Model
Firmware
Firmware Age
Static Hostname
t480

Merupakan nama permanen server.

Lokasi konfigurasi

/etc/hostname
Machine ID

Contoh

d2a875e4163b4b72818ebe37c5971e8a
Yang dipahami

Machine ID adalah identitas unik dari sebuah instalasi Linux.

Machine ID:

tetap
tidak berubah ketika reboot
digunakan oleh banyak service Linux

Contoh penggunaan:

systemd
journald
cloud-init
monitoring
automation
Boot ID

Boot ID berbeda dengan Machine ID.

Boot ID akan berubah setiap kali sistem melakukan reboot.

Contoh

Boot 1

AAAA

Restart

Boot 2

BBBB

Sehingga log dapat dipisahkan berdasarkan sesi boot.

Contoh command

journalctl -b

Menampilkan log boot saat ini.

journalctl -b -1

Menampilkan log boot sebelumnya.

Operating System
Ubuntu 24.04.3 LTS

Memahami arti:

Ubuntu
Versi 24.04
Patch .3
LTS (Long Term Support)
Kernel
Linux 6.14

Belajar bahwa:

Ubuntu ≠ Linux

Linux adalah kernel.

Ubuntu adalah distribusi Linux.

Architecture
x86_64

Menunjukkan CPU menggunakan arsitektur 64-bit.

Hardware Information

Belajar membaca

Vendor
Model
Firmware
Firmware Version

Informasi ini penting saat troubleshooting hardware atau virtualisasi.

Konsep Penting Hari Ini
Hostname bukan identitas utama.

Hostname dapat berubah.

Misalnya

t480

menjadi

platform-lab

Tanpa mengubah isi sistem.

Machine ID adalah identitas mesin.

Machine ID tetap sama sepanjang umur instalasi Linux.

Ketika membuat template VM, Machine ID harus dibuat ulang agar setiap VM memiliki identitas yang unik.

Boot ID adalah identitas sesi boot.

Setiap kali reboot, Boot ID berubah sehingga log dapat dipisahkan berdasarkan setiap proses boot.

Diskusi Engineering

Pertanyaan:

Mengapa Machine ID tidak boleh sama?

Jawaban:

Karena Machine ID merupakan identitas unik sistem. Jika dua mesin memiliki Machine ID yang sama, beberapa service dapat menganggap keduanya sebagai mesin yang sama sehingga menimbulkan konflik identitas.

Pertanyaan:

Mengapa Boot ID berubah setiap reboot?

Jawaban:

Karena setiap proses boot merupakan sesi yang berbeda. Boot ID memungkinkan log dikelompokkan berdasarkan sesi boot sehingga memudahkan analisis masalah setelah restart.

Pertanyaan:

Apakah IP Address dapat menjadi identitas mesin?

Kesimpulan:

Tidak selalu.

IP dapat berubah karena:

DHCP
VPN
Cloud
Re-deployment

Di production, banyak sistem menggunakan identifier unik daripada mengandalkan IP Address.

Cara Berpikir yang Dipelajari

Hari ini kita mulai membangun pola pikir:

❌ Jangan hanya bertanya:

"Command apa yang harus saya jalankan?"

Tetapi mulai bertanya:

"Bagaimana sistem mengenali sebuah mesin?"

Ini adalah cara berpikir seorang Platform Engineer.

Hasil Hari Ini

✔ Memahami Hostname

✔ Memahami FQDN

✔ Memahami Machine ID

✔ Memahami Boot ID

✔ Memahami informasi dasar sistem menggunakan hostnamectl

✔ Memahami perbedaan Linux Kernel dan Ubuntu

✔ Mulai memahami konsep identitas sistem

Insight Terbesar Hari Ini

Nama sebuah server bisa berubah. IP Address bisa berubah. Tetapi setiap sistem yang baik memiliki sebuah identitas unik yang digunakan untuk mengenali resource tersebut.

Konsep ini akan terus muncul saat mempelajari:

Docker (Container ID)
Kubernetes (Node UID, Pod UID)
OpenSearch (Node ID)
Git (Commit SHA)
Cloud (Instance ID)


Anda punya 500 VM.

Salah satu server bermasalah.

Hostname

k3s-worker-08

Tiba-tiba hostname berubah menjadi

ubuntu

Tetapi Machine ID tetap sama.

Menurut Anda,

bagaimana Prometheus, Grafana, OpenSearch, atau Ansible masih bisa mengetahui bahwa itu sebenarnya mesin yang sama?

Tidak perlu jawaban sempurna.