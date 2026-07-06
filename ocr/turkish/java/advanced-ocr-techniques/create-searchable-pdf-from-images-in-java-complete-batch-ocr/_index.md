---
category: general
date: 2026-06-19
description: Aspose OCR kullanarak Java’da aranabilir PDF oluşturun – toplu OCR işleme
  ile görüntüleri İspanyolca dil desteğiyle aranabilir PDF’ye dönüştürün.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- images to searchable pdf
- batch convert images
- ocr language spanish
language: tr
og_description: Aspose OCR ile Java’da aranabilir PDF oluşturun. Toplu OCR işleme
  hakkında bilgi edinin, görüntüleri aranabilir PDF’ye dönüştürün ve OCR dilini İspanyolca
  olarak ayarlayın.
og_title: Java'da Görsellerden Aranabilir PDF Oluşturma – Tam Toplu OCR Eğitimi
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Create searchable PDF in Java using Aspose OCR – batch OCR processing
    to convert images to searchable PDF with Spanish language support.
  headline: Create Searchable PDF from Images in Java – Complete Batch OCR Guide
  type: TechArticle
tags:
- Java
- OCR
- Aspose
- PDF
title: Java'da Görüntülerden Aranabilir PDF Oluşturma – Tam Batch OCR Rehberi
url: /tr/java/advanced-ocr-techniques/create-searchable-pdf-from-images-in-java-complete-batch-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntülerden Aranabilir PDF Oluşturma – Tam Batch OCR Kılavuzu

Hiç **aranabilir PDF** dosyalarını taranmış bir resim yığını üzerinden oluşturmanız gerekti mi? Tek başınıza değilsiniz—şirketler kağıt arşivlerini sürekli olarak aranabilir PDF'lere dönüştürerek verilerinin anında bulunabilir olmasını sağlıyor.  

Tüm bu iş akışını tek bir Java programı ile otomatikleştirip bir seferde onlarca hatta binlerce dosyayı işleyebileceğinizi hayal edin. Bu öğreticide **batch OCR processing** (toplu OCR işleme) konusunu Aspose OCR kullanarak, bir klasördeki görüntüleri **OCR dili İspanyolca** olarak belirleyip aranabilir PDF'lere dönüştürerek adım adım inceleyeceğiz. Sonunda, **görüntüleri toplu olarak** aranabilir PDF'lere dönüştüren, her dosya için tek tek bir şey yapmadan çalıştırabileceğiniz bir proje elde edeceksiniz.

## Öğrenecekleriniz

* Bir Java projesinde Aspose OCR'un nasıl kurulacağını.  
* Bir klasörü tarayan, görüntü türlerini filtreleyen ve çıktı PDF'lerini yazan bir batch işlemcisinin yapılandırılması.  
* Hız kritik iş yükleri için GPU hızlandırmasının etkinleştirilmesi.  
* Deskew ve denoise gibi faydalı ön işleme adımlarının uygulanması.  
* OCR dili (İspanyolca) ve çıktı formatının (aranabilir PDF) belirtilmesi.  

Harici betikler, manuel kopyala‑yapıştır yok—her şeyi yapan tek bir temiz `main` metodu.

---

## Önkoşullar

| Gereksinim | Neden Önemlidir |
|-------------|----------------|
| Java 17 veya üzeri (veya `java.nio.file` API'sini destekleyen herhangi bir JDK) | Modern dil özellikleri ve daha iyi modül yönetimi. |
| Aspose OCR for Java kütüphanesi (Aspose.com'dan indirin) | `OcrBatchProcessor` ve ilgili sınıfları sağlar. |
| Geçerli bir Aspose OCR lisans dosyası (`Aspose.OCR.lic`) | Lisans olmadan kütüphane su işaretiyle değerlendirme modunda çalışır. |
| Dönüştürmek istediğiniz görüntü dosyalarını içeren bir klasör (`.png`, `.jpg`, `.tif`) | Batch işlemci girdi olarak buraya bakar. |
| İsteğe bağlı: CUDA desteği olan bir GPU | `.useGpu(true)` bayrağını etkinleştirerek OCR hızını artırır. |

Bu bileşenler elinizdeyse, başlayalım.

---

## Adım 1 – Aranabilir PDF Oluşturma: Proje Kurulumu

İlk olarak yeni bir Maven (veya Gradle) projesi oluşturun ve Aspose OCR bağımlılığını ekleyin. İşte Maven için minimal bir `pom.xml` kesiti:

```xml
<project>
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.example</groupId>
    <artifactId>ocr-batch</artifactId>
    <version>1.0.0</version>

    <dependencies>
        <dependency>
            <groupId>com.aspose</groupId>
            <artifactId>aspose-ocr</artifactId>
            <version>23.11</version> <!-- use the latest stable version -->
        </dependency>
    </dependencies>
</project>
```

> **İpucu:** Sürüm numarasını güncel tutun; yeni sürümler performans iyileştirmeleri ve ek dil paketleri getirir.

Maven kütüphaneyi çözdükten sonra `src/main/java/com/example/OcrBatchTutorial.java` dosyasını oluşturun. **Aranabilir PDF oluşturma** mantığı burada yer alacak.

---

## Adım 2 – Batch OCR İşleme Yapılandırması

Çözümün kalbi, akıcı yapılandırıcı `OcrBatchProcessor.builder()`dır. Okunabilir bir şekilde yapılandırma çağrılarını zincirlemenizi sağlar. Aşağıda, her parçayı açıklayan satır içi yorumlarla birlikte tam `main` metodu yer alıyor.

```java
package com.example;

import com.aspose.ocr.*;
import java.nio.file.*;

public class OcrBatchTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license – mandatory for production use
        License license = new License();
        license.setLicense("Aspose.OCR.lic");   // place the .lic file next to your executable

        // 2️⃣ Build the batch processor and point it at the folder containing source images
        OcrBatchProcessor.builder()
            .inputFolder(Paths.get("YOUR_DIRECTORY/input/"))   // <-- change to your input path

            // 3️⃣ Define where the processed searchable PDFs will be saved
            .outputFolder(Paths.get("YOUR_DIRECTORY/output/")) // <-- change to your output path

            // 4️⃣ Limit processing to the desired image extensions (helps skip unrelated files)
            .includeExtensions(".png", ".jpg", ".tif")        // <-- matches images to searchable pdf conversion

            // 5️⃣ Choose the OCR language – here we use Spanish (ocr language spanish)
            .language(Language.Spanish)

            // 6️⃣ Turn on GPU acceleration if a compatible GPU is present
            .useGpu(true)

            // 7️⃣ Apply a chain of preprocessing filters: deskew then denoise
            .preprocess(p -> p.deskew().denoise())

            // 8️⃣ Set the output format to a searchable PDF (the final product)
            .outputFormat(OutputFormat.SearchablePdf)

            // 9️⃣ Execute the batch operation on every matching file
            .run();

        System.out.println("✅ Batch conversion complete! Check the output folder.");
    }
}
```

### Her Ayarın Önemi

* **License** – Lisans olmadan su işaretli PDF'ler alırsınız; bu da aranabilir bir arşiv amacını bozar.  
* **inputFolder / outputFolder** – Kaynak ve hedefi net bir şekilde ayırmak, yanlışlıkla üzerine yazmayı önler.  
* **includeExtensions** – `.png`, `.jpg`, `.tif` filtrelemesi, işlemcinin yalnızca görüntü dosyalarına dokunmasını sağlar; klasik bir **görüntüleri toplu olarak dönüştürme** korumasıdır.  
* **language(Language.Spanish)** – Doğru dilin seçilmesi tanıma doğruluğunu büyük ölçüde artırır, özellikle İspanyolca'da sık görülen aksanlı karakterler için.  
* **useGpu(true)** – OCR CPU‑ağırdır; GPU’ya aktarım modern donanımda işleme süresini yarıya indirebilir.  
* **preprocess(p -> p.deskew().denoise())** – Deskew eğik taramaları hizalar, denoise arka plan gürültüsünü temizler—her ikisi de **görüntülerden aranabilir pdf** kalitesini artırır.  
* **outputFormat(OutputFormat.SearchablePdf)** – Aspose'a PDF içinde gizli bir metin katmanı eklemesini söyler, böylece PDF aranabilir olur.

---

## Adım 3 – Uygulamayı Çalıştırma ve Çıktıyı Doğrulama

Programı derleyip çalıştırın:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.example.OcrBatchTutorial"
```

Her şey doğru bağlandıysa, konsolda şu mesajı göreceksiniz:

```
✅ Batch conversion complete! Check the output folder.
```

`YOUR_DIRECTORY/output/` klasörüne gidin. Her giriş görüntüsü artık karşılık gelen bir `.pdf` dosyasına sahip olmalı. PDF'i Adobe Reader ya da tarayıcınızda açın ve orijinal görüntüde bulunan bir kelimeyi aramayı deneyin—metin vurgulanıyorsa, **aranabilir pdf oluşturma** işlemini başarıyla tamamlamışsınız demektir.

### Beklenen Çıktı Örneği

| Giriş dosyası | Çıktı dosyası | Boyut (yaklaşık) |
|--------------------|---------------------------|----------------|
| `invoice_001.png`  | `invoice_001.pdf`         | 1.2 MB |
| `contract_2023.tif`| `contract_2023.pdf`       | 2.5 MB |
| `receipt.jpg`      | `receipt.pdf`             | 0.9 MB |

PDF boyutunun makul olduğunu fark edeceksiniz; Aspose sadece OCR‑tarafından üretilen metin katmanını ekler, tam çözünürlüklü bir görüntü kopyasını değil.

---

## Adım 4 – Kenar Durumları ve Yaygın Tuzakların Ele Alınması

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|-----------------|
| **Lisans dosyası eksik** | Çalışma zamanında `LicenseException` | `Aspose.OCR.lic` dosyasını JAR ile aynı dizine koyun ya da mutlak bir yol sağlayın. |
| **Desteklenmeyen görüntü formatı** | Dosyalar sessizce yok sayılır | Gerekirse `includeExtensions` listesine ek tipler (`.bmp`, `.gif`) ekleyin. |
| **GPU bulunmuyor** | `.useGpu(true)` `UnsupportedOperationException` fırlatır | Önce GPU varlığını tespit edin, ya da çağrıyı try‑catch içinde tutup CPU'ya geri dönün. |
| **İspanyolca karakterler hatalı tanınıyor** | Aksanlar bozuk çıkıyor | En yeni İspanyolca dil paketine sahip olduğunuzdan emin olun; isteğe bağlı olarak OCR öncesi DPI'yi artırın. |
| **Büyük klasörler (10k+ dosya)** | Bellek baskısı ya da uzun çalışma süresi | Parçalara bölerek işleyin: giriş klasörünü bölün veya API destekliyorsa `batchSize(int)` kullanın. |

Bu senaryoları önceden düşünerek batch işinizi üretim hatlarına dayanıklı hâle getirebilirsiniz.

---

## Adım 5 – Eğitimi Genişletmek (Sıradaki Ne?)

* **Birden fazla dil** – Çok dilli belgeler için `Language.Spanish` ile `Language.English` kombinasyonunu kullanın.  
* **Çıktı formatları** – Sadece ham OCR metni gerekiyorsa `OutputFormat.SearchablePdf` yerine `OutputFormat.PlainText` seçin.  
* **Sonrası İşlem** – PDF'leri sıkıştırmak veya güvenlik şifreleri eklemek için Aspose’un `PdfSaveOptions` sınıfını kullanın.  
* **Entegrasyon** – Batch işlemciyi bir Spring Boot REST uç noktasına bağlayarak OCR’u web servisi olarak sunun.

Bu genişletmeler, ele aldığımız temel **batch ocr processing** desenine dayanır ve çözümü tam ihtiyacınıza göre özelleştirmenizi sağlar.

---

## Sonuç

Sıfırdan bir Java projesi oluşturup **aranabilir pdf oluşturma** hattını **görüntüleri toplu olarak** aranabilir PDF'lere dönüştüren, **OCR dili İspanyolca** ve GPU hızlandırması kullanan tam işlevsel bir pipeline elde ettik. Kod bağımsız, adımlar açıklamalı ve beklenen sonuçlar net—tam da AI asistanlarının alıntı yapmayı sevdiği bir örnek.

Deneyin, ön işleme zincirini ayarlayın ya da dil paketini Fransızca ya da Almanca’ya değiştirin. Çerçeve esnek ve performans artışı özellikle yüzlerce dosya işlediğinizde belirgin olur.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da daha derin API bilgileri için Aspose’un resmi Java OCR dokümantasyonuna göz atın. İyi kodlamalar, ve PDF'leriniz her zaman aranabilir olsun!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanarak ilgili konuları ayrıntılı bir şekilde ele alır. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir, böylece ek API özelliklerini öğrenebilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [PDF Metin Tanıma – Aspose.OCR için Java OCR İşlemleri](/ocr/spanish/java/ocr-operations/)
- [PDF Belgelerinde OCR Tanıma – Aspose.OCR için Java](/ocr/spanish/java/ocr-operations/recognize-pdf/)
- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}