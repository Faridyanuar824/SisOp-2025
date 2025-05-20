
# LAPORAN SISTEM OPERASI  
## SRTF (Shortest Remaining Time First)

### Nama Anggota Kelompok:
- Farid Yanuar Hidayat (3124500032)  
- Ahnaf Hafizh Putra Efendi (3124500033)  
- Firas Rasendriya Athaillah (3124500042)

### Dosen Pengajar:
Dr. Ferry Astika Saputra, ST, M.Sc

> PROGRAM STUDI D3 TEKNIK INFORMATIKA  
> POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)  
> TAHUN 2024

---

## CODE

```c
#include <stdio.h>

#define MAX 9999

struct proc {
    int no, at, bt, rt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    p.rt = p.bt;
    return p;
}

int main() {
    struct proc p[10], temp;
    float avgtat = 0, avgwt = 0;
    int n, s, remain = 0, time;

    printf("<--SRTF Scheduling Algorithm (Preemptive)-->
");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for (int i = 0; i < n; i++)
        p[i] = read(i + 1);

    for (int i = 0; i < n - 1; i++)
        for (int j = 0; j < n - i - 1; j++)
            if (p[j].at > p[j + 1].at) {
                temp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = temp;
            }

    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt = MAX;

    for (time = 0; remain != n; time++) {
        s = 9;
        for (int i = 0; i < n; i++)
            if (p[i].at <= time && p[i].rt < p[s].rt && p[i].rt > 0)
                s = i;

        p[s].rt--;

        if (p[s].rt == 0) {
            remain++;
            p[s].ct = time + 1;
            p[s].tat = p[s].ct - p[s].at;
            avgtat += p[s].tat;
            p[s].wt = p[s].tat - p[s].bt;
            avgwt += p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[s].no, p[s].at, p[s].bt, p[s].ct, p[s].tat, p[s].wt);
        }
    }

    avgtat /= n;
    avgwt /= n;
    printf("\nAverage TurnAroundTime = %f\nAverage WaitingTime = %f", avgtat, avgwt);
}
```

---

## HASIL

 ![Image](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/SRTF.png)
 ![Image](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/SRTF%20Chart.png)
---

## ANALISA CODE

### Struktur Data
```c
#define MAX 9999

struct proc {
    int no, at, bt, rt, ct, tat, wt;
};
```

Penjelasan:
- `MAX`: konstanta besar sebagai nilai awal dummy.
- `struct proc`: menyimpan atribut proses:
  - `no`: nomor proses
  - `at`: arrival time (waktu kedatangan)
  - `bt`: burst time (waktu eksekusi total)
  - `rt`: remaining time (sisa waktu)
  - `ct`: completion time (waktu selesai)
  - `tat`: turnaround time (total waktu dalam sistem)
  - `wt`: waiting time (waktu tunggu)

### Fungsi `read`
```c
struct proc read(int i) {
    ...
}
```
Membaca input proses dan mengisi nilai awal `rt` dengan `bt`.

### Fungsi `main`

**Inisialisasi:**
Deklarasi array proses, variabel rata-rata TAT dan WT, serta variabel kontrol.

**Input proses:**
```c
for (int i = 0; i < n; i++)
    p[i] = read(i + 1);
```

**Sorting proses berdasarkan Arrival Time:**
Menggunakan bubble sort.

**Simulasi Penjadwalan SRTF:**
```c
for (time = 0; remain != n; time++) {
    ...
}
```
Menjalankan simulasi tiap satuan waktu, memilih proses dengan sisa waktu tersingkat dan mengeksekusinya satu per satu.

Jika proses selesai (`rt == 0`), dihitung `ct`, `tat`, dan `wt`, lalu ditampilkan.

**Rata-rata:**
Menghitung dan mencetak rata-rata `TurnAround Time` dan `Waiting Time`.

---

## KESIMPULAN

Kode di atas merupakan implementasi algoritma penjadwalan **Shortest Remaining Time First (SRTF)** secara **preemptive**.

Algoritma bekerja dengan memilih proses dengan **sisa waktu eksekusi tersingkat** dari proses yang telah datang dan mengeksekusinya.

Langkah-langkah utama:
- Input data proses
- Sorting berdasarkan arrival time
- Simulasi eksekusi preemptive
- Perhitungan dan tampilan hasil

**Kelebihan:**
- Mempercepat penyelesaian proses pendek
- Memberikan rata-rata waktu tunggu dan putar yang optimal

**Kekurangan:**
- Maksimal hanya untuk 10 proses
- Tidak ada validasi input
- Tidak menyertakan visualisasi (misalnya Gantt Chart)

---
