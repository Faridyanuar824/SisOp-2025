# Programming Exercise - Chapter 4 (Threading)

Referensi: [GitHub Repository OSC10E Chapter 4](https://github.com/ferryastika/osc10e/tree/master/ch4)

## A. Penerapan Thread pada Contoh `SumTask.java` (Java)

### Penjelasan

# Esai: Penerapan Thread pada Java, Linux (POSIX), dan Windows

Dalam pengembangan perangkat lunak modern, penggunaan *multithreading* menjadi hal yang sangat penting, terutama untuk meningkatkan performa aplikasi dalam memanfaatkan kemampuan prosesor multicore. Pada bab ini, kita membandingkan dan mempelajari implementasi *thread* dalam tiga platform pemrograman yang berbeda: Java (SumTask), Linux (POSIX thread), dan Windows (Win32 API).

## 1. Penerapan Thread di Java: SumTask.java

Java merupakan bahasa pemrograman berorientasi objek yang menyediakan dukungan multithreading secara langsung melalui kelas `Thread` dan antarmuka `Runnable`. Contoh `SumTask.java` merupakan ilustrasi sederhana dari bagaimana Java memanfaatkan *thread* untuk melakukan pembagian pekerjaan dalam proses perhitungan total elemen array.

Dalam implementasi ini, array dibagi menjadi beberapa bagian, dan setiap bagian dihitung oleh sebuah *thread* yang berjalan secara paralel. Dengan demikian, perhitungan dapat diselesaikan lebih cepat dibandingkan jika dilakukan secara linear (satu proses tunggal).

Kelebihan utama dari pendekatan ini adalah kemudahan dalam penggunaan dan portabilitas yang tinggi. Java menyembunyikan detail teknis dari sistem operasi sehingga developer dapat fokus pada logika program tanpa harus memahami detail *thread management* seperti pada bahasa tingkat rendah.

# Program Java: SumTask.java

Program ini menunjukkan cara menggunakan thread untuk menjumlahkan elemen array secara paralel menggunakan `Callable` dan `ExecutorService` di Java.

```java
import java.util.concurrent.*;

public class SumTask implements Callable<Long> {
    private int[] array;
    private int start, end;

    public SumTask(int[] array, int start, int end) {
        this.array = array;
        this.start = start;
        this.end = end;
    }

    @Override
    public Long call() {
        long sum = 0;
        for (int i = start; i < end; i++) {
            sum += array[i];
        }
        return sum;
    }

    public static void main(String[] args) throws InterruptedException, ExecutionException {
        int[] array = new int[1000000];
        for (int i = 0; i < array.length; i++) {
            array[i] = 1; // simplifikasi agar hasil diketahui: 1 juta
        }

        int numThreads = 4;
        ExecutorService executor = Executors.newFixedThreadPool(numThreads);
        Future<Long>[] results = new Future[numThreads];

        int chunkSize = array.length / numThreads;
        for (int i = 0; i < numThreads; i++) {
            int start = i * chunkSize;
            int end = (i == numThreads - 1) ? array.length : start + chunkSize;
            results[i] = executor.submit(new SumTask(array, start, end));
        }

        long total = 0;
        for (Future<Long> result : results) {
            total += result.get();
        }

        executor.shutdown();

        System.out.println("Total sum: " + total);
    }
}
```
## B. Penerapan Thread di Linux (thrd-posix.c) dan Windows (thrd-win32.c)

## 2. Penerapan Thread di Linux: POSIX (thrd-posix.c)

Pada sistem Linux, pembuatan *thread* biasanya dilakukan dengan menggunakan pustaka **POSIX Threads** atau sering disingkat **pthreads**. Dalam contoh `thrd-posix.c`, sebuah thread dibuat dengan fungsi `pthread_create`, kemudian dieksekusi bersamaan dengan thread utama. Setelah selesai, `pthread_join` digunakan untuk menunggu hingga thread tersebut selesai sebelum program utama melanjutkan proses.

POSIX thread menawarkan kontrol lebih rinci dibanding Java. Programmer dapat mengatur atribut thread seperti prioritas, ukuran stack, dan kebijakan penjadwalan. Hal ini membuat pthreads sangat cocok untuk aplikasi yang membutuhkan efisiensi tinggi dan pengelolaan sumber daya secara manual, seperti pada aplikasi server, sistem real-time, atau embedded systems.

Namun, karena menggunakan bahasa C dan membutuhkan manajemen memori secara manual, penggunaan POSIX threads memiliki kompleksitas lebih tinggi dan rentan terhadap kesalahan seperti race condition atau deadlock jika tidak dikelola dengan baik.

## 3. Penerapan Thread di Windows: Win32 API (thrd-win32.c)

Sementara itu, pada platform Microsoft Windows, pembuatan *thread* dilakukan menggunakan **Win32 API**. Contoh `thrd-win32.c` menunjukkan bahwa sebuah thread dapat dibuat melalui fungsi `CreateThread`. Setelah thread dibuat, program utama dapat menggunakan `WaitForSingleObject` untuk menunggu hingga thread selesai dieksekusi.

Seperti POSIX, Win32 API memberikan kontrol penuh terhadap pengelolaan thread, termasuk pengaturan prioritas, kontrol sinkronisasi, dan akses ke fitur-fitur lain seperti *mutex*, *semaphore*, dan *event*. Namun, penggunaan API Windows bersifat spesifik terhadap sistem operasi Windows, sehingga portabilitasnya sangat rendah dibanding Java maupun POSIX.

Meskipun kuat dan fleksibel, pengembangan aplikasi berbasis Win32 API membutuhkan pemahaman mendalam mengenai sistem operasi Windows dan struktur internalnya. Oleh karena itu, API ini umumnya digunakan dalam aplikasi desktop tingkat lanjut atau sistem backend berbasis Windows.

## Kesimpulan

Ketiga pendekatan implementasi thread yang dibahas di atas memiliki kelebihan dan kekurangan masing-masing. Java menawarkan kemudahan dan portabilitas tinggi, cocok untuk pemula maupun pengembangan aplikasi yang dapat berjalan di berbagai platform. POSIX thread di Linux memberikan kontrol penuh dan efisiensi tinggi, sangat cocok untuk aplikasi sistem dan performa tinggi. Sedangkan Win32 API di Windows memberikan akses mendalam terhadap pengelolaan proses dan thread, meskipun hanya berjalan di lingkungan Windows.

Pemilihan teknologi yang digunakan sangat bergantung pada kebutuhan aplikasi, target platform, serta pengalaman dari pengembang itu sendiri. Pemahaman terhadap perbedaan ini penting agar kita dapat memilih strategi multithreading yang paling tepat untuk proyek yang sedang dikembangkan.

## Perbandingan Singkat

| Aspek         | Java (`SumTask`)        | Linux (`pthread`)         | Windows (`CreateThread`)    |
|---------------|--------------------------|----------------------------|------------------------------|
| Portabilitas  | Tinggi (cross-platform)  | Tinggi di Unix/Linux       | Terbatas ke Windows          |
| Kemudahan     | Sangat mudah             | Sedang                     | Cukup kompleks               |
| Performa      | Baik                     | Sangat baik                | Sangat baik                  |
| Kontrol       | Terbatas                 | Detail & fleksibel         | Detail & fleksibel           |

---
