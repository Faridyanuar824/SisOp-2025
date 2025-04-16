# Tugas: Perbedaan Multiprogramming dan Multitasking, Fungsi OS, dan Virtualisasi Container

## 1. Perbedaan Multiprogramming dan Multitasking

| Aspek | Multiprogramming | Multitasking |
|-------|------------------|--------------|
| **Pengertian** | Teknik untuk mengeksekusi beberapa program dalam satu waktu dengan menyimpan banyak program di memori utama. | Teknik di mana satu pengguna dapat menjalankan banyak tugas (task) secara bersamaan pada satu sistem. |
| **Fokus** | Eksekusi *multiple programs* satu per satu, tetapi secara bergantian. | Eksekusi *multiple tasks* secara hampir bersamaan. |
| **Tujuan** | Memaksimalkan penggunaan CPU. | Memberi ilusi bahwa beberapa proses berjalan secara bersamaan. |
| **Jenis Sistem** | Biasanya digunakan pada sistem batch atau sistem komputer besar. | Digunakan pada sistem operasi modern seperti Windows, Linux, macOS. |
| **Contoh** | Menjalankan compiler, kalkulator, dan text editor dalam satu sistem. | Membuka browser, mengetik di Word, dan mendengarkan musik secara bersamaan. |

---

## 2. Fungsi Sistem Operasi (Operating System / OS)

Sistem Operasi adalah perangkat lunak yang bertindak sebagai penghubung antara pengguna dan perangkat keras komputer.

### Fungsi Utama OS:
1. **Manajemen Proses**  
   Mengatur proses yang berjalan, menjadwalkan CPU, mengelola status proses (running, waiting, etc).

2. **Manajemen Memori**  
   Mengalokasikan dan mengelola penggunaan RAM oleh proses-proses yang berjalan.

3. **Manajemen Penyimpanan**  
   Mengatur sistem file dan akses ke media penyimpanan seperti HDD atau SSD.

4. **Manajemen Perangkat Keras (I/O Management)**  
   Mengontrol komunikasi antara sistem dan perangkat keras (keyboard, mouse, printer, dll).

5. **Manajemen Keamanan**  
   Mengatur hak akses, otentikasi, dan proteksi data.

6. **Antarmuka Pengguna**  
   Menyediakan GUI atau CLI agar user dapat berinteraksi dengan sistem.

7. **Manajemen File**  
   Mengatur pembuatan, penghapusan, pembacaan dan penulisan file dalam sistem.

---

## 3. Virtualisasi dan Container

### A. Virtualisasi

Virtualisasi adalah proses menjalankan beberapa sistem operasi (guest OS) pada satu mesin fisik (host OS) melalui software hypervisor.

**Contoh**: VMware, VirtualBox, Microsoft Hyper-V

**Kelebihan:**
- Menjalankan OS berbeda di satu mesin.
- Isolasi sistem yang kuat.
- Cocok untuk uji coba sistem atau software.

### B. Container

Container adalah metode virtualisasi tingkat aplikasi yang berjalan di atas OS host, berbagi kernel yang sama namun tetap terisolasi.

**Contoh**: Docker, Podman, LXC

**Ciri-ciri Container:**
- Ringan dan cepat dibanding VM.
- Menggunakan image untuk deployment.
- Ideal untuk DevOps dan microservices.

### Perbandingan VM dan Container

| Aspek         | Virtual Machine (VM) | Container |
|---------------|----------------------|-----------|
| **Ukuran**    | Lebih besar (GB)     | Lebih kecil (MB) |
| **Startup**   | Lama (menit)         | Cepat (detik) |
| **Isolasi**   | Kuat                 | Cukup kuat |
| **OS**        | Punya OS sendiri     | Berbagi kernel host |
| **Contoh**    | VirtualBox, VMware   | Docker, Kubernetes |

---

_Disusun oleh: Farid Yanuar Hidayat_  
_Mahasiswa Politeknik Elektronika Negeri Surabaya (PENS)_

