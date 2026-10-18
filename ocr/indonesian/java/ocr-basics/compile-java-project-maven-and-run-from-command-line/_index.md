---
category: general
date: 2026-10-18
description: Kompilasi proyek Java Maven dan jalankan dari baris perintah menggunakan
  perintah Maven clean, compile, dan exec. Pelajari cara membangun dan menjalankan
  aplikasi Java secara efisien.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: id
lastmod: 2026-10-18
og_description: Kompilasi proyek Java dengan Maven dan jalankan dari command line
  dengan panduan langkah demi langkah. Kuasai perintah Maven clean compile run untuk
  membangun dan menjalankan aplikasi Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Kompilasi proyek Java Maven – jalankan dari baris perintah
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Kompilasi proyek Java Maven dan jalankan dari baris perintah
url: /id/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Kompilasi proyek java maven dan jalankan dari command line

Jika Anda perlu **compile java project maven** dan meluncurkan kelas yang dihasilkan langsung dari terminal, panduan ini menunjukkan cara melakukannya secara tepat. Pada akhir tutorial Anda akan dapat membersihkan artefak lama, mengkompilasi kode sumber, dan **execute java class command line** menggunakan satu rangkaian perintah Maven.

Tutorial ini mencakup semua yang perlu Anda ketahui untuk **build and run java app** dengan Maven, termasuk plugin yang diperlukan, jebakan umum, dan tips untuk shell berbasis Windows‑ dan Unix‑. Tidak diperlukan dokumentasi eksternal—cukup ikuti langkah‑langkah di bawah ini.

## Prasyarat

Sebelum Anda mulai, pastikan Anda memiliki:

* Java Development Kit (JDK) 8 atau yang lebih baru terpasang dan `JAVA_HOME` sudah diset.
* Apache Maven 3.6+ tersedia di `PATH` Anda.
* Proyek Maven yang berisi `pom.xml` dan kelas Java dengan metode `public static void main(String[] args)` (untuk contoh ini kelasnya adalah `com.aspose.ocr.examples.SimpleOcrDemo`).

## Kompilasi java project maven

Langkah pertama adalah menghapus semua kelas yang sebelumnya telah dikompilasi serta artefak build lainnya. Menjalankan `mvn clean` menjamin awal yang bersih dan mencegah bytecode usang menyebabkan kesalahan runtime.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Mengapa bersih?* Maven menyimpan kelas yang dikompilasi di `target/`. Jika Anda melewatkan fase clean, file `.class` lama dapat tetap ada dan menyembunyikan masalah kompilasi, terutama setelah melakukan refactoring nama paket.

## Eksekusi java class command line

Setelah pembersihan, kompilasi file sumber. Fase `compile` Maven menerjemahkan semua sumber `src/main/java` menjadi bytecode dan menempatkan hasilnya di `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Sekarang Anda memiliki output **maven compile source code** yang siap dijalankan. Perintah berikut menjalankan kelas yang telah dikompilasi tanpa memerlukan JAR terpisah.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Goal `exec:java` dari plugin **maven clean compile run** meluncurkan kelas yang ditentukan langsung dari direktori output yang telah dikompilasi. Ini adalah cara tercepat untuk **execute java class command line** selama pengembangan.

### Output yang diharapkan

Ketika demo berjalan dengan sukses Anda akan melihat sesuatu yang mirip dengan:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Jika Anda menerima `ClassNotFoundException`, periksa kembali nama kelas yang fully‑qualified dan pastikan berada di bawah `src/main/java`.

## Alur kerja Maven clean compile run

Menggabungkan ketiga perintah tersebut menghasilkan alur kerja yang ringkas dan dapat diulang:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Mengapa menggabungkannya?* Menggabungkan fase-fase tersebut menghilangkan kebutuhan menekan **Enter** tiga kali dan mengurangi kemungkinan melupakan langkah. Maven akan mengeksekusi fase-fase dalam urutan mereka muncul, menjamin build bersih sebelum eksekusi.

### Tips untuk alur kerja yang lebih lancar

| Tip | Description |
|-----|-------------|
| **Gunakan profil** | Definisikan profil Maven yang menggabungkan `clean`, `compile`, dan `exec:java` sehingga Anda dapat menjalankan `mvn demo` alih-alih mengetik seluruh rangkaian. |
| **Tambahkan opsi JVM** | Berikan `-Dexec.args="-Xmx512m"` untuk meningkatkan ukuran heap bagi aplikasi yang intensif memori. |
| **Lintas‑platform** | Di Windows gunakan `mvn.cmd` sementara shell Unix menggunakan `mvn`. Perintah yang sama bekerja di kedua lingkungan. |

## Bangun dan jalankan aplikasi java dengan Maven

Jika Anda lebih suka artefak yang dapat didistribusikan, Anda dapat membiarkan Maven mengemas kelas yang telah dikompilasi ke dalam JAR yang dapat dijalankan dan kemudian mengeksekusinya dengan perintah standar `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Pendekatan ini berguna ketika Anda perlu **build and run java app** pada server yang tidak memiliki Maven terpasang. Namun, untuk pengembangan cepat urutan **maven clean compile run** lebih cepat karena melewati langkah packaging.

## Maven compile source code – jebakan umum

Meskipun perintahnya sederhana, pengembang sering menghadapi masalah berikut:

1. **Missing `exec-maven-plugin`**  
   Jika Maven tidak dapat menemukan goal `exec:java`, tambahkan plugin ke `pom.xml` Anda:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven mengompilasi ke `target/classes`. Jika Anda memindahkan file secara manual atau mengubah direktori output default, goal `exec:java` mungkin tidak menemukan kelas Anda. Pertahankan layout default kecuali Anda memiliki alasan khusus untuk mengubahnya.

3. **Using the wrong JDK version**  
   Maven mewarisi JDK dari `JAVA_HOME`. Mengompilasi kode sumber dengan JDK 11 sementara menjalankan pada JDK 8 akan menyebabkan `UnsupportedClassVersionError`. Verifikasi versi JDK dengan `java -version` dan `mvn -v`.

4. **Shell quoting problems**  
   Pada Unix, bungkus nilai `-Dexec.mainClass` dengan tanda kutip tunggal jika mengandung karakter khusus:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Pada Windows, tanda kutip ganda berfungsi dengan baik.

Dengan menangani poin-poin ini Anda dapat secara andal **execute java class command line** di lingkungan apa pun.

## Tips pro: otomatisasi dengan skrip

Untuk tim yang sering membangun ulang demo, buat skrip shell atau batch kecil:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Buat dapat dieksekusi (`chmod +x run-demo.sh`) dan jalankan `./run-demo.sh`. Ini menghilangkan kesalahan pengetikan dan memastikan setiap pengembang mengikuti urutan **maven clean compile run** yang tepat.

## Kesimpulan

Anda sekarang tahu cara **compile java project maven** dan langsung **execute java class command line** menggunakan goal clean, compile, dan exec Maven. Alur kerja langkah‑demi‑langkah menjamin build yang bersih, menghilangkan artefak usang, dan memungkinkan Anda **build and run java app** dengan satu baris perintah.  

Selanjutnya, Anda dapat menjelajahi:

* Menambahkan **shade plugin** untuk menghasilkan uber‑JAR untuk deployment.  
* Mengonfigurasi profil Maven untuk lingkungan yang berbeda (dev, test, prod).  
* Mengintegrasikan unit test dengan `mvn test` sebelum langkah kompilasi.

Bereksperimenlah dengan variasi ini untuk menyesuaikan alur kerja ke dalam proyek Anda, dan Anda akan memiliki pipeline build yang kuat dan dapat diulang yang berfungsi di Windows, macOS, dan Linux. Selamat coding!

## Apa yang Harus Anda Pelajari Selanjutnya?

Tutorial berikut mencakup topik yang terkait erat yang membangun teknik yang ditunjukkan dalam panduan ini. Setiap sumber mencakup contoh kode lengkap yang berfungsi dengan penjelasan langkah‑demi‑langkah untuk membantu Anda menguasai fitur API tambahan dan mengeksplorasi pendekatan implementasi alternatif dalam proyek Anda sendiri.

- [Cara Menggunakan OCR di Java – Panduan Lengkap Langkah‑per‑Langkah](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Jalankan OCR pada Gambar dengan Java – Panduan Lengkap Aspose OCR](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Cara Melakukan OCR dengan Aspose OCR di Java – Panduan Langkah‑per‑Langkah](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}