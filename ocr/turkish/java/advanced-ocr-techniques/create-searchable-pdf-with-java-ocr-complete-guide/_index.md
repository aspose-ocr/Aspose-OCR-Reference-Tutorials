---
category: general
date: 2026-05-25
description: Aspose OCR kullanarak Java’da aranabilir PDF oluşturun. PDF’yi aranabilir
  PDF’ye nasıl dönüştüreceğinizi, OCR için PDF’yi nasıl yükleyeceğinizi öğrenin ve
  GPU ile nasıl hızlandırabileceğinizi keşfedin.
draft: false
keywords:
- create searchable pdf
- convert pdf to searchable pdf
- load pdf for ocr
- ocr pdf with gpu
language: tr
og_description: Aspose OCR kullanarak Java’da aranabilir PDF oluşturun. Bu öğreticide
  PDF’yi aranabilir PDF’ye nasıl dönüştüreceğiniz, OCR için PDF’yi nasıl yükleyeceğiniz
  ve GPU hızlandırmasını nasıl kullanacağınız gösterilmektedir.
og_title: Java OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  headline: Create Searchable PDF with Java OCR – Complete Guide
  type: TechArticle
- description: Create searchable PDF in Java using Aspose OCR. Learn how to convert
    PDF to searchable PDF, load PDF for OCR, and accelerate with GPU.
  name: Create Searchable PDF with Java OCR – Complete Guide
  steps:
  - name: Runs OCR on each page image.
    text: Runs OCR on each page image.
  - name: Generates an invisible text layer that matches the visual content.
    text: Generates an invisible text layer that matches the visual content.
  - name: Embeds that layer into a new PDF, preserving the original appearance.
    text: Embeds that layer into a new PDF, preserving the original appearance.
  type: HowTo
tags:
- OCR
- Java
- PDF
- Aspose
title: Java OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/java/advanced-ocr-techniques/create-searchable-pdf-with-java-ocr-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz

Tar scanned belgelerden **create searchable PDF** dosyaları oluşturmanız gerektiğinde, nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok geliştirici, özellikle performans önemli olduğunda, yalnızca görüntü içeren PDF'leri metin‑aranabilir varlıklara dönüştürmeye çalışırken aynı sorunla karşılaşıyor.

Bu öğreticide, Aspose OCR for Java kullanarak **creates searchable PDF** dosyaları oluşturan uygulamalı bir çözümü adım adım inceleyeceğiz. Ayrıca **convert PDF to searchable PDF**, **load PDF for OCR** ve hatta **OCR PDF with GPU** hızlandırmasını nasıl yapacağınızı göstereceğiz—hepsi tek bir, okunması kolay betikte. Sonunda çalıştırılabilir bir programınız ve her adımın neden önemli olduğuna dair net bir anlayışınız olacak.

> **Ne Kazanacaksınız**  
> * Karışık‑dilli bir PDF okuyan tam bir Java projesi  
> * Modern donanımlarda işleme süresini hızlandıran GPU‑destekli OCR  
> * Herhangi bir belge yönetim sistemine ekleyebileceğiniz aranabilir bir PDF çıktısı  

## Önkoşullar

* Java 17 (veya daha yeni) yüklü – eski sürümler gerekli API'leri içermeyebilir.  
* Bağımlılık yönetimi için Maven veya Gradle – örneklerde Maven kullanacağız.  
* Aspose OCR for Java lisansı (ücretsiz deneme testi için çalışır).  
* Tar scanned sayfalar içeren bir PDF dosyası (demo `mixed_lang.pdf` kullanır).  

Bu maddeler size yabancı geliyorsa panik yapmayın – aşağıdaki adımlar sizi çalıştırmaya hazır hale getirecek tam komutları içeriyor.

![Aspose OCR Java kullanarak aranabilir PDF oluşturma](https://example.com/images/create-searchable-pdf.png "Aspose OCR Java kullanarak aranabilir PDF oluşturma")

## Adım 1: Projeyi Kurun ve **Create Searchable PDF** – Proje Başlatma

İlk olarak, bir Maven projesi oluşturun. Bir terminal açın ve şu komutu çalıştırın:

```bash
mvn archetype:generate -DgroupId=com.example.ocr \
    -DartifactId=SearchablePdfDemo -DarchetypeArtifactId=maven-archetype-quickstart \
    -DinteractiveMode=false
```

Klasöre girin:

```bash
cd SearchablePdfDemo
```

`pom.xml` dosyasına Aspose OCR bağımlılığını ekleyin:

```xml
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- check Maven Central for the latest -->
    </dependency>
</dependencies>
```

> **Neden önemli:** **create searchable pdf** işlemi, Aspose OCR kütüphanesinde bulunan `OcrEngine` sınıfına dayanır. Doğru sürüm olmadan derleme hataları veya eksik özellikler alırsınız.

Şimdi `src/main/java/com/example/ocr/` altında ana Java sınıfı `QuickDemo.java` oluşturun.

## Adım 2: GPU Hızlandırmayı Etkinleştirin – **OCR PDF with GPU**

GPU hızlandırması, çok sayfalı bir OCR işinin süresini dakikalarca kısaltabilir. Aspose OCR, bunu tek bir satırla açıp kapatmanıza izin verir:

```java
// Enable GPU processing
engine.getEngineOptions().setUseGpu(true);
```

Eğer makinenizde uyumlu bir NVIDIA veya AMD GPU ve gerekli sürücüler yüklüyse, OCR motoru ağır işi grafik kartına devredecektir. Aksi takdirde, çağrı güvenli bir şekilde CPU işlemine geri döner—çökme olmaz, sadece daha yavaş çalışır.

> **Pro ipucu:** Linux'ta, JVM'i başlatmadan önce `LD_LIBRARY_PATH` değişkenini CUDA kütüphanelerine işaret edecek şekilde ayarlamanız gerekebilir.

## Adım 3: **Load PDF for OCR** ve Dil Desteğini Yapılandırma

Şimdi gerçekten **load pdf for ocr** yapıyoruz. Aspose OCR, PDF sayfalarını dahili olarak görüntüler gibi işler, bu yüzden motoru dosyaya yönlendirmeniz yeterlidir:

```java
// Load the source PDF document (image‑only PDF)
engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");
```

Ardından, motoru hangi dili beklediğinizi belirtin. Demo’da Thai (Tay) diline odaklandık, ancak belge birden fazla betik içeriyorsa bir dil dizisi geçirebilirsiniz:

```java
engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
```

Özel bir sözlüğünüz (örneğin, alan‑spesifik terimler) varsa, bunu ekleyin:

```java
engine.getEngineOptions().getSpellCorrectorOptions()
      .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");
```

> **Neden dil ayarlamalısınız?** OCR doğruluğu dil modeline bağlıdır. Doğru `OcrLanguage` sağlamak, özellikle Latin dışı betikler için hatalı tanıma oranını büyük ölçüde azaltır.

## Adım 4: Tek Çağrıyla **Convert PDF to Searchable PDF**

Aspose OCR, **convert PDF to searchable PDF** işlemini tek bir metod çağrısıyla yapabildiği için öne çıkar—görüntü ve metin katmanlarını manuel olarak birleştirmenize gerek kalmaz.

```java
// Export a searchable PDF in a single operation
engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");
```

Arka planda, motor:

1. Her sayfa görüntüsü üzerinde OCR çalıştırır.  
2. Görsel içeriğe eşleşen görünmez bir metin katmanı oluşturur.  
3. Bu katmanı yeni bir PDF'e gömer, orijinal görünümü korur.

Sonuç, girdiyle tamamen aynı görünüme sahip ama herhangi bir PDF görüntüleyici tarafından indekslenebilen bir dosyadır.

## Adım 5: Tanınan Metni Alın ve Çıktıyı Doğrulayın

Aranabilir bir PDF zaten kaydetmiş olsak da, günlükleme veya daha fazla işleme için ham metni de isteyebilirsiniz:

```java
// Output the recognized text to the console
System.out.println(engine.recognize().getText());
```

Programı çalıştırdığınızda, konsolda çıkarılan Tay metninin yazdırıldığını ve ardından dizininizde yeni oluşturulmuş `mixed_lang_searchable.pdf` dosyasını görmelisiniz.

### Beklenen Konsol Çıktısı (kısaltılmış)

```
สวัสดีครับ นี่คือเอกสารตัวอย่าง...
...
```

Oluşturulan PDF'i Adobe Reader veya herhangi bir görüntüleyicide açın, **Ctrl + F** tuşlarına basın ve konsolda gördüğünüz kelimeleri arayabileceksiniz. Bu, **create searchable pdf** dosyalarını başarıyla oluşturduğumuzun kanıtıdır.

## Adım 6: Yaygın Tuzaklar ve Yüksek‑Performanslı OCR için **Pro Tips**

| Sorun | Belirti | Çözüm |
|-------|----------|-----|
| **GPU not detected** | Hız artışı yok, motor CPU'ya geri döner | CUDA sürücülerinin yüklü olduğundan ve `java.library.path`'in GPU kütüphanelerini içerdiğinden emin olun. |
| **Missing fonts** | Metin katmanı bozuk karakterler gösteriyor | Ana işletim sistemine uygun dil yazı tiplerini kurun veya `engine.getEngineOptions().setEmbedFonts(true)` ile gömün. |
| **Large PDFs (> 500 pages)** | Bellek yetersizliği hataları | JVM yığın boyutunu (`-Xmx4g`) artırın ve işi çekirdekler arasında dağıtmak için `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors())` ayarlayın. |
| **Custom dictionary not applied** | Yazım düzeltici göz ardı ediliyor gibi görünüyor | Yolun mutlak olduğundan ve dosyanın UTF-8 kodlamasını kullandığından emin olun. |

> **Unutmayın:** `engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());` satırı, **ocr pdf with gpu** yapmak ve çok‑çekirdekli CPU'ları tam olarak kullanmak istediğinizde kritiktir. Bu, motorun her çekirdek için bir işçi oluşturmasını sağlar, GPU'yu meşgul tutarken CPU ön‑ve son‑işlemeyi yapar.

## Tam Çalışan Örnek

Aşağıda, tartıştığımız tüm adımları içeren eksiksiz, çalıştırmaya hazır Java programı yer alıyor. Yer tutucu yolları kendi dizinlerinizle değiştirin.

```java
import com.aspose.ocr.*;

public class QuickDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine engine = new OcrEngine();

        // Step 2: Enable GPU acceleration and use all available CPU cores
        engine.getEngineOptions().setUseGpu(true);
        engine.getEngineOptions().setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 3: Configure language support and a custom spell‑corrector dictionary
        engine.getEngineOptions().setLanguage(OcrLanguage.THAI);
        engine.getEngineOptions().getSpellCorrectorOptions()
              .setUserDictionaryPath("YOUR_DIRECTORY/thai_custom.txt");

        // Step 4: Load the source PDF document (this is where we **load pdf for ocr**)
        engine.getImage().loadFromFile("YOUR_DIRECTORY/mixed_lang.pdf");

        // Step 5: Export a searchable PDF in a single operation (**convert pdf to searchable pdf**)
        engine.saveToSearchablePdf("YOUR_DIRECTORY/mixed_lang_searchable.pdf");

        // Step 6: Output the recognized text to the console
        System.out.println(engine.recognize().getText());
    }
}
```

Derleyin ve çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass="com.example.ocr.QuickDemo"
```

Her şey doğru bağlandıysa, çıkarılan metnin yazdırıldığını ve orijinal dosyanın yanında yeni bir aranabilir PDF gördüğünüzü göreceksiniz.

## Sonuç

Java'da Aspose OCR kullanarak **create searchable pdf** dosyalarını nasıl oluşturacağınızı yeni gösterdik; proje kurulumundan GPU‑hızlandırmalı işleme kadar her şeyi kapsadık. **loading pdf for OCR** yaparak, dil desteğini yapılandırarak ve tek satır **convert pdf to searchable pdf** metodunu çağırarak, arama motorları veya dahili geri getirme sistemleri için hazır, tamamen indekslenmiş bir belge elde edersiniz.

Sırada ne var? `OcrLanguage.THAI` yerine `OcrLanguage.ENGLISH` deneyin veya çok dilli PDF'ler için birden fazla dili birleştirin. DPI'nin doğruluğu nasıl etkilediğini görmek için `engine.getEngineOptions().setResolution(300)` ayarıyla deney yapın, ya da eski görüntüleyicilerde daha iyi render almak için özel yazı tiplerini gömün.

Performans ayarı, lisanslama veya bu iş akışını bir Spring Boot servisine entegre etme hakkında sorularınız mı var? Aşağıya yorum bırakın veya daha derin bilgi için Aspose OCR Java belgelerine bakın. Kodlamaktan keyif alın ve bu statik taramaları aranabilir hazinelere dönüştürmenin tadını çıkarın!

## İlgili Öğreticiler

- [PDF Metnini Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/english/java/ocr-operations/recognize-pdf/)
- [.NET'te Aspose.OCR ile PDF OCR Nasıl Yapılır](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}