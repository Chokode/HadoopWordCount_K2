# Wordcount Using Hadoop and Java 
Kelompok 2
- Eldisja Hadasa - 2106640133
- Handaneswari Pramudhyta Imanda - 2106731346
- Syauqi Auliya Muhammad - 2106707201
- Muhammad Aqil Muzakky - 2106731604
</br>

# Introduction
ReadMe ini menyediakan penjelasan mengenai wordcount yang dijalankan pada dua software yaitu hadoop dan java. Kemudian, akan dibandingkan hasil runtime dari keduanya dan dari hasil eksperimen tersebut maka akan ditarik kesimpulan sesuai dengan hasil yang didapat. 

# Hadoop 
Hadoop adalah software open-source yang digunakan untuk menyimpan dan memproses data yang sangat besar di cluster komputer terdistribusi. Hadoop terdiri dari dua komponen utama yaitu Hadoop Distributed File System (HDFS) dan MapReduce. HDFS adalah sistem file terdistribusi yang dirancang untuk menyimpan data di berbagai node dalam sebuah cluster. Sedangkan MapReduce adalah model pemrograman yang digunakan untuk memproses data secara paralel di atas HDFS. Wordcount adalah program contoh dalam lingkungan Hadoop yang digunakan untuk menghitung jumlah kata dalam teks. Prosesnya dimulai dengan membagi teks input menjadi blok-blok kecil yang ditangani oleh node-node dalam klaster Hadoop. Setiap node melakukan tugas mapping dengan memisahkan teks menjadi kata-kata dan menghasilkan pasangan (key, value) di mana kata adalah kunci sementara dan nilai adalah 1. Hasil mapping dikumpulkan dan disusun ulang berdasarkan kunci. Kemudian, node-node reducer menggabungkan nilai-nilai untuk setiap kunci yang sama dan menghasilkan pasangan (key, total_count) di mana kunci adalah kata dan total_count adalah jumlah kemunculan kata tersebut dalam teks. Proses ini dilakukan secara terdistribusi di klaster Hadoop, memanfaatkan paralelisme dan distribusi untuk mempercepat penghitungan jumlah kata.

# Java 
Java adalah bahasa pemrograman dengan pendekatan WORA "write once, run everywhere" yang menyebabkan bahasa ini bersifat platform independen. Selain itu, java memiliki memori yang terkelola dengan baik, karena alokasi dan dealokasi memori dilakukan secara otomatis. Pada perbandingan kali ini, wordcount dilakukan dengan looping pada program.<br> 
Berikut ini langkah-langkah looping untuk wordcount pada Java. <br>
1. Menghitung banyaknya baris pada file.
2. Memecah setiap baris yang ada menjadi banyak kata.
3. Menghitung banyaknya kata pada setiap baris.
4. Menghitung banyaknya karakter pada sebuah kata.
5. Mengulangi dari langkah 2 sampai semua kata selesai dihitung.<br>

Setelah wordcount selesai dilakukan, runningtime dari program dihitung dengan cara mengurangi waktu dimulainya program dengan waktu selesainya program.


# Java vs Hadoop 
Java berfokus pada pengembangan aplikasi yang portabel, skalabel, dan mudah dipelihara. Karena karakteristiknya yang bersifat platform independen, Java dapat digunakan untuk mengembangkan berbagai jenis aplikasi, contohnya aplikasi desktop, web, mobile, dan game. Sedangkan, Hadoop berfokus pada pemrosesan data terdistribusi yang scalable dan efisien. Hal ini dikarenakan Hadoop dirancang khusus untuk memproses dan menganalisis data dengan volume besar dan kompleks. <br>

# Tahapan Instalasi Hadoop
Hadoop merupakan pertama
1. Membuka terminal dan menginstall hadoop menggunakan homebrew 
<img width="571" alt="Screenshot 2023-06-24 at 23 07 31" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/cb7759c2-5fc6-40b6-b56e-7200a7dee4ec">

2. Mencari pathway meuju JavaVirtualMachine
 <img width="554" alt="Screenshot 2023-06-24 at 23 08 47" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/b229bfb5-57eb-4f26-826a-2fb5a701207e">

3. Mendisplay files dalam directory hadoop yang telah didownload
<img width="598" alt="Screenshot 2023-06-24 at 23 12 32" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/07ddb7be-4447-4853-9d6e-9bf1c221f676">

4. Mengimport JavaHome sesuai dengan pathway JavaVirtualMachine dalam file hadoop-env.sh
<img width="543" alt="Screenshot 2023-06-24 at 23 17 00" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/2be749fd-8a6e-45a0-8e29-074d0b8a3ec9">

5. Mengubah konfigurasi core file core-site.xml
<img width="566" alt="Screenshot 2023-06-24 at 23 20 55" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/0738d923-592f-4cf7-b2a2-2ce2168fbf9d">

6. Mengubah konfigurasi core file hdfs-site.xml
<img width="607" alt="Screenshot 2023-06-24 at 23 21 18" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/97c1c5ab-1754-4bfe-a2c5-689adf81f057">

7. Mengubah konfigurasi core file mapred-site.xml
<img width="593" alt="Screenshot 2023-06-24 at 23 22 15" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/d5e30f8e-4952-4521-a6d5-a8aaecbaf17f">

8. Mengubah konfigurasi core file yarn-site.xml
<img width="758" alt="Screenshot 2023-06-24 at 23 22 56" src="https://github.com/Chokode/HadoopWordCount_K2/assets/134858335/38bd9b9a-bf0b-45cf-b8be-cfe91f178a43">





# Experiment 
Percobaan digunakan menggunakan 6 dataset dengan size sebagai berikut: 
- file 1 : 1 MB 
- file 2 : 10 MB 
- file 3 : 100 MB 
- file 4 : 1000 MB 
- file 5 : 5000 MB 
- file 6 : 10.000 MB <br>

Untuk mendapatkan file tersbut, digunakan aplikasi DontRunItWillOverloadTxt. Aplikasi tersebut dapat membuat text file sesuai ukuran yang kita inginkan. 
### Eksperimen Hadoop
Pertama-tama, kita harus memastikan bahwa file-file yang akan digunakan untuk eksperimen sudah berada pada folder yang benar. Berikut contoh directory dari salah satu file yang akan digunakan dalam eksperimen ini: 
> \\wsl.localhost\Ubuntu-20.04\home\handaneswari\hadoop\hadoop-3.3.2
Kemudian kita akan menjalankan beberapa command agar wordcount pada hadoop berjalan: 
```
hdfs dfs -put seribu.tut inpd output
hdfs dfs -put seribu.txt input
cd $HADOOP_HOME
bin/yarn jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.2.jar wordcount input output
hdfs dfs -cat output/part-r-00000

```
Pada kode diatas digunakan file seribu.txt sebesar 1000 MB sebagai contoh. Pada line pertama kita akan memindahkan file seribu.txt menjadi input dari program dan mejadikan outputnya dengan nama seribu.txt. Kemduian kita akan menjalankan program wordcount pada input dan menyimpan hasilnya pada directory output yang sudah kita set sebelumnya. 
Perlu diketahui bahwa kita tidak bisa menggunakan output dengan nama file yang sama. Jika ingin memberi nama output dengan nama yang sama, maka kita harus menggunakan command : 
```
hdfs dfs -rm -r output
```
### Eksperimen Java 
Untuk eksperimen java, digunakan kode sebagai berikut : 
```
import java.io.BufferedReader;
import java.io.FileReader;
import java.io.IOException;

public class FileCounter {
    public static void main(String[] args) {
        String filename = "onegb.txt"; // Replace with the actual file name

        long startTime = System.currentTimeMillis();

        int lineCount = 0;
        int wordCount = 0;
        int charCount = 0;

        try (BufferedReader br = new BufferedReader(new FileReader(filename))) {
            String line;
            while ((line = br.readLine()) != null) {
                lineCount++;
                String[] words = line.trim().split("\\s+");
                wordCount += words.length;
                charCount += line.length();
            }
        } catch (IOException e) {
            e.printStackTrace();
        }

        long endTime = System.currentTimeMillis();
        long runningTime = endTime - startTime;

        System.out.println("Number of lines: " + lineCount);
        System.out.println("Number of words: " + wordCount);
        System.out.println("Number of characters: " + charCount);
        System.out.println("Running time: " + runningTime + " milliseconds");
    }
}

```
Dari kode tersebut, kita hanya perlu mengubah nama file sesuai dengan yang ingin diuji. 

# Comparation
### Running Time Table 

|     Data (MB)      | Hadoop   |   Java     |
|---------- |----------|------------|
|   1       |    14    |    0.208   |
|   10      |    25    |    0.409   |
|   100     |    26    |    2.075   |
|   1000    |    69    |    28.359  |
|   5000    |    296   |    120     |
|   10.000  |    831   |    213     |


### Graph 
Berikut grafik yang dibuat berdasarkan data percobaan yang telah dilakuakn : 
![Hadoop (S) and Java (S) ](https://github.com/Chokode/HadoopWordCount_K2/assets/88542494/736e204a-e9df-4b99-aaca-252b30e277fa)

# Analysis
Dari hasil yang didapatkan dapat dilihat peforma runtime Java jauh lebih cepat daripada Hadoop. Hal ini dikarenakan hadoop selalu menginisialisasi cluster, penjadwalan tugas, dan overhead komunikasi antar node. Sehingga, terjadi delay yang signifikan pada runtime relatif terhadap ukuran data yang sebenarnya. Mekanisme penyimpanan dan pembagian hadoop yang mengharuskan data  dipartisi dan didistribusikan di antara beberapa node juga menyebabkan overhead dan memperlambat runtime program.

Berbeda dengan hadoop, Java memiliki pendekatan sekuensial dalam eksekusi kode. Pemrosesan sekuensial adalah pemrosesan data secara berurutan, tanpa overhead tambahan yang terkait dengan pemrosesan data terdistribusi. Oleh karena itu, wordcount pada kasus ini lebih cepat menggunakan Java karena file-file yang digunakan ukurannya relatif kecil untuk diproses dengan Hadoop.

# Conclusion 
Pada kasus kali ini, wordcount lebih cepat dilakukan oleh Java daripada Hadoop. Hal ini disebabkan oleh overhead konfigurasi pada Hadoop yang disebabkan ukuran file dianggap relatif kecil oleh Hadoop. Sehingga, overhead untuk inisialisasi dan penjadwalan task MapReduce pada Hadoop lebih terasa serta membuat peforma Hadoop lebih lambat dibandingkan dengan Java yang menggunakan pendekatan sekuensial.
