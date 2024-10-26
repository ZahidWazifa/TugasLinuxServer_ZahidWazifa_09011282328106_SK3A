   **Nama: Zahid Wazifa**
   
   **NIM: 09011282328106**
   
   **Kelas: SK3A**
   
   **Dosen Pengampu Mata Kuliah: 	Adi Hermansyah, S.Kom., M.T**


---

# WriteUp Akses Server Base OS dengan protokol SSH
## 1. Defenisi Protokol SSH
SSH (Secure Shell) adalah protokol kriptografi yang memungkinkan akses, kontrol, dan modifikasi pada sistem server jarak jauh. Protokol ini menggunakan kunci kriptografi publik dan privat untuk memvalidasi sistem komputer jarak jauh dan memungkinkan komunikasi melalui transmisi data yang sensitif, sehingga memastikan keamanan dan integritas dalam komunikasi jarak jauh. berdasarkan [informasi grafis](https://www.ssh.com/hs-fs/hubfs/SSH_Client_Server.png?width=556&name=SSH_Client_Server.png) ini menjelaskan bagaimanaa protokol ssh bekerja.

## 2. hal yang dibutuhkan 
### 2.1 Host Side Operation System

untuk host side yang dibutuhkann merupkan sebuah operation system berbasis server, dalam hal ini saya menggunakan sebuah wordpress server yang mana server ini menggunakan sistem operasi berbasis ubuntu yang dapat diunduh di [Link Referensi](https://www.vulnhub.com/entry/webgoat-1,365/)
setelah melakukan import file image virtual box maka aka tampil tampilan ui sebagai berikut:

[![](https://github.com/ZahidWazifa/Test-fix/blob/master/IPADDRESS.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

### 2.2 Client Side Operation System
  
Untuk client side ini opeasi sistem yang digunakan bebas, karena untuk melakukan koneski yang paling dibutuhkan adalah kemampuan dari operasi sistem untuk melakukan koneksi ke server dengan protokol ssh. dalam hal ini saya menggunakan sistem operasi Kali Linux untuk melakukan koneksi ke server, dan oleh karena itu maka digunakan [Tools Open-SSH](https://ubuntu.com/server/docs/openssh-server) untuk melakukan koneksi tampilan awal dari openssh seperti berikut:

[![](https://github.com/ZahidWazifa/Test-fix/blob/master/SSH.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

## 3. Pembahasan
### 3.1 Koneksi default port
#### 3.1.1 cek alamat ip host server

setelah melakukan inisialiasi pada proses sebelumnya, check ip address pada host server untuk melakukan koneksi dengan memasukkan perintah berikut ini
```
$ ifconfig 
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/IPADDRESS.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

#### 3.1.2 cek open port pada host server
untuk mengecek alamat port yang terbuka pada host server, maka pada client side kita melakukan *Port Scanning* menggunakan tools [nmap](https://nmap.org/) dengan memasukkan perintah berikut ini
```
$ nmap <alamat ip Host Server>
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/PortScanning.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

#### 3.1.3 melakukan koneksi pada default port untuk protokol ssh
untuk melakukan koneksi ke host server pada default port yaitu 22  menggunakan protokol ssh dapat menggunakan perintah berikut ini
```
$ ssh -p 22 <usernameHost@alamatiphost>
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/LoginServerUsingdefaultport(22).png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

### 3.2 Konfigurasi untuk port 40 pada host server
sebelum melakukan modfikasi lebih baik kita masuk ke mode super users agar kita dapat leluasa melakukan modifikasi dengan perintah berikut ini:
```
$ sudo su
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/SuperUSers.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

#### 3.2.1 modifikasi file *ssh_config* 
sebelum melakukan konfigurasi maka kita harus melakukan file backup agar file sistem utama tidak corrupt jika terjadi hal yang tidak diinginkan dengan memasukkan perintah berikut ini:
```
$ cp /etc/ssh/ssh_config /etc/ssh/ssh_config.backup
```
setelah melakukan backup, maka kita akan melakukan modifikasi pada file *ssh_config* dengan memasukkan perintah berikut ini:
```
$ nano /etc/ssh_config
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/ConfigFIleForPort.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

setelah membuka file *ssh_config* menggunakan perintah nano ubah konfigurasi dengan beberapa hal ini dengan mengubah baris yang terdapat unsur port 22:
```
Protocol 2
Port 40
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/ChangePortto40.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

setelah melakukan modifikasi maka perubahan pada file harus disimpan dengan memasukkan kombinasi keyboard *ctrl+x* dan masukkan opsi *Yes*
#### 3.2.2 menerapkan perubahan pada sistem 
untuk menerapkan perubahan sistem maka kita harus melakukan konfirmasi dengan ufw agar perubahan dapat diterapkan dengan perintah berikut ini:
```
$ ufw allow 40/tcp
$ ufw enable
```
dan untuk mengecek status ufw dapat menggunakan perintah berikut ini:
```
$ ufw status
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/AllowingUFWFirewall.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

untuk mengecek status port menggunakan tulpn makan dapat memasukkan perintah berikut ini
```
$ ss -tuln | grep ssh
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/TULPN.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)

### 3.3 Koneksi ke port 40
setelah melakukan konfigurasi pada file sistem maka, kita bisa melakukan koneksi ke port 40 seperti sebelumnya dengan perintah berikut ini:
```
$ ssh -p 40 <usernameHost@alamatiphost>
```
[![](https://github.com/ZahidWazifa/Test-fix/blob/master/WebgoatPort40.png)](https://github.com/ZahidWazifa/TugasLinuxServer_ZahidWazifa_09011282328106_SK3A)
