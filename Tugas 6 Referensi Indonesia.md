## Tugas Referensi Indonesia Nomor 3 dan 4

### **Topik: Proses**

#### **3. Jelaskan tindakan yang diambil oleh sebuah kernel ketika alih konteks antar proses.**

Ketika kernel melakukan **alih konteks (context switch)** antar proses, ada beberapa langkah penting yang dilakukan:

1. **Menyimpan status proses saat ini:**
   - Kernel menyimpan isi register CPU, program counter, dan stack pointer dari proses yang sedang berjalan ke dalam Process Control Block (PCB) miliknya.

2. **Memilih proses berikutnya:**
   - Scheduler kernel memilih proses lain dari antrian siap (ready queue) untuk dijalankan.

3. **Memuat status proses baru:**
   - Informasi dari PCB proses baru diambil dan diisikan kembali ke register CPU.

4. **Melanjutkan eksekusi:**
   - Proses baru mulai dijalankan dari titik terakhir ia diberhentikan.

Proses ini memerlukan waktu dan merupakan bagian penting dalam manajemen multiprogramming.

---

#### **4. Informasi apa saja yang disimpan pada tabel proses saat alih konteks dari satu proses ke proses lain.**

Tabel proses (PCB - Process Control Block) menyimpan informasi penting berikut:

- **Informasi Identitas:** PID (Process ID), Parent PID
- **Informasi CPU:** Register CPU, Program Counter, Stack Pointer
- **Status Proses:** Ready, Running, Waiting, Terminated
- **Informasi Memori:** Base dan limit register, pointer ke tabel halaman
- **Informasi I/O:** File descriptor, resource yang sedang digunakan
- **Informasi Penjadwalan:** Prioritas, waktu CPU yang telah digunakan, waktu masuk ready queue

Informasi tersebut dibutuhkan untuk menyimpan dan memulihkan keadaan proses saat terjadi context switch.

---

### **Topik: Thread**

#### **3. Sebutkan dua perbedaan antara user level thread dan kernel thread. Saat kondisi bagaimana salah satu dari thread tersebut lebih baik?**

| Aspek | **User Level Thread (ULT)** | **Kernel Level Thread (KLT)** |
|-------|------------------------------|-------------------------------|
| **Manajemen Thread** | Dikelola oleh pustaka di user space | Dikelola langsung oleh kernel |
| **Context Switch** | Cepat, tidak perlu akses kernel | Lebih lambat, perlu mode switching |

**Kapan lebih baik?**
- **ULT:** Baik untuk aplikasi ringan/interaktif yang butuh switching cepat.
- **KLT:** Cocok untuk pemrosesan berat dan sistem multi-core karena bisa dijadwalkan oleh kernel.

---

#### **4. Jelaskan tindakan yang diambil oleh sebuah kernel saat alih konteks antara kernel level thread.**

Saat context switch antar KLT terjadi, kernel akan:

1. **Menyimpan status thread aktif:** ke dalam struktur kontrol thread (mirip PCB).
2. **Memilih thread baru:** menggunakan scheduler thread kernel.
3. **Memuat status thread baru:** dari memorinya ke register CPU.
4. **Melanjutkan eksekusi thread baru.**

Karena dilakukan di level kernel, maka melibatkan perpindahan mode dari user ke kernel dan sebaliknya (lebih berat dibanding ULT).

---

### **Topik: Penjadwalan Proses (Soal Tabel Proses)**

#### **3. Keuntungan menggunakan time quantum size berbeda di sistem multilevel**

- **Respon cepat:** Time quantum kecil pada level atas memberikan respon cepat untuk proses interaktif.
- **Efisiensi untuk proses berat:** Time quantum besar pada level bawah mengurangi overhead context switching.
- **Fleksibilitas:** Menyesuaikan eksekusi berdasarkan karakteristik proses.
- **Menghindari starvation:** Proses level bawah tetap dapat berjalan saat proses level atas selesai atau time quantum habis.

---

#### **4. Diagram Gantt untuk 4 algoritma penjadwalan**

**Data Proses:**
| Proses | Burst Time | Prioritas |
|--------|------------|-----------|
| P1     | 10         | 3         |
| P2     | 1          | 1         |
| P3     | 2          | 3         |
| P4     | 1          | 4         |
| P5     | 5          | 2         |

**Semua proses datang di waktu t = 0**

---

#### **A. FCFS**
```
| P1 | P2 | P3 | P4 | P5 |
0   10  11  13  14  19
```

---

#### **B. SJF**
```
| P2 | P4 | P3 | P5 | P1 |
0   1   2   4   9   19
```

---

#### **C. Prioritas Non-Preemptive**
```
| P2 | P5 | P1 | P3 | P4 |
0   1   6  16  18  19
```

---

#### **D. Round Robin (Quantum = 2ms)**
```
| P1 | P2 | P3 | P4 | P5 | P1 | P5 | P1 | P5 | P1 | P1 |
0   2   3   5   6   8  10  12  14  15  17  19
```

