---
category: general
date: 2026-10-18
description: Biên dịch dự án Java Maven và chạy từ dòng lệnh bằng các lệnh Maven clean,
  compile và exec. Tìm hiểu cách xây dựng và chạy ứng dụng Java một cách hiệu quả.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: vi
lastmod: 2026-10-18
og_description: Biên dịch dự án Java Maven và chạy từ dòng lệnh với hướng dẫn từng
  bước. Thành thạo lệnh Maven clean compile run để xây dựng và chạy ứng dụng Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Biên dịch dự án Java Maven – chạy từ dòng lệnh
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
title: Biên dịch dự án Java Maven và chạy từ dòng lệnh
url: /vi/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Biên dịch dự án java bằng Maven và chạy từ dòng lệnh

Nếu bạn cần **compile java project maven** và khởi chạy lớp kết quả trực tiếp từ terminal, hướng dẫn này sẽ chỉ cho bạn cách thực hiện. Khi kết thúc tutorial, bạn sẽ có thể làm sạch các artifact cũ, biên dịch mã nguồn, và **execute java class command line** bằng một chuỗi lệnh Maven duy nhất.

Tutorial này bao phủ mọi thứ bạn cần biết để **build and run java app** với Maven, bao gồm các plugin cần thiết, những khó khăn thường gặp, và các mẹo cho shell dựa trên Windows và Unix. Không cần tài liệu bên ngoài—chỉ cần làm theo các bước dưới đây.

## Yêu cầu trước

* Java Development Kit (JDK) 8 hoặc mới hơn đã được cài đặt và `JAVA_HOME` được thiết lập.
* Apache Maven 3.6+ có sẵn trên `PATH` của bạn.
* Một dự án Maven chứa `pom.xml` và một lớp Java có phương thức `public static void main(String[] args)` (đối với ví dụ này lớp là `com.aspose.ocr.examples.SimpleOcrDemo`).

## Biên dịch dự án java bằng Maven

Bước đầu tiên là loại bỏ bất kỳ lớp đã biên dịch trước đó và các artifact xây dựng khác. Chạy `mvn clean` đảm bảo khởi đầu sạch sẽ và ngăn chặn bytecode cũ gây lỗi thời gian chạy.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*​Tại sao phải clean?* Maven lưu các lớp đã biên dịch trong `target/`. Nếu bạn bỏ qua giai đoạn clean, các file `.class` cũ có thể còn lại và che giấu các vấn đề biên dịch, đặc biệt sau khi đổi tên package.

## Thực thi lớp Java từ dòng lệnh

Sau khi clean, biên dịch các file nguồn. Giai đoạn `compile` của Maven chuyển tất cả các nguồn `src/main/java` thành bytecode và đặt kết quả vào `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Bây giờ bạn đã có đầu ra **maven compile source code** sẵn sàng để thực thi. Lệnh tiếp theo chạy lớp đã biên dịch mà không cần JAR riêng.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Mục tiêu `exec:java` của plugin **maven clean compile run** khởi chạy lớp được chỉ định trực tiếp từ thư mục đầu ra đã biên dịch. Đây là cách nhanh nhất để **execute java class command line** trong quá trình phát triển.

### Đầu ra mong đợi

Khi demo chạy thành công, bạn sẽ thấy một thứ gì đó tương tự như:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Nếu bạn nhận được `ClassNotFoundException`, hãy kiểm tra lại tên lớp đầy đủ và đảm bảo nó nằm dưới `src/main/java`.

## Quy trình Maven clean compile run

Kết hợp ba lệnh lại với nhau tạo ra một quy trình ngắn gọn, có thể lặp lại:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*​Tại sao phải chuỗi chúng lại?* Kết hợp các giai đoạn loại bỏ nhu cầu nhấn **Enter** ba lần và giảm khả năng quên bước. Maven sẽ thực thi các giai đoạn theo thứ tự chúng xuất hiện, đảm bảo một bản dựng sạch trước khi thực thi.

### Mẹo để quy trình mượt mà hơn

| Mẹo | Mô tả |
|-----|-------|
| **Use a profile** | Định nghĩa một profile Maven gộp `clean`, `compile`, và `exec:java` để bạn có thể chạy `mvn demo` thay vì gõ toàn bộ chuỗi. |
| **Add JVM options** | Truyền `-Dexec.args="-Xmx512m"` để tăng kích thước heap cho các ứng dụng tiêu tốn nhiều bộ nhớ. |
| **Cross‑platform** | Trên Windows dùng `mvn.cmd` trong khi shell Unix dùng `mvn`. Lệnh này hoạt động trong cả hai môi trường. |

## Xây dựng và chạy ứng dụng Java với Maven

Nếu bạn muốn một artifact có thể phân phối, bạn có thể để Maven đóng gói các lớp đã biên dịch của bạn thành một JAR có thể chạy và sau đó thực thi nó bằng lệnh chuẩn `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Cách tiếp cận này hữu ích khi bạn cần **build and run java app** trên máy chủ không có Maven. Tuy nhiên, cho phát triển nhanh, chuỗi **maven clean compile run** nhanh hơn vì nó bỏ qua bước đóng gói.

## Maven compile source code – những khó khăn thường gặp

Mặc dù các lệnh đơn giản, các nhà phát triển thường gặp phải các vấn đề sau:

1. **Missing `exec-maven-plugin`**  
   Nếu Maven không thể tìm thấy mục tiêu `exec:java`, hãy thêm plugin vào `pom.xml` của bạn:

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
   Maven biên dịch vào `target/classes`. Nếu bạn tự di chuyển file hoặc thay đổi thư mục đầu ra mặc định, mục tiêu `exec:java` có thể không tìm thấy lớp của bạn. Giữ layout mặc định trừ khi bạn có lý do cụ thể để thay đổi.

3. **Using the wrong JDK version**  
   Maven kế thừa JDK từ `JAVA_HOME`. Biên dịch mã nguồn JDK 11 trong khi chạy trên JDK 8 sẽ gây ra `UnsupportedClassVersionError`. Xác minh phiên bản JDK bằng `java -version` và `mvn -v`.

4. **Shell quoting problems**  
   Trên Unix, bao quanh giá trị `-Dexec.mainClass` bằng dấu nháy đơn nếu nó chứa ký tự đặc biệt:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Trên Windows, dấu nháy kép hoạt động tốt.

Bằng cách giải quyết các điểm này, bạn có thể đáng tin cậy **execute java class command line** trong bất kỳ môi trường nào.

## Mẹo chuyên nghiệp: tự động hoá bằng script

Đối với các nhóm thường xuyên xây dựng lại demo, tạo một script shell hoặc batch nhỏ:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Đánh dấu nó là thực thi (`chmod +x run-demo.sh`) và chạy `./run-demo.sh`. Điều này loại bỏ lỗi gõ và đảm bảo mọi nhà phát triển tuân theo chuỗi **maven clean compile run** chính xác.

## Kết luận

Bây giờ bạn đã biết cách **compile java project maven** và ngay lập tức **execute java class command line** bằng cách sử dụng các mục tiêu clean, compile và exec của Maven. Quy trình từng bước đảm bảo một bản dựng sạch, loại bỏ các artifact cũ, và cho phép bạn **build and run java app** bằng một dòng lệnh duy nhất.  

Tiếp theo, bạn có thể khám phá:

* Thêm **shade plugin** để tạo một uber‑JAR cho việc triển khai.  
* Cấu hình các profile Maven cho các môi trường khác nhau (dev, test, prod).  
* Tích hợp các unit test với `mvn test` trước bước biên dịch.

Thử nghiệm các biến thể này để phù hợp quy trình với dự án của bạn, và bạn sẽ có một pipeline xây dựng mạnh mẽ, có thể lặp lại, hoạt động trên Windows, macOS và Linux. Chúc lập trình vui vẻ!

## Bạn nên học gì tiếp theo?

Các tutorial sau đây bao phủ các chủ đề liên quan chặt chẽ, xây dựng trên các kỹ thuật được trình bày trong hướng dẫn này. Mỗi tài nguyên bao gồm các ví dụ mã hoạt động đầy đủ với giải thích từng bước để giúp bạn làm chủ các tính năng API bổ sung và khám phá các cách triển khai thay thế trong dự án của mình.

- [Cách sử dụng OCR trong Java – Hướng dẫn chi tiết từng bước](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Chạy OCR trên hình ảnh với Java – Hướng dẫn Aspose OCR đầy đủ](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Cách thực hiện OCR với Aspose OCR trong Java – Hướng dẫn chi tiết từng bước](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}