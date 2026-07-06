---
category: general
date: 2026-02-22
description: Java'da OCR'yi kullanarak görüntüden metin çıkarmak, OCR doğruluğunu
  artırmak ve OCR için görüntüyü yüklemek üzerine pratik kod örnekleri.
draft: false
keywords:
- how to use OCR
- extract text from image
- improve OCR accuracy
- load image for OCR
- OCR preprocessing
language: tr
og_description: Java’da OCR kullanarak görüntüden metin çıkarmak ve OCR doğruluğunu
  artırmak nasıl yapılır? Hazır‑çalıştır örnek için bu rehberi izleyin.
og_title: Java'da OCR Nasıl Kullanılır – Tam Adım Adım Rehber
tags:
- OCR
- Java
- Image Processing
title: Java'da OCR Nasıl Kullanılır – Tam Adım Adım Rehber
url: /tr/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/
---

neği, ön işleme ve sonucu gösteriyor")

Now final shortcodes remain.

Now produce final content with all translations.

Check for any missed bold phrases: keep them unchanged.

Check for any other markdown links: none.

Check for any code block placeholders: they remain.

Check for any URLs: only image URL, unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java'da OCR Nasıl Kullanılır – Tam Adım‑Adım Kılavuz

Titrek bir ekran görüntüsünde **how to use OCR** yapmanız gerektiğinde ve çıktının neden karışık göründüğünü merak ettiğiniz oldu mu? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada—fiş tarama, formları dijitalleştirme veya memlerden metin çekme—güvenilir sonuçlar elde etmek birkaç basit ayara bağlıdır.

Bu öğreticide **how to use OCR**'ı *extract text from image* dosyalarından metin çıkarmak için adım adım gösterecek, **improve OCR accuracy**'yi nasıl artıracağınızı gösterecek ve popüler bir Java OCR kütüphanesi kullanarak **load image for OCR**'ı doğru şekilde nasıl yapacağınızı göstereceğiz. Sonunda, herhangi bir projeye ekleyebileceğiniz bağımsız bir programınız olacak.

## Öğrenecekleriniz

- **load image for OCR** için ihtiyacınız olan tam kod (gizli bağımlılık yok).
- Hangi ön işleme bayraklarının **improve OCR accuracy**'yi artırdığını ve neden önemli olduklarını.
- OCR sonucunu nasıl okuyacağınızı ve konsola nasıl yazdıracağınızı.
- Yaygın tuzaklar—örneğin ilgi bölgesi (ROI) ayarlamayı unutmak veya gürültü azaltmayı göz ardı etmek—ve bunlardan nasıl kaçınılacağını.

### Önkoşullar

- Java 17 veya daha yeni (kod, herhangi bir güncel JDK ile derlenir).
- `OcrEngine`, `ImagePreprocessingOptions`, `OcrInput` ve `OcrResult` sınıflarını sağlayan bir OCR kütüphanesi (örneğin, örnek kodda kullanılan hayali `com.example.ocr` paketi). Kullandığınız gerçek kütüphane ile değiştirin.
- Referans alabileceğiniz bir klasöre yerleştirilmiş örnek bir görüntü (`skewed_noisy.png`).

> **Pro ipucu:** Ticari bir SDK kullanıyorsanız, lisans dosyasının sınıf yolunuzda (classpath) olduğundan emin olun; aksi takdirde motor bir başlatma hatası verir.

---

## Adım 1: Bir OCR Motoru Örneği Oluşturun – **how to use OCR** etkili bir şekilde

İhtiyacınız olan ilk şey bir `OcrEngine` nesnesidir. Bunu, pikselleri yorumlayacak beyin olarak düşünün.

```java
// Step 1: Initialize the OCR engine
import com.example.ocr.OcrEngine;

OcrEngine ocrEngine = new OcrEngine();
```

*Neden önemli:* Bir motor olmadan dil modelleri, karakter setleri veya görüntü sezgileri için bağlamınız olmaz. Erken oluşturmak, daha sonra ön işleme seçenekleri eklemenizi de sağlar.

---

## Adım 2: Görüntü Ön İşlemeyi Yapılandırın – **improve OCR accuracy**

Ön işleme, gürültülü bir taramayı temiz, makine‑okunabilir metne dönüştüren gizli sosdur. Aşağıda, görüntünün ilgili kısmına odaklanmak için deskew, yüksek seviyeli gürültü azaltma, otomatik kontrast ve ilgi bölgesi (ROI) etkinleştiriyoruz.

```java
import com.example.ocr.ImagePreprocessingOptions;
import java.awt.Rectangle;

// Step 2: Set up preprocessing to improve OCR accuracy
ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
preprocessing.setDeskewEnabled(true); // Correct image rotation
preprocessing.setNoiseReductionLevel(
        ImagePreprocessingOptions.NoiseReduction.HIGH); // Reduce speckles
preprocessing.setAutoContrastEnabled(true); // Boost contrast
preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600)); // Process a sub‑region only

ocrEngine.setPreprocessingOptions(preprocessing);
```

*Neden önemli:*  
- **Deskew** döndürülmüş metni hizalar; bu, tamamen düz olmayan fiş tararken esastır.  
- **Noise reduction** karakter olarak yorumlanabilecek rastgele pikselleri kaldırır.  
- **Auto‑contrast** ton aralığını genişletir, soluk harflerin öne çıkmasını sağlar.  
- **ROI** motorun alakasız kenarları görmezden gelmesini söyler, zaman ve bellek tasarrufu sağlar.

Bunlardan birini atladığınızda, **improve OCR accuracy** sonuçlarında muhtemelen bir düşüş göreceksiniz.

---

## Adım 3: Görüntüyü OCR İçin Yükleyin – **load image for OCR** doğru şekilde

Şimdi motoru okumak istediğimiz dosyaya yönlendiriyoruz. `OcrInput` sınıfı birden fazla görüntüyü kabul edebilir, ancak bu örnek için basit tutuyoruz.

```java
import com.example.ocr.OcrInput;

// Step 3: Load the image you want to extract text from
OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png"); // replace with your real path
```

*Neden önemli:* Yol mutlak ya da çalışma dizinine göre göreceli olmalıdır; aksi takdirde motor bir `FileNotFoundException` fırlatır. Ayrıca, `add` metodunun adı, birkaç görüntüyü kuyruğa ekleyebileceğinizi gösterir—toplu işleme için kullanışlıdır.

---

## Adım 4: OCR'ı Gerçekleştir ve Tanınan Metni Çıktıla – **how to use OCR** uçtan‑uca

Son olarak, motoru metni tanıması ve yazdırması için istiyoruz. `OcrResult` nesnesi ham dizeyi, güven skorlarını ve satır‑satır meta verileri (daha sonra ihtiyaç duyarsanız) içerir.

```java
import com.example.ocr.OcrResult;

// Step 4: Run OCR and print the extracted text
OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Beklenen çıktı** (örnek görüntü “Hello, OCR World!” içeriyorsa):

```
=== OCR Output ===
Hello, OCR World!
```

Sonuç karışık görünüyorsa, Adım 2'ye geri dönün ve ön işleme seçeneklerini ayarlayın—belki gürültü azaltma seviyesini düşürün veya ROI dikdörtgenini değiştirin.

---

## Tam, Çalıştırılabilir Örnek

Aşağıda, `OcrDemo.java` adlı bir dosyaya kopyalayıp yapıştırabileceğiniz tam bir Java programı bulunmaktadır. Tartıştığımız tüm adımları birleştirir.

```java
// OcrDemo.java – A complete, runnable example showing how to use OCR in Java
import com.example.ocr.OcrEngine;
import com.example.ocr.ImagePreprocessingOptions;
import com.example.ocr.OcrInput;
import com.example.ocr.OcrResult;
import java.awt.Rectangle;

public class OcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing (this is the key to improve OCR accuracy)
        ImagePreprocessingOptions preprocessing = new ImagePreprocessingOptions();
        preprocessing.setDeskewEnabled(true);
        preprocessing.setNoiseReductionLevel(
                ImagePreprocessingOptions.NoiseReduction.HIGH);
        preprocessing.setAutoContrastEnabled(true);
        preprocessing.setRegionOfInterest(new Rectangle(100, 200, 800, 600));
        ocrEngine.setPreprocessingOptions(preprocessing);

        // 3️⃣ Load the image you want to extract text from
        OcrInput ocrInput = new OcrInput();
        // 👉 Replace the path with your own image location
        ocrInput.add("YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run the OCR engine and print the result
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

Dosyayı kaydedin, `javac OcrDemo.java` ile derleyin ve `java OcrDemo` ile çalıştırın. Her şey doğru ayarlandıysa, çıkarılan metni konsolda göreceksiniz.

---

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|------|-------|
| **Görüntüm JPEG formatında olsaydı ne olur?** | `OcrInput.add()` metodu, PNG, JPEG, BMP, TIFF gibi desteklenen herhangi bir raster formatını kabul eder. Sadece dosya yolundaki uzantıyı değiştirin. |
| **Birden fazla sayfayı aynı anda işleyebilir miyim?** | Kesinlikle. Her dosya için `ocrInput.add()` çağırın, ardından aynı `ocrInput`'u `recognize()`'a gönderin. Motor, birleştirilmiş bir `OcrResult` döndürecektir. |
| **OCR sonucu boş çıkarsa ne olur?** | ROI'nun gerçekten metin içerdiğini iki kez kontrol edin. Ayrıca `setDeskewEnabled(true)`'un açık olduğundan emin olun; 90° bir dönüşüm motorun görüntüyü boş olarak algılamasına neden olur. |
| **Dil modelini nasıl değiştiririm?** | Çoğu kütüphane, `OcrEngine` üzerinde bir `setLanguage(String)` metodu sunar. `recognize()`'den önce çağırın, örneğin `ocrEngine.setLanguage("eng")`. |
| **Güven skorlarını elde etmenin bir yolu var mı?** | Evet, `OcrResult` genellikle satır veya karakter başına `getConfidence()` sağlar. Düşük güvenilir sonuçları filtrelemek için bunu kullanın. |

---

## Sonuç

**how to use OCR**'ı Java'da baştan sona ele aldık: motoru oluşturmak, **improve OCR accuracy** için ön işleme yapılandırmak, **load image for OCR**'ı doğru şekilde yapmak ve sonunda çıkarılan metni yazdırmak. Tam kod parçacığı çalıştırmaya hazır ve açıklamalar her satırın “neden”ini yanıtlıyor.

Bir sonraki adıma hazır mısınız? ROI dikdörtgenini değiştirerek görüntünün farklı bölümlerine odaklanmayı deneyin, `NoiseReduction.MEDIUM` ile deney yapın veya çıktıyı aranabilir bir PDF'ye entegre edin. Ayrıca **extract text from image** gibi bulut hizmetlerini kullanarak ilgili konuları keşfedebilir ya da çok iş parçacıklı bir kuyrukla binlerce dosyayı toplu işleyebilirsiniz.

OCR, görüntü ön işleme veya Java entegrasyonu hakkında daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar! 

![OCR kullanma örneği](/images/ocr-demo.png "how to use OCR – Java örneği, ön işleme ve sonucu gösteriyor")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}