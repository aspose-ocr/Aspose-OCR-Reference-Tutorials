---
category: general
date: 2026-04-29
description: Aspose OCR kullanarak Java’da görüntüden metin çıkarma – OCR için görüntüyü
  nasıl yükleyeceğinizi ve makbuzdan metni JSON formatında nasıl tanıyacağınızı öğrenin.
draft: false
keywords:
- extract text from image java
- load image for OCR
- recognize text from receipt
- Aspose OCR Java
- JSON OCR result
language: tr
og_description: Aspose OCR ile Java’da görüntüden metin çıkarma. Bu öğreticide, OCR
  için görüntünün nasıl yükleneceği ve makbuzdan metnin nasıl tanınacağı, JSON olarak
  çıktılanması gösterilmektedir.
og_title: Java ile görüntüden metin çıkarma – Tam Kılavuz
tags:
- Java
- OCR
- Aspose
title: görüntüden metin çıkarma java – OCR için görüntü yükleme
url: /tr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# görüntüden metin çıkarma java – Tam Kılavuz

Hiç **extract text from image java** yapmanız gerektiğinde hangi kütüphaneyi seçeceğinizden emin olmadınız mı? Yalnız değilsiniz. Birçok geliştirici, OCR için görüntüyü yüklemeye çalıştığında ve ardından ham metni tüketmesi zor bir formatta aldığında bir duvara çarpar.  

Bu öğreticide, sadece **load image for OCR** yapmakla kalmayıp aynı zamanda **recognize text from receipt** yapan ve düzenli bir JSON dizesi üreten temiz, uçtan‑uca bir çözümü adım adım inceleyeceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz, ekstra ayar gerektirmeyen hazır bir Java sınıfına sahip olacaksınız.

## Öğrenecekleriniz

- Aspose OCR for Java’yi nasıl kuracağınız (ağır işleri zahmetsiz yapan kütüphane).  
- Diskten **load image for OCR** için tam adımlar.  
- Sonuçları JSON formatında döndürecek şekilde motoru nasıl yapılandıracağınız, bu da sonraki işlemler için mükemmeldir.  
- **recognize text from receipt** görüntülerini nasıl tanıyıp çıktıyı doğrulayacağınız.  

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok; sadece çalışan bir JDK ve rahat ettiğiniz bir IDE yeterli.

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| **Java 17+** (veya herhangi bir güncel JDK) | Aspose OCR, modern Java çalışma zamanları için derlenmiş ikili dosyalar sunar. |
| **Maven veya Gradle** (Aspose OCR bağımlılığını çekmek için) | Bağımlılık yönetimini çok kolaylaştırır. |
| **Bir örnek fiş resmi** (ör. `receipt.png`) | **recognize text from receipt** işlemini göstermek için bu dosyayı kullanacağız. |
| **İnternet bağlantısı** (bir kez) | İlk kez Aspose JAR dosyasını indirmek için gerekir. |

Bu gereksinimlere zaten sahipseniz, harika—hadi başlayalım.

## Adım 1: Aspose OCR’yi Projeye Ekleyin

İlk olarak Aspose OCR kütüphanesine ihtiyacınız var. Maven kullanıyorsanız, `pom.xml` dosyanıza aşağıdaki snippet’i ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Check the latest version on Maven Central -->
</dependency>
```

Gradle için ise şu şekilde görünür:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

> **Pro ipucu:** Sürüm numarasını kilitleyin. Daha sonra yükseltmek, kodunuzu kırabilecek ince API değişikliklerine yol açabilir.

Bağımlılık çözüldükten sonra, **extract text from image java** yapan Java kodunu yazmaya hazırsınız.

## Adım 2: OCR İçin Görüntüyü Yükleyin

Şimdi **load image for OCR** yapan tam satırı göstereceğiz. Aspose, kullanışlı bir `ImageStream.fromFile` yardımcı metoduna sahiptir.

```java
// Step 2: Load the image you want to process
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));
```

`YOUR_DIRECTORY` kısmını fiş dosyanızın mutlak ya da göreli yolu ile değiştirin. Yol yanlışsa, motor `FileNotFoundException` fırlatır; bu yüzden yazımını iki kez kontrol edin.

> **Neden Önemli:** Görüntünün doğru yüklenmesi temeldir. Görüntü okunamazsa OCR motorunun tanıyacak bir şeyi olmaz ve boş bir JSON sonucu elde edersiniz.

## Adım 3: Motoru JSON Döndürmesi İçin Ayarlayın

Aspose OCR, XML, düz metin veya JSON üretebilir. Modern API’ler için JSON en esnek olandır, bu yüzden formatı açıkça ayarlayacağız.

```java
ocrEngine.getResultSettings()
         .setResultFormat(OcrResultFormat.JSON); // XML is also available
```

Eğer alt sisteminiz XML tercih ediyorsa, tek bir değişiklikle `OcrResultFormat.XML`’e geçebilirsiniz. API, birbirinin yerine kullanılabilecek şekilde tasarlanmıştır.

## Adım 4: Tanıma İşlemini Çalıştırın

Görüntü yüklendi ve format ayarlandı, bir sonraki adım **recognize text from receipt** işlemini gerçekleştirmektir. İşte asıl ağır iş burada gerçekleşir.

```java
// Step 4: Perform OCR
OcrResult ocrResult = ocrEngine.recognize();
```

`recognize()` çağrısı, motor görüntüyü analiz edip bitene kadar bloklanır. Büyük görüntüler için bu işlemi arka plan thread’inde çalıştırmak isteyebilirsiniz, ancak tipik bir fiş için bir saniyenin çok altında tamamlanır.

## Adım 5: JSON Sonucunu Alın

Son olarak ham JSON dizesini çıkarıp ekrana bastırıyoruz. Bu dize, tanınan her metin parçasını, sınırlama kutusunu, güven skorlarını ve daha fazlasını içerir.

```java
// Step 5: Retrieve the JSON string
String jsonResult = ocrResult.getResultAsString();
System.out.println(jsonResult);
```

### Beklenen Çıktı

Temiz bir fişe karşı tam programı çalıştırdığınızda aşağıdakine benzer bir sonuç alırsınız:

```json
{
  "pages": [
    {
      "blocks": [
        {
          "text": "Store Name",
          "confidence": 0.98,
          "rectangle": { "x": 12, "y": 15, "width": 200, "height": 30 }
        },
        {
          "text": "Date: 2026-04-28",
          "confidence": 0.95,
          "rectangle": { "x": 12, "y": 50, "width": 180, "height": 20 }
        },
        {
          "text": "Total $23.45",
          "confidence": 0.99,
          "rectangle": { "x": 12, "y": 120, "width": 150, "height": 25 }
        }
      ]
    }
  ]
}
```

Her fiş satırının ayrı bir blok ve bir güven skoru olduğunu görebilirsiniz. Artık bu JSON’u herhangi bir sonraki sisteme besleyebilirsiniz—veritabanına kaydedin, HTTP üzerinden gönderin ya da bir makine‑öğrenme modeline besleyin.

## Tam Çalışan Örnek

Aşağıda her şeyi bir araya getiren, bağımsız bir Java sınıfı yer alıyor. Kopyalayıp yapıştırın, görüntü yolunu ayarlayın ve `mvn compile exec:java` (veya eşdeğer Gradle komutunu) çalıştırın.

```java
import com.aspose.ocr.*;

public class JsonExportExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the image you want to process
        // Make sure the path points to a real receipt image on your machine
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/receipt.png"));

        // Step 3: Configure the engine to return results in JSON format
        ocrEngine.getResultSettings()
                 .setResultFormat(OcrResultFormat.JSON); // XML is also available

        // Step 4: Run the OCR recognition process
        OcrResult ocrResult = ocrEngine.recognize();

        // Step 5: Retrieve the raw JSON string and output it
        String jsonResult = ocrResult.getResultAsString();
        System.out.println(jsonResult);
    }
}
```

> **Dikkat Edilmesi Gerekenler:**  
> • **Dosya yolu hataları** – Windows ile macOS/Linux arasındaki slash’ları iki kez kontrol edin.  
> • **Bellek yetersizliği** – büyük görüntüler için `ocrEngine.setMemoryOptimization(true)` gerekebilir.  
> • **Dil ayarları** – fişiniz Latin dışı karakterler içeriyorsa, `ocrEngine.setLanguage(OcrLanguage.SPANISH)` (veya desteklenen başka bir dil) çağrısını `recognize()` öncesinde yapın.

## Çözümü Test Etme

1. **Programı çalıştırın** – konsolda bir JSON bloğu görmelisiniz.  
2. **JSON’u doğrulayın** – çıktıyı <https://jsonlint.com/> adresine yapıştırarak geçerli bir yapı olduğundan emin olun.  
3. **Parse edin** – gerçek bir projede, JSON’u POJO’lara haritalamak için Jackson ya da Gson gibi bir kütüphane kullanırsınız.

Eğer boş bir `pages` dizisi alıyorsanız, en yaygın nedenler şunlardır: görüntü dosyası bulunamıyor ya da görüntü motorun varsayılan ayarları için çok bulanıktır. İkinci durumda DPI’yı artırmayı ya da ön‑işleme (ör. ikilileştirme) uygulamayı deneyin.

## Varyasyonlar ve Kenar Durumları

| Senaryo | Ne Değiştirilir |
|----------|----------------|
| **Birden fazla sayfa** (ör. çok‑sayfalı PDF’in görüntülere dönüştürülmesi) | Her görüntü üzerinde döngü kurun, döngü içinde `ocrEngine.setImage(...)` çağırın ve JSON sonuçlarını birleştirin. |
| **Farklı çıktı formatı** | `OcrResultFormat.JSON` yerine `OcrResultFormat.XML` ya da `OcrResultFormat.PLAIN_TEXT` kullanın. |
| **Performans ayarı** | Hız için `ocrEngine.setRecognitionMode(OcrRecognitionMode.FAST)`, kalite için `OcrRecognitionMode.ACCURATE` seçin. |
| **Fiş dışı belgeler** | Tablo çıkarımı gerekiyorsa `ocrEngine.getPageSegmentationSettings().setDetectTables(true)` ayarını değiştirin. |

Bu ince ayarlar, **extract text from image java** akışını gerçek dünya problemlerine uyarlamanızı sağlar.

## Sonuç

Aspose OCR kullanarak **extract text from image java** işlemini üretim‑hazır, kısa bir yöntemle ele aldık. Beş adımı izleyerek—motoru oluşturun, **load image for OCR**, JSON çıktıyı ayarlayın, **recognize text from receipt** yapın ve son olarak JSON’u okuyun—OCR’u herhangi bir Java backend’ine minimum çabayla entegre edebilirsiniz.  

İleride yapabilecekleriniz:

- JSON’u daha sonra analiz için bir NoSQL veritabanına kaydetmek.  
- Sonuçları, fişler hakkında soruları yanıtlayan bir sohbet botuna yönlendirmek.  
- PDF, DOCX ve diğer formatları işlemek için Apache Tika ile birleştirmek.

Deneyin, ayarları belgelerinize göre özelleştirin ve makinenin ağır işini yapmasına izin verin; siz değer yaratmaya odaklanın.

---

![görüntüden metin çıkarma java](placeholder-image.png "görüntüden metin çıkarma java")

*Şekil: OCR boru hattının görsel temsili – görüntü dosyasından JSON çıktısına.*  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}