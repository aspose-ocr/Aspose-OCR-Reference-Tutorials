---
category: general
date: 2026-10-18
description: Maven kullanarak Java projesini derleyin ve komut satırından Maven clean,
  compile ve exec komutlarıyla çalıştırın. Java uygulamasını verimli bir şekilde nasıl
  derleyip çalıştıracağınızı öğrenin.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: tr
lastmod: 2026-10-18
og_description: Java projesini Maven ile derleyin ve komut satırından adım adım bir
  rehberle çalıştırın. Maven clean compile run komutlarını öğrenerek Java uygulamasını
  oluşturun ve çalıştırın.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Java projesini Maven ile derle – komut satırından çalıştır
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
title: Java projesini Maven ile derle ve komut satırından çalıştır
url: /tr/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maven ile Java projesi derleme ve komut satırından çalıştırma

Eğer **compile java project maven** yapmanız ve ortaya çıkan sınıfı doğrudan bir terminalden başlatmanız gerekiyorsa, bu kılavuz tam olarak nasıl yapılacağını gösterir. Eğitim sonunda eski artefaktları temizleyebilecek, kaynak kodunu derleyebilecek ve tek bir Maven komut zinciri kullanarak **execute java class command line** yapabileceksiniz.

Eğitim, Maven ile **build and run java app** yapmak için bilmeniz gereken her şeyi kapsar; gerekli eklentiler, yaygın tuzaklar ve Windows‑ ve Unix‑tabanlı kabuklar için ipuçları dahil. Harici bir dokümantasyon gerekmez—sadece aşağıdaki adımları izleyin.

## Önkoşullar

* Java Development Kit (JDK) 8 veya daha yeni bir sürüm yüklü ve `JAVA_HOME` ayarlanmış.
* Apache Maven 3.6+ `PATH`'inizde bulunuyor.
* `pom.xml` dosyasını ve `public static void main(String[] args)` metoduna sahip bir Java sınıfını içeren bir Maven projesi (bu örnek için sınıf `com.aspose.ocr.examples.SimpleOcrDemo`).

## Maven ile Java projesi derleme

İlk adım, daha önce derlenmiş sınıfları ve diğer yapı artefaktlarını kaldırmaktır. `mvn clean` çalıştırmak temiz bir başlangıç sağlar ve eski bayt kodunun çalışma zamanı hatalarına yol açmasını önler.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Why clean?* Maven derlenmiş sınıfları `target/` içinde saklar. Temizleme aşamasını atlayırsanız, eski `.class` dosyaları kalabilir ve özellikle paket adlarını yeniden düzenledikten sonra derleme sorunlarını gizleyebilir.

## Java sınıfını komut satırından çalıştırma

Temizlemeden sonra, kaynak dosyaları derleyin. Maven'in `compile` aşaması tüm `src/main/java` kaynaklarını bayt koduna çevirir ve sonuçları `target/classes` içine koyar.

```bash
# Step 2: Compile the source code
mvn compile
```

Artık yürütmeye hazır bir **maven compile source code** çıktısına sahipsiniz. Sonraki komut, ayrı bir JAR'a ihtiyaç duymadan derlenmiş sınıfı çalıştırır.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java` hedefi, **maven clean compile run** eklentisinin, belirtilen sınıfı doğrudan derlenmiş çıktı dizininden başlatır. Bu, geliştirme sırasında **execute java class command line** yapmanın en hızlı yoludur.

### Beklenen çıktı

Demo başarılı bir şekilde çalıştığında aşağıdakine benzer bir şey görmelisiniz:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Eğer `ClassNotFoundException` alırsanız, tam nitelikli sınıf adını iki kez kontrol edin ve `src/main/java` altında bulunduğundan emin olun.

## Maven clean compile run iş akışı

Üç komutu bir araya getirerek kompakt, tekrarlanabilir bir iş akışı elde edersiniz:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Why chain them?* Aşamaları birleştirmek, **Enter** tuşuna üç kez basma ihtiyacını ortadan kaldırır ve bir adımı unutma olasılığını azaltır. Maven, fazları göründükleri sırayla çalıştırır ve yürütmeden önce temiz bir yapı garantiler.

### Daha sorunsuz bir iş akışı için ipuçları

| Tip | Açıklama |
|-----|-------------|
| **Use a profile** | `clean`, `compile` ve `exec:java` adımlarını bir araya getiren bir Maven profili tanımlayın, böylece tam zinciri yazmak yerine `mvn demo` çalıştırabilirsiniz. |
| **Add JVM options** | Bellek yoğun uygulamalar için yığın boyutunu artırmak amacıyla `-Dexec.args="-Xmx512m"` parametresini geçirin. |
| **Cross‑platform** | Windows'ta `mvn.cmd` kullanın, Unix kabuklarında ise `mvn` kullanın. Aynı komut her iki ortamda da çalışır. |

## Maven ile Java uygulamasını derleme ve çalıştırma

Eğer dağıtılabilir bir artefakt tercih ediyorsanız, Maven'in derlenmiş sınıflarınızı çalıştırılabilir bir JAR içine paketlemesine izin verebilir ve ardından standart `java -jar` komutuyla çalıştırabilirsiniz:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Bu yaklaşım, Maven'in yüklü olmadığı bir sunucuda **build and run java app** yapmanız gerektiğinde faydalıdır. Ancak, hızlı geliştirme için **maven clean compile run** sırası daha hızlıdır çünkü paketleme adımını atlar.

## Maven compile source code – yaygın tuzaklar

Komutlar basit olsa da, geliştiriciler genellikle aşağıdaki sorunlarla karşılaşır:

1. **Missing `exec-maven-plugin`**  
   Maven `exec:java` hedefini bulamazsa, eklentiyi `pom.xml` dosyanıza ekleyin:

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
   Maven `target/classes` dizinine derler. Dosyaları manuel olarak taşırsanız veya varsayılan çıktı dizinini değiştirirseniz, `exec:java` hedefi sınıfınızı bulamayabilir. Belirli bir nedeniniz yoksa varsayılan düzeni koruyun.

3. **Using the wrong JDK version**  
   Maven, JDK'yi `JAVA_HOME`'dan alır. JDK 11 kaynak koduyla derleme yapıp JDK 8 üzerinde çalıştırmak `UnsupportedClassVersionError` hatasına yol açar. JDK sürümünü `java -version` ve `mvn -v` komutlarıyla doğrulayın.

4. **Shell quoting problems**  
   Unix'te, `-Dexec.mainClass` değerinde özel karakterler varsa tek tırnak içinde sarın: `mvn exec:java -Dexec.mainClass='com.example.Main'`. Windows'ta çift tırnaklar sorunsuz çalışır.

Bu noktalara değinerek, herhangi bir ortamda güvenilir bir şekilde **execute java class command line** yapabilirsiniz.

## Pro ipucu: bir betikle otomatikleştirin

Demo'yu sık sık yeniden derleyen ekipler için küçük bir shell veya batch betiği oluşturun:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Betiği çalıştırılabilir yapın (`chmod +x run-demo.sh`) ve `./run-demo.sh` komutunu çalıştırın. Bu, yazım hatalarını ortadan kaldırır ve her geliştiricinin tam **maven clean compile run** sırasını takip etmesini sağlar.

## Sonuç

Artık **compile java project maven** ve Maven'in clean, compile ve exec hedeflerini kullanarak anında **execute java class command line** yapmayı biliyorsunuz. Adım adım iş akışı temiz bir yapı garantiler, eski artefaktları ortadan kaldırır ve tek bir komut satırıyla **build and run java app** yapmanızı sağlar.  

Sonra şunları keşfedebilirsiniz:

* Deploy için bir uber‑JAR üretmek amacıyla **shade plugin** eklemek.  
* Farklı ortamlar (dev, test, prod) için Maven profilleri yapılandırmak.  
* Derleme adımından önce `mvn test` ile birim testleri entegre etmek.

Bu varyasyonları deneyerek iş akışını kendi projelerinize uyarlayın; böylece Windows, macOS ve Linux'ta çalışan sağlam, tekrarlanabilir bir yapı hattına sahip olursunuz. İyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki eğitimler, bu kılavuzda gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [Java'da OCR Kullanımı – Tam Adım Adım Kılavuz](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Java ile Görüntüde OCR Çalıştırma – Tam Aspose OCR Kılavuzu](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Java'da Aspose OCR ile OCR Gerçekleştirme – Adım Adım Kılavuz](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}