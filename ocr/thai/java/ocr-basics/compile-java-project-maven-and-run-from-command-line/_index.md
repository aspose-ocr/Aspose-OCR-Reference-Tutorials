---
category: general
date: 2026-10-18
description: คอมไพล์โปรเจกต์ Java ด้วย Maven และรันจากบรรทัดคำสั่งโดยใช้คำสั่ง Maven
  clean, compile และ exec. เรียนรู้วิธีสร้างและรันแอป Java อย่างมีประสิทธิภาพ.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: th
lastmod: 2026-10-18
og_description: คอมไพล์โปรเจกต์ Java ด้วย Maven และรันจากบรรทัดคำสั่งด้วยคู่มือขั้นตอนต่อขั้นตอน.
  เชี่ยวชาญการใช้ Maven clean compile run เพื่อสร้างและรันแอป Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: คอมไพล์โครงการ Java ด้วย Maven – รันจากบรรทัดคำสั่ง
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
title: คอมไพล์โปรเจกต์ Java ด้วย Maven และรันจากบรรทัดคำสั่ง
url: /th/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# คอมไพล์โปรเจกต์ Java ด้วย Maven และรันจากบรรทัดคำสั่ง

หากคุณต้องการ **compile java project maven** และเรียกใช้คลาสที่ได้โดยตรงจากเทอร์มินัล คู่มือนี้จะแสดงให้คุณทราบอย่างชัดเจน ในตอนท้ายของบทเรียนคุณจะสามารถทำความสะอาด artifacts เก่า, คอมไพล์ซอร์สโค้ด, และ **execute java class command line** ด้วยการใช้คำสั่ง Maven เพียงชุดเดียว

บทเรียนนี้ครอบคลุมทุกสิ่งที่คุณต้องรู้เพื่อ **build and run java app** ด้วย Maven รวมถึงปลั๊กอินที่จำเป็น, ปัญหาที่พบบ่อย, และเคล็ดลับสำหรับเชลล์บน Windows‑ และ Unix‑based. ไม่จำเป็นต้องอ้างอิงเอกสารภายนอก—เพียงทำตามขั้นตอนด้านล่าง

## ข้อกำหนดเบื้องต้น

* ติดตั้ง Java Development Kit (JDK) 8 หรือใหม่กว่าและตั้งค่า `JAVA_HOME`.
* มี Apache Maven 3.6+ อยู่ใน `PATH` ของคุณ.
* โปรเจกต์ Maven ที่มีไฟล์ `pom.xml` และคลาส Java ที่มีเมธอด `public static void main(String[] args)` (สำหรับตัวอย่างนี้คลาสคือ `com.aspose.ocr.examples.SimpleOcrDemo`).

## คอมไพล์โปรเจกต์ Java ด้วย Maven

ขั้นตอนแรกคือการลบคลาสที่คอมไพล์ไว้ก่อนหน้าและ artifacts การสร้างอื่น ๆ การรัน `mvn clean` จะรับประกันการเริ่มต้นใหม่และป้องกัน bytecode ที่ล้าสมัยจากการทำให้เกิดข้อผิดพลาดขณะรัน

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*ทำไมต้อง clean?* Maven จะเก็บคลาสที่คอมไพล์ไว้ใน `target/`. หากข้ามขั้นตอน clean ไฟล์ `.class` เก่าอาจยังคงอยู่และทำให้ปัญหาการคอมไพล์ไม่ปรากฏ, โดยเฉพาะหลังจากทำการรีแฟคเตอร์ชื่อแพ็กเกจ

## เรียกใช้คลาส Java จากบรรทัดคำสั่ง

หลังจากทำการ clean แล้ว ให้คอมไพล์ไฟล์ซอร์ส Maven จะทำขั้นตอน `compile` เพื่อแปลงซอร์สทั้งหมดใน `src/main/java` เป็น bytecode และวางผลลัพธ์ใน `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

ตอนนี้คุณมีผลลัพธ์ **maven compile source code** พร้อมสำหรับการรัน คำสั่งต่อไปจะรันคลาสที่คอมไพล์แล้วโดยไม่ต้องใช้ JAR แยก

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

เป้าหมาย `exec:java` ของปลั๊กอิน **maven clean compile run** จะเปิดคลาสที่ระบุโดยตรงจากไดเรกทอรีผลลัพธ์ที่คอมไพล์แล้ว นี่เป็นวิธีที่เร็วที่สุดในการ **execute java class command line** ระหว่างการพัฒนา

### ผลลัพธ์ที่คาดหวัง

เมื่อเดโมทำงานสำเร็จคุณควรเห็นผลลัพธ์คล้ายกับ:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

หากคุณได้รับ `ClassNotFoundException` ให้ตรวจสอบชื่อคลาสแบบเต็มอีกครั้งและยืนยันว่ามันอยู่ภายใต้ `src/main/java`.

## กระบวนการทำงาน Maven clean compile run

การรวมคำสั่งสามคำสั่งเข้าด้วยกันให้กระบวนการทำงานที่กระชับและทำซ้ำได้:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*ทำไมต้องเชื่อมต่อกัน?* การรวมขั้นตอนเข้าด้วยกันทำให้ไม่ต้องกด **Enter** สามครั้งและลดความเสี่ยงที่จะลืมขั้นตอน Maven จะดำเนินการตามลำดับที่ปรากฏ, รับประกันการสร้างที่สะอาดก่อนการรัน

### เคล็ดลับเพื่อกระบวนการทำงานที่ราบรื่น

| เคล็ดลับ | คำอธิบาย |
|-----|-------------|
| **ใช้โปรไฟล์** | กำหนดโปรไฟล์ Maven ที่รวม `clean`, `compile`, และ `exec:java` เพื่อให้คุณรัน `mvn demo` แทนการพิมพ์คำสั่งทั้งหมด |
| **เพิ่มตัวเลือก JVM** | ส่ง `-Dexec.args="-Xmx512m"` เพื่อเพิ่มขนาด heap สำหรับแอปที่ใช้หน่วยความจำสูง |
| **ข้ามแพลตฟอร์ม** | บน Windows ใช้ `mvn.cmd` ส่วนเชลล์ Unix ใช้ `mvn`. คำสั่งเดียวกันทำงานได้ในทั้งสองสภาพแวดล้อม |

## สร้างและรันแอป Java ด้วย Maven

หากคุณต้องการ artifact ที่สามารถแจกจ่ายได้, คุณสามารถให้ Maven แพคเกจคลาสที่คอมไพล์เป็น JAR ที่รันได้และจากนั้นรันด้วยคำสั่งมาตรฐาน `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

วิธีนี้มีประโยชน์เมื่อคุณต้อง **build and run java app** บนเซิร์ฟเวอร์ที่ไม่มีการติดตั้ง Maven อย่างไรก็ตามสำหรับการพัฒนาอย่างรวดเร็วลำดับ **maven clean compile run** จะเร็วกว่าเพราะข้ามขั้นตอนการแพคเกจ

## Maven compile source code – ปัญหาที่พบบ่อย

แม้ว่าคำสั่งจะตรงไปตรงมา, นักพัฒนามักพบปัญหาต่อไปนี้:

1. **Missing `exec-maven-plugin`**  
   หาก Maven ไม่พบเป้าหมาย `exec:java`, ให้เพิ่มปลั๊กอินนี้ใน `pom.xml` ของคุณ:

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
   Maven คอมไพล์ไปที่ `target/classes`. หากคุณย้ายไฟล์ด้วยตนเองหรือเปลี่ยนไดเรกทอรีผลลัพธ์เริ่มต้น, เป้าหมาย `exec:java` อาจไม่พบคลาสของคุณ. คงโครงสร้างเริ่มต้นไว้ยกเว้นคุณมีเหตุผลเฉพาะที่จะเปลี่ยน

3. **Using the wrong JDK version**  
   Maven สืบทอด JDK จาก `JAVA_HOME`. การคอมไพล์ด้วยซอร์สโค้ด JDK 11 แล้วรันบน JDK 8 จะทำให้เกิด `UnsupportedClassVersionError`. ตรวจสอบเวอร์ชัน JDK ด้วย `java -version` และ `mvn -v`.

4. **Shell quoting problems**  
   บน Unix ให้ใส่ค่า `-Dexec.mainClass` ในเครื่องหมายอัญประกาศเดี่ยวหากมีอักขระพิเศษ:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   บน Windows เครื่องหมายอัญประกาศคู่ทำงานได้ดี

โดยการแก้ไขจุดเหล่านี้คุณจะสามารถ **execute java class command line** อย่างเชื่อถือได้ในทุกสภาพแวดล้อม

## เคล็ดลับระดับมืออาชีพ: ทำอัตโนมัติด้วยสคริปต์

สำหรับทีมที่ต้องสร้างเดโมบ่อยครั้ง, สร้างสคริปต์เชลล์หรือ batch เล็ก ๆ:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

ทำให้สคริปต์สามารถรันได้ (`chmod +x run-demo.sh`) และรัน `./run-demo.sh`. วิธีนี้จะขจัดข้อผิดพลาดจากการพิมพ์และทำให้ทุกคนในทีมปฏิบัติตามลำดับ **maven clean compile run** อย่างแม่นยำ

## สรุป

ตอนนี้คุณรู้วิธี **compile java project maven** และทันที **execute java class command line** ด้วยเป้าหมาย clean, compile, และ exec ของ Maven. กระบวนการทำงานแบบขั้นตอน‑ต่อ‑ขั้นตอนรับประกันการสร้างที่ใหม่, ขจัด artifacts ที่ล้าสมัย, และทำให้คุณ **build and run java app** ด้วยบรรทัดคำสั่งเดียว  

ต่อไปคุณอาจสำรวจ:

* การเพิ่ม **shade plugin** เพื่อสร้าง uber‑JAR สำหรับการปรับใช้.  
* การกำหนดค่า Maven profiles สำหรับสภาพแวดล้อมต่าง ๆ (dev, test, prod).  
* การรวม unit test ด้วย `mvn test` ก่อนขั้นตอนคอมไพล์.

ลองทดลองกับการปรับเปลี่ยนเหล่านี้เพื่อให้กระบวนการทำงานสอดคล้องกับโปรเจกต์ของคุณ, และคุณจะมี pipeline การสร้างที่แข็งแรงและทำซ้ำได้ซึ่งทำงานได้บน Windows, macOS, และ Linux. Happy coding!

## สิ่งที่คุณควรเรียนต่อไป?

บทเรียนต่อไปนี้ครอบคลุมหัวข้อที่เกี่ยวข้องอย่างใกล้ชิดซึ่งต่อยอดจากเทคนิคที่แสดงในคู่มือนี้. แต่ละแหล่งข้อมูลมีตัวอย่างโค้ดทำงานครบถ้วนพร้อมคำอธิบายขั้นตอน‑ต่อ‑ขั้นตอนเพื่อช่วยคุณเชี่ยวชาญฟีเจอร์ API เพิ่มเติมและสำรวจวิธีการนำไปใช้แบบอื่นในโปรเจกต์ของคุณ.

- [วิธีใช้ OCR ใน Java – คู่มือขั้นตอน‑ต่อ‑ขั้นตอนเต็มรูปแบบ](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [รัน OCR บนภาพด้วย Java – คู่มือ Aspose OCR เต็มรูปแบบ](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [วิธีทำ OCR ด้วย Aspose OCR ใน Java – คู่มือขั้นตอน‑ต่อ‑ขั้นตอน](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}