---
category: general
date: 2026-10-18
description: قم بتجميع مشروع جافا باستخدام Maven وتشغيله من سطر الأوامر باستخدام أوامر Maven clean
  و compile و exec. تعلم كيفية بناء وتشغيل تطبيق جافا بكفاءة.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: ar
lastmod: 2026-10-18
og_description: قم بتجميع مشروع جافا باستخدام Maven وتشغيله من سطر الأوامر مع دليل
  خطوة بخطوة. إتقان أوامر Maven clean و compile و run لبناء وتشغيل تطبيق جافا.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: تجميع مشروع جافا باستخدام Maven – تشغيل من سطر الأوامر
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
title: تجميع مشروع جافا باستخدام مافن وتشغيله من سطر الأوامر
url: /ar/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# تجميع مشروع جافا باستخدام Maven وتشغيله من سطر الأوامر

إذا كنت بحاجة إلى **compile java project maven** وإطلاق الفئة الناتجة مباشرةً من الطرفية، يوضح لك هذا الدليل بالضبط كيفية القيام بذلك. في نهاية البرنامج التعليمي ستكون قادرًا على تنظيف القطع الأثرية القديمة، وتجميع شفرة المصدر، و**execute java class command line** باستخدام سلسلة أوامر Maven واحدة.

يغطي الدليل كل ما تحتاج معرفته لـ **build and run java app** باستخدام Maven، بما في ذلك الإضافات المطلوبة، المشكلات الشائعة، ونصائح لأوامر Windows و Unix. لا حاجة لأي وثائق خارجية—فقط اتبع الخطوات أدناه.

## المتطلبات المسبقة

* Java Development Kit (JDK) 8 أو أحدث مثبت ومُعَرَّف `JAVA_HOME`.
* Apache Maven 3.6+ متاح في `PATH` الخاص بك.
* مشروع Maven يحتوي على ملف `pom.xml` وفئة جافا مع طريقة `public static void main(String[] args)` (في هذا المثال الفئة هي `com.aspose.ocr.examples.SimpleOcrDemo`).

## تجميع مشروع جافا باستخدام Maven

الخطوة الأولى هي إزالة أي فئات تم تجميعها مسبقًا وغيرها من القطع الأثرية للبناء. تشغيل `mvn clean` يضمن بداية نظيفة ويمنع بايت كود قديم من التسبب بأخطاء وقت التشغيل.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*لماذا التنظيف؟* يخزن Maven الفئات المجمعة في `target/`. إذا تخطيت مرحلة التنظيف، قد تظل ملفات `.class` القديمة وتُخفي مشاكل التجميع، خاصةً بعد إعادة هيكلة أسماء الحزم.

## تنفيذ فئة جافا من سطر الأوامر

بعد التنظيف، قم بتجميع ملفات المصدر. مرحلة `compile` في Maven تُحوِّل جميع مصادر `src/main/java` إلى بايت كود وتضع النتائج في `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

الآن لديك ناتج **maven compile source code** جاهز للتنفيذ. الأمر التالي يشغل الفئة المجمعة دون الحاجة إلى JAR منفصل.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

هدف `exec:java` في إضافة **maven clean compile run** يُطلق الفئة المحددة مباشرةً من دليل الإخراج المجمّع. هذه هي أسرع طريقة لـ **execute java class command line** أثناء التطوير.

### النتيجة المتوقعة

عند تشغيل العرض التجريبي بنجاح، يجب أن ترى شيئًا مشابهًا لـ:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

إذا تلقيت استثناء `ClassNotFoundException`، فتحقق مرة أخرى من اسم الفئة المؤهل بالكامل وتأكد من وجوده تحت `src/main/java`.

## سير عمل Maven clean compile run

جمع الأوامر الثلاثة معًا ينتج سير عمل مضغوط وقابل للتكرار:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*لماذا ربطها معًا؟* دمج المراحل يلغي الحاجة للضغط على **Enter** ثلاث مرات ويقلل من احتمال نسيان خطوة. سيقوم Maven بتنفيذ المراحل بالترتيب الذي تظهر فيه، مما يضمن بناء نظيف قبل التنفيذ.

### نصائح لسير عمل أكثر سلاسة

| نصيحة | الوصف |
|-----|-------------|
| **استخدام ملف تعريف** | عرّف ملف تعريف Maven يجمع بين `clean` و `compile` و `exec:java` بحيث يمكنك تشغيل `mvn demo` بدلاً من كتابة السلسلة الكاملة. |
| **إضافة خيارات JVM** | مرّر `-Dexec.args="-Xmx512m"` لزيادة حجم الذاكرة للتطبيقات التي تستهلك الذاكرة. |
| **متعدد المنصات** | على Windows استخدم `mvn.cmd` بينما تستخدم القشور Unix الأمر `mvn`. يعمل الأمر نفسه في كلا البيئتين. |

## بناء وتشغيل تطبيق جافا باستخدام Maven

إذا كنت تفضّل قطعة قابلة للتوزيع، يمكنك السماح لـ Maven بتعبئة الفئات المجمعة في JAR قابل للتنفيذ ثم تشغيله باستخدام الأمر القياسي `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

هذا النهج مفيد عندما تحتاج إلى **build and run java app** على خادم لا يتوفر فيه Maven. ومع ذلك، لتطوير سريع تكون سلسلة **maven clean compile run** أسرع لأنها تتخطى خطوة التعبئة.

## Maven compile source code – المشكلات الشائعة

على الرغم من أن الأوامر بسيطة، غالبًا ما يواجه المطورون المشكلات التالية:

1. **Missing `exec-maven-plugin`**  
   إذا لم يتمكن Maven من العثور على هدف `exec:java`، أضف الإضافة إلى ملف `pom.xml` الخاص بك:

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
   يقوم Maven بالتجميع إلى `target/classes`. إذا قمت بنقل الملفات يدويًا أو غيرت دليل الإخراج الافتراضي، قد لا يتمكن هدف `exec:java` من العثور على فئتك. احتفظ بالتخطيط الافتراضي ما لم يكن لديك سبب محدد لتغييره.

3. **Using the wrong JDK version**  
   يرث Maven نسخة JDK من `JAVA_HOME`. تجميع شفرة المصدر باستخدام JDK 11 أثناء التشغيل على JDK 8 سيسبّب `UnsupportedClassVersionError`. تحقق من نسخة JDK باستخدام `java -version` و `mvn -v`.

4. **Shell quoting problems**  
   على Unix، ضع قيمة `-Dexec.mainClass` بين علامات اقتباس مفردة إذا احتوت على أحرف خاصة:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   على Windows، علامات الاقتباس المزدوجة تعمل بشكل جيد.

من خلال معالجة هذه النقاط، يمكنك تنفيذ **execute java class command line** بثقة في أي بيئة.

## نصيحة احترافية: أتمتة باستخدام سكريبت

للفرق التي تعيد بناء العرض التجريبي بشكل متكرر، أنشئ سكريبت صغير للشل أو دفعة:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

اجعلها قابلة للتنفيذ (`chmod +x run-demo.sh`) وشغّل `./run-demo.sh`. هذا يلغي أخطاء الكتابة ويضمن أن كل مطور يتبع سلسلة **maven clean compile run** الدقيقة.

## الخلاصة

أنت الآن تعرف كيفية **compile java project maven** و**execute java class command line** فورًا باستخدام أهداف clean و compile و exec في Maven. يضمن سير العمل خطوة بخطوة بناءً نظيفًا، ويزيل القطع الأثرية القديمة، ويسمح لك بـ **build and run java app** باستخدام سطر أوامر واحد.  

بعد ذلك، قد ترغب في استكشاف:

* إضافة **shade plugin** لإنشاء Uber‑JAR للنشر.  
* تكوين ملفات تعريف Maven لبيئات مختلفة (dev، test، prod).  
* دمج اختبارات الوحدة باستخدام `mvn test` قبل خطوة التجميع.

جرّب هذه التغييرات لتناسب سير العمل في مشاريعك الخاصة، وستحصل على خط أنابيب بناء قوي وقابل للتكرار يعمل عبر Windows و macOS و Linux. برمجة سعيدة!

## ما الذي يجب أن تتعلمه بعد ذلك؟

الدروس التالية تغطي مواضيع ذات صلة وثيقة تبني على التقنيات التي تم توضيحها في هذا الدليل. كل مورد يتضمن أمثلة شفرة كاملة مع شروحات خطوة بخطوة لمساعدتك على إتقان ميزات API إضافية واستكشاف أساليب تنفيذ بديلة في مشاريعك.

- [How to Use OCR in Java – Complete Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Run OCR on Image with Java – Complete Aspose OCR Guide](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [How to Perform OCR with Aspose OCR in Java – Step‑by‑Step Guide](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}