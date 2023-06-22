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
Hadoop adalah software open-source yang digunakan untuk menyimpan dan memproses data yang sangat besar di cluster komputer terdistribusi. Hadoop terdiri dari dua komponen utama yaitu Hadoop Distributed File System (HDFS) dan MapReduce. HDFS adalah sistem file terdistribusi yang dirancang untuk menyimpan data di berbagai node dalam sebuah cluster. Sedangkan MapReduce adalah model pemrograman yang digunakan untuk memproses data secara paralel di atas HDFS. 

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