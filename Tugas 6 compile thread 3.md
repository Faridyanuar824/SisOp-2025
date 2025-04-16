# TUGAS COMPILE THREAD 3

## Compile Thread 3

### Code

```c
#include <stdio.h>
#include <pthread.h>

pthread_cond_t cond1 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond2 = PTHREAD_COND_INITIALIZER;
pthread_cond_t cond3 = PTHREAD_COND_INITIALIZER;
pthread_mutex_t lock = PTHREAD_MUTEX_INITIALIZER;
int done = 1;

void *foo(void *arg) {
    int thread_num = *(int *)arg;
    while (1) {
        pthread_mutex_lock(&lock);
        while (done != thread_num) {
            if (thread_num == 1) {
                pthread_cond_wait(&cond1, &lock);
            } else if (thread_num == 2) {
                pthread_cond_wait(&cond2, &lock);
            } else {
                pthread_cond_wait(&cond3, &lock);
            }
        }

        printf("%d ", thread_num);
        fflush(stdout);

        if (done == 3) {
            done = 1;
            pthread_cond_signal(&cond1);
        } else if (done == 1) {
            done = 2;
            pthread_cond_signal(&cond2);
        } else if (done == 2) {
            done = 3;
            pthread_cond_signal(&cond3);
        }

        pthread_mutex_unlock(&lock);
    }
    return NULL;
}

int main() {
    pthread_t tid1, tid2, tid3;
    int n1 = 1, n2 = 2, n3 = 3;

    pthread_create(&tid1, NULL, foo, &n1);
    pthread_create(&tid2, NULL, foo, &n2);
    pthread_create(&tid3, NULL, foo, &n3);

    pthread_join(tid1, NULL);
    pthread_join(tid2, NULL);
    pthread_join(tid3, NULL);

    return 0;
}
```


---
### Cara Menjalankan Program

1. Buka terminal di Linux.
2. Ketik perintah berikut untuk membuat file C:
   ```bash
   nano print-123.c
   ```
3. Tempelkan kode program ke dalam file tersebut.
4. Simpan dan keluar dengan `Ctrl + X`, tekan `Y`, lalu `Enter`.
5. Kompilasi program dengan perintah:
   ```bash
   gcc -pthread print-123.c -o print-123
   ```
6. Jalankan program:
   ```bash
   ./print-123
   ```

## Penjelasan program

### 1. Inisialisasi dan Sinkronisasi
Program menggunakan tiga **condition variable** (`cond1`, `cond2`, `cond3`) dan satu **mutex (`lock`)** untuk mengatur giliran antar thread.

Ada juga variabel `done` yang digunakan untuk menandai giliran thread mana yang aktif:
- `done = 1` → thread 1 mencetak angka
- `done = 2` → thread 2 mencetak angka
- `done = 3` → thread 3 mencetak angka

### 2. Fungsi `foo()`
Fungsi ini dijalankan oleh masing-masing thread. Cara kerjanya:
- Thread akan **mengunci mutex** dulu supaya tidak ada thread lain yang bisa ubah `done` di saat bersamaan.
- Jika belum gilirannya (misalnya `done != 2` untuk thread ke-2), thread akan **menunggu (wait)** di `cond` masing-masing.
- Jika sudah gilirannya, thread akan:
  - Mencetak angka sesuai nomornya (misalnya `2`).
  - Mengubah nilai `done` ke thread selanjutnya.
  - Memberi **sinyal (`signal`)** ke thread berikutnya untuk bangun.
  - Melepaskan mutex agar thread lain bisa lanjut.

### 3. Bagian `main()`
Di fungsi `main`, program akan:
- Membuat tiga thread (`tid1`, `tid2`, `tid3`), masing-masing diberi angka identitas 1, 2, dan 3.
- Thread pertama akan langsung berjalan karena `done` dimulai dari 1.
- Thread lainnya akan menunggu giliran sesuai sinyal yang diberikan.

---

## Urutan Eksekusi

Ilustrasi urutannya seperti ini:

1. `done = 1` → Thread 1 jalan, cetak `1` → sinyal untuk thread 2  
2. `done = 2` → Thread 2 jalan, cetak `2` → sinyal untuk thread 3  
3. `done = 3` → Thread 3 jalan, cetak `3` → sinyal kembali ke thread 1  
4. Ulangi dari langkah 1...

---

## Output Program
Saat dijalankan, program akan mencetak:
![Output](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/Ouput%20thread.png)<br>
Program akan mencetak angka `1 2 3` secara terus menerus dalam urutan berulang.  
Untuk menghentikan program, tekan `Ctrl+C`.



