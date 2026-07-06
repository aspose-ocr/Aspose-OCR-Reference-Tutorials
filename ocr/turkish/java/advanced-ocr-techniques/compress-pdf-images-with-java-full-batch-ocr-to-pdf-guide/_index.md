---
category: general
date: 2026-07-05
description: Java kullanarak PNG'yi PDF'ye dönüştürürken PDF görüntülerini sıkıştırın.
  OCR için görüntü ön işleme öğrenin, JPG metin tanıma yapın ve tek bir öğreticide
  toplu OCR'yi PDF'ye dönüştürün.
draft: false
keywords:
- compress pdf images
- convert png to pdf
- image preprocessing for ocr
- recognize text jpg
- batch ocr to pdf
language: tr
og_description: Java kullanarak PDF görüntülerini sıkıştırın ve PNG'yi PDF'ye dönüştürün.
  Bu rehber, OCR için görüntü ön işleme, JPG'den metin tanıma ve toplu OCR'dan PDF'ye
  dönüştürmeyi kapsar.
og_title: Java ile PDF Görüntülerini Sıkıştır – Tam Batch OCR Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  headline: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  type: TechArticle
- description: Compress PDF images while converting PNG to PDF using Java. Learn image
    preprocessing for OCR, recognize text JPG, and batch OCR to PDF in one tutorial.
  name: Compress PDF Images with Java – Full Batch OCR to PDF Guide
  steps:
  - name: Expected Output
    text: 'Running the program prints a line for each image, e.g.:'
  - name: What if my server has no GPU?
    text: Just set `gpuSettings.setEnabled(false)`. The rest of the pipeline remains
      unchanged, and you still get multithreaded CPU processing.
  - name: My PDFs are still too large—can I lower the quality further?
    text: Yes. Adjust `options.setImageQuality(70)` or even `50`. Lower values shrink
      size more aggressively but may blur fine glyphs. Test with a representative
      sample.
  - name: How do I handle other image formats (TIFF, BMP)?
    text: 'Add the extensions to the filter lambda:'
  - name: Can I keep the original color images instead of binarizing?
    text: Replace `.addBinarize()` with `.addGrayscale()` in the preprocessor builder
      if you need color retention for downstream analysis.
  type: HowTo
tags:
- ocr
- java
- pdf
- image-processing
title: Java ile PDF Görüntülerini Sıkıştırma – Tam Toplu OCR'dan PDF'ye Kılavuz
url: /tr/java/advanced-ocr-techniques/compress-pdf-images-with-java-full-batch-ocr-to-pdf-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java ile PDF Görüntülerini Sıkıştırma – Tam Toplu OCR'dan PDF'ye Rehber

Hiç **PDF görüntülerini sıkıştırma** ihtiyacı duydunuz mu, bir klasördeki PNG'leri aranabilir PDF'lere dönüştürürken? Tek başınıza değilsiniz. Birçok otomasyon hattında en büyük sorun, görüntü kalitesi, OCR doğruluğu ve nihai PDF boyutunu aynı anda dengelemek.

Bu öğreticide, **PNG'yi PDF'ye dönüştürme**, **OCR için görüntü ön işleme** uygulama ve sonunda **PDF görüntülerini sıkıştırma** yoluyla çıktının hafif kalmasını sağlayan pratik bir çözümü adım adım inceleyeceğiz. Sonunda **JPG'den metin tanıma**, **toplu OCR'dan PDF'ye** iş akışını kurma ve PDF'lerinizi düzenli tutma konularını öğreneceksiniz.

## Öğrenecekleriniz

- Aspose OCR for Java'ı kurma ve bir lisans uygulama.
- Motoru çoklu iş parçacığı, GPU hızlandırma ve yazım düzeltme için yapılandırma.
- Yeniden kullanılabilir **OCR için görüntü ön işleme** hattı (gürültü giderme, kontrast, ikiliye çevirme) oluşturma.
- **PdfSaveOptions** kullanarak **PDF görüntülerini sıkıştırma**, okunabilirliği kaybetmeden.
- Bir dizini döngüyle işleyerek **PNG'yi PDF'ye dönüştürme** ve toplu olarak **JPG'den metin tanıma**.
- Herhangi bir projeye ekleyebileceğiniz, tam ve çalıştırmaya hazır bir Java programı.

> **Önkoşullar**: Java 8+, Maven veya Gradle, bir Aspose OCR for Java lisansı ve işlemek istediğiniz PNG/JPG görüntülerinin bulunduğu bir klasör.

---

## Adım 1: Aspose OCR Lisansını Uygulama (Üretim İçin Gereklidir)

Herhangi bir OCR API'sini çağırmadan önce geçerli bir lisans yüklemelisiniz; aksi takdirde deneme sınırlamalarıyla takılı kalırsınız.

```java
import com.aspose.ocr.*;

public class LicenseSetup {
    public static void loadLicense() throws Exception {
        License license = new License();
        // Point to your license file – keep it out of source control!
        license.setLicense("Aspose.OCR.Java.lic");
    }
}
```

*Bu neden önemlidir*: Lisanslı bir motor GPU desteğini, daha yüksek doğruluğu açar ve PDF dosyalarınızı şişirecek filigranları kaldırır.

---

## Adım 2: OCR Motorunu Yapılandırma – İş Parçacıkları, GPU ve Yazım Düzeltme

Hızlı bir OCR motoru, herhangi bir **toplu OCR'dan PDF'ye** işinin belkemiğidir. Host CPU'nun kaldırabileceği kadar iş parçacığı başlatacağız, GPU hızlandırmayı (uyumlu bir kartınız varsa) etkinleştireceğiz ve OCR hatalarını temizlemek için yazım düzeltmeyi sıkılaştıracağız.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.gpu.GPUSettings;
import com.aspose.ocr.spell.SpellCorrectionOptions;

public class EngineConfig {
    public static OcrEngine createEngine() {
        OcrEngine ocrEngine = new OcrEngine();

        // Use all available logical processors
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Enable GPU – huge speedup for large batches
        GPUSettings gpu = new GPUSettings();
        gpu.setEnabled(true);
        ocrEngine.setGpuSettings(gpu);

        // Light spell correction: fix common typos without over‑correcting
        SpellCorrectionOptions spellOpts = new SpellCorrectionOptions();
        spellOpts.setMaxEditDistance(1);
        ocrEngine.getSpellCorrection().setOptions(spellOpts);

        return ocrEngine;
    }
}
```

*Pro ipucu*: GPU'suz bir başsız sunucuda çalışıyorsanız sadece `gpu.setEnabled(false)` ayarlayın – kod hâlâ çalışır, sadece biraz daha yavaş olur.

---

## Adım 3: Görüntü Ön İşleme Hattı Oluşturma

Ham taramalar genellikle gürültü, düşük kontrast veya dengesiz aydınlatmadan muzdariptir. **OCR için görüntü ön işleme**, özellikle **JPG'den metin tanıma** senaryolarında tanıma oranlarını büyük ölçüde artırır.

```java
import com.aspose.ocr.*;

public class PreprocessorSetup {
    public static ImagePreprocessor createPreprocessor() {
        return new ImagePreprocessor.Builder()
                .addDenoise(0.7)      // Reduce grain while preserving edges
                .addContrast(1.15)    // Boost contrast for clearer glyphs
                .addBinarize()        // Convert to black‑and‑white for OCR
                .build();
    }
}
```

*Bunları neden zincirliyoruz*: İlk olarak gürültü giderme, ikilileştiricinin lekeleri artırmasını önler; kontrast, karakterlerin öne çıkmasını sağlar; son olarak ikiliye çevirme, OCR motoruna temiz bir ikili görüntü sunar.

---

## Adım 4: PDF Kaydetme Seçeneklerini Hazırlama – **PDF Görüntülerini Verimli Şekilde Sıkıştırma**

Aspose PDF çıktısını ince ayar yapmanıza izin verir. Görüntü sıkıştırmasını açacağız ve boyut ile okunabilirliği dengeleyen bir kalite seviyesi belirleyeceğiz.

```java
import com.aspose.ocr.pdf.PdfSaveOptions;

public class PdfOptions {
    public static PdfSaveOptions createOptions() {
        PdfSaveOptions options = new PdfSaveOptions();
        options.setCompressImages(true);   // This is the key to compress PDF images
        options.setImageQuality(90);       // 90% retains sharp text while shrinking file size
        return options;
    }
}
```

*Sonuç*: Her aranabilir PDF belirgin şekilde daha küçük olur—arşivleme veya e‑posta ile gönderim için idealdir.

---

## Adım 5: Klasörü İşleyin – **PNG'yi PDF'ye Dönüştürme** ve **JPG'den Metin Tanıma** Tek Döngüde

Şimdi her şeyi bir araya getiriyoruz. Döngü, giriş dizininde dolaşır, her PNG veya JPG üzerinde OCR çalıştırır ve bir aranabilir PDF'yi çıktı klasörüne yazar. PDF adı, kaynak görüntü adını yansıtır.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.pdf.PdfSaveOptions;
import java.io.File;

public class BatchOcrTutorial {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license
        LicenseSetup.loadLicense();

        // 2️⃣ Engine & preprocessing
        OcrEngine ocrEngine = EngineConfig.createEngine();
        ocrEngine.setPreprocessor(PreprocessorSetup.createPreprocessor());

        // 3️⃣ PDF options (compress PDF images)
        PdfSaveOptions pdfOptions = PdfOptions.createOptions();

        // 4️⃣ Define input / output folders
        File inputFolder = new File("YOUR_DIRECTORY/input");
        File outputFolder = new File("YOUR_DIRECTORY/output");
        if (!outputFolder.exists()) outputFolder.mkdirs();

        // 5️⃣ Filter PNG & JPG files
        File[] imageFiles = inputFolder.listFiles((dir, name) ->
                name.toLowerCase().endsWith(".png") || name.toLowerCase().endsWith(".jpg"));

        if (imageFiles == null || imageFiles.length == 0) {
            System.out.println("No PNG or JPG files found in the input folder.");
            return;
        }

        // 6️⃣ Process each file
        for (File image : imageFiles) {
            // Recognize text – works for both PNG and JPG
            ocrEngine.recognizeImage(image.getAbsolutePath());

            // Build output PDF path (same base name)
            String pdfPath = outputFolder.getAbsolutePath() + File.separator +
                    image.getName().replaceAll("\\.(png|jpg)$", ".pdf");

            // Save as searchable PDF – this step also compresses images
            ocrEngine.saveAsSearchablePdf(pdfPath, pdfOptions);

            System.out.println("✅ Processed: " + image.getName() + " → " + pdfPath);
        }

        System.out.println("🎉 All files have been converted and compressed!");
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda her görüntü için bir satır yazdırır, örneğin:

```
✅ Processed: invoice1.png → /output/invoice1.pdf
✅ Processed: receipt23.jpg → /output/receipt23.pdf
🎉 All files have been converted and compressed!
```

Her oluşturulan PDF'yi bir görüntüleyicide açtığınızda seçilebilir, aranabilir metin görürsünüz; dosya boyutu genellikle **%30‑50 daha küçük** olur, sıkıştırılmamış sürüme kıyasla.

---

## Yaygın Sorular ve Kenar Durumları

### Sunucumda GPU yoksa ne olur?

Sadece `gpuSettings.setEnabled(false)` ayarlayın. Boru hattının geri kalanı değişmeden kalır ve hâlâ çoklu iş parçacıklı CPU işleme alırsınız.

### PDF'lerim hâlâ çok büyük—kaliteyi daha da düşürebilir miyim?

Evet. `options.setImageQuality(70)` ya da hatta `50` gibi bir değere ayarlayın. Daha düşük değerler boyutu daha agresif küçültür ancak ince karakterleri bulanıklaştırabilir. Temsilci bir örnekle test edin.

### Diğer görüntü formatları (TIFF, BMP) nasıl ele alınır?

Filtre lambda'sına uzantıları ekleyin:

```java
name.toLowerCase().endsWith(".png") ||
name.toLowerCase().endsWith(".jpg") ||
name.toLowerCase().endsWith(".tif") ||
name.toLowerCase().endsWith(".bmp")
```

Aynı ön işleme hattı çoğu raster formatı için çalışır.

### Binarize etmek yerine orijinal renkli görüntüleri koruyabilir miyim?

Renkli analiz için renk korumasına ihtiyacınız varsa, ön işleyici oluşturucuda `.addBinarize()` yerine `.addGrayscale()` kullanın.

## Üretim‑Hazır Toplu OCR için Pro İpuçları

- **Bellek yönetimi**: Görüntü başına nesne oluşturma/iyileştirme yükünden kaçınmak için tek bir `OcrEngine` örneğini (gösterildiği gibi) yeniden kullanın.
- **Hata yönetimi**: Tüm toplu işlemi durdurmadan hataları kaydetmek için dosya başına bloğu `try/catch` içinde sarın.
- **Günlükleme**: Ölçeklenebilir çözümler için `System.out.println` yerine uygun bir günlükleme çerçevesi (SLF4J, Log4j) kullanın.
- **Paralellik**: Çok büyük klasörler için alt‑dizinleri paralel akışlarla işlemeyi düşünün, ancak GPU rekabetine dikkat edin.
- **Güvenlik**: Lisans dosyasını depodan dışarıda tutun ve dosya sistemi izinleriyle koruyun.

## Sonuç

**PDF görüntülerini sıkıştırma** ve **toplu OCR'dan PDF'ye** dönüşümünü **PNG'yi PDF'ye dönüştürme**, **JPG'den metin tanıma** ve sağlam bir **OCR için görüntü ön işleme** hattı uygulayarak nasıl gerçekleştireceğimizi gösterdik. Tam Java programı bağımsızdır, modern bir JDK üzerinde çalışır ve arşivleme ya da sonraki analizler için hafif, aranabilir PDF'ler üretir.

Sonraki adımlar? Farklı ön işleme parametreleriyle denemeler yapın, İngilizce dışındaki OCR dillerini deneyin veya iş akışını bir klasörü izleyen ve dosyaları anlık işleyen bir Spring Boot mikroservisine entegre edin. Lisans yükleme, motor yapılandırma, ön işleme ve PDF sıkıştırma temel kavramları aynı kalır; bu da size OCR‑odaklı herhangi bir proje için sağlam bir temel sağlar.

Sorularınız mı var ya da kendi ayarlamalarınızı paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın, iyi kodlamalar!

![Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output](alt="Diagram of batch OCR workflow showing input images, preprocessing, OCR engine, and compressed PDF output")

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve benzer konuları kapsayan içerikler sunar. Her kaynak, ek API özelliklerini öğrenmenize ve projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olacak tam çalışan kod örnekleri ve adım adım açıklamalar içerir.

- [PDF Metin Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose OCR ile metin görüntüsü tanıma – Tam Java OCR Öğreticisi](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Java'da Aspose.OCR BufferedImage kullanarak Görüntüyü Metne Dönüştürme](/ocr/english/java/advanced-ocr-techniques/perform-ocr-buffered-image/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}