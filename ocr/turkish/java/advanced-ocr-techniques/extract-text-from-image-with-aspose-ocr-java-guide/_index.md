---
category: general
date: 2026-02-14
description: Java'da Aspose OCR kullanarak görüntüden metin çıkarın. Kesin sonuçlar
  elde etmek için ilgi bölgeleriyle form alanlarından metin nasıl çıkarılır öğrenin.
draft: false
keywords:
- extract text from image
- extract text from form
language: tr
og_description: Aspose OCR'i Java’da kullanarak görüntüden metin çıkarın. Bu öğreticide,
  ilgi alanları aracılığıyla form alanlarından metin nasıl çıkarılacağını gösterir.
og_title: Aspose OCR ile Görüntüden Metin Çıkarma – Java Rehberi
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCR ile Görüntüden Metin Çıkarma – Java Rehberi
url: /tr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Metin Çıkarma Aspose OCR – Java Rehberi

Hiç **extract text from image** yapmanız gerektiğinde bütün resmi ayrıştırıp CPU döngülerini boşa harcayıp gürültülü sonuçlar aldınız mı? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada—fatura tarayıcıları, pasaport okuyucular veya veri giriş formları gibi—tüm tuval yerine sadece birkaç alana ihtiyacınız olur.  

İyi haber şu ki Aspose OCR, **extract text from image** *ve* belirli form alanlarından çokgenler tanımlayarak metin çıkarmanıza izin verir. Bu öğreticide Java kullanarak **extract text from form** alanlarından nasıl metin çıkaracağınızı, neden bu yaklaşımın önemli olduğunu ve sorunlar çıktığında neyi ayarlamanız gerektiğini tam olarak göreceksiniz.

Aşağıda kütüphaneyi kurmaktan zorlayıcı kenar durumlarını ele almaya kadar her şeyi kapsayacağız; böylece sonunda sadece ihtiyacınız olan verileri çeken, çalıştırmaya hazır bir kod parçacığına sahip olacaksınız.

## Gereksinimler

- Java 17 (veya herhangi bir yeni JDK) – daha yeni sürümler daha iyi Unicode desteğine sahiptir.  
- Aspose.OCR for Java 23.10 (veya okuma zamanındaki en son sürüm).  
- Açıkça tanımlanmış alanlar içeren `form.png` adlı örnek bir görüntü.  
- Bir IDE veya basit bir metin düzenleyici—IntelliJ IDEA, VS Code veya hatta Notepad işinizi görecektir.

Ana demo için Maven/Gradle sihirbazlığı gerekmez; sadece Aspose OCR JAR dosyasını sınıf yolunuza ekleyin.

---

## Adım 1 – OCR Motorunu Başlatın ve Görüntünüzü Yükleyin

Motorun ilk ihtiyacı üzerinde çalışacağı bir bitmap’dir. `form.png` dosyasına işaret edeceğiz; bu dosya kaynak dosyayla aynı klasörde bulunur.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Neden bu önemli:*  
Yeni bir `OcrEngine` oluşturmak temiz bir başlangıç sağlar, kalan ayarların çalışmanızı etkilemesini önler. Görüntüyü erken yüklemek dosyanın var olduğunu doğrular, böylece sonraki adımlarda zaman kaybetmeden faydalı bir istisna alırsınız.

> **Pro tip:** Görüntünüz çok büyükse (5 MB’ın üzerindeyse), önce yeniden boyutlandırmayı düşünün. Aspose OCR, her iki boyutta da 2000 px’nin altındaki görüntülerde daha hızlı çalışır.

## Adım 2 – Okumak İstediğiniz Alanlar İçin Çokgenleri Tanımlayın

Bir *Region of Interest* (ROI), motorun nerede bakacağını belirten bir çokgendir. Aşağıda iki dikdörtgen oluşturuyoruz—biri “First Name”, diğeri “Date of Birth” için. Koordinatları kendi formunuza göre ayarlayın.

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Neden çokgenler, dikdörtgenler yerine?*  
Çokgenler, eğik veya dikdörtgen olmayan kutularla başa çıkma esnekliği sağlar—tam olarak hizalanmamış basılı formları tararken yaygın bir durumdur.

## Adım 3 – Aspose OCR’ı Yalnızca Bu Bölgeler Üzerinde Çalışacak Şekilde Ayarlayın

Şimdi çokgenleri motora bağlıyoruz. `setRegionsOfInterest` metodu bir liste kabul eder, böylece istediğiniz kadar alan ekleyebilirsiniz.

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*Arka planda ne oluyor?*  
Aspose OCR, her çokgeni ayrı bir bitmap’e kırpar, tanıma algoritmasını çalıştırır ve ardından sonuçları birleştirir. Bu, çevredeki grafiklerden kaynaklanan yanlış pozitifleri büyük ölçüde azaltır.

## Adım 4 – OCR İşlemini Çalıştırın

Her şey yapılandırıldıktan sonra OCR’ı başlatıyoruz. `process()` çağrısı, çıkarılan metni ve güven skorlarını tutan bir `OcrResult` nesnesi döndürür.

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

Alan bazında güven skoru gerekiyorsa, `ocrResult.getRegions()` metodunu inceleyebilirsiniz—her bölge kendi skorunu taşır. Çoğu basit form için genel metin yeterlidir.

## Adım 5 – Çıkarılan Metni Görüntüleyin (veya Depolayın)

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada veritabanına, JSON dosyasına yazabilir veya bir API üzerinden gönderebilirsiniz.

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen çıktı (örnek):**

```
=== Extracted Text ===
John Doe
12/04/1990
```

İki satır, tanımladığımız iki çokgene karşılık gelir. Fazladan boşluk görürseniz `String.trim()` ile temizleyin.

## Çok Sayıda Alanı Olan Formdan Metin Çıkarma

Bir formda düzinelerce girdi olduğunda koordinatları manuel olarak yazmak zahmetli olur. İşte hızlı bir desen:

1. **Create a CSV** where each row holds `fieldName, x1, y1, x2, y2, x3, y3, x4, y4`.  
2. **Load the CSV** at runtime, loop through each line, build a `Polygon`, and add it to the ROI list.  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Neden zahmet?*  
ROI üretimini otomatikleştirmek, aynı Java kodunu birden fazla form düzeniyle yeniden kullanmanıza olanak tanır ve projenizi DRY (Don’t Repeat Yourself) tutar.

## Dikkat Etmeniz Gereken Kenar Durumları ve İpuçları

- **Rotated scans:** Eğer bütün görüntü döndürülmüşse, `ocrEngine.getEngineOptions().setRotateAngle(degrees)` metodunu çağırın.  
- **Low contrast:** Okunabilirliği artırmak için `ocrEngine.getEngineOptions().setContrast(1.5f)` ayarlayın.  
- **Non‑Latin scripts:** `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)` (veya desteklenen başka bir dil) ile dili değiştirin.  
- **Partial OCR failures:** Her zaman `ocrResult.getConfidence()` değerini kontrol edin; %80’in altına düşerse kullanıcıdan manuel doğrulama isteyin.  

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenip çalıştırılmaya hazır tam program yer alıyor. `YOUR_DIRECTORY` kısmını `form.png` dosyasının bulunduğu klasörle değiştirin.

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

Derlemek için:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

Tanımlı ROI’lara ait iki metin satırını görmelisiniz.

## Sık Sorulan Sorular

**S: Bu PDF’lerle çalışır mı?**  
C: Doğrudan değil. Önce her PDF sayfasını bir görüntüye dönüştürün (ör. Aspose PDF kullanarak) ve ardından görüntüyü OCR motoruna besleyin.

**S: Formumda onay kutuları varsa ne yapmalıyım?**  
C: OCR, boolean durumları okuyamaz, ancak onay kutusu alanını bir ROI olarak ele alıp piksel yoğunluğunu inceleyerek işaretli olup olmadığını tahmin edebilirsiniz.

**S: Çok sayfalı bir formdan tek seferde metin çıkarabilir miyim?**  
C: Her sayfa görüntüsü üzerinde döngü kurun, aynı ROI listesini yeniden kullanın ve sonuçları birleştirin.

## Sonuç

Aspose OCR kullanarak **extract text from image** için tam bir uçtan uca çözüm üzerinden ilerledik ve aynı tekniğin **extract text from form** alanlarından nokta atışıyla metin çıkarma imkanı sunduğunu gösterdik. Çokgen tanımlayarak, motorun odak noktasını sınırlayarak ve yaygın tuzakları ele alarak, tüm resmi işlemeye gerek kalmadan hızlı ve temiz veri elde edersiniz.

Bir sonraki adıma hazır mısınız? Bu OCR çıktısını bir JSON yüküne dönüştürmeyi deneyin ya da doğrulama için bir makine‑öğrenme modeline besleyin. Ufkunuz sınırsız ve şimdi siz... 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}