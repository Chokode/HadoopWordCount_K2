# Wordcount Using Hadoop and Java 
# Introduction
ReadMe ini menyediakan penjelasan mengenai wordcount yang dijalankan pada dua software yaitu hadoop dan java. Kemudian, akan dibandingkan hasil runtime dari keduanya dan dari hasil eksperimen tersebut maka akan ditarik kesimpulan sesuai dengan hasil yang didapat. 

# Hadoop 
jelasin apa itu hadoop, metode word count nya gimana, instalasi nya gimana, how to use hadoop 
# Java 
jelasin apa itu java, metode wordcount nya gimana, kode nya apa 
# Java vs Hadoop 
jelasin gimana in theory java vs hadoop 
# Experiment 
Percobaan digunakan menggunakan 6 dataset dengan size sebagai berikut: 
- file 1 : 1 MB 
- file 2 : 10 MB 
- file 3 : 100 MB 
- file 4 : 1000 MB 
- file 5 : 5000 MB 
- file 6 : 10.000 MB 
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
Kita akan mengubah setiap file input dengan nama dan directory file yang kita gunakan. 

# Comparation
### Running Time Table 

| Data (MB) |         Time          |
|           | Hadoop   |   Java     |
|---------- |----------|------------|
|   1       |    14    |    0.198   |
|   10      |    25    |    0.567   |
|   100     |    26    |    1.389   |
|   1000    |    69    |    9.77    |
|   5000    |    296   |    120     |
|   10.000  |    831   |    213     |

### Graph 


# Kesimpulan 
