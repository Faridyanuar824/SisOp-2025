# LAPORAN SISTEM OPERASI  
## SJF SCHEDULING WITH ARRIVAL TIME

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
1. yang ada di ppt Ch5
   ![Image](https://github.com/user-attachments/assets/2952e3bc-965a-410d-af73-d1d43ecf8c44)
   ![Image](https://github.com/user-attachments/assets/d7c3d5f6-7cd1-49f6-9f5f-52aa8f727fa3)
2. yang ditampilkan di layar
   ![Image](https://github.com/user-attachments/assets/126b3b96-7ee8-4a51-80df-5042a0203a51)
   ![Image](https://github.com/user-attachments/assets/76e2600a-127f-46cd-9155-b87c38ea22e2)

---

## ANALISA CODE  
### SJF With Arrival Time

#### Deklarasi Struct:
```c
#include<stdio.h>
struct proc
{
    int no,at,bt,it,ct,tat,wt;
};
```

No : nomor proses (P1,P2,dst)
At : Arrival Time (waktu kedatangan proses)
Bt : Burst Time (waktu eksekusi proses)
It : Internal Time (waktu mulai eksekusi)
Ct : Completion Time (waktu selesai eksekusi)
Tat : Turn Around Time (waktu total dari kedatangan sampai selesai)
Wt : Waiting Time (waktu menunggu sebelum dieksekusi)
 

---

#### Fungsi Input:
```c
struct proc read(int i)
{
    struct proc p;
    printf("\nProcess No: %d\n",i);
    p.no=i;
    printf("Enter Arrival Time: ");
    scanf("%d",&p.at);
    printf("Enter Burst Time: ");
    scanf("%d",&p.bt);
    return p;
}
```

Fungsi code diatas berfungsi :
Menerima input dari user untuk arrival time dan burst time
Mengembalikan struct proc yang sudah diisi


---

#### Input Proses:
```c
    for(int i=0;i<n;i++)
        p[i]=read(i+1);
```

untuk code diatas merupakan input proses untuk mengisi array proses dengan memanggil fungsi read() kemudian nomor proses dimulai dari 1 ( i + 1 )

---

#### Sorting
```c
    for(int i=0;i<n-1;i++)
        for(j=0;j<n-i-1;j++)    
            if(p[j].at>p[j+1].at)
            {
            temp=p[j];
            p[j]=p[j+1];
            p[j+1]=temp;
            }
```

Untuk code diatas merupakan sorting berdasarkan arrival time menggunakan bubble sort untuk mengurutkan proses berdasarkan arrival time

---

#### Seleksi Proses Pertama:
```c
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
```


untuk code diatas merupakan seleksi proses pertama memilih proses dengan burst time terpendek diantara proses yang datang bersamaan diawal ( memastikan sjf dimulai dari proses terpendek yang datang pertama )

---

#### Initialisasi Proses Pertama:
```c
    p[0].it=p[0].at;
    p[0].ct=p[0].it+p[0].bt;
```


inisialisasi proses pertama dimana proses pertama langsung dieksekusi saat datang it ( waktu mulai ), ct ( waktu mulai + burst time )

---

```c
        for(j=i+1,min=i;j<n&&p[j].at<=p[i-1].ct;j++)
            if(p[j].bt<p[min].bt)
                min=j;
        temp=p[i];
        p[i]=p[min];
        p[min]=temp;
        if(p[i].at<=p[i-1].ct)
            p[i].it=p[i-1].ct;
        else
            p[i].it=p[i].at;
        p[i].ct=p[i].it+p[i].bt;
    }
```

Code diatas merupakan Penjadwalan Proses Berikutnya dengan mencari proses dengan burst time terpendek yang sudah datang, menukar proses ke posisi saat ini, menghitung waktu mulai dan selesai

---

```c
    for(int i=0;i<n;i++)
    {
        p[i].tat=p[i].ct-p[i].at;
        avgtat+=p[i].tat;
        p[i].wt=p[i].tat-p[i].bt;
        avgwt+=p[i].wt;
        printf("P%d\t\t%d\t%d\t%d\t%d\t%d\t%d\n",p[i].no,p[i].at,p[i].bt,p[i].ct,p[i].tat,p[i].wt,p[i].wt);
    }
    avgtat/=n,avgwt/=n;
```


Code diatas merupakan perhitungan metrik dengan perhitungannya seperti berikut : 
TAT = Completion Time - Arrival Time, WT = TAT - Burst Time, RT = WT (untuk non-preemptive)

---

```c
    printf("\nAverage TurnAroundTime=%f\nAverage WaitingTime=%f",avgtat,avgwt);
}
```


Output dengan format output jelas dan terstruktur, menampilkan semua metrik penting, rata-rata membantu analisis performa algoritma

  
---

## KESIMPULAN
Laporan ini membahas implementasi algoritma penjadwalan Shortest Job First (SJF) dengan mempertimbangkan waktu kedatangan (arrival time) pada sistem operasi. Algoritma ini bekerja secara non-preemptive, di mana proses dengan burst time terpendek diprioritaskan untuk dieksekusi terlebih dahulu. Kode program yang dikembangkan menggunakan bahasa C dan mencakup fitur seperti pengurutan proses berdasarkan arrival time, pemilihan proses dengan burst time terpendek, serta perhitungan metrik kinerja seperti turnaround time, waiting time, dan response time. Hasil pengujian menunjukkan bahwa algoritma ini mampu mengoptimalkan waktu tunggu dan waktu penyelesaian proses, yang terlihat dari nilai rata-rata turnaround time dan waiting time yang dihasilkan. 

Secara keseluruhan, laporan ini berhasil mendemonstrasikan cara kerja algoritma SJF dengan arrival time secara jelas dan terstruktur. Analisis kode yang disertakan membantu memahami setiap tahapan, mulai dari input proses, pengurutan, penjadwalan, hingga perhitungan metrik. Dengan demikian, laporan ini tidak hanya memberikan pemahaman teoritis tetapi juga praktis tentang implementasi algoritma penjadwalan SJF dalam konteks nyata. Hasil ini dapat menjadi referensi berguna untuk pengembangan sistem operasi atau aplikasi lain yang memerlukan manajemen proses yang efisien.
