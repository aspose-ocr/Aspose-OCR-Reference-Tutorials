---
category: general
date: 2026-02-19
description: Aspose OCR ile Java’da bir JPG görüntüsünden aranabilir PDF oluşturun.
  JPG’yi PDF’ye dönüştürün ve görüntüden metni hızlıca tanıyın.
draft: false
keywords:
- create searchable pdf
- image to searchable pdf
- recognize text from image
- extract text from jpg
- convert jpg to pdf
language: tr
og_description: Aspose OCR ile bir JPG görüntüsünden aranabilir PDF oluşturun. JPG'yi
  PDF'ye dönüştürmeyi ve Java'da görüntüden metin tanımayı öğrenin.
og_title: JPG'den Aranabilir PDF Oluştur – Java OCR Öğreticisi
tags:
- aspose-ocr
- java
- pdf
- ocr
title: JPG'den Aranabilir PDF Oluştur – Görüntüyü Aranabilir PDF'ye Dönüştürme Java
  Kılavuzu
url: /tr/java/ocr-operations/create-searchable-pdf-from-jpg-image-to-searchable-pdf-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG'den Aranabilir PDF Oluşturma – Görüntüden Aranabilir PDF Java Rehberi

Hiç taranmış bir resimden **searchable PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—bir JPG'nin aranabilir olması gerektiğinde birçok geliştirici aynı sorunla karşılaşıyor. İyi haber şu ki, Aspose OCR for Java ile bu görüntüyü sadece birkaç satır kodla tamamen **searchable PDF**'ye dönüştürebilirsiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: bir JPG'yi yüklemek, metni tanımak ve sonucu aranabilir bir PDF olarak kaydetmek. Sonuna kadar **convert jpg to pdf**, **extract text from jpg** nasıl yapılır ve bu yaklaşımın PDF oluşturulduktan sonra OCR yapmaktan genellikle daha güvenilir neden olduğunu öğreneceksiniz.

## Gereksinimler

Başlamadan önce, makinenizde aşağıdakilerin olduğundan emin olun:

* **Java Development Kit (JDK) 8 veya daha yeni** – kod standart Java API'lerini kullanır.
* **Aspose OCR for Java** kütüphanesi – Maven Central'dan alabilir veya JAR'ı Aspose sitesinden indirebilirsiniz.
* Okunabilir metin içeren bir **sample JPG** (ör. taranmış bir fatura veya bir belgenin ekran görüntüsü).

Ek bir çerçeve (framework) gerekmez; örnek sade bir Java projesiyle çalışır.

## Adım 1 – Projeyi Kurun ve Aspose OCR'yi Ekleyin

İlk olarak, yeni bir Maven projesi oluşturun (ya da JAR'ı sınıf yoluna eklediğiniz bir klasör). Maven kullanıyorsanız, bu bağımlılığı `pom.xml` dosyanıza ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **Pro tip:** Her zaman Aspose Maven deposundaki en son sürümü kontrol edin; yeni sürümler performans iyileştirmeleri ve hata düzeltmeleri içerir.

Bağımlılık çözüldükten sonra, **searchable PDF** oluşturacak Java kodunu yazmaya hazırsınız.

## Adım 2 – Görüntüyü Yükleyin (image to searchable pdf)

İlk gerçek adım, OCR motorunu kaynak görüntüye yönlendirmektir. İşte **image to searchable pdf** dönüşümünün gerçekten başladığı yer.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the JPG you want to turn into a searchable PDF
        // Replace "YOUR_DIRECTORY/input.jpg" with the actual path to your file
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

> **Neden önemli:** `setImage`, Aspose'a hangi bitmap'i analiz edeceğini söyler. Düşük çözünürlüklü bir görüntü sağlarsanız OCR kalitesi düşer, bu yüzden en iyi sonuçlar için JPG'nin en az 300 dpi olduğundan emin olun.

## Adım 3 – Görüntüden Metni Tanıyın

Motor artık hangi görüntüyle çalışacağını bildiğine göre, ona **recognize text from image** yapmasını isteyebiliriz. Aspose OCR, dil algılama, karakter segmentasyonu ve güven puanı gibi işlemleri arka planda halleder.

```java
        // Perform OCR and directly output a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);
```

`recognize()` çağrısı akıcı bir arayüz döndürür, böylece `save` metodunu zincirleyebiliriz. `OcrOutputFormat.SEARCHABLE_PDF` belirterek, kütüphane orijinal görüntünün görünümünü korurken PDF içine görünmez bir metin katmanı ekler.

> **Köşe durumu:** JPG'niz birden fazla sayfa içeriyorsa (ör. ayrı JPG'ler olarak kaydedilmiş çok sayfalı bir TIFF), her dosya üzerinde döngü yapıp ortaya çıkan PDF'leri daha sonra birleştirmeniz gerekir. Aynı OCR motoru her yineleme için yeniden kullanılabilir.

## Adım 4 – Sonucu Doğrulayın

Kaydetme işlemi tamamlandıktan sonra, basit bir konsol mesajı her şeyin sorunsuz gerçekleştiğini bildirir.

```java
        // Let the user know the PDF is ready
        System.out.println("Searchable PDF created.");
    }
}
```

`output-searchable.pdf` dosyasını Adobe Acrobat gibi bir görüntüleyicide açtığınızda, gizli metni seçebilmeniz, kopyalamanız veya arama yapabilmeniz gerekir—tam da bir **searchable PDF**'den beklediğiniz gibi.

### Beklenen Çıktı

Programı çalıştırdığınızda şu çıktı verir:

```
Searchable PDF created.
```

Oluşturulan PDF, orijinal JPG'yi gösterirken metin seçimine izin verir. PDF'nin “Properties → Description → PDF Producer” bölümünü açarsanız, `Aspose.OCR for Java` gibi bir şey göreceksiniz.

## Tam Çalışan Örnek

Aşağıda tam, çalıştırmaya hazır kaynak dosya bulunmaktadır. IDE'nize kopyalayıp yapıştırın, dosya yollarını ayarlayın ve çalıştırın.

```java
import com.aspose.ocr.*;

public class SearchablePdfExample {
    public static void main(String[] args) throws Exception {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image containing the text to be recognized
        // Make sure the path points to a real JPG on your disk
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 3: Recognize the text and directly save it as a searchable PDF
        ocrEngine.recognize()
                 .save("YOUR_DIRECTORY/output-searchable.pdf", OcrOutputFormat.SEARCHABLE_PDF);

        // Step 4: Notify that the PDF has been created
        System.out.println("Searchable PDF created.");
    }
}
```

> **OCR başarısız olursa ne olur?**  
> * Genellikle bu, görüntünün çok gürültülü olması veya dilin kutudan çıkınca desteklenmemesinden kaynaklanır. Görüntüyü ön işleme (kontrastı artırma, eğikliği düzeltme) yaparak ya da dili `ocrEngine.getLanguage().setLanguage(OcrLanguage.English);` ile açıkça ayarlayarak doğruluğu artırabilirsiniz.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Question | Answer |
|----------|--------|
| **PDF yerine düz metni çıkarabilir miyim?** | Evet. `ocrEngine.recognize().save("output.txt", OcrOutputFormat.TEXT);` kullanın. |
| **PNG işlemek gerekirse ne olur?** | Aynı API çalışır; sadece `fromFile` içinde dosya uzantısını değiştirin. |
| **Oluşturulan PDF tüm görüntüleyicilerde gerçekten aranabilir mi?** | Modern görüntüleyiciler (Adobe Reader, Foxit, Chrome) gizli metin katmanını tanır. Eski araçlar bunu görmezden gelebilir. |
| **PDF sayfa boyutunu nasıl kontrol edebilirim?** | Aspose OCR varsayılan olarak görüntü boyutlarını kullanır. Özel boyutlandırma için PDF'yi manuel olarak oluşturup OCR metin katmanını üzerine yerleştirin—bu gelişmiş bir senaryodur. |

## Performans İpuçları

* **Batch processing:** Birçok görüntü için tek bir `OcrEngine` örneğini yeniden kullanın, böylece yerel kütüphane yüklemeleri tekrarlanmaz.
* **Thread safety:** Motor **thread‑safe** değildir; paralel çalıştırıyorsanız her thread için bir tane oluşturun.
* **Memory usage:** Büyük görüntüler çok RAM tüketebilir. `OutOfMemoryError` alırsanız, motoru beslemeden önce görüntüyü küçültün.

## Sonraki Adımlar

Artık **searchable PDF** oluşturmayı bildiğinize göre, ilgili görevleri keşfetmek isteyebilirsiniz:

* **Convert jpg to pdf** OCR olmadan (düz bir görüntü PDF'si için Aspose PDF kütüphanesini kullanın).  
* **Extract text from jpg** indeksleme için bir `.txt` dosyasına çıkarın.  
* **Combine multiple searchable PDFs** tek bir belgeye birleştirin, Aspose PDF’nin `PdfFileEditor`'ını kullanarak.  

Bunların hepsi, az önce kurduğunuz aynı temele dayanır.

---

### Hızlı Özet

* Aspose OCR for Java kullanarak bir JPG'den **searchable PDF** oluşturduk.  
* Süreç, görüntüyü yüklemeyi, metni tanımayı ve **searchable PDF** olarak kaydetmeyi kapsadı.  
* Artık **image to searchable PDF**, **recognize text from image**, **extract text from jpg**, ve **convert jpg to pdf** için yeniden kullanılabilir bir deseniniz var.

Kendi belgelerinizle deneyin, gerekirse dil ayarlarını değiştirin ve OCR'un sizin için ağır işi yapmasına izin verin. İyi kodlamalar!  

![Create searchable PDF example](placeholder.png){alt="Aranabilir PDF oluşturma örneği"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}