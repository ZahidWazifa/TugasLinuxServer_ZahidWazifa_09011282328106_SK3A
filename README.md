   **Nama: Zahid Wazifa**
   
   **NIM: 09011282328106**
   
   **Kelas: SK3A**
   
   **Dosen Pengampu Mata Kuliah: 	Adi Hermansyah, S.Kom., M.T**


---

# WriteUp Akses Server Base OS dengan protokol SSH
# Defenisi Protokol SSH
SSH (Secure Shell) adalah protokol kriptografi yang memungkinkan akses, kontrol, dan modifikasi pada sistem server jarak jauh. Protokol ini menggunakan kunci kriptografi publik dan privat untuk memvalidasi sistem komputer jarak jauh dan memungkinkan komunikasi melalui transmisi data yang sensitif, sehingga memastikan keamanan dan integritas dalam komunikasi jarak jauh. berdarsarkan [informasi grafis](https://www.ssh.com/hs-fs/hubfs/SSH_Client_Server.png?width=556&name=SSH_Client_Server.png) ini menjelaskan bagaimanaa protokol ssh bekerja.

# hal yang dibutuhkan 
- **Host Side Operation System**

untuk host side yang dibutuhkann merupkan sebuah operation system berbasis server, dalam hal ini saya menggunakan sebuah wordpress server yang mana server ini menggunakan sistem operasi berbasis ubuntu yang dapat diunduh di [Link Referensi](https://www.vulnhub.com/entry/webgoat-1,365/)
setelah melakukan import file image virtual box maka aka tampil tampilan ui sebagai berikut:

![](https://github.com/ZahidWazifa/Test-fix/blob/master/IPADDRESS.png)

- **Client Side Operation System**
  
Untuk client side ini opeasi sistem yang digunakan bebas, karena untuk melakukan koneski yang paling dibutuhkan adalah kemampuan dari operasi sistem untuk melakukan koneksi ke server dengan protokol ssh. dalam hal ini saya menggunakan sistem operasi Kali Linux untuk melakukan koneksi ke server, dan oleh karena itu maka digunakan [Tools Open-SSH](https://ubuntu.com/server/docs/openssh-server) untuk melakukan koneksi tampilan awal dari openssh seperti berikut:

![](https://github.com/ZahidWazifa/Test-fix/blob/master/SSH.png)

# Koneksi dan Konfigurasi
