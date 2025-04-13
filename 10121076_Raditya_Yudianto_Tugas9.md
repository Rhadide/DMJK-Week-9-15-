**Dokumen Perencanaan Proyek: Perancangan & Implementasi Jaringan Enterprise PT. Nusantara Network**

**Disusun oleh Tim [1]:**

1.  **Nadhilah Nur** - Network Architect
2.  **Raditya Yudianto** - Network Engineer
3.  **Irwan Maulana** - Network Services Specialist
4.  **Cantika Ade Qutnindra** - Security & Documentation Specialist

**Tanggal Pengumpulan:** Minggu, [Pekan 9], [2025]

---

**Daftar Isi**

1.  Pendahuluan
    1.1. Latar Belakang
    1.2. Tujuan Proyek
    1.3. Ruang Lingkup Proyek
2.  Pembagian Kelompok dan Peran
3.  Analisis Kebutuhan Jaringan PT. Nusantara Network
    3.1. Struktur Organisasi & Lokasi
    3.2. Kebutuhan Segmentasi dan Keamanan (VLAN & ACL)
    3.3. Kebutuhan Konektivitas (Inter-VLAN, WAN, Internet)
    3.4. Kebutuhan Layanan Jaringan (DHCP, DNS, NAT)
    3.5. Kebutuhan Manajemen & Skalabilitas
4.  Timeline Rencana Kerja Proyek (Pekan 9-15)
5.  Sketsa Awal Desain Jaringan
    5.1. Pendekatan Desain
    5.2. Deskripsi Tekstual Sketsa Awal
6.  Kendala dan Solusi
7.  Kesimpulan
8.  Lampiran

---

**1. Pendahuluan**

**1.1. Latar Belakang**
PT. Nusantara Network adalah perusahaan teknologi informasi yang sedang berkembang, dengan operasi yang tersebar di dua lokasi: Kantor Pusat (Gedung A) dan Kantor Cabang (Gedung B). Struktur perusahaan mencakup empat departemen utama di kantor pusat (IT, Keuangan, SDM, Server Farm) dan dua departemen di kantor cabang (Marketing, Operasional). Seiring pertumbuhan perusahaan, kebutuhan akan infrastruktur jaringan yang andal, aman, efisien, dan mudah dikelola menjadi krusial. Jaringan saat ini (jika ada) tidak lagi memadai untuk mendukung operasi bisnis yang kompleks dan terdistribusi. Proyek ini bertujuan merancang dan mensimulasikan implementasi jaringan enterprise yang memenuhi kebutuhan spesifik PT. Nusantara Network, mengintegrasikan konsep-konsep jaringan modern.

**1.2. Tujuan Proyek**
Tujuan utama dari proyek akhir semester ini adalah:
*   Merancang arsitektur jaringan enterprise yang robust, scalable, dan aman untuk PT. Nusantara Network.
*   Mensimulasikan implementasi desain jaringan menggunakan perangkat lunak simulasi (Cisco Packet Tracer).
*   Mengimplementasikan segmentasi jaringan menggunakan VLAN untuk setiap departemen.
*   Mengkonfigurasi routing inter-VLAN dan routing dinamis (OSPF) untuk konektivitas antar gedung melalui WAN.
*   Mengimplementasikan layanan jaringan esensial: DHCP untuk alokasi IP otomatis, DNS untuk resolusi nama internal/eksternal, dan NAT untuk akses internet.
*   Menerapkan kebijakan keamanan jaringan menggunakan Access Control Lists (ACL) sesuai kebutuhan antar departemen.
*   Mendokumentasikan seluruh proses perancangan, implementasi, dan pengujian secara komprehensif.
*   Mengembangkan kemampuan kolaborasi tim, manajemen proyek, dan presentasi teknis.

**1.3. Ruang Lingkup Proyek**
Proyek ini mencakup:
*   Analisis kebutuhan jaringan berdasarkan studi kasus PT. Nusantara Network.
*   Perancangan topologi jaringan fisik dan logis.
*   Perancangan skema pengalamatan IP (Subnetting).
*   Konfigurasi VLAN dan Trunking pada switch.
*   Konfigurasi routing Inter-VLAN.
*   Konfigurasi routing dinamis OSPF antar router utama (Core, Router A, Router B).
*   Simulasi koneksi WAN antar Gedung A dan Gedung B.
*   Konfigurasi DHCP Server untuk alokasi IP pada setiap VLAN.
*   Konfigurasi DNS Server untuk resolusi nama internal (`nusantara-network.local`).
*   Konfigurasi NAT (PAT/Overload) pada Core Router untuk akses internet.
*   Implementasi ACL standar dan extended untuk memenuhi kebijakan keamanan yang ditentukan.
*   Pengujian konektivitas end-to-end dan fungsionalitas semua layanan dan fitur keamanan.
*   Pembuatan dokumentasi teknis lengkap dan materi presentasi akhir.
*   Pembuatan video demo/tutorial singkat.

**2. Pembagian Kelompok dan Peran**

Berdasarkan hasil diskusi kelompok, pembagian peran adalah sebagai berikut:

*   **Network Architect:** Dhilah
    *   Tanggung Jawab Utama: Desain topologi keseluruhan, perencanaan pengalamatan IP dan subnetting, dokumentasi visual dan tertulis desain.
*   **Network Engineer:** Radit
    *   Tanggung Jawab Utama: Implementasi konfigurasi routing (statis/dinamis), konfigurasi VLAN/trunking, pengaturan koneksi WAN.
*   **Network Services Specialist:** Irwan
    *   Tanggung Jawab Utama: Implementasi DHCP, DNS, NAT, konfigurasi server dasar jika diperlukan, memastikan konektivitas layanan.
*   **Security & Documentation Specialist:** Cantika
    *   Tanggung Jawab Utama: Implementasi ACL dan kebijakan keamanan, pengujian keamanan, koordinasi dokumentasi keseluruhan, persiapan materi presentasi.

Semua anggota kelompok akan berkolaborasi dalam setiap tahapan proyek untuk memastikan pemahaman menyeluruh dan kesuksesan implementasi.

**3. Analisis Kebutuhan Jaringan PT. Nusantara Network**

Berdasarkan studi kasus, kebutuhan jaringan PT. Nusantara Network dianalisis sebagai berikut:

**3.1. Struktur Organisasi & Lokasi**
*   **Gedung A (Kantor Pusat):**
    *   IT Dept: 40 komputer + perangkat jaringan
    *   Finance Dept: 25 komputer
    *   HR Dept: 20 komputer
    *   Server Farm: 10 server
*   **Gedung B (Kantor Cabang):**
    *   Marketing Dept: 30 komputer
    *   Operations Dept: 35 komputer
*   Total host (perkiraan kasar awal): (40+25+20) + (30+35) + 10 Server = 85 + 65 + 10 = 160 host, belum termasuk perangkat jaringan dan potensi pertumbuhan.

**3.2. Kebutuhan Segmentasi dan Keamanan (VLAN & ACL)**
*   **VLAN:** Setiap departemen (IT, Finance, HR, Server Farm, Marketing, Operations) harus berada dalam VLAN terpisah. Ini meningkatkan keamanan dengan membatasi broadcast domain dan mempermudah manajemen traffic.
*   **ACL:** Dibutuhkan kontrol akses antar departemen. Kebijakan contoh yang perlu diimplementasikan (dan mungkin disempurnakan):
    *   IT: Akses ke semua departemen & server farm. Terbatas akses masuk dari Finance/HR.
    *   Finance: Akses ke HR & server farm (terbatas). Tidak bisa diakses Marketing/Operations.
    *   HR: Akses ke semua departemen (koordinasi). Akses terbatas ke server farm (hanya server SDM - perlu klarifikasi/asumsi server khusus).
    *   Marketing/Operations: Akses terbatas ke server farm. Tidak akses ke Finance.
    *   Server Farm: Keamanan tinggi, akses sangat diatur via ACL.

**3.3. Kebutuhan Konektivitas (Inter-VLAN, WAN, Internet)**
*   **Inter-VLAN Routing:** Diperlukan mekanisme routing antar VLAN di setiap gedung agar departemen yang diizinkan dapat berkomunikasi. Kemungkinan menggunakan Router atau Switch.
*   **WAN:** Koneksi antar Gedung A dan Gedung B diperlukan. Studi kasus menyebutkan "bandwidth terbatas", menyiratkan perlunya desain routing yang efisien.
*   **Routing Dinamis:** OSPF diamanatkan untuk manajemen rute antar gedung (antar Router A, Router B, dan kemungkinan Core Router). Ini memberikan redundansi dan adaptasi otomatis terhadap perubahan topologi.
*   **Akses Internet:** Karyawan/Server memerlukan akses ke internet. NAT harus diimplementasikan pada gateway (kemungkinan Core Router) untuk mentranslasikan alamat IP privat ke satu atau beberapa alamat IP publik yang diberikan ISP.

**3.4. Kebutuhan Layanan Jaringan (DHCP, DNS, NAT)**
*   **DHCP:** Diperlukan untuk alokasi alamat IP otomatis di setiap VLAN departemen untuk memudahkan manajemen pengalamatan IP klien. Setiap VLAN harus memiliki pool DHCP sendiri.
*   **DNS:** Diperlukan server DNS internal untuk resolusi nama host internal (e.g., `fileserver.nusantara-network.local`) dan mampu meneruskan (forward) query untuk nama eksternal ke DNS publik (e.g., 8.8.8.8). Server DNS kemungkinan ditempatkan di Server Farm.
*   **NAT:** Seperti disebutkan di 3.3, NAT (spesifiknya PAT/Overload karena biasanya IP Publik terbatas) diperlukan untuk akses internet.

**3.5. Kebutuhan Manajemen & Skalabilitas**
*   **Manajemen Terpusat:** Kebutuhan ini menyiratkan desain yang memudahkan monitoring dan konfigurasi (misalnya, penggunaan protokol standar seperti SNMP, dokumentasi yang baik).
*   **Skalabilitas:** Desain harus mempertimbangkan potensi pertumbuhan jumlah pengguna atau penambahan departemen/layanan di masa depan. Penggunaan skema pengalamatan IP yang terstruktur dan routing dinamis mendukung skalabilitas.

**4. Timeline Rencana Kerja Proyek (Pekan 9-15)**

| Pekan | Tanggal Deadline (Jumat, 23:59 WIB) | Tugas Utama Kelompok                                                               | Deliverable                                  | Penanggung Jawab Utama Koordinasi |
| :---- | :---------------------------------- | :--------------------------------------------------------------------------------- | :------------------------------------------- | :-------------------------------- |
| **9** | [Pekan 9]                   | Perencanaan Proyek & Desain Awal                   | Dokumen Perencanaan Proyek                   | Cantika (Documentation)           |
| **10**| [Pekan 10]                  | Desain Topologi & Skema Pengalamatan      | Dokumen Desain Jaringan (Diagram, Tabel IP) | Dhilah (Architect)                |
| **11**| [Pekan 11]                  | Implementasi Topologi Dasar & VLAN       | Laporan Implementasi Tahap 1 + File Simulasi | Radit (Engineer)                  |
| **12**| [Pekan 12]                  | Implementasi Routing & WAN | Laporan Implementasi Tahap 2 + File Simulasi | Radit (Engineer)                  |
| **13**| [Pekan 13]                  | Implementasi Layanan Jaringan                                                         | Laporan Implementasi Tahap 3 + File Simulasi | Irwan (Services)                  |
| **14**| [Pekan 14]                  | Implementasi Keamanan & Pengujian                            | Laporan Implementasi Tahap 4 + File Simulasi | Cantika (Security)                |
| **15**| **Rabu**, [Pekan 15], 23:59 WIB | Finalisasi Dokumentasi & Presentasi                | Laporan Akhir, Video Demo, Slide Presentasi  | Cantika (Documentation)           |

**5.  Sketsa Awal Desain Jaringan**
![alt text](https://github.com/Rhadide/DMJK-Week-9-15-/blob/main/resources/Week9_Sketsa.jpg?raw=true)
## Komponen Utama

### Koneksi Internet
- Koneksi internet utama terhubung ke **ISP** yang kemudian terhubung ke **Core Router**

### Core Router
- Berfungsi sebagai **gateway utama** dengan implementasi **NAT** untuk akses internet
- Menerapkan **Access Control List (ACL)** untuk kebijakan keamanan
- Menggunakan **OSPF** sebagai protokol routing dinamis antar gedung
- Menjadi penghubung utama antara **Router A** (Gedung A) dan **Router B** (Gedung B)

### Gedung A (Kantor Pusat)
- **Router A** terhubung ke Core Router dan Switch A
- **Switch A** mendistribusikan koneksi ke 4 switch departemen:
  * **Switch IT (3)** untuk Departemen IT
  * **Switch FIN (2)** untuk Departemen Keuangan
  * **Switch HR (1)** untuk Departemen SDM
  * **Switch SRV (1)** untuk Server Farm
- Implementasi **VLAN**:
  * **VLAN 10**: Departemen IT (40 PC)
  * **VLAN 20**: Departemen Keuangan (25 PC)
  * **VLAN 30**: Departemen SDM (20 PC)
  * **VLAN 40**: Server Farm (10 Server)

### Gedung B (Kantor Cabang)
- **Router B** terhubung ke Core Router dan Switch B
- **Switch B** mendistribusikan koneksi ke 2 switch departemen:
  * **Switch MRKT (2)** untuk Departemen Marketing
  * **Switch OPS (2)** untuk Departemen Operasional
- Implementasi **VLAN**:
  * **VLAN 50**: Departemen Marketing (30 PC)
  * **VLAN 60**: Departemen Operasional (35 PC)

## Pertimbangan Desain
- Setiap departemen ditempatkan dalam **VLAN terpisah** untuk keamanan dan manajemen traffic
- Koneksi antar gedung menggunakan jaringan **WAN** dengan implementasi **OSPF**
- Struktur jaringan mendukung persyaratan untuk implementasi layanan **DHCP** dan **DNS**
- **Core Router** dengan implementasi **NAT** memungkinkan semua departemen untuk mengakses internet
- Desain memfasilitasi penerapan **ACL** untuk mengontrol akses antar departemen sesuai kebijakan keamanan

**6. Kendala dan Solusi**

*   **Kendala 1:** Koordinasi kerja tim dalam lingkungan pembelajaran jarak jauh (jika relevan).
    *   **Solusi 1:** Menggunakan platform kolaborasi (misal: Meet, Zoom), menjadwalkan pertemuan rutin virtual, dan komunikasi yang jelas antar anggota.
*   **Kendala 2:** Pembagian beban kerja yang merata dan tepat waktu sesuai peran dan timeline.
    *   **Solusi 2:** Monitoring progress mingguan oleh seluruh tim, komunikasi proaktif jika ada hambatan, dan fleksibilitas untuk saling membantu antar peran.

**7. Kesimpulan**

Dokumen perencanaan ini menandai dimulainya proyek perancangan dan implementasi jaringan PT. Nusantara Network. Kelompok telah dibentuk, peran telah dibagi, dan analisis kebutuhan awal berdasarkan studi kasus telah dilakukan. Timeline kerja untuk 7 pekan ke depan telah disusun, memberikan panduan langkah demi langkah. Sketsa desain awal secara konseptual telah dibuat sebagai dasar untuk pengembangan desain detail pada pekan berikutnya. Tim siap untuk melanjutkan ke tahap Desain Topologi dan Skema Pengalamatan (Pekan 10).
