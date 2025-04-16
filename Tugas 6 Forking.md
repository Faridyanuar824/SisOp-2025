
# Apa Itu Forking?

## Pengertian

**Forking** adalah proses menciptakan salinan dari sebuah proses yang sedang berjalan. Di sistem operasi **Unix/Linux**, forking dilakukan menggunakan fungsi `fork()` dalam bahasa C. Proses baru yang dibuat disebut **child process**, sementara proses asalnya disebut **parent process**.

Fungsi `fork()` memungkinkan sebuah program untuk menjalankan dua proses secara paralel: satu salinan (child) dan satu proses asli (parent).

---

## Contoh Kode C

```c
#include <stdio.h>
#include <unistd.h>

int main() {
    pid_t pid = fork();

    if (pid == 0) {
        // Ini dijalankan oleh child process
        printf("Halo dari Child Process!\n");
    } else if (pid > 0) {
        // Ini dijalankan oleh parent process
        printf("Halo dari Parent Process!\n");
    } else {
        // Error saat forking
        perror("Fork gagal");
    }

    return 0;
}
```

### Contoh Output
```
Halo dari Parent Process!
Halo dari Child Process!
```

> Catatan: Urutan cetak bisa berbeda karena kedua proses berjalan paralel.

---

## Kenapa Forking Itu Penting?

- **Menjalankan Proses Paralel**  
  Cocok untuk server, multiproses, atau aplikasi multitasking.

- **Dasar dari Shell dan Daemon**  
  Saat terminal menjalankan perintah, shell akan melakukan `fork()`.

- **Isolasi Memori Proses**  
  Proses child memiliki salinan sendiri dari memori, aman dan stabil.

---

## Fakta Menarik

| Aspek | Keterangan |
|-------|------------|
| Sistem Operasi | Tersedia di Unix/Linux, BSD, macOS |
| Alternatif di Windows | `CreateProcess()` |
| Kombinasi Umum | `fork()` + `exec()` untuk menjalankan program baru |
| Istilah Populer | *Fork Bomb* – eksploitasi `fork()` berlebihan yang bisa merusak sistem |

---

## Perbedaan Fork vs Thread (Singkat)

| Aspek | Fork (Process) | Thread |
|-------|----------------|--------|
| Memori | Terpisah | Berbagi memori |
| Overhead | Lebih besar | Lebih ringan |
| Keamanan | Lebih aman (isolasi) | Kurang aman (bisa saling ganggu) |

---

_Disusun untuk pembelajaran sistem operasi dan pemrograman tingkat lanjut._
