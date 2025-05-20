# LAPORAN SISTEM OPERASI  
## SRTF (Shortest Remaining Time First)

### Nama Anggota Kelompok:
- Farid Yanuar Hidayat (3124500032)  
- Ahnaf Hafizh Putra Efendi (3124500033)  
- Firas Rasendriya Athaillah (3124500042)

### Dosen Pengajar:
Dr. Ferry Astika Saputra, ST, M.Sc

##PROGRAM STUDI D3 TEKNIK INFORMATIKA  
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)  
TAHUN 2024

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

**inisialisasi dengan Deklarasi array**
```c
int main()
{
    struct proc p[10],temp;
    float avgtat=0,avgwt=0;
    int n,s,remain=0,time;

```
Code diatas merupakan fungsi main bagian inisialisasi dengan Deklarasi array proses (maks 10 proses), Variabel untuk menyimpan rata-rata TAT dan WT, Variabel kontrol algoritma


**Input Proses:**
```c
    printf("<--SRTF Scheduling Algorithm (Preemptive)-->\n");
    printf("Enter Number of Processes: ");
    scanf("%d",&n);
    for(int i=0;i<n;i++)
        p[i]=read(i+1);

```
Code diatas merupakan fungsi main bagian input pproses dengan membaca jumlah proses dan detail setiap proses

```c
    for(int i=0;i<n-1;i++)
        for(int j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }

```
Code diatas merupakan fungsi main bagian sorting proses, dengan Mengurutkan proses berdasarkan arrival time (AT) menggunakan bubble sort

```c
    printf("\nProcess\t\tAT\tBT\tCT\tTAT\tWT\n");
    p[9].rt=MAX; // Inisialisasi proses dummy
    for(time=0;remain!=n;time++)
    {
        s=9; // Indeks proses dummy
// Mencari proses dengan sisa waktu tersingkat yang sudah datang
        for(int i=0;i<n;i++)
            if(p[i].at<=time&&p[i].rt<p[s].rt&&p[i].rt>0)
                s=i;
        p[s].rt--; // Eksekusi proses 1 unit waktu
// Jika proses selesai
        if(p[s].rt==0)
        {
            remain++;
            p[s].ct=time+1;
            p[s].tat=p[s].ct-p[s].at;
            avgtat+=p[s].tat;
            p[s].wt=p[s].tat-p[s].bt;
            avgwt+=p[s].wt;
            printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n",p[s].no,p[s].at,p[s].bt,p[s].ct,p[s].tat,p[s].wt);
        }
    }

```
Kemudian code diatas merupakan simulasi SRTF dengan mencari setiap satuan waktu kemudian mencari proses dengan sisa waktu tersingjat yang sudah datang kemudian kurangi sisa waktu proses tersebut, jika sisa waktu = 0, proses selesai kemudian menghitung completion time, turn around time, dan waiting time, tampilkan hasil proses tersebut

```c
    avgtat/=n,avgwt/=n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}


```
Menghitung dan menampilkan rata-rata TAT dan WT

---

## KESIMPULAN

Kode di atas merupakan implementasi algoritma penjadwalan proses Shortest Remaining Time First (SRTF) yang bersifat preemptive. Program ini menggunakan struktur data untuk merepresentasikan setiap proses dengan atribut seperti waktu kedatangan, waktu eksekusi, sisa waktu eksekusi, waktu penyelesaian, serta waktu tunggu dan waktu putar. Algoritma ini bekerja dengan cara selalu memilih proses yang memiliki sisa waktu eksekusi tersingkat dari proses-proses yang sudah tiba pada sistem, kemudian mengeksekusinya secara preemptive jika ditemukan proses lain dengan sisa waktu lebih pendek. Setiap kali proses selesai dijalankan, program akan menghitung berbagai metrik kinerja seperti completion time, turnaround time, dan waiting time.

Program ini diawali dengan pengurutan proses berdasarkan waktu kedatangannya menggunakan algoritma bubble sort. Kemudian simulasi dijalankan satuan waktu demi satuan waktu hingga semua proses selesai dieksekusi. Pada akhir eksekusi, program menampilkan detail setiap proses beserta perhitungan rata-rata turnaround time dan waiting time. Meskipun implementasinya sudah benar dan terstruktur dengan baik, kode ini memiliki beberapa keterbatasan seperti jumlah proses maksimum yang tetap (10 proses), kurangnya penanganan input tidak valid, dan tidak adanya visualisasi grafik penjadwalan seperti Gantt Chart.


---
