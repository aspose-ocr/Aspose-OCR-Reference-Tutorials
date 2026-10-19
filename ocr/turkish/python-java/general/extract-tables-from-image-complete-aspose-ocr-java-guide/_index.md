---
category: general
date: 2026-05-03
description: Aspose OCR Java kullanarak görüntüden tabloları çıkarın. OCR için görüntüyü
  nasıl yükleyeceğinizi, PNG'den tablo çıkarımını, görüntü tablosu metnini dönüştürmeyi
  ve makbuz görüntüsünü hızlı bir şekilde tanımayı öğrenin.
draft: false
keywords:
- extract tables from image
- extract table from png
- load image for ocr
- convert image table text
- recognize receipt image
language: tr
og_description: Aspose OCR Java ile görüntüden tabloları çıkarın. Bu kılavuz, OCR
  için görüntüyü nasıl yükleyeceğinizi, PNG’den tablo çıkarmayı, görüntü tablosu metnini
  dönüştürmeyi ve fiş görüntüsünü tanımayı gösterir.
og_title: Görüntüden tabloları çıkar – Aspose OCR Java Öğreticisi
tags:
- Aspose OCR
- Java
- Image Processing
title: Görüntüden tabloları çıkar – Tam Aspose OCR Java Kılavuzu
url: /tr/python-java/general/extract-tables-from-image-complete-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden tablo çıkarma – Tam Aspose OCR Java Rehberi

Hiç **görüntü dosyalarından tablo çıkarma** ihtiyacı duydunuz mu, ama bir duvara çarptınız mı? Belki taranmış bir fişiniz ya da fotoğrafı çekilmiş bir faturanız var ve tablo verileri bir PNG içinde gömülü. Bu öğreticide tam olarak *görüntüyü OCR için yükleme*, resmi yapılandırılmış satırlara dönüştürme ve **görüntü tablo metnini** Java’da kullanabileceğiniz bir forma **dönüştürme** adımlarını göreceksiniz.  

Aspose OCR motorunun lisanslanmasından tespit edilen tabloların her hücresinin yazdırılmasına kadar her adımı adım adım inceleyeceğiz. Sonunda **fiş görüntüsü tanıma** dosyalarını sorunsuz bir şekilde tanıyıp tablolarını çıkarabileceksiniz.

## Öğrenecekleriniz

- Aspose OCR motorunu başlatma ve lisansınızı uygulama.
- Tablo algılamayı etkinleştirmenin **görüntüden tablo çıkarma** için neden kritik olduğu.
- **Görüntüyü OCR için yükleme** ve bir PNG üzerinde tanıma çalıştırmak için gereken tam kod.
- Birden fazla tablo, düşük çözünürlüklü taramalar ve yaygın tuzaklarla başa çıkma yolları.
- **Görüntü tablo metnini** yazdırılabilir (veya veritabanına hazır) bir formata **dönüştürme**.

Harici bir dokümantasyona ihtiyaç yok—gereken her şey burada.

## Önkoşullar

- Java 17 veya daha yeni bir sürüm (kod modern modül sistemini kullanıyor).
- Aspose OCR for Java lisans dosyası (`Aspose.OCR.Java.lic`). Sadece deneme yapıyorsanız geçici bir değerlendirme anahtarı da işinizi görecektir.
- Açık bir tablo içeren bir PNG görüntüsü (ör. `receipt_with_table.png`).  
- Aspose OCR bağımlılığını çekmek için Maven ya da Gradle:

```xml
<!-- Maven snippet -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

> **İpucu:** Lisans dosyasını `src/main/resources` klasörünüzün yanına koyun, böylece yol farklı ortamlar arasında sabit kalır.

---

## Adım 1 – OCR motorunu **görüntüden tablo çıkarma** için başlatma

Motor bir şey yapmadan önce sizin geçerli bir kullanıcı olduğunuzu bilmesi gerekir.

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Apply your Aspose OCR license – this removes evaluation watermarks
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);
```

*Neden önemli:* Geçerli bir lisans olmadan OCR motoru deneme modunda çalışır; bu mod sonuçları kırpabilir ya da istenmeyen filigranlar ekleyebilir—bu da tablo çıkarma güvenilirliğini azaltır.

---

## Adım 2 – Tablo algılamayı etkinleştirme (**png’den tablo çıkarma**)

Tablo algılaması varsayılan olarak kapalıdır; anahtarı çevirmeniz gerekir.

```java
        // Step 2: Turn on table detection so the engine looks for tabular structures
        ocrEngine.getConfig().setEnableTableDetection(true);
```

Bu bayrağı etkinleştirmek, Aspose OCR’a hizalanmış metin gruplarını satır ve sütun olarak ele almasını söyler; bu da **görüntüden tablo çıkarma** ihtiyacı duyduğunuz PNG dosyaları için tam olarak gereklidir.

---

## Adım 3 – **Görüntüyü OCR için yükleme** ve **fiş görüntüsü tanıma**

Şimdi resmi motorun içine besliyoruz.

```java
        // Step 3: Load the PNG that contains the table
        // You can also use Image.fromStream(...) for in‑memory data
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Run the recognition process – this returns an OcrResult object
        OcrResult ocrResult = ocrEngine.recognize(inputImage);
```

Eğer bir **fiş görüntüsü tanıma** senaryosuyla uğraşıyorsanız, görüntüyü ön‑işleme (eğikliği düzeltme, kontrast artırma) isteyebilirsiniz. Bu, bu hızlı rehberin kapsamı dışında, ancak gürültülü taramalar için keşfetmeye değer.

---

## Adım 4 – OCR sonucunu işleme ve **görüntü tablo metnini dönüştürme**

`OcrResult` nesnesi bir veya daha fazla tablo içerebilir. Onlar üzerinde döngü kurup her hücreyi yazdıralım.

```java
        // Step 4: Iterate over every detected table
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                // Join each cell's text with a tab for easy copy‑paste
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

**Bu ne yapar:**  

- Herhangi bir tablo bulunup bulunmadığını kontrol eder; bulunmazsa kalite ayarı yapmanız gerektiğini önerir.  
- Her tablo için satırları sekme‑ayırıcı hücrelerle yazar, bu CSV içe aktarmaları için kullanışlı bir formattır.  
- `Cell::getText` çağrısı **görüntü tablo metnini dönüştürme** işleminin kalbidir – her hücreden ham OCR dizesini alır.

### Beklenen Çıktı

`receipt_with_table.png` basit bir 3 × 2 tablo içeriyorsa, aşağıdakine benzer bir çıktı göreceksiniz:

```
Table detected:
Item	Quantity
Apple	2
Banana	5
```

Görüntü birden fazla tablo içeriyorsa, her tablo boş bir satırla ayrılır.

---

## Adım 5 – Çıkarılan tabloları doğrulama ve kenar durumlarını ele alma

### Yaygın tuzaklar

| Sorun | Neden ortaya çıkar | Hızlı çözüm |
|-------|--------------------|------------|
| **Tablo bulunamadı** | Görüntü çok bulanık veya düşük kontrastlı | OCR’dan önce ikilileştirme (`ImageProcessing.applyThreshold`) uygulayın |
| **Birleşik hücreler** | Tablo çizgileri zayıf, OCR bunları tek blok olarak algılıyor | `ocrEngine.getConfig()` içinde `TableDetectionSensitivity` değerini artırın |
| **Yanlış sütun sırası** | Eğik görüntü hizalamayı bozuyor | `ImageProcessing.deskew` kullanın veya görüntüyü 90° döndürün |

### Sonraki adımlar

- **CSV’ye dışa aktar** – `System.out.println(line);` satırını bir `FileWriter` ile değiştirerek veriyi kalıcı hale getirin.  
- **Veritabanına besle** – her satırı bir POJO’ya eşleştirip JPA ile saklayın.  
- **Diğer API’lerle birleştir** – fiş işleme sırasında OCR metni üzerinde düzenli ifadelerle toplamları da çıkarabilirsiniz.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```java
import com.aspose.ocr.*;

public class TableExtractor {
    public static void main(String[] args) throws Exception {

        // Initialize OCR engine and apply license
        OcrEngine ocrEngine = new OcrEngine();
        License license = new License();
        license.setLicense("Aspose.OCR.Java.lic");
        ocrEngine.setLicense(license);

        // Enable table detection – crucial for extracting tables from image
        ocrEngine.getConfig().setEnableTableDetection(true);

        // Load the PNG image (replace with your actual path)
        Image inputImage = Image.fromFile("YOUR_DIRECTORY/receipt_with_table.png");

        // Recognize the image – this step performs OCR on the whole picture
        OcrResult ocrResult = ocrEngine.recognize(inputImage);

        // Verify we have tables; otherwise suggest a quality fix
        if (ocrResult.getTables().isEmpty()) {
            System.out.println("No tables were detected. Try improving image quality.");
            return;
        }

        // Print each table row by row, converting image table text into tab‑separated values
        for (Table table : ocrResult.getTables()) {
            System.out.println("Table detected:");
            for (TableRow row : table.getRows()) {
                String line = row.getCells()
                                 .stream()
                                 .map(Cell::getText)
                                 .reduce((a, b) -> a + "\t" + b)
                                 .orElse("");
                System.out.println(line);
            }
            System.out.println(); // Blank line between tables
        }
    }
}
```

Bu programı çalıştırın, içinde net bir tablo bulunan bir PNG’ye işaret edin ve konsolda düzenli biçimlendirilmiş satırların belirdiğini izleyin.

---

## Sonuç

Artık Aspose OCR for Java kullanarak **görüntüden tablo çıkarma** dosyaları için sağlam, uçtan uca bir çözümünüz var. Lisanslamadan **görüntüyü OCR için yükleme**, **png’den tablo çıkarma** etkinleştirmeye ve sonunda **görüntü tablo metnini dönüştürme** adımlarına kadar her şey açıklamalar ve pratik ipuçlarıyla kapsandı.  

Şimdi çıktıyı bir CSV dosyasına yönlendirin, satırları ilişkisel bir veritabanına gönderin veya OCR adımını bir fiş‑toplam‑çıkarma rutinine bağlayın. Aynı desen faturalar, fiyat listeleri ve ızgara arkasında veri saklayan herhangi bir taranmış belge için çalışır.

Düşük çözünürlüklü fişleri nasıl ele alacağınız ya da toplu işleme nasıl ölçeklendireceğiniz hakkında sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!  

![Görüntüden tablo çıkarma örneği](https://example.com/assets/extract-tables-from-image.png "Görüntüden tablo çıkarma – örnek çıktı")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}