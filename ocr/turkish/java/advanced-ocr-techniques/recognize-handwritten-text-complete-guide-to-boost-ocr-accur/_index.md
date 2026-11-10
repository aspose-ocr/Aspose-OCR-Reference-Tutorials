---
category: general
date: 2026-03-07
description: El yazısı metni tanımayı öğrenin, OCR doğruluğunu artırın ve görüntü
  dosyalarında OCR çalıştırın. Özel sözlükle adım adım Java örneği.
draft: false
keywords:
- recognize handwritten text
- improve ocr accuracy
- run OCR on image
- load image for OCR
- OCR engine configuration
- custom dictionary OCR
language: tr
og_description: Java OCR motoru ile el yazısı metni tanıyın. OCR doğruluğunu artırmak
  için rehberimizi izleyin, görüntüde OCR çalıştırın ve OCR için görüntüyü yükleyin.
og_title: El yazısı tanıma – Tam Java Öğreticisi
tags:
- OCR
- Java
- Handwriting Recognition
title: El yazısı tanıma – OCR Doğruluğunu Artırmak İçin Tam Rehber
url: /tr/java/advanced-ocr-techniques/recognize-handwritten-text-complete-guide-to-boost-ocr-accur/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# el yazısı tanıma – Tam Java Öğreticisi

Bir fotoğraftan **el yazısı tanıma** yapmanız gerektiğinde ama sürekli anlamsız sonuçlar alıyor musunuz? Tek başınıza değilsiniz. Birçok projede—fiş tarayıcıları, not alma uygulamaları veya arşivleme araçları—el yazısı OCR'si hareketli bir hedefi kovalamak gibi hissettirebilir.  

İyi haber? Birkaç yapılandırma ayarıyla **OCR doğruluğunu artırabilirsiniz** ve **run OCR on image** dosyalarının tamamı sadece birkaç Java satırıyla yapılabilir. Aşağıda tam olarak nasıl **load image for OCR** yapılacağını, yazım düzeltmesini nasıl etkinleştireceğinizi ve hatta kendi sözlüğünüzü nasıl ekleyeceğinizi göreceksiniz.

Bu öğreticide şunları ele alacağız:

* Minimum önkoşullar (Java 11+, bir OCR kütüphanesi ve örnek bir görüntü).
* Yazım düzeltmeleri için OCR motorunu nasıl yapılandıracağınız.
* Alan‑spesifik kelimeler için özel bir sözlük ekleme.
* Tanıma hattını çalıştırma ve düzeltilmiş sonucu yazdırma.

Sonunda, varsayılan ayarlara göre çok daha az hatayla **el yazısı tanıma** yapabilen, çalıştırmaya hazır bir programınız olacak.

---

## İhtiyacınız Olanlar

| Öğe | Neden Önemli |
|------|----------------|
| **Java 11 or newer** | Örnek, modern `var` anahtar sözcüğünü ve `try‑with‑resources` yapısını kullanır. |
| **OCR library** (e.g., `com.example.ocr` – replace with your actual vendor) | `OcrEngine`, `OcrResult` ve yapılandırma nesnelerini sağlar. |
| **Handwritten image** (`handwritten_note.jpg`) | Tanıma yapmak istediğiniz metni içeren örnek bir JPEG. |
| **Optional custom dictionary** (`custom_dict.txt`) | Sektöre özgü terimler, kısaltmalar veya özel adların tanınmasını iyileştirir. |

Henüz bir OCR JAR'ınız yoksa, sağlayıcının Maven deposundan en son sürümü alın ve projenizin sınıf yoluna ekleyin.

---

## 1. Adım – OCR Motorunu Oluşturma ve Yapılandırma  

İlk yapmanız gereken, motoru örneklemek ve yerleşik yazım‑düzeltme özelliğini açmaktır. Bu tek başına el yazısı notlarda sıkça görülen birçok hatalı kelimeyi ortadan kaldırabilir.

```java
import com.example.ocr.OcrEngine;
import com.example.ocr.OcrConfig;

// Create an OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Enable spell‑correction to automatically fix common mistakes
OcrConfig config = ocrEngine.getConfig();
config.setEnableSpellCorrection(true);
```

**Neden Önemli:** El yazısı karakterler sık sık diğer harflere benzer (ör., “m” vs. “n”). Yazım‑düzeltmeyi etkinleştirmek, motorun en olası kelimeyi tahmin eden bir dil modeli uygulamasını sağlar ve genel **OCR doğruluğunu** artırır.

---

## 2. Adım – (İsteğe Bağlı) Özel Sözlük Eklemek  

Notlarınızda varsayılan sözlükte bulunmayan jargon, ürün kodları veya isimler varsa, motoru satır başına bir kelime içeren düz metin dosyasına yönlendirebilirsiniz.

```java
// Path to a custom dictionary; comment out if you don't need it
config.setCustomDictionaryPath("YOUR_DIRECTORY/custom_dict.txt");
```

**Pro ipucu:** Dosyanın UTF‑8 kodlamalı olduğundan ve boş satır içermediğinden emin olun; motor her satırı ayrı bir token olarak okur. Özel bir liste sağlamak, uzmanlaşmış alanlarda **OCR doğruluğunu** %15'e kadar artırabilir.

---

## 3. Adım – OCR İçin Görüntüyü Yükleme  

Şimdi, motoru el yazısı resmini temsil eden bir bayt akışıyla beslememiz gerekiyor. `ImageInputStream` sınıfı dosya G/Ç'yi soyutlar ve OCR motorunun desteklediği herhangi bir görüntü formatıyla çalışmasını sağlar.

```java
import com.example.ocr.ImageInputStream;

// Load the image you want to process
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/handwritten_note.jpg");
```

**Görüntü büyük olursa ne olur?** Çoğu OCR motoru bir `maxResolution` parametresi kabul eder. Bellek kullanımını düşük tutmak için görüntüyü önceden `java.awt.Image` gibi bir kütüphane ile küçültebilirsiniz.

---

## 4. Adım – Görüntüde OCR Çalıştırma ve Düzeltlenmiş Metni Alma  

Motor yapılandırıldı ve görüntü yüklendiğinde, gerçek tanıma tek bir metod çağrısıdır. Sonuç nesnesi ham metni ve her satır için güven skorlarını içerir.

```java
import com.example.ocr.OcrResult;

// Perform the recognition
OcrResult ocrResult = ocrEngine.recognize(imageStream);

// Extract the corrected text
String correctedText = ocrResult.getText();
```

Hata ayıklamanız gerekiyorsa, `ocrResult.getConfidence()` 0 ile 1 arasında bir float döndürerek genel kesinliği gösterir.

---

## 5. Adım – Sonucu Görüntüleme  

Son olarak, temizlenmiş çıktıyı konsola yazdırın. Gerçek bir uygulamada bunu bir veritabanına kaydedebilir veya sonraki bir NLP hattına besleyebilirsiniz.

```java
public class HandwrittenOcrDemo {
    public static void main(String[] args) {
        // Steps 1‑4 are encapsulated above; just print the result
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

**Expected output (example):**

```
Corrected text:
Meeting notes:
- Discuss quarterly targets
- Review budget allocations
- Assign action items to team leads
```

Ham taramada bulunan yazım hatalarının, yazım‑düzeltme bayrağı ve isteğe bağlı sözlük sayesinde nasıl yok olduğunu fark edin.

---

## Tam, Çalıştırılabilir Örnek  

Aşağıda, kopyalayıp yolları ayarlayarak doğrudan çalıştırabileceğiniz tek bir Java dosyası bulunmaktadır (`javac HandwrittenOcrDemo.java && java HandwrittenOcrDemo`). Gerekli tüm import'lar ve yorumlar eklenmiştir.

```java
// HandwrittenOcrDemo.java
// -----------------------------------------------------
// Demonstrates how to recognize handwritten text,
// improve OCR accuracy with spell‑correction, and
// optionally use a custom dictionary.
// -----------------------------------------------------

import com.example.ocr.OcrEngine;
import com.example.ocr.OcrConfig;
import com.example.ocr.ImageInputStream;
import com.example.ocr.OcrResult;

public class HandwrittenOcrDemo {
    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable spell‑correction (crucial for accuracy)
        OcrConfig config = ocrEngine.getConfig();
        config.setEnableSpellCorrection(true);

        // 3️⃣ (Optional) Attach a custom dictionary
        //    Uncomment and point to your file if needed
        // config.setCustomDictionaryPath("YOUR_DIRECTORY/custom_dict.txt");

        // 4️⃣ Load the image you want to process
        ImageInputStream imageStream = new ImageInputStream(
                "YOUR_DIRECTORY/handwritten_note.jpg"
        );

        // 5️⃣ Run OCR on the image and fetch corrected text
        OcrResult ocrResult = ocrEngine.recognize(imageStream);
        String correctedText = ocrResult.getText();

        // 6️⃣ Show the output
        System.out.println("Corrected text:");
        System.out.println(correctedText);
    }
}
```

### Kodu Çalıştırma

```bash
javac -cp ocr-lib.jar HandwrittenOcrDemo.java
java -cp .:ocr-lib.jar HandwrittenOcrDemo
```

`ocr-lib.jar` dosyasını indirdiğiniz gerçek JAR adıyla değiştirin. Program, temizlenmiş transkripsiyonu konsola yazdıracaktır.

---

## Yaygın Sorular ve Kenar Durumları  

### Görüntü döndürülmüşse ne olur?

Birçok OCR kütüphanesi bir `setAutoRotate(true)` bayrağı sunar. `recognize` metodunu çağırmadan önce bunu etkinleştirin:

```java
config.setAutoRotate(true);
```

### Özel sözlüğüm uygulanmıyor—neden?

Dosya yolunun mutlak ya da çalışma dizinine göre göreceli olduğundan ve her satırın bir yeni satır karakteri (`\n`) ile bittiğinden emin olun. Ayrıca sözlük dosyasının UTF‑8 kodlamalı olduğunu doğrulayın; aksi takdirde motor bilinmeyen karakterleri atlayabilir.

### Birden fazla görüntüyü toplu olarak nasıl işleyebilirim?

Tanıma mantığını bir döngü içine alın:

```java
for (String path : imagePaths) {
    ImageInputStream stream = new ImageInputStream(path);
    OcrResult result = ocrEngine.recognize(stream);
    System.out.println("File: " + path);
    System.out.println(result.getText());
}
```

Aynı `OcrEngine` örneğini yeniden kullanmayı unutmayın; her görüntü için yeni bir motor oluşturmak gereksizdir ve performansı düşürebilir.

### Tarama PDF'lerinde çalışır mı?

Kütüphaneniz PDF'yi giriş formatı olarak destekliyorsa, her sayfayı önce bir görüntüye çıkararak (`Apache PDFBox` gibi) hâlâ `ImageInputStream` kullanabilirsiniz. Raster bir görüntünüz olduğunda aynı işlem hattı geçerli olur.

---

## OCR Doğruluğunu Azamiye Çıkarma İpuçları  

| İpucu | Sebep |
|-----|--------|
| **Görüntüyü ön‑işleme** (kontrastı artır, ikilileştir) | Daha temiz pikseller hatalı tanımlamaları azaltır. |
| **Yüksek çözünürlüklü tarama kullanın (≥300 dpi)** | Daha fazla detay motorun daha çok ipucu almasını sağlar. |
| **Dil modellerini etkinleştirin** (`config.setLanguage("en")`) | Yazım‑düzeltmeyi doğru kelime dağarcığıyla hizalar. |
| **Özel bir sözlük sağlayın** | Genel modellerin kaçırdığı alan‑spesifik kelimeleri ele alır. |
| **Otomatik döndürmeyi etkinleştirin** | Farklı açılarda çekilen fotoğrafları işler. |

Bunların birkaçını bir arada uygulamak, tipik notlar için **el yazısı tanıma** başarı oranlarını %90'ın üzerine çıkarabilir.

---

## Sonuç  

Java OCR motoru kullanarak **el yazısı tanıma**, yazım‑düzeltme ve özel sözlük ile **OCR doğruluğunu artırma**, ve **load image for OCR** yaptıktan sonra **run OCR on image** dosyalarını çalıştırma konularını gösteren eksiksiz bir uçtan‑uca örnek üzerinden geçtik.  

Kod kendi içinde bağımsızdır, açıklamalar *ne* ve *neden* olduğunu kapsar ve artık boru hattını kendi projelerinize uyarlamak için sağlam bir temele sahipsiniz—ister makbuzları toplu işlemek, ders notlarını dijitalleştirmek, ister tanınan metni sonraki bir AI modeline beslemek olsun.  

### Sıradaki Adımlar?

* Farklı görüntü ön‑işleme kütüphanelerini (OpenCV, TwelveMonkeys) deneyerek kontrast ayarlarının sonuçları nasıl etkilediğini görün.  
* Çok dilli notlarınız varsa dil modelini başka bir yerel ayara geçirmeyi deneyin.  
* OCR adımını bir Spring Boot mikroservisine entegre edin, böylece diğer uygulamalar **run OCR on image** işlemini bir REST uç noktası üzerinden yapabilir.  

Herhangi bir sorunla karşılaşırsanız veya daha fazla ayar fikriniz varsa, aşağıya bir yorum bırakın. Kodlamanın tadını çıkarın, ve el yazısı taramalarınız nihayet okunabilir metinlere dönüşsün!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}