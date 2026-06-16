---
category: general
date: 2026-04-29
description: Aspose OCR akış modunu kullanarak tiff dosyalarını nasıl OCR yapacağınızı
  öğrenin. Bu kılavuz, döşeli TIFF görüntülerinden metin döşemelerini verimli bir
  şekilde nasıl çıkaracağınızı gösterir.
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: tr
og_description: Aspose OCR akışı kullanarak TIFF üzerinde OCR nasıl yapılır. Büyük
  TIFF görüntülerinden metin parçalarını çıkarmak için adım adım kod.
og_title: tiff OCR nasıl yapılır – Tam Akış Kılavuzu
tags:
- OCR
- Java
- Aspose
- TIFF
title: tiff'i nasıl OCR'layabilirsiniz – Büyük TIFF'leri akıtın ve Java'da metin parçalarını
  çıkarın
url: /tr/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr tiff – Büyük TIFF'leri Akıtma ve Metin Parçalarını Java'da Çıkarma

Hiç **how to ocr tiff** dosyalarının bir kerede belleğe sığmayacak kadar büyük olduğunu merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, TIFF görüntülerinin onlarca parçaya bölündüğü zaman bir duvara çarpar ve normal `ocrEngine.recognize()` çağrısı sadece tıkanır.  

İyi haber? Aspose OCR’ın akış (streaming) modu, her bir parçayı ayrı bir akış olarak beslemenize izin verir, böylece **extract text tiles** yaparken heap’iniz patlamaz. Bu öğreticide, tamamen çalıştırılabilir bir Java örneği üzerinden adım adım ilerleyecek, her satırın neden önemli olduğunu açıklayacak ve kaçınmanız gereken tuzakları göstereceğiz.

> **What you’ll get:** an runnable program that stitches together tiled TIFFs on‑the‑fly, prints the combined text, and shows you how to adapt the code for other languages or image formats.

---

## Prerequisites

- **Java 17** veya daha yeni bir sürüm (kod try‑with‑resources kullandığı için JDK 8+ çalışır, ancak JDK 17 güncel LTS’dir).
- **Aspose.OCR for Java** kütüphanesi (v23.10 veya sonrası). Maven ile ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- Bireysel TIFF parçalarını içeren bir klasör (ör. `tile_0.tif`, `tile_1.tif`, …).  
- İsteğe bağlı: IntelliJ IDEA veya VS Code gibi bir IDE – ama basit bir metin düzenleyicisi de iş görür.

---

## Step 1 – Prepare the Tile Paths (Why It Matters)

OCR motorunun bir şeyler yapabilmesi için her bir görüntü parçasının nerede olduğunu bilmesi gerekir. Yolları sabit kodlamak bir demo için sorun değil, fakat üretimde muhtemelen bir dizini tarar ya da bir manifest dosyası okursunuz.

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** parçaları sözlük sırasına göre (0, 1, 2…) tutun; çünkü motor tanınan metni aynı sırada birleştirir.

---

## Step 2 – Enable Streaming Mode on the OCR Engine (Primary Keyword)

Şimdi `OcrEngine` örneğini oluşturup akış modunu açıyoruz. Bu, **how to ocr tiff** yaparken tüm görüntüyü RAM’e yüklemeden çalışmanın özüdür.

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
`setEnableStreaming(true)` çağrısı yapıldığında, motor gelen her `ImageStream`i bir öncekinin devamı olarak kabul eder. İçsel bir sanal tuval oluşturur, parçaları sanal olarak birleştirir ve sonunda tek bir OCR çalıştırır. Bu, çok‑gigabaytlık bir TIFF’i bir kerede yüklemeye çalıştığınızda ortaya çıkacak “OutOfMemoryError” hatasını önler.

---

## Step 3 – Append Each Tile as an Input Stream (Secondary Keyword)

Her bir parçayı motora besleyen döngü burada. `try‑with‑resources` bloğu dosya tutamacının hızlıca kapanmasını sağlar; bu, onlarca dosyayla çalışırken kritik önemdedir.

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

Dikkat edin, **extract text tiles** ifadesi doğal olarak yer alıyor: her yineleme bir parçadan metni *çıkartıyor* ve büyüyen sonuç kümesine ekliyor.

---

## Step 4 – Run Recognition and Output the Combined Text (Primary Keyword)

Tüm parçalar kuyruğa alındıktan sonra tek bir çağrı sanal görüntü üzerinde OCR gerçekleştirir. Sonuç, tek bir dev TIFF’e sahipmiş gibi tam metni içerir.

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output** (parçalar “Hello World” ifadesini bölünmüş olarak içeriyorsa):

```
=== OCR Output ===
Hello World
```

Parçalar daha fazla satır içeriyorsa, sağladığınız sırayla görüneceklerdir. `ocrResult.getText()` değerini dosyaya yazarak sonraki işlemlere de aktarabilirsiniz.

---

## Step 5 – Full, Runnable Example (All Steps in One Place)

Aşağıda `StreamingExample.java` dosyasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Tüm importlar, yorumlar ve hata yönetimi dahil.

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Kaydedin, derleyin ve çalıştırın:

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

Konsolda birleştirilmiş OCR metninin çıktısını görmelisiniz.

---

## Advanced Tips & Common Pitfalls (Why This Works)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory errors** | Tam boyutlu bir TIFF’i `BufferedImage` olarak yüklemek heap’in tamamını tüketir. | Akış modunu (`setEnableStreaming(true)`) kullanın – motor hiçbir zaman bütün görüntüyü materyalleştirmez. |
| **Tile order mismatch** | Dosyalar alfabetik olarak sıralanır, sayısal sıralama (ör. `tile_10.tif` `tile_2.tif`’den önce) bozulur. | Sayıları sıfırla doldurun (`tile_00.tif`, `tile_01.tif`) veya `Comparator` ile programatik olarak sıralayın. |
| **Wrong language** | OCR varsayılan olarak İngilizce; başka bir dildeki metin bozuk çıkar. | `ocrEngine.getLanguageSettings().setLanguage("fr")` gibi (desteklenen ISO kodlarından) bir dil ayarlayın. |
| **Partial failures** | Tek bir bozuk parça tüm süreci durdurur. | Parça başına `IOException` yakalayın, loglayın ve devam edip etmeyeceğinize karar verin. |
| **Performance bottleneck** | Çok sayıda küçük dosya okurken disk I/O baskın olur. | Parçaları bir ZIP içinde paketleyip bellekten akıtın, ya da hızlı bir SSD kullanın. |

---

## When to Use Streaming vs. Single‑Image OCR

- **Streaming** şu durumlar için idealdir:
  - Çok sayfalı TIFF’ler veya gigapiksel taramalar.
  - Bellek kısıtlı olduğunda (ör. Docker konteynerleri, mobil cihazlar).
  - Görüntü parçalarını zaten alan bir pipeline (ör. kamera akışları).

- **Single‑image OCR** şu durumlarda rahatlıkla kullanılabilir:
  - Küçük PNG/JPEG dosyaları (< 5 MB).
  - Tek seferlik taramalar ve basitlik performanstan daha önemli olduğunda.

---

## Conclusion

Artık **how to ocr tiff** dosyalarını Aspose OCR’ın akış özellikleriyle nasıl işleyebileceğinizi, **extract text tiles** işlemini verimli bir şekilde nasıl yapacağınızı biliyorsunuz. Motoru başlatma, akış modunu etkinleştirme, her parçayı ekleme ve sonunda sanal tuval üzerinde tanıma yapma adımları, üretime hazır kod için gereken “ne”, “neden” ve “nasıl”ı kapsıyor.

Sonraki adımlar? `"en"` yerine başka bir dil kodu deneyin ya da farklı görüntü formatları (`.png`, `.jpg`) ile oynayın. OCR sonucunu doğrudan bir arama indeksine ya da PDF oluşturucuya da aktarabilirsiniz. Desen aynı kalır: akıt, birleştir, tanı.

Yüzlerce parçaya ölçeklendirme konusunda sorularınız mı var, yoksa hata yönetimiyle ilgili yardıma mı ihtiyacınız var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}