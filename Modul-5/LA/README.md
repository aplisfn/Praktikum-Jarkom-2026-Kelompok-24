# Modul 5 - Enterprise Network dengan VRRP, DHCP Server, GRE Tunnel, dan OSPF

## Topologi Jaringan

![Topologi](images/topologi.png)

Pada praktikum ini dilakukan implementasi jaringan enterprise yang menghubungkan dua site, yaitu Jakarta sebagai Head Quarter (HQ) dan Surabaya sebagai Branch Office. Kedua site dihubungkan melalui jaringan ISP menggunakan FortiGate dan GRE Tunnel. Routing antar-site menggunakan OSPF sehingga seluruh jaringan dapat saling berkomunikasi secara otomatis.

---

# Konfigurasi Perangkat

## Cisco Router Jakarta

Cisco Router Jakarta dikonfigurasi menggunakan metode Router-on-a-Stick untuk VLAN 10, VLAN 20, dan VLAN 60. Router ini juga berperan dalam implementasi VRRP bersama MikroTik Jakarta.

![Cisco Router Jakarta](images/CiscoJKT1.png)

![Cisco Router Jakarta](images/CiscoJKT2.png)

---

## Switch Jakarta

Switch Jakarta digunakan untuk implementasi VLAN dan trunk yang menghubungkan router, server, dan client.

![Switch Jakarta](images/SwitchJKT1.png)

---

## MikroTik Jakarta

MikroTik Jakarta dikonfigurasi sebagai DHCP Relay menuju Ubuntu Server dan sebagai backup gateway menggunakan VRRP.

![MikroTik Jakarta](images/MikrotikJKT.png)

---

## Ubuntu Server

Ubuntu Server berfungsi sebagai DHCP Server untuk VLAN 10 dan VLAN 20 serta Web Server pada VLAN 60.

### DHCP Server

![Ubuntu DHCP](images/Ubuntu1.png)

### Web Server

![Ubuntu Web Server](images/Ubuntu2.png)

---

## MikroTik ISP

MikroTik ISP berfungsi sebagai penghubung antara site Jakarta dan Surabaya serta menyediakan akses internet menggunakan NAT Masquerade.

![MikroTik ISP](images/MikrotikISP.png)

---

## FortiGate Jakarta

FortiGate Jakarta berfungsi sebagai firewall utama, endpoint GRE Tunnel, serta menjalankan OSPF untuk pertukaran routing antar-site.

### Interface dan Routing

![FGJKT1](images/FGJKT1.png)

![FGJKT2](images/FGJKT2.png)

### Firewall Policy

![FGJKT3](images/FGJKT3.png)

### OSPF Neighbor

![FGJKT4](images/FGJKT4.png)

### Routing OSPF

![FGJKT5](images/FGJKT5.png)

---

## Switch Surabaya

Switch Surabaya dikonfigurasi dengan VLAN 30 dan VLAN 40 serta trunk menuju MikroTik Surabaya.

![Switch Surabaya](images/SwitchSBY.png)

---

## MikroTik Surabaya

MikroTik Surabaya berfungsi sebagai gateway VLAN 30 dan VLAN 40 serta DHCP Server untuk VLAN 30.

![MikroTik Surabaya](images/MikrotikSBY.png)

---

## FortiGate Surabaya

FortiGate Surabaya berfungsi sebagai endpoint GRE Tunnel dan menjalankan OSPF bersama FortiGate Jakarta.

![FGSBY1](images/FGSBY1.png)

![FGSBY2](images/FGSBY2.png)

![FGSBY3](images/FGSBY3.png)

![FGSBY4](images/FGSBY4.png)

---

# Hasil Pengujian

## Client VLAN 30 Mendapat DHCP

![DHCP VLAN30](images/vlan30sby.png)

Client VLAN 30 berhasil memperoleh alamat IP secara otomatis dari DHCP Server MikroTik Surabaya.

---

## Client VLAN 40 Menggunakan IP Static

![VLAN40](images/vlan40sby.png)

Client VLAN 40 menggunakan alamat IP statik sesuai konfigurasi praktikum.

---

## Pengujian Internet dari Jakarta

![Internet Jakarta](images/perc9-ping88-1.png)

Client Jakarta melakukan ping ke internet menggunakan alamat 8.8.8.8.

---

## Pengujian Internet dari Surabaya

![Internet Surabaya](images/perc9-ping88-2.png)

Client Surabaya berhasil melakukan ping ke internet menggunakan alamat 8.8.8.8.

---

## Pengujian GRE Tunnel dan OSPF

![GRE dan OSPF](images/perc9-1.png)

GRE Tunnel berhasil terbentuk antara FortiGate Jakarta dan FortiGate Surabaya. OSPF berhasil membentuk neighbor dengan status Full sehingga pertukaran routing antar-site dapat berjalan dengan baik.

---

## Pengujian Antar Site

![Ping Antar Site](images/perc9-2-antar-client.png)

Client Jakarta dan Surabaya berhasil saling berkomunikasi melalui jaringan GRE Tunnel dan routing OSPF.

---

## Pengujian Web Server Jakarta dari Surabaya

![Web Server](images/WebServer.png)

Web Server Jakarta berhasil diakses dari site Surabaya menggunakan alamat IP 192.168.60.10.

---

# Analisis

Pada praktikum ini dilakukan implementasi jaringan enterprise yang menghubungkan dua lokasi berbeda menggunakan GRE Tunnel dan OSPF. Teknologi VRRP digunakan untuk menyediakan gateway virtual sehingga ketersediaan layanan tetap terjaga apabila salah satu perangkat mengalami gangguan. Ubuntu Server berhasil berfungsi sebagai DHCP Server dan Web Server, sedangkan MikroTik ISP berhasil menyediakan konektivitas internet bagi kedua site.

Penggunaan GRE Tunnel memungkinkan komunikasi antar-site melalui jaringan ISP, sementara OSPF mempermudah distribusi routing secara otomatis tanpa perlu menambahkan route secara manual pada setiap perangkat. Hasil pengujian menunjukkan seluruh VLAN berhasil beroperasi dengan baik, client memperoleh alamat IP sesuai konfigurasi, internet dapat diakses dari kedua site, serta komunikasi antar-site dan akses web server berjalan dengan sukses.

---

# Kesimpulan

1. VLAN dan trunk berhasil dikonfigurasi sesuai rancangan topologi.
2. VRRP berhasil menyediakan gateway virtual pada site Jakarta.
3. DHCP Server dan DHCP Relay berjalan dengan baik.
4. GRE Tunnel antara Jakarta dan Surabaya berhasil dibangun.
5. OSPF berhasil membentuk neighbor dan mendistribusikan route antar-site.
6. Seluruh client dapat mengakses internet dari kedua lokasi.
7. Client Jakarta dan Surabaya dapat saling berkomunikasi melalui jaringan antar-site.
8. Web Server Jakarta berhasil diakses dari Surabaya.
9. Seluruh tujuan praktikum berhasil dicapai.
