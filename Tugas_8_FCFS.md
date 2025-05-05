# LAPORAN SISTEM OPERASI  
## CPU SCHEDULING  

### Nama Anggota Kelompok:
- Farid Yanuar Hidayat (3124500032)
- Ahnaf Hafizh Putra Efendi (3124500033)

### Dosen Pengajar:
Dr. Ferry Astika Saputra ST, M.Sc

### PROGRAM STUDI D3 TEKNIK INFORMATIKA  
POLITEKNIK ELEKTRONIKA NEGERI SURABAYA (PENS)  
TAHUN 2024  

---

## CODE

### FCFS With Arrival Time

```c
#include<stdio.h>
struct proc { int no, at, bt, ct, tat, wt; };
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    printf("Enter Arrival Time: ");
    scanf("%d", &p.at);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    p.no = i;
    return p;
}
int main() {
    struct proc p[10], tmp;
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;
    printf("<--FCFS Scheduling Algorithm (Non-Preemptive)-->
");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) p[i] = read(i+1);
    for (int i = 0; i < n-1; i++)
        for (int j = 0; j < n-i-1; j++)
            if (p[j].at > p[j+1].at) {
                tmp = p[j];
                p[j] = p[j+1];
                p[j+1] = tmp;
            }
    printf("\nProcessNo\tAT\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        ct += p[i].bt;
        p[i].ct = ct;
        p[i].tat = p[i].ct - p[i].at;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].at, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }
    avgtat /= n; avgwt /= n;
    printf("\nAverage TurnAroundTime= %f\nAverage WaitingTime= %f", avgtat, avgwt);
}
```

### FCFS Without Arrival Time

```c
#include<stdio.h>
struct proc { int no, bt, ct, tat, wt; };
struct proc read(int i) {
    struct proc p;
    printf("\nProcess No: %d\n", i);
    printf("Enter Burst Time: ");
    scanf("%d", &p.bt);
    p.no = i;
    return p;
}
int main() {
    struct proc p[10];
    float avgtat = 0, avgwt = 0;
    int n, ct = 0;
    printf("<--FCFS Scheduling Algorithm Without Arrival Time (Non-Preemptive)-->
");
    printf("Enter Number of Processes: ");
    scanf("%d", &n);
    for (int i = 0; i < n; i++) p[i] = read(i+1);
    printf("\nProcessNo\tBT\tCT\tTAT\tWT\tRT\n");
    for (int i = 0; i < n; i++) {
        ct += p[i].bt;
        p[i].ct = p[i].tat = ct;
        avgtat += p[i].tat;
        p[i].wt = p[i].tat - p[i].bt;
        avgwt += p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\n", p[i].no, p[i].bt, p[i].ct, p[i].tat, p[i].wt, p[i].wt);
    }
    avgtat /= n; avgwt /= n;
    printf("\nAverage TurnAroundTime= %f\nAverage WaitingTime= %f", avgtat, avgwt);
}
```

---

## HASIL
- **FFCS With Arrival Time**
- ![Single vs Multithread](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/FFCS%20With%20Arrival%20Time%20.png)  
- **FFCS Without Arrival Time**
- ![Single vs Multithread](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/FFCS%20Without%20Arrival%20Time%20.png)  

*(Tambahkan hasil screenshot/hasil running di sini jika perlu)*

---

## ANALISA CODE

### FCFS With Arrival Time
- **Struct `proc`**: Menyimpan data proses (nomor, arrival time, burst time, completion time, turnaround time, waiting time).
- **Fungsi `read`**: Membaca input dari pengguna.
- **Sorting**: Proses diurutkan berdasarkan arrival time menggunakan bubble sort.
- **Perhitungan**: Completion time, Turnaround time, Waiting time, Response time.
- **Output**: Menampilkan tabel hasil.

### FCFS Without Arrival Time
- Sama seperti di atas, tanpa sorting arrival time.
- CT, TAT langsung dihitung berurutan sesuai urutan input.

---

## KESIMPULAN

- **FCFS With Arrival Time**: Lebih kompleks karena mempertimbangkan waktu kedatangan.
- **FCFS Without Arrival Time**: Lebih sederhana, cocok untuk sistem batch di mana semua proses tersedia sejak awal.

Perhitungan WT = TAT - BT berlaku di kedua metode.

---

## 📅 Tahun Ajaran 2024  
D3 Teknik Informatika PENS
