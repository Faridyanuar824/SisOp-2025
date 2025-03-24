# Laporan Sistem Operasi

## Tugas Appendix dan Timeline OS

**Nama:** Farid Yanuar Hidayat  
**NRP:** 3124500032  
**Dosen Pengajar:** Dr. Ferry Astika Saputra, ST, M.Sc  
**Program Studi:** D3 Teknik Informatika, Politeknik Elektronika Negeri Surabaya (PENS)  
**Tahun:** 2025  

---

## Timeline OS

![Contoh Gambar](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/timline%20os.PNG)

| **Tahun** | **Kategori** | **Konsep/Fitur OS** |
|-----------|-------------|----------------------|
| **1950**  | Mainframes | No software |
|           | Minicomputers | No software |
|           | Desktop Computers | No software |
|           | Handheld Computers | No software |
| **1960**  | Mainframes | Compilers, Time-shared, Batch, Resident Monitors |
|           | Minicomputers | Compilers, Resident Monitors |
|           | Desktop Computers | Compilers |
| **1970**  | Mainframes | Multiuser, Networked, MULTICS |
|           | Minicomputers | Multiuser, Time-shared |
|           | Desktop Computers | Interactive |
| **1980**  | Mainframes | Distributed Systems, Multiprocessor |
|           | Minicomputers | Multiuser, Networked, Clustered, UNIX |
|           | Desktop Computers | Multiuser, Networked, Multiprocessor, UNIX |
|           | Handheld Computers | Interactive |
| **1990**  | Mainframes | Fault-Tolerant |
|           | Minicomputers | Fault-Tolerant |
|           | Desktop Computers | Multiprocessor, Networked, UNIX |
| **2000**  | Smartphones | LINUX, Multiprocessor, Networked |
| **2010**  | Smartphones | Interactive, LINUX |

---

## Rangkuman Appendix

### 1. Pendahuluan
Sistem operasi adalah perangkat lunak yang mengelola perangkat keras dan perangkat lunak lainnya.

**Peran utama OS:**
- Menyediakan antarmuka pengguna.
- Mengelola sumber daya (CPU, memori, penyimpanan, perangkat I/O).
- Menyediakan layanan untuk aplikasi.

**Contoh sistem operasi:** Windows, Linux, macOS, Unix.

### 2. Struktur Sistem Operasi
OS terdiri dari berbagai komponen utama, termasuk kernel, shell, dan API.

**Arsitektur OS:**
- **Monolithic Kernel**: Semua fungsi OS dijalankan dalam satu kernel besar.
- **Layered OS**: Terbagi menjadi lapisan-lapisan dengan tanggung jawab tertentu.
- **Microkernel**: Hanya menyediakan fungsi esensial, sementara layanan lain dijalankan sebagai proses user-space.
- **Modular OS**: Memungkinkan ekstensi dan modul tambahan (contoh: Linux kernel dengan modul loadable).

### 3. Manajemen Proses
Proses adalah program yang sedang dieksekusi dengan status tertentu:
- **New**: Baru dibuat.
- **Ready**: Siap dieksekusi.
- **Running**: Sedang berjalan di CPU.
- **Waiting**: Menunggu event atau I/O.
- **Terminated**: Proses selesai.

### 4. Manajemen Memori
Teknik Manajemen Memori:
- **Paging**: Memori dibagi menjadi blok kecil (page) untuk menghindari fragmentasi eksternal.
- **Segmentation**: Memori dibagi menjadi segmen berdasarkan kebutuhan logis program.
- **Virtual Memory**: Memungkinkan program lebih besar dari RAM untuk berjalan menggunakan swap ke disk.

### 5. Sistem File dan Manajemen Penyimpanan
Sistem File mengatur penyimpanan dan akses data di media penyimpanan.

**Jenis Sistem File:**
- **FAT32**: Sederhana, tetapi memiliki keterbatasan ukuran file.
- **NTFS**: Mendukung fitur keamanan dan enkripsi.
- **EXT4**: Sistem file utama di Linux.

### 6. Manajemen Input/Output (I/O)
Teknik Manajemen I/O:
- **Polling**: CPU terus mengecek status perangkat I/O.
- **Interrupt-Driven I/O**: Perangkat mengirimkan sinyal ke CPU saat siap digunakan.
- **Direct Memory Access (DMA)**: Transfer data langsung antara memori dan perangkat tanpa menggunakan CPU.

### 7. Keamanan dan Proteksi Sistem
Teknik Keamanan:
- **Autentikasi**: Verifikasi identitas pengguna.
- **Otorisasi**: Menentukan hak akses pengguna terhadap sumber daya.
- **Enkripsi**: Mengamankan data dengan enkripsi sehingga hanya bisa dibaca oleh pihak yang berwenang.

Proteksi OS:
- **Mode User vs. Mode Kernel**: Memisahkan operasi sistem kritis dari proses pengguna.
- **Access Control Lists (ACL)**: Mengatur hak akses pengguna terhadap file dan direktori.
- **Firewall dan Antivirus**: Memfilter lalu lintas jaringan dan mencegah malware.

### 8. Sistem Operasi Terdistribusi
OS terdistribusi memungkinkan banyak komputer bekerja bersama sebagai satu sistem.

**Keuntungan OS Terdistribusi:**
- **Skalabilitas**: Bisa menambah lebih banyak komputer sesuai kebutuhan.
- **Keandalan**: Jika satu komputer gagal, sistem tetap berjalan.
- **Efisiensi**: Memanfaatkan sumber daya secara optimal.

Contoh OS Terdistribusi:
- **Google File System (GFS)** untuk penyimpanan skala besar.
- **Hadoop HDFS** untuk pemrosesan data besar.

### 9. Virtualisasi dan Cloud Computing
Virtualisasi memungkinkan satu komputer menjalankan beberapa OS dengan bantuan hypervisor.

**Jenis Virtualisasi:**
- **Full Virtualization**: OS tamu berjalan seolah-olah di mesin fisik.
- **Para-Virtualization**: OS tamu sadar bahwa dia berjalan di lingkungan virtual.
- **Containerization**: Menggunakan teknologi seperti Docker untuk menjalankan aplikasi secara terisolasi.

**Cloud Computing:**
- **IaaS (Infrastructure as a Service)**: Penyewaan server virtual (misalnya AWS EC2).
- **PaaS (Platform as a Service)**: Platform pengembangan aplikasi (misalnya Google App Engine).
- **SaaS (Software as a Service)**: Aplikasi berbasis cloud (misalnya Google Docs, Dropbox).

### Kesimpulan
Sistem operasi memiliki berbagai tugas penting, mulai dari manajemen proses, memori, penyimpanan, hingga keamanan. Dengan berkembangnya teknologi, OS kini juga mendukung komputasi terdistribusi, virtualisasi, dan cloud computing. Pemahaman konsep sistem operasi sangat penting bagi pengembang perangkat lunak, administrator sistem, dan peneliti di bidang komputer.
