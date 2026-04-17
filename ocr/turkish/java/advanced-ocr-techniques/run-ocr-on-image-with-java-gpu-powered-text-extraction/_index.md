---
category: general
date: 2026-03-07
description: Java kullanarak görüntüde OCR çalıştırın. PNG'den metin tanımayı, makbuzdan
  metin çıkarmayı ve tam bir Java OCR örneğiyle OCR için görüntüyü yüklemeyi öğrenin.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: tr
og_description: Java ile görüntüde OCR çalıştırın. Bu rehber, PNG'den metin tanıma,
  makbuzdan metin çıkarma ve tam bir Java OCR örneği kullanarak OCR için görüntü yükleme
  yöntemlerini gösterir.
og_title: Java ile Görüntüde OCR Çalıştır – GPU Destekli Metin Çıkarma
tags:
- OCR
- Java
- GPU
- Image Processing
title: Java ile Görüntüde OCR Çalıştır – GPU Destekli Metin Çıkarma
url: /tr/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüde OCR Çalıştırma Java ile – GPU Destekli Metin Çıkarma

Java’da **görüntüde OCR çalıştırma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici, taranmış bir fişten ya da PNG ekran görüntüsünden metin çıkarmaya ilk kez çalıştıklarında aynı duvara çarpıyor.

Bu öğreticide, **tam bir Java OCR örneği** üzerinden adım adım ilerleyeceğiz; bu örnek **PNG dosyalarından metin tanıma** yapmanın yanı sıra **fiş görüntülerinden metin çıkarma** işlemini de gösteriyor ve hız için GPU hızlandırmasından yararlanıyor. Sonunda, bir görüntüyü OCR’a yükleyen, işleyen ve düz metin sonucunu ekrana yazdıran çalıştırılabilir bir programınız olacak.

## Öğrenecekleriniz

- Basit bir `ImageInputStream` kullanarak **OCR için görüntü yükleme** nasıl yapılır.
- Modern donanımlarda motorun daha hızlı çalışması için GPU desteğinin nasıl etkinleştirileceği.
- **PNG’den metin tanıma** ve bir fişten faydalı satırları çıkarma adımları.
- Yaygın tuzaklar (ör. yanlış GPU cihaz kimliği) ve en iyi uygulama ipuçları.
- IDE’nize kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir kod parçacığı.

**Önkoşullar**

- Java 17 veya daha yeni bir sürüm (kod, kısalık için `var` anahtar kelimesini kullanıyor, ancak Java 8 kullanıyorsanız açık tiplerle değiştirebilirsiniz).
- `OcrEngine`, `ImageInputStream` ve `OcrResult` sınıflarını sağlayan bir OCR kütüphanesi (örneğin, hayali *FastOCR* SDK’sı; kullandığınız gerçek kütüphane ile değiştirin).
- Performans artışı istiyorsanız GPU‑destekli bir makine (isteğe bağlı ama tavsiye edilir).

---

## Adım 1: Görüntüde OCR Çalıştır – GPU Hızlandırmasını Etkinleştir

İlk olarak OCR motorunu oluşturup GPU’yu kullanmasını söylememiz gerekiyor. Bu adım kritiktir; çünkü GPU desteği olmadan motor CPU’ya geri döner ve yüksek çözünürlüklü fişler için belirgin şekilde yavaşlayabilir.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**Neden önemli:**  
GPU hızlandırması, OCR motorlarının gerçekleştirdiği ağır matris hesaplamalarını devre dışı bırakır. Birden fazla GPU’nuz varsa, `setGpuDeviceId` değerini değiştirerek en çok belleğe sahip olanı seçebilirsiniz. GPU’nun etkinleştirilmemesi, “OCR neden bu kadar yavaş?” şikayetlerinin yaygın bir kaynağıdır.

> **Pro ipucu:** Makinenizde uyumlu bir GPU yoksa, `setUseGpu(true)` çağrısı sadece yok sayılır—çökmez, sadece işlem daha yavaş gerçekleşir.

---

## Adım 2: OCR İçin Görüntü Yükleme

Motor hazır olduğuna göre, ona bir görüntü beslememiz gerekiyor. Aşağıdaki örnek, diskte saklanan bir PNG fişi nasıl yükleyeceğinizi gösterir. Yolunu, OCR kütüphanenizin desteklediği herhangi bir görüntü formatı ile değiştirebilirsiniz.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**Köşe durumu:**  
Dosya mevcut değilse ya da yol hatalıysa, `ImageInputStream` bir `IOException` fırlatır. Çağrıyı bir try‑catch bloğuna sarın ve yardımcı bir mesaj kaydedin:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Adım 3: PNG’den Metin Tanıma

Görüntü yüklendiğinde, OCR motoru artık sihrini yapabilir. Bu adım **PNG’den metin tanıma** (veya desteklenen diğer formatlardan) gerçekleştirir ve bir `OcrResult` nesnesi döndürür.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**Arka planda neler oluyor?**  
Motor, ön işleme (eğikliği düzeltme, ikilileştirme) yapar, karakterleri tespit etmek için bir sinir ağı çalıştırır ve ardından bunları metin satırlarına birleştirir. GPU’yu daha önce etkinleştirdiğimiz için bu sinir ağı hesaplamaları grafik kartında gerçekleşir ve toplam çalışma süresinden saniyeler tasarruf sağlar.

---

## Adım 4: Fişten Metin Çıkarma

Tanıma tamamlandıktan sonra genellikle sadece ham metin gerekir. `OcrResult` sınıfı genellikle tek bir `String` döndüren bir `getText()` metodu sunar. Ardından bu metni (ör. toplam tutar, tarih gibi bilgileri çekmek için regex) işleyebilirsiniz.

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Tipik fiş çıktısı:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Bu dizeyi kendi ayrıştırıcınıza besleyerek toplam tutarı, satır kalemlerini ya da vergi bilgilerini çekebilirsiniz.

---

## Adım 5: Tam Java OCR Örneği – Çalıştırmaya Hazır

Her şeyi bir araya getirdiğimizde, **tam Java OCR örneği** aşağıdadır; bu dosyayı `Main.java` içine yapıştırabilirsiniz. OCR kütüphanenizin sınıf yolunda olduğundan emin olun.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**Beklenen konsol çıktısı** (yukarıdaki örnek fişi varsayarsak):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

Çıktı bozuk görünüyorsa, görüntünün net (yüksek DPI) olduğundan ve OCR dil paketinin fişinizin diliyle eşleştiğinden emin olun.

---

## Yaygın Sorular & Tuzaklar

| Soru | Cevap |
|----------|--------|
| *GPU’m algılanmazsa ne olur?* | Motor otomatik olarak CPU’ya geçer. Sürücüleri kontrol edin ve `setGpuDeviceId` değerinin mevcut bir cihazla eşleştiğinden emin olun (`nvidia-smi` Linux’ta yardımcı olabilir). |
| *JPEG veya TIFF dosyalarını işleyebilir miyim?* | Evet—sadece `ImageInputStream` içinde dosya uzantısını değiştirin. OCR kütüphanesi genellikle formatı otomatik algılar. |
| *Birçok fişi toplu işlemek mümkün mü?* | Tanıma kodunu bir döngü içinde çalıştırın ve aynı `OcrEngine` örneğini yeniden kullanın; her görüntü için yeniden başlatmak GPU belleğini boşa harcar. |
| *Düşük kontrastlı fişlerde doğruluğu nasıl artırırım?* | Görüntüyü OCR motoruna vermeden önce ön işleme (kontrast artırma, gri tonlamaya çevirme) yapın. Bazı kütüphaneler bir `preprocess` API’si sunar. |

---

## Sonuç

Artık **Java’da görüntüde OCR çalıştırma**, resmi yüklemeden fişten temiz metin çıkarma sürecine kadar her adımı biliyorsunuz. Bu rehber **PNG’den metin tanıma**, **fişten metin çıkarma** ve **java OCR örneği** konularını kapsadı ve projenize uyarlayabileceğiniz bir temel sağladı.

Sonraki adımlar? GPU bayrağını kapatarak performans farkını gözlemleyin, farklı görüntü çözünürlükleriyle deney yapın ya da toplam tutarları otomatik çekmek için bir regex‑tabanlı ayrıştırıcı entegre edin. Daha ileri konulara meraklıysanız, **OCR sonrası işleme**, **dil modeli düzeltmesi** veya **toplu işleme boru hatları**na bakabilirsiniz.

Kodlamanın tadını çıkarın, ve fişleriniz her zaman okunabilir olsun!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}