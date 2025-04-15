# Konsep Single Thread dan Multithread

##Penjelasan

**Single thread** adalah model eksekusi program di mana hanya satu urutan instruksi (thread) yang dijalankan dalam satu waktu. Dalam arsitektur ini, sebuah aplikasi bekerja secara linear dari awal hingga akhir tanpa adanya proses yang berjalan secara paralel. Jika sebuah proses sedang menunggu (seperti membaca file atau menerima input), maka seluruh aplikasi akan terhenti sampai proses tersebut selesai. Meskipun sederhana dan mudah diimplementasikan, pendekatan ini tidak memanfaatkan kemampuan prosesor modern yang biasanya memiliki banyak inti (multi-core).

Sebaliknya, **multithread** memungkinkan sebuah program menjalankan banyak thread secara bersamaan. Masing-masing thread dapat melakukan tugas yang berbeda secara paralel—misalnya, satu thread membaca file, sementara thread lain menampilkan data ke layar. Pendekatan ini sangat efisien pada komputer modern karena bisa mempercepat eksekusi program, meningkatkan responsivitas aplikasi, dan mengoptimalkan penggunaan CPU. Namun, pemrograman multithread memerlukan manajemen sinkronisasi data yang baik agar tidak terjadi konflik (*race condition*) saat beberapa thread mengakses data yang sama.

##Ilustrasi

![Single vs Multithread](https://github.com/Faridyanuar824/SisOp-2025/blob/main/img/Single%20Thread%20VS%20Multi%20Thread.png)  

