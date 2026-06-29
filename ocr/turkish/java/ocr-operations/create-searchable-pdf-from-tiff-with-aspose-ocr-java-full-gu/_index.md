---
category: general
date: 2026-06-28
description: Aspose OCR kullanarak Java’da çok sayfalı bir TIFF’ten aranabilir PDF
  oluşturun. TIFF’i PDF’ye nasıl dönüştüreceğinizi ve anında aranabilirlik için OCR
  metin katmanı eklemeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- add ocr text layer pdf
language: tr
og_description: Aspose OCR kullanarak Java'da bir TIFF görüntüsünden aranabilir PDF
  oluşturun. Bu kılavuz, TIFF'i PDF'ye dönüştürmeyi ve aranabilir belgeler için OCR
  metin katmanı eklemeyi gösterir.
og_title: Aspose OCR (Java) ile TIFF'ten Aranabilir PDF Oluştur
schemas:
- author: Aspose
  dateModified: '2026-06-28'
  description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  headline: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  type: TechArticle
- description: Create searchable PDF from a multi‑page TIFF in Java using Aspose OCR.
    Learn how to convert TIFF to PDF and add OCR text layer PDF for instant searchability.
  name: Create Searchable PDF from TIFF with Aspose OCR (Java) – Full Guide
  steps:
  - name: What if my TIFF is single‑page?
    text: The same code works—Aspose treats a single‑page TIFF as a one‑element collection,
      so no extra handling is required.
  - name: Can I control the OCR language?
    text: 'Yes. Before calling `recognizeAndExportPdf`, set the language on the engine:'
  - name: How do I skip embedding the original image to reduce file size?
    text: Just set `pdfOptions.setEmbedOriginalImage(false)`. The PDF will contain
      only the searchable text layer, which dramatically shrinks the file but loses
      the visual representation.
  - name: Is the generated PDF truly searchable on all platforms?
    text: Modern PDF readers (Adobe Acrobat, Foxit, even browsers) honor the text
      layer. Some older, lightweight viewers might ignore it—test on your target platform
      if you’re unsure.
  type: HowTo
tags:
- Aspose OCR
- Java
- PDF Generation
title: Aspose OCR (Java) ile TIFF'ten Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/java/ocr-operations/create-searchable-pdf-from-tiff-with-aspose-ocr-java-full-gu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIFF'ten Aranabilir PDF Oluşturma Aspose OCR (Java) – Tam Kılavuz

Hiç bir taranmış TIFF'ten **aranabilir PDF** oluşturmanın saatlerce üçüncü‑taraf araçlarla uğraşmadan nasıl yapılacağını merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler sürekli büyük görüntü dosyalarını gerçekten arayabileceğiniz PDF'lere dönüştürmenin güvenilir bir yoluna ihtiyaç duyuyor.  

Bu öğreticide, sadece **TIFF'i PDF'ye dönüştürmek** değil, aynı zamanda **OCR metin katmanı PDF** eklemek için otomatik bir pratik, uçtan uca çözümü adım adım göstereceğiz; sadece birkaç Java satırıyla gerçekten aranabilir bir belge elde edeceksiniz.

## Öğrenecekleriniz

- Aspose OCR for Java'ı nasıl kuracağınızı ve bir lisans uygulayacağınızı (isteğe bağlı ama önerilir) öğrenin.  
- `OcrEngine` kullanarak **TIFF'i PDF'ye dönüştürmek** için kesin adımları öğrenin.  
- `PdfExportOptions`'ı nasıl yapılandıracağınızı, böylece oluşturulan dosyanın görünmez, aranabilir bir metin katmanı içermesini—gerçek dünyada **OCR metin katmanı PDF ekleme** ne anlama geldiğini—öğrenin.  
- Beklenen çıktıyı ve her şeyin doğru çalıştığını hızlıca kontrol etmeyi öğrenin.

Aspose ile ilgili önceden bir deneyime ihtiyacınız yok; temel bir Java geliştirme ortamı (JDK 8+ ve herhangi bir IDE) yeterli.

---

## Adım 1: Projenizi Hazırlayın ve Aspose OCR Lisansını Uygulayın  

Herhangi bir OCR API'sini çağırmadan önce, Aspose OCR JAR'larını sınıf yolunuza eklemeniz gerekir. Ticari bir lisansınız varsa, `.lic` dosyasını erişilebilir bir yere koyun ve `License` sınıfını ona yönlendirin. Bu adım zorunlu değildir—Aspose değerlendirme modunda çalışır, ancak lisans su işaretlerini kaldırır ve tam özellik setini açar.

```java
// Apply your Aspose OCR license (optional for full features)
License license = new License();
license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");
```

> **Pro ipucu:** Lisans dosyasını kaynak kontrolünüzün dışına tutarak yanlışlıkla ifşa edilmesini önleyin.

---

## Adım 2: OCR Motorunu Oluşturun  

`OcrEngine` nesnesi oluşturmak, **aranabilir pdf oluşturma** yönündeki ilk gerçek adımdır. Motor, tüm OCR ayarlarını tutar ve daha sonra dönüşümü yönetecektir.

```java
// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();
```

Neden ayrı bir motor? Aynı yapılandırmayı birden çok dosya arasında yeniden kullanmanıza olanak tanır; bu, onlarca TIFF'i toplu işleme yaptığınızda kullanışlıdır.

---

## Adım 3: Çok Sayfalı TIFF'inizi Yükleyin  

Aspose OCR, çok sayfalı bir TIFF'i yüklemeyi çok kolay hâle getirir. Dosya yolunu bir `OcrInput` nesnesine eklemeniz yeterlidir; kütüphane otomatik olarak her sayfayı algılar ve kuyruğa alır.

```java
// Load a multi‑page TIFF image as OCR input
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically
```

Eğer **TIFF'i PDF'ye dönüştürmek** için tek tek sayfa işlemek isterseniz, bir döngü içinde `ocrInput.add(pageStream)` çağrısı yapabilirsiniz—Aspose her çağrıyı ayrı bir sayfa olarak ele alır.

---

## Adım 4: PDF Dışa Aktarma Seçeneklerini Yapılandırma – OCR Metin Katmanını Eklemek  

Bu, **OCR metin katmanı pdf ekleme** için sihrin gerçekleştiği yerdir. Birkaç bayrağı değiştirerek Aspose'a orijinal bitmap'i gömmesini (görsel bütünlüğün korunması için) *ve* arama motorlarının indeksleyebileceği gizli bir metin katmanı oluşturmasını söylersiniz.

```java
// Configure PDF export options
PdfExportOptions pdfOptions = new PdfExportOptions();
pdfOptions.setEmbedOriginalImage(true);      // keep the bitmap as background
pdfOptions.setCreateSearchablePdf(true);     // generate hidden text layer for search
pdfOptions.setAuthor("John Doe");
pdfOptions.setTitle("OCR Output");
```

- `setEmbedOriginalImage(true)`: PDF'in taranmış görüntüyle tam olarak aynı görünmesini sağlar.  
- `setCreateSearchablePdf(true)`: görünmez metin katmanını oluşturur—bu, **OCR metin katmanı pdf ekleme**'nin özüdür.  

Gösterildiği gibi metadata'yı (yazar, başlık, konu) zenginleştirmekten çekinmeyin; bu, belge yönetimini ileride kolaylaştırır.

---

## Adım 5: OCR'ı Çalıştırın ve Aranabilir PDF'yi Dışa Aktarın  

Şimdi her şeyi bir araya getiriyoruz. `recognizeAndExportPdf` metodu ağır işi yapar: her TIFF sayfasında OCR çalıştırır, görsel görüntüyü yazar ve aranabilir metni üstüne bindirir.

```java
// Perform OCR recognition and export the result as a searchable PDF
ocrEngine.recognizeAndExportPdf(
    ocrInput,
    "YOUR_DIRECTORY/searchable.pdf",
    pdfOptions
);

System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
```

Konsol başarı mesajını yazdırdığında, bir TIFF dosyasından **aranabilir pdf oluşturmuş** olursunuz. Ortaya çıkan `searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açın, `Ctrl+F` tuşuna basın ve orijinal görüntüde yer alan bir kelimeyi aramayı deneyin—anında bulunmalıdır.

---

## Sonucu Doğrulama – Hızlı Kontrol Listesi  

1. **Görsel bütünlük** – PDF, kaynak TIFF ile tam olarak aynı görünmelidir (`setEmbedOriginalImage` sayesinde).  
2. **Aranabilirlik** – Görüntüleyicinin arama fonksiyonunu kullanın; gizli metin katmanı eşleşmeler döndürmelidir.  
3. **Metadata** – PDF özelliklerini açarak daha önce ayarladığınız yazar ve başlığı doğrulayın.  

Bu kontrollerden herhangi biri başarısız olursa, `setCreateSearchablePdf(true)`'in etkin olduğundan ve lisansınızın (varsa) kısıtlamalı değerlendirme modunda olmadığından emin olun.

---

## Kenar Durumları ve Yaygın Sorular  

### TIFF'im tek sayfalıysa ne olur?  

Aynı kod çalışır—Aspose tek sayfalı TIFF'i tek elemanlı bir koleksiyon olarak ele alır, bu yüzden ekstra bir işlem gerekmez.

### OCR dilini kontrol edebilir miyim?  

Evet. `recognizeAndExportPdf`'yi çağırmadan önce motor üzerindeki dili ayarlayın:

```java
ocrEngine.getLanguage().setLanguage(OcrLanguage.English);
```

`English` ifadesini desteklenen herhangi bir dil enum'u ile değiştirin.

### Dosya boyutunu azaltmak için orijinal görüntünün gömülmesini nasıl atlayabilirim?  

Sadece `pdfOptions.setEmbedOriginalImage(false)` ayarlayın. PDF yalnızca aranabilir metin katmanını içerecek, bu dosyayı büyük ölçüde küçültecek ancak görsel temsili kaybedecektir.

### Oluşturulan PDF tüm platformlarda gerçekten aranabilir mi?  

Modern PDF okuyucular (Adobe Acrobat, Foxit, hatta tarayıcılar) metin katmanını tanır. Bazı eski, hafif okuyucular bunu görmezden gelebilir—eğer emin değilseniz hedef platformunuzda test edin.

---

## Tam Çalışan Örnek  

Aşağıda eksiksiz, çalıştırmaya hazır Java sınıfı yer almaktadır. Yer tutucu yolları gerçek yollarla değiştirin, Aspose OCR JAR'larını projenize ekleyin ve çalıştırın.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Apply your Aspose OCR license (optional for full features)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.Java.lic");

        // Step 2: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 3: Load a multi‑page TIFF image as OCR input
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/multipage.tif");   // all pages are added automatically

        // Step 4: Configure PDF export options
        PdfExportOptions pdfOptions = new PdfExportOptions();
        pdfOptions.setEmbedOriginalImage(true);    // keep the bitmap as background
        pdfOptions.setCreateSearchablePdf(true);   // generate hidden text layer for search
        pdfOptions.setAuthor("John Doe");
        pdfOptions.setTitle("OCR Output");

        // Step 5: Perform OCR recognition and export the result as a searchable PDF
        ocrEngine.recognizeAndExportPdf(
            ocrInput,
            "YOUR_DIRECTORY/searchable.pdf",
            pdfOptions
        );

        System.out.println("Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Beklenen çıktı (konsol):**

```
Searchable PDF generated at YOUR_DIRECTORY/searchable.pdf
```

`searchable.pdf` dosyasını açın ve orijinal TIFF'te yer alan herhangi bir kelimeyi aramayı deneyin—voilà, başarıyla **aranabilir pdf oluşturmuş** oldunuz!

---

## Sonuç  

Aspose OCR for Java kullanarak bir TIFF'ten **aranabilir PDF** oluşturmanın eksiksiz, üretim‑hazır bir yolunu adım adım gösterdik. `PdfExportOptions`'ı yapılandırarak otomatik olarak **OCR metin katmanı PDF** eklemiş olursunuz; statik görüntüleri anında aranabilir belgelere dönüştürürsünüz.  

Daha ileri gitmeye hazırsanız, aşağıdakilerle denemeler yapmayı düşünün:

- Özel sayfa boyutları veya DPI ayarlarıyla **TIFF'i PDF'ye dönüştürmek**.  
- OCR sonrası filigranlar veya dijital imzalar eklemek.  
- Basit bir `for` döngüsüyle bir klasördeki TIFF'leri toplu işleme.  

Bu uzantıların her biri, ele aldığımız aynı temel kavramlar üzerine inşa edildiği için geçişi sorunsuz bulacaksınız.  

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Aşağıya yorum bırakın, iyi kodlamalar!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak adım adım açıklamalı eksiksiz çalışan kod örnekleri içerir.

- [PDF Metni Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/english/java/ocr-operations/recognize-pdf/)
- [.NET'te Aspose.OCR ile PDF'yi OCR Yapma](/ocr/english/net/text-recognition/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}