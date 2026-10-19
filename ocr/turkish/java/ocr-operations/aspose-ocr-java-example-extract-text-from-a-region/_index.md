---
category: general
date: 2026-05-03
description: Aspose OCR Java örneği, OCR için görüntüyü nasıl yükleyeceğinizi ve sadece
  birkaç satır kodla bir bölgeden metin nasıl çıkarılacağını gösterir.
draft: false
keywords:
- aspose ocr java example
- load image for OCR
- extract text from region
language: tr
og_description: Aspose OCR Java örneği, OCR için bir görüntünün yüklenmesini ve belirli
  bir bölgeden metin çıkarılmasını gösterir; fatura işleme için mükemmeldir.
og_title: Aspose OCR Java Örneği – Bölge Metni Çıkarma
tags:
- Aspose OCR
- Java
- Image Processing
title: 'Aspose OCR Java Örneği: Bir Bölgeden Metin Çıkarma'
url: /tr/java/ocr-operations/aspose-ocr-java-example-extract-text-from-a-region/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Java Örneği: Bir Bölgeden Metin Çıkarma

Bir görüntüden sadece ihtiyacınız olan kısmı almanızı sağlayan bir **Aspose OCR Java örneği** mi arıyorsunuz? Bu rehberde **OCR için bir görüntü yüklemeyi** ve **bir bölgeden metin çıkarmayı** adım adım inceleyeceğiz; fatura numaraları, form alanları veya daha büyük bir resmin içinde gizli herhangi bir veri parçası için mükemmeldir.

Neden OCR'ı tüm sayfayı taramak yerine bir dikdörtgene sınırlayacağınızı merak ediyor olabilirsiniz. Kısa cevap: hız ve doğruluk. Motor yalnızca tanımlı bir dilimi incelediğinde alakasız gürültüyü atlar, daha hızlı çalışır ve genellikle daha temiz sonuçlar üretir. Bu öğreticinin sonunda, tam da bunu yapan, yeni başlayanların sıkça takıldığı yaygın tuzaklardan kaçınmak için birkaç ipucu içeren bağımsız bir Java programına sahip olacaksınız.

## Gereksinimler

- **Java Development Kit (JDK) 11** veya daha yeni bir sürüm kurulu olmalı.
- **Aspose.OCR for Java** kütüphanesi (en son JAR dosyasını Maven Central deposundan veya Aspose indirme portalından alabilirsiniz).
- Okumak istediğiniz metni içeren bir görüntü dosyası – demo için `invoice.png` dosyasını kullanacağız; bu dosya fatura numarasını sağ‑üst köşeye yakın bir yerde tutar.
- Sevdiğiniz bir IDE veya basit bir metin editörü ve bir terminal; herhangi bir derleme aracı (Maven, Gradle veya düz `javac`) işinizi görecektir.

Hepsi bu. Ek OCR motorları, yerel ikili dosyalar yok; sadece saf Java ve Aspose.

![Aspose OCR Java örnek ekran görüntüsü](/images/aspose-ocr-java-example.png "Aspose OCR Java örneği bölge çıkarımını gösteriyor")

## Aspose OCR Java Örneği – OCR Motorunu Başlatma

Her OCR iş akışının ilk ihtiyacı bir motor örneğidir. Aspose, görüntü yüklemeden dil seçimine kadar her şeyi yöneten hafif bir `OcrEngine` sınıfı sunar.

```java
import com.aspose.ocr.*;

public class RegionOcrExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**Neden önemli:** Motoru önceden oluşturmak, yapılandırılacak temiz bir nesne sağlar. Bir toplu işlem yapıyorsanız aynı `OcrEngine`i birden fazla görüntüde yeniden kullanabilirsiniz; bu bellek ve başlatma süresinden tasarruf eder.

## OCR için Görüntü Yükleme

Şimdi motorun tarayacağı resmi belirtelim. Aspose, düşük seviyeli `FileInputStream` kalıbını soyutlayan `ImageStream.fromFile` yardımcı metodunu sağlar.

```java
        // Step 2: Load the image that contains the invoice
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/invoice.png"));
```

**İpucu:** `YOUR_DIRECTORY` ifadesini `invoice.png` dosyanızı sakladığınız mutlak ya da göreli yol ile değiştirin. Dosya bulunamazsa Aspose bir `IOException` fırlatır; üretim kodunda bunu bir try‑catch bloğuna almanız iyi olur.

## Bir Bölge Tanımlama ve Metin Çıkarma

Şimdi gösterinin yıldızı geliyor: motorun nerede bakacağını belirten dikdörtgen. `java.awt.Rectangle` yapıcı metodu `(x, y, width, height)` alır – tüm ölçüler piksel cinsindendir.

```java
        // Step 3: Define the region where the invoice number is located (x, y, width, height)
        java.awt.Rectangle invoiceRegion = new java.awt.Rectangle(120, 250, 300, 80);
        ocrEngine.setRegion(invoiceRegion);   // restrict recognition to this area
```

**Nasıl çalışır:** `setRegion` çağrısıyla OCR taramasını, sol kenardan 120 piksel, üstten 250 piksel başlayan ve 300 piksel genişliğinde bir dilime sınırlarsınız. Bu sayıları kendi düzeninize göre ayarlayın; hızlı bir yol, piksel koordinatlarını gösteren herhangi bir grafik editöründe görüntüyü açmaktır.

## Dili Etkinleştir ve Tanıma Çalıştır

Aspose OCR onlarca dili destekler, ancak bir fatura numarası için sadece İngilizceye ihtiyacımız var. Doğru dili etkinleştirmek yanlış pozitifleri büyük ölçüde azaltır.

```java
        // Step 4: Enable English language for recognition
        ocrEngine.getLanguage().setEnglish(true);

        // Step 5: Perform recognition and output the extracted text
        if (ocrEngine.recognize()) {
            System.out.println("Extracted region text: " + ocrEngine.getText());
        } else {
            System.err.println("OCR recognition failed.");
        }
    }
}
```

**Neden sadece İngilizce etkinleştiriliyor?** OCR motoru, etkinleştirilmiş tüm dil setlerinden karakter eşleştirmeye çalışır; bu, metin sadece alfanümerik olduğunda motoru şaşırtabilir. Dil kapsamını daraltmak hem hızı hem de kesinliği artırır.

### Beklenen Çıktı

Her şey doğru ayarlandığında aşağıdakine benzer bir şey görmelisiniz:

```
Extracted region text: INV-12345
```

Dikdörtgen birkaç piksel kaymışsa, çıktı bozuk ya da boş olabilir. Bu basit bir doğrulama kontrolüdür: programı çalıştırın, konsola bakın ve metnin görüntüde gördüklerinizle eşleştiğinden emin olun.

## Kodu Çalıştır ve Çıktıyı Doğrula

Maven kullandığınızı varsayalım, `pom.xml` dosyanıza Aspose OCR bağımlılığını ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- Use the latest version available -->
</dependency>
```

Derleyin ve çalıştırın:

```bash
mvn compile exec:java -Dexec.mainClass=RegionOcrExample
```

Ya da düz `javac` tercih ediyorsanız:

```bash
javac -cp "aspose-ocr-23.10.jar" RegionOcrExample.java
java -cp ".:aspose-ocr-23.10.jar" RegionOcrExample
```

**Extracted region text** satırının konsola yazdırıldığını görmelisiniz. “OCR recognition failed” hatası alırsanız, dosya yolunu tekrar kontrol edin ve bölgenin gerçekten okunabilir karakterler içerdiğinden emin olun.

## Kenar Durumları ve Yaygın Varyasyonlar

| Durum | Değiştirilecek Şey |
|-----------|----------------|
| **Birden fazla dil** (ör. İngilizce + İspanyolca) | `ocrEngine.getLanguage().setSpanish(true);` ifadesini İngilizceyle birlikte çağırın. |
| **Bölge görüntü sınırları dışında** | Aspose dikdörtgeni sessizce kırpar, ancak veri kaybı yaşarsınız. `ImageInfo` (`ocrEngine.getImage().getWidth()`) kullanarak boyutları kontrol edip bölgeyi ayarlamadan önce doğrulayın. |
| **Dinamik faturalar** (farklı düzenler) | “Invoice #” gibi anahtar kelimeleri bulmak için tüm görüntüde hafif bir ön‑tarama yapıp ardından dikdörtgeni programatik olarak hesaplamayı düşünün. |
| **Yüksek DPI görüntüler** | Tarama belgelerinde daha iyi doğruluk için `ocrEngine.getImage().setResolution(300);` değerini artırın. |
| **Performans ayarı** | Gereksiz dilleri devre dışı bırakın, bölgeyi mümkün olduğunca küçük tutun ve birçok dosya arasında tek bir `OcrEngine` örneğini yeniden kullanın. |

## Saha Deneyiminden Pro İpuçları

- **Pro ipucu:** Sadece rakamlara (fatura numaraları için yaygın) ihtiyacınız varsa, `ocrEngine.getLanguage().setDigits(true);` ile sayısal modu etkinleştirin. Bu, alfabetik gürültüyü ortadan kaldırır.
- **Dikkat edilmesi gereken:** Şeffaf PNG'ler. Aspose bazen alfa kanalını yanlış yorumlayabilir; görüntüyü önce katı arka planlı bir JPEG'e dönüştürmek tuhaf boş çıktıları çözebilir.
- **Unutmayın:** Dikdörtgen, ekranınızdaki UI ölçeklendirmesinden değil, görüntünün yerel koordinat sistemini kullanır. Üretimde işleyeceğiniz tam dosyayla her zaman test edin.

## Sıradaki Adımlar?

Şimdi bölge‑tabanlı çıkarım için sağlam bir **Aspose OCR Java örneği** elde ettiğinize göre, bunu birkaç faydalı yönde genişletebilirsiniz:

- **Toplu işleme:** Faturalar klasöründe döngü kurarak aynı `OcrEngine`i yeniden kullanın; bu, iş hacmini artırır.
- **Veri doğrulama:** Çıkarılan metni `INV-\\d{5}` gibi bir regex ile işleyerek geçerli bir fatura numarası yakaladığınızdan emin olun.
- **PDF entegrasyonu:** Aspose.PDF kullanarak çıkarılan metni orijinal belgeye geri yerleştirip denetim izleri oluşturun.
- **Bulut dağıtımı:** Kodu hafif bir REST servisine (Spring Boot) sararak diğer sistemlerin talep üzerine çağırmasını sağlayın.

Bu adımlar aynı temel kavramları—**OCR için görüntü yükleme**, **bir bölgeden metin çıkarma** ve sonuçları işleme—kullanır; bu yüzden geçiş sorunsuz olacaktır.

---

*Kodlamaktan keyif alın! Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da topluluğun zorlayıcı düzenler için gerçek dünya ipuçlarını paylaştığı Aspose forumlarını kontrol edin.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}