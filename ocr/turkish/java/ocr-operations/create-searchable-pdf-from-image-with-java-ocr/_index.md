---
category: general
date: 2026-04-26
description: Aspose OCR kullanarak Java'da bir görüntüden aranabilir PDF oluşturun.
  Görüntüyü PDF'ye dönüştürmeyi, görüntüyü OCR ile PDF'ye çevirmeyi ve görüntüden
  metni hızlıca çıkarmayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- ocr image to pdf
- extract text from image
- how to set language
language: tr
og_description: Aspose OCR kullanarak bir görüntüden aranabilir PDF oluşturun. Bu
  kılavuz, görüntüyü PDF'ye dönüştürmeyi, görüntüyü OCR ile PDF'ye dönüştürmeyi ve
  görüntüden metin çıkarmayı gösterir.
og_title: Java OCR ile görüntüden aranabilir PDF oluştur
tags:
- Java
- OCR
- PDF
title: Java OCR ile görüntüden aranabilir PDF oluştur
url: /tr/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Resimden Java OCR ile aranabilir PDF oluşturma

Tarayıcıdan bir fatura alarak **create searchable PDF** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—bir PDF'i gerçekten arayabilmek isteyen birçok geliştirici bu engelle karşılaşıyor. İyi haber? Aspose OCR for Java ile **convert image to PDF** yapabilir, OCR'ı anında çalıştırabilir ve sadece birkaç satır kodla düzenli bir aranabilir dosya elde edebilirsiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: bir resmi yükleme, motorun hangi dili bekleyeceğini belirtme, OCR gerçekleştirme ve sonunda bir **searchable PDF** kaydetme. Sonunda **extract text from image**'i manuel olarak nasıl yapacağınızı, dil ayarlarını nasıl ince ayar yapacağınızı ve birkaç yaygın kenar durumunu nasıl yöneteceğinizi de öğreneceksiniz. Hiçbir dış hizmet, gizli komut satırı aracı yok—sadece saf Java.

## İhtiyacınız olanlar

- Java 17 veya daha yeni bir sürüm (API eski sürümlerle de çalışır, ancak 17 en uygun sürümdür).  
- Aspose OCR for Java kütüphanesi – en son JAR'ı Maven Central'dan alabilirsiniz (`com.aspose:aspose-ocr:23.10`).  
- Okunabilir metin içeren bir görüntü dosyası (PNG, JPG veya TIFF çalışır).  
- Biraz IDE sabrı — IntelliJ IDEA veya VS Code yeterli olacaktır.

Eğer bunlara zaten sahipseniz, harika! Yoksa, aşağıdaki Maven snippet'i sizi hemen çalışır duruma getirecek:

```xml
<!-- Add to your pom.xml -->
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

Temel hazırlıklar tamam olduğuna göre, koda dalalım.

## Adım 1: OCR motorunu başlatma – **create searchable pdf**'in kalbi

Herhangi bir dönüşüm gerçekleşmeden önce bir `OcrEngine` örneği oluşturmalısınız. Bunu, pikselleri okuyup karakterlere dönüştürecek beyin olarak düşünün.

```java
import com.aspose.ocr.*;

public class PdfExportDemo {
    public static void main(String[] args) throws Exception {
        // Step 1: Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

*Neden önemli:* Motor, tüm tanıma ayarlarını (dil, doğruluk modu vb.) tutar. Bir kez örnekleyip birden çok görüntüde yeniden kullanmak, her dosya için yeni bir motor oluşturmak yerine daha verimlidir.

## Adım 2: **How to set language** – Fransızca, Almanca veya herhangi bir betik için doğruluğu artırma

Kaynak belgenin dilini biliyorsanız, OCR motoruna söyleyin. Bu, işleme hızını artırır ve hatalı tanımlamaları azaltır.

```java
        // Step 2: (Optional) Specify the language to improve text extraction
        ocrEngine.getRecognitionSettings().setLanguage(OcrLanguage.FRENCH);
```

`OcrLanguage.FRENCH`'i `ENGLISH`, `SPANISH`, `GERMAN` vb. ile değiştirebilirsiniz. Emin değilseniz, satırı kaldırıp Aspose'un tahmin etmesine izin verin—ancak doğrulukta hafif bir düşüş bekleyin.

## Adım 3: **convert image to pdf** yapmak istediğiniz görüntüyü yükleyin

`setImage` metodu bir dosya yolu, `InputStream` veya hatta bir `java.awt.Image` nesnesi alabilir. Eğer bir bayt diziniz (örneğin bir web yüklemesinden) varsa, onu `ByteArrayInputStream` içine sarıp doğrudan geçirebilirsiniz.

```java
        // Step 3: Load the image that contains the text to be recognized
        ocrEngine.setImage("YOUR_DIRECTORY/french_invoice.png");
```

## Adım 4: OCR'ı gerçekleştir ve **ocr image to pdf**'yi tek bir çağrıda yap

Aspose bu adımı sorunsuz hâle getirir: `recognizeToPdf` tanıma motorunu çalıştırır ve tek seferde aranabilir bir PDF yazar.

```java
        // Step 4: Recognize the text and save it as a searchable PDF
        ocrEngine.recognizeToPdf("YOUR_DIRECTORY/french_invoice_searchable.pdf");
```

Arka planda, kütüphane orijinal görüntüyle hizalanan görünmez bir metin katmanı oluşturur. Sonuç dosyasını Adobe Reader'da açtığınızda, arama kutusuna bir kelime yazıp eşleşen konuma anında atlayabileceksiniz.

## Adım 5: Sonucu doğrulama – çıktı nasıl görünüyor?

```java
        // Step 5: Inform the user that the PDF has been created
        System.out.println("Searchable PDF generated.");
    }
}
```

Programı çalıştırın, ardından `french_invoice_searchable.pdf` dosyasını açın. Faturada bulunduğundan emin olduğunuz bir kelimeyi (ör. “Total”) aramayı deneyin. Vurgulama doğru yere geliyorsa, **create searchable pdf** işlemini başarıyla tamamlamışsınız.  
![Create searchable PDF example](example.png)<!-- alt text includes primary keyword -->

### Beklenen çıktı

```
Searchable PDF generated.
```

Ve `YOUR_DIRECTORY` içinde paylaşabileceğiniz, indeksleyebileceğiniz veya arşivleyebileceğiniz bir PDF dosyası.

## Adım 6: Görüntüden ham metni çıkarma (isteğe bağlı)

Bazen daha fazla işleme için düz metne ihtiyaç duyarsınız—belki bir veritabanına beslemek ya da duygu analizi yapmak için. Aspose, tanınan metni doğrudan almanıza izin verir:

```java
        // Optional: Get the extracted text as a String
        String extractedText = ocrEngine.getText();
        System.out.println("Extracted text:");
        System.out.println(extractedText);
```

Bu snippet, PDF oluşturmadan **extract text from image**'i gösterir. Görsel düzen yerine sadece içeriği önemsediğinizde kullanışlıdır.

## Birden çok sayfa veya görüntü işleme

Kaynağınız çok sayfalı bir TIFF veya JPEG'lerden oluşan bir klasörse ne yaparsınız? Dosyalar üzerinde döngü kurup her biri için `recognizeToPdf` çağırabilir, ardından PDF'leri Aspose PDF veya başka bir kütüphane ile birleştirebilirsiniz. İşte hızlı bir örnek:

```java
import java.io.File;
import com.aspose.pdf.*;

public class MultiPageDemo {
    public static void main(String[] args) throws Exception {
        OcrEngine engine = new OcrEngine();
        File folder = new File("YOUR_DIRECTORY/images");
        Document finalDoc = new Document();

        for (File img : folder.listFiles((d, n) -> n.matches(".*\\.(png|jpg|tif)"))) {
            engine.setImage(img.getAbsolutePath());
            // Save each page as a temporary PDF
            String tempPdf = img.getName() + ".pdf";
            engine.recognizeToPdf(tempPdf);
            // Append to final document
            Document pageDoc = new Document(tempPdf);
            finalDoc.getPages().add(pageDoc.getPages().get_Item(1));
        }
        finalDoc.save("YOUR_DIRECTORY/combined_searchable.pdf");
        System.out.println("All pages merged into searchable PDF.");
    }
}
```

**Pro tip:** Birleştirdikten sonra geçici PDF'leri silerek çalışma alanını düzenli tutun.

## Yaygın tuzaklar ve nasıl kaçınılır

- **Low‑resolution images:** OCR doğruluğu 150 dpi'nin altında ciddi şekilde düşer. Mümkünse ölçeklendirin veya daha yüksek çözünürlüklü bir tarama isteyin.  
- **Skewed pages:** Döndürülmüş bir görüntü motoru şaşırtabilir. Hafif eğimi otomatik düzeltmek için `ocrEngine.getImagePreprocessingSettings().setDeskew(true)` kullanın.  
- **Unsupported language:** Ayarladığınız dilin Aspose OCR lisansınızda bulunduğundan emin olun; aksi takdirde motor İngilizceye geri dönecektir.  
- **Large files:** 30 MB bir TIFF işlemek bellek yoğun olabilir. Daha küçük parçalara bölmeyi veya JVM yığınını (`-Xmx2g`) artırmayı düşünün.

## Sonraki adımlar – bundan sonra nereye gidilir

Artık **create searchable pdf** temelini kavradığınıza göre, aşağıdakileri keşfetmek isteyebilirsiniz:

- **Batch conversion:** Çok sayfalı deseni bir zamanlayıcıyla birleştirerek gelen taramaları geceleyin işleyin.  
- **Metadata injection:** Aspose PDF'i kullanarak aranabilir PDF'e başlık, yazar veya özel etiketler ekleyin.  
- **Digital signatures:** OCR sonrası PDF'i bir sertifika ile güvence altına alın, yasal belgeler için uyumluluğu sağlayın.

Bu uzantıların tümü, ele aldığımız temel kavramlara dayanır: OCR motorunu başlatma, isteğe bağlı olarak dili ayarlama, görüntüyü yükleme ve `recognizeToPdf`'yi çağırma.

---

### TL;DR

Aspose OCR for Java kullanarak bir görüntüden **create searchable PDF** oluşturmayı gösteren tam, çalıştırılabilir bir örnek üzerinden geçtik. Adımlar arasında motoru başlatma, isteğe bağlı olarak dili ayarlama (“how to set language” sorusuna yanıt), görüntüyü yükleme, OCR gerçekleştirme, aranabilir bir PDF kaydetme ve isteğe bağlı olarak düz metin çıkarma bulunuyor. Ayrıca çoklu sayfa işleme, yaygın tuzaklar ve daha fazla otomasyon fikirlerini de ele aldık.

Kendi makbuzlarınız, sözleşmeleriniz veya el yazısı notlarınızla deneyin—bu sabit resimleri saniyeler içinde tamamen aranabilir belgelere dönüştürün. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}