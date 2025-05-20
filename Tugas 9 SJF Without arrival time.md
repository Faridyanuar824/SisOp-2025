# LAPORAN SISTEM OPERASI  
## SJF SCHEDULING WITHOUT ARRIVAL TIME

---

### Nama Anggota Kelompok:

- Farid Yanuar Hidayat (3124500032)  
- Ahnaf Hafizh Putra Efendi (3124500033)  
- Firas Rasendriya Athaillah (3124500042)  

### Dosen Pengajar:

Dr Ferry Astika Saputra ST, M.Sc

### PROGRAM STUDI D3 TEKNIK INFORMATIKA  
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)  
TAHUN 2024

---

## CODE  
### SJF Without Arrival Time

```c
#include<stdio.h>

struct proc {
    int no, bt, ct, tat, wt;
};

struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}

int main() {
    struct proc p[10], tmp;
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;

    printf("<--SJF Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);

    for(int i = 0; i < n; i++)
        p[i] = read(i + 1);

    for(int i = 0; i < n - 1; i++)
        for(int j = 0; j < n - i - 1; j++)
            if(p[j].bt > p[j + 1].bt) {
                tmp = p[j];
                p[j] = p[j + 1];
                p[j + 1] = tmp;
            }

    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");

    for(int i = 0; i < n; i++) {
        ct += p[i].bt;
        p[i].ct = p[i].tat = ct;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }

    avgtat /= n;
    avgwt /= n;
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
}
```

---

## HASIL  
![Image](https://github.com/user-attachments/assets/dc62b4ea-f278-4563-b029-8c4c1d8b2760)
![Image](https://github.com/user-attachments/assets/8ca7024e-05c1-44aa-963d-dfafddd8821c)

---

## ANALISA CODE  
### SJF Without Arrival Time

#### Deklarasi Struct:
```c
struct proc {
    int no, bt, ct, tat, wt;
};
```
Struct ini menyimpan semua atribut proses yang diperlukan untuk scheduling.  
- bt adalah waktu CPU yang dibutuhkan proses.  
- ct, tat, dan wt dihitung selama algoritma berjalan.  

*Kelebihan:*  
Menggunakan struct membuat data terorganisir dan mudah diakses.

---

#### Fungsi Input:
```c
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    p.no = i;
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    return p;
}
```
Fungsi read ini untuk membaca input burst time dari user. i adalah nomor proses yang di-passing dari loop di main().  
Return value: struct proc yang sudah terisi.  

*Kenapa dipisah?*  
Modularitas—memisahkan logika input dari perhitungan.

---

#### Sorting Bubble Sort:
```c
for(int i = 0; i < n - 1; i++)
    for(int j = 0; j < n - i - 1; j++)
        if(p[j].bt > p[j + 1].bt) {
            tmp = p[j];
            p[j] = p[j + 1];
            p[j + 1] = tmp;
        }
```

Kode di atas merupakan sorting proses menggunakan *bubble sort*  
dengan mengurutkan proses berdasarkan burst time terkecil ke terbesar (*SJF*).  
Menggunakan Bubble Sort (sederhana untuk dataset kecil)  
*Kenapa sorting penting?* Karena SJF membutuhkan proses dengan bt terpendek dijalankan pertama.

---

#### Perhitungan CT, TAT, WT:
```c
ct += p[i].bt;
p[i].ct = p[i].tat = ct;
avgtat += p[i].tat;
p[i].wt = p[i].tat - p[i].bt;
avgwt += p[i].wt;
```
- *Completion Time (CT):* CT = CT sebelumnya + BT proses saat ini.  
- *Turn Around Time (TAT):* Karena arrival time (AT) = 0, maka TAT = CT.  
- *Waiting Time (WT):* WT = TAT - BT (waktu menunggu sebelum dieksekusi).  
- *Response Time (RT):* Pada non-preemptive, RT = WT karena proses tidak di-interrupt.

---

#### Output Tabel:
```c
printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
```

Output hasil dengan menampilkan tabel berisi:  
*ProcessNo | BT | CT | TAT | WT | RT*  
RT = WT karena non-preemptive  
Format \t digunakan untuk alignment tabel

---

#### Perhitungan Rata-rata:
```c
avgtat /= n;
avgwt /= n;
printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f", avgtat, avgwt);
```

Perhitungan rata rata avgtat dan avgwt diakumulasi selama iterasi, lalu dibagi jumlah proses (n). .2f untuk mencetak 2 angka di belakang koma.
Kenapa penting? Metrik untuk mengukur efisiensi scheduling.
  

- .2f untuk mencetak 2 angka di belakang koma.  
- *Kenapa penting?* Metrik untuk mengukur efisiensi scheduling.

---

## KESIMPULAN
Laporan ini menjelaskan implementasi algoritma Shortest Job First (SJF) Non-Preemptive tanpa memperhitungkan arrival time. Program menggunakan struktur data struct proc untuk menyimpan atribut proses seperti burst time, completion time, turnaround time, dan waiting time. Proses diurutkan berdasarkan burst time terkecil ke terbesar menggunakan Bubble Sort, memastikan proses dengan eksekusi terpendek dijalankan lebih dulu. Perhitungan metrik kinerja seperti turnaround time dan waiting time dilakukan secara akurat, dengan hasil ditampilkan dalam bentuk tabel. Kelebihan algoritma ini adalah kemampuannya meminimalkan waiting time untuk proses-proses pendek, sementara keterbatasannya terletak pada ketidakefisienan Bubble Sort untuk data besar dan ketidakmampuan menangani kasus dengan arrival time yang bervariasi. 

Secara keseluruhan, program berhasil mendemonstrasikan prinsip SJF Non-Preemptive dengan baik. Modularitas kode melalui fungsi read() memudahkan pengembangan lebih lanjut. Namun, untuk skenario dunia nyata yang lebih kompleks, diperlukan algoritma lain seperti SJF Preemptive atau Priority Scheduling yang mampu menangani arrival time dan interupsi proses. Hasil eksekusi program menunjukkan bahwa SJF Non-Preemptive efektif untuk kasus sederhana dengan burst time yang sudah diketahui sebelumnya.
