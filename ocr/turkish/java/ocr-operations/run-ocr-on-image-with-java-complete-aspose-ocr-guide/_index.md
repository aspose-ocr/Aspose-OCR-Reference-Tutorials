---
category: general
date: 2026-02-09
description: Aspose OCR'i Java’da kullanarak görüntüde OCR çalıştırın – PNG’den metin
  nasıl çıkarılacağını ve sadece birkaç adımda otomatik dil algılamalı OCR’yi nasıl
  etkinleştireceğinizi öğrenin.
draft: false
keywords:
- run OCR on image
- extract text from PNG
- auto detect language OCR
- Aspose OCR Java
- Hindi OCR example
language: tr
og_description: Görüntüde OCR'yi anında çalıştırın. Bu rehber, PNG dosyalarından metin
  nasıl çıkarılacağını ve Aspose OCR for Java kullanarak otomatik dil algılamalı OCR'yi
  nasıl etkinleştirileceğini gösterir.
og_title: Java ile Görüntüde OCR Çalıştırma – Tam Aspose OCR Öğreticisi
tags:
- OCR
- Java
- Aspose
title: Java ile Görüntüde OCR Çalıştırma – Tam Aspose OCR Rehberi
url: /tr/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile Görüntü Üzerinde OCR Çalıştırma – Tam Aspose OCR Rehberi

Hiç **run OCR on image** dosyalarını çalıştırmanız gerekti ama nereden başlayacağınızı bilmiyor muydunuz? Belki Hindi metni içeren birkaç PNG ekran görüntünüz var ve Java'nın büyük bir makine‑öğrenimi kurulumuna ihtiyaç duymadan kelimeleri çıkarıp çıkaramayacağını merak ediyorsunuzdur. İyi haber: yapabilirsiniz ve Aspose OCR ile şaşırtıcı derecede basit.

Bu öğreticide, **extracts text from PNG** dosyalarından metin çıkaran gerçek bir örnek üzerinden ilerleyecek, **auto detect language OCR** özelliğini nasıl etkinleştireceğinizi gösterecek ve hazır‑çalıştırılabilir bir Java programı sunacağız. Sonunda, konsola Hindi karakterlerini yazdıran çalışan bir kod parçacığına sahip olacaksınız ve her satırın neden önemli olduğunu anlayacaksınız.

## Gereksinimler

- **Java Development Kit (JDK) 8** veya daha yeni – kod, herhangi bir yeni sürümle derlenir.  
- **Aspose.OCR for Java** kütüphanesi – en son JAR'ı Aspose web sitesinden veya Maven Central'dan alın.  
- Devanagari alfabesini içeren bir örnek görüntü (`hindi_sample.png`) – herhangi bir ekran görüntüsü aracıyla oluşturabilirsiniz.  
- Bir IDE veya basit metin düzenleyici – ben IntelliJ IDEA kullanıyorum, ancak düz `javac` de işe yarar.

Harici hizmetler yok, bulut API anahtarları yok, sadece yerel bir JAR ve bir resim. Basit, değil mi?

## Adım 1: Aspose OCR'yi Projenize Ekleyin

İlk olarak, Aspose OCR JAR'ının sınıf yolunuzda (classpath) olduğundan emin olun. Maven kullanıyorsanız, bu bağımlılığı ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

Manuel yolu tercih ediyorsanız, `aspose-ocr-23.10.jar` dosyasını indirin ve `libs/` klasörünüze koyun, ardından şu şekilde derleyin:

```bash
javac -cp "libs/*" LanguageExample.java
```

> **Pro ipucu:** JAR sürüm numarasını kaynak dosyanızın en üstündeki bir yorumda tutun – gelecekteki kendinize hangi API yüzeyini hedeflediğinizi hatırlatır.

## Adım 2: OCR Motoru Örneğini Oluşturun

Şimdi tüm ağır işleri yapan çekirdek nesneyi başlatıyoruz. `OcrEngine`'i işlemin beyni olarak düşünün.

```java
// Step 2: Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Neden burada örnekleniyor? Motor, yapılandırma ayarlarını (örneğin dil) ve yeniden kullanılabilir kaynakları tutar, bu yüzden uygulama başına bir kez oluşturmak yükü azaltır.

## Adım 3: Dil Ayarlarını Yapılandırın (ve Auto‑Detect'i Etkinleştirin)

Eğer dili önceden biliyorsanız—örneğin Hindi—motoru Devanagari'ye odaklanması için söyleyebilirsiniz. Bu, doğruluğu artırır ve işleme süresini hızlandırır.

```java
// Step 3a: Force Hindi (Devanagari) recognition
ocrEngine.getConfiguration().setLanguage(Language.HINDI);

// Step 3b (optional): Let the engine guess the language if you're unsure
ocrEngine.getConfiguration().setAutoDetectLanguage(true);
```

`setAutoDetectLanguage(true)` satırı **auto detect language OCR** anahtarıdır. Karışık‑dilli bir görüntü sağladığınızda, motor her betiği otomatik olarak tanımlamaya çalışır. Her dosyayı manuel olarak etiketleyemediğiniz toplu işler için kullanışlıdır.

## Adım 4: PNG Görüntüsü Üzerinde OCR Çalıştırın

İşte **run OCR on image** verisini gerçekten çalıştırdığımız yer. `recognize` yöntemi bir dosya yolu alır, bitmap'i okur ve bir `RecognitionResult` döndürür.

```java
// Step 4: Perform OCR on the PNG file
RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");
```

`YOUR_DIRECTORY` ifadesini gerçek klasör yolu ile değiştirin. Dosya bulunamazsa, Aspose net bir istisna fırlatır – daha sonra neden başarısız olduğunu tahmin etmenize gerek kalmaz.

## Adım 5: Çıkarılan Metni Alın ve Görüntüleyin

Son olarak, sonuç nesnesinden tanınan dizeyi alın ve yazdırın. Hindi için, terminaliniz UTF‑8 destekliyorsa konsolda Unicode karakterlerini göreceksiniz.

```java
// Step 5: Output the recognized Hindi text
System.out.println("Hindi text:");
System.out.println(result.getText());
```

**Beklenen çıktı** (örnek görüntü “नमस्ते दुनिया” diyor varsayarsak):

```
Hindi text:
नमस्ते दुनिया
```

Auto‑detect'i etkinleştirdiyseniz ve görüntü İngilizce de içeriyorsa, çıktı iki betiği de güzel bir şekilde karışık olarak içerecektir.

## Tam Çalışan Örnek

Aşağıda tam, çalıştırılabilir program yer alıyor. `LanguageExample.java` dosyasına kopyalayıp yapıştırın, görüntü yolunu ayarlayın ve hazırsınız.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.enums.*;

public class LanguageExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Specify the language to be recognized (Hindi – Devanagari script)
        ocrEngine.getConfiguration().setLanguage(Language.HINDI);

        // Step 3: (Optional) Enable automatic fallback to language detection
        ocrEngine.getConfiguration().setAutoDetectLanguage(true);

        // Step 4: Run OCR on the input image
        RecognitionResult result = ocrEngine.recognize("YOUR_DIRECTORY/hindi_sample.png");

        // Step 5: Print the extracted Hindi text
        System.out.println("Hindi text:");
        System.out.println(result.getText());
    }
}
```

> **Not:** Bir IDE kullanıyorsanız, projenin derleme yolunun Aspose OCR JAR'ını içerdiğinden emin olun. IntelliJ'de *File → Project Structure → Libraries* yolunu izleyin ve JAR'ı ekleyin.

## Yaygın Sorular ve Kenar Durumları

### PNG'im düşük çözünürlükte olsaydı ne olur?

OCR doğruluğu 150 dpi'nin altına düştüğünde keskin bir şekilde azalır. Motorun önüne beslemeden önce görüntüyü ImageMagick gibi bir araçla (`convert input.png -resize 200% output.png`) yükseltin. `auto detect language OCR` bayrağı hâlâ çalışır, ancak daha az hatalı tanıma görürsünüz.

### Bir döngüde birden fazla görüntüyü işleyebilir miyim?

Kesinlikle. `recognize` çağrısını bir `for` döngüsü içinde sarın ve aynı `OcrEngine` örneğini yeniden kullanın. Motoru yeniden kullanmak, her yinelemede dil modellerini yeniden yüklemeyi önler, bu da hem bellek hem de CPU zamanını tasarruf ettirir.

```java
String[] files = {"img1.png", "img2.png", "img3.png"};
for (String file : files) {
    RecognitionResult r = ocrEngine.recognize(file);
    System.out.println("Text from " + file + ":");
    System.out.println(r.getText());
}
```

### Unicode olmayan konsolları nasıl yönetirim?

Terminaliniz bozuk semboller gösteriyorsa, Java'yı başlatırken dosya kodlamasını UTF‑8 olarak ayarlayın:

```bash
java -Dfile.encoding=UTF-8 -cp "libs/*" LanguageExample
```

### Güven skorlarını almanın bir yolu var mı?

Evet. `RecognitionResult` içinde `getConfidence()` bulunur ve her tanınan satır için 0 ile 1 arasında bir float döndürür. Bu değerleri çıkarmak için `result.getLines()` üzerinde dönebilirsiniz—düşük güvenilirlikli sonuçları filtrelemek için kullanışlıdır.

## Üretim Kullanımı için Pro İpuçları

- **Dil modellerini önbellekle**: Binlerce görüntü işliyorsanız, motoru tüm toplu işlem boyunca canlı tutun.
- **Paralel işleme**: Her görüntüyü bir `Callable` içine sarın ve bir iş parçacığı havuzuna gönderin. Motorun iş parçacığı‑güvenli olmadığını unutmayın; her iş parçacığı için bir tane oluşturun.
- **Günlükleme**: Büyük işler için `System.out.println` yerine uygun bir logger (SLF4J) kullanın.
- **Bellek yönetimi**: İşiniz bittiğinde yerel kaynakları serbest bırakmak için `ocrEngine.dispose()` çağırın.

## Görsel Genel Bakış

![Run OCR on image example diagram](ocr_flow.png "Run OCR on image example diagram")

Yukarıdaki diyagram akışı gösterir: **run OCR on image → language configuration → auto detect language OCR (optional) → extract text from PNG**.

## Sonuç

Aspose OCR for Java kullanarak **run OCR on image** dosyalarını nasıl çalıştıracağınızı, dil‑spesifik ayarlarla **extract text from PNG** nasıl yapacağınızı ve esnek, çok‑dilli senaryolar için **auto detect language OCR**'yi nasıl açıp kapatacağınızı yeni gösterdik. Tam kod örneği kopyalanmaya, derlenmeye ve çalıştırılmaya hazır—gizli adım yok, harici hizmet yok.

Bir sonraki meydan okumaya hazır mısınız? `Language.HINDI` yerine `Language.AUTO` kullanarak karışık‑betik bir belge besleyin, ya da PDF girişiyle deney yapın (Aspose OCR ayrıca PDF'yi de destekler). Bu kod parçacığını bir Spring Boot REST uç noktasına entegre ederek OCR'yi bir web servisi olarak da sunabilirsiniz.

Kodlamaktan keyif alın, ve görüntüleriniz her zaman okunabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}