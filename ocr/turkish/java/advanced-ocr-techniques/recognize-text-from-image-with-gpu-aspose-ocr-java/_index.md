---
category: general
date: 2026-04-26
description: Java'da GPU hızlandırmalı Aspose OCR kullanarak görüntüden metin tanımayı
  öğrenin. GPU bellek sınırını ayarlama ve OCR için görüntü yükleme adımlarını içerir.
draft: false
keywords:
- recognize text from image
- set gpu memory limit
- load image for ocr
- Aspose OCR Java
- GPU acceleration OCR
language: tr
og_description: GPU hızlandırmalı Aspose OCR'i Java'da kullanarak görüntüden metni
  hızlı bir şekilde tanıma yöntemini keşfedin. GPU bellek sınırını ayarlama ve OCR
  için görüntü yükleme adım adım rehberi.
og_title: GPU Aspose OCR (Java) ile görüntüden metin tanıma
tags:
- OCR
- Java
- GPU
- Aspose
title: GPU Aspose OCR (Java) kullanarak görüntüden metin tanıma
url: /tr/java/advanced-ocr-techniques/recognize-text-from-image-with-gpu-aspose-ocr-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU Aspose OCR (Java) ile görüntüden metin tanıma

Java backend'inde **görüntüden metin tanıma** işlemini hızlıca yapmanız gerektiğinde? Aspose OCR’ın GPU hızlandırması sayesinde her taramadan saniyeler kazanabilirsiniz—CPU’nun megabaytlarca pikseli işlemesini beklemek kalmadı. Bu öğreticide GPU'yu nasıl etkinleştireceğinizi, isteğe bağlı **GPU bellek sınırını ayarlamayı**, ve son olarak **OCR için görüntüyü yüklemeyi** adım adım göstereceğiz; böylece sadece birkaç satır kodla temiz bir metin dizesi elde edeceksiniz.

CUDA‑destekli bir kartta demoyu çalıştırmak için ihtiyacınız olan her şeyi ele alacağız, her ayarın neden önemli olduğunu açıklayacağız ve tamamen çalışır bir örnek sunacağız. Sonunda, belge‑işleme hattı ya da gerçek‑zamanlı mobil‑backend gibi herhangi bir Java servisine GPU‑hızlandırmalı OCR ekleyebileceksiniz.

## Gereksinimler

- **Java 17** veya daha yeni (Aspose OCR JAR modern JVM'leri hedefler)  
- En az **2 GB VRAM**'e sahip **CUDA‑uyumlu bir GPU** (demo kullanımını 1024 MB ile sınırlar)  
- **Aspose.OCR for Java** kütüphanesi (Aspose sitesinden indirin veya Maven'dan çekin)  
- İşlemek istediğiniz bir görüntü dosyası – tercihen yüksek çözünürlüklü bir tarama ya da fotoğraf  

Harici hizmet yok, bulut anahtarı yok, sadece yerel kurulum. GPU'nuz yoksa bile kodu çalıştırabilirsiniz; `setUseGpu(true)` çağrısı otomatik olarak CPU'ya geri dönecektir.

## Adım 1: Aspose OCR'ı projenize ekleyin ve görüntüden metin tanıyın

İlk olarak, Aspose OCR JAR dosyasının sınıf yolunuzda (classpath) olduğundan emin olun. Maven kullanıyorsanız şunu ekleyin:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- check for the latest version -->
</dependency>
```

Kütüphane mevcut olduğunda bir `OcrEngine` örneği oluşturun. Bu nesne **görüntüden metin tanıma** işlemlerinin giriş noktasıdır.

```java
// Step 1: Create the OCR engine
OcrEngine ocrEngine = new OcrEngine();
```

Neden önce `OcrEngine` örneği oluşturuyoruz? Tüm tanıma ayarlarını (GPU bayrakları, dil paketleri vb.) içinde tutar ve her taramayı izole eder; böylece aynı motoru birden fazla görüntüde bellek sızıntısı olmadan yeniden kullanabilirsiniz.

## Adım 2: GPU hızlandırmasını etkinleştirin ve isteğe bağlı **GPU bellek sınırını ayarlayın**

GPU hızlandırması, büyük ölçekli OCR'ı mümkün kılan gizli sosdur. Aspose bunu tek bir çağrıyla açmanıza izin verir:

```java
// Step 2: Turn on GPU acceleration (requires a CUDA‑enabled GPU)
ocrEngine.getRecognitionSettings().setUseGpu(true);
```

GPU'nuz diğer iş yükleriyle paylaşılıyorsa, motorun ne kadar VRAM alabileceğini sınırlamak isteyebilirsiniz. İşte **GPU bellek sınırını ayarlama** burada devreye girer:

```java
// Optional: Limit the amount of GPU memory the engine may use (in MB)
ocrEngine.getRecognitionSettings().setGpuMemoryLimit(1024);
```

Bellek sınırı belirlemek, paralel olarak birçok yüksek çözünürlüklü görüntü işlenirken bellek taşması hatalarını önler. Değer megabayt cinsindendir, yani `1024` “en fazla 1 GB VRAM kullan” anlamına gelir.

> **Pro ipucu:** 4 GB bir kartta, 2 GB sınırı genellikle güvenli bir denge noktasıdır; GPU'nuzun boşta kaldığını fark ederseniz daha yüksek değerlerle deney yapabilirsiniz.

## Adım 3: **OCR için görüntüyü yükleyin** – motoru dosyanıza yönlendirin

Motor hazır olduğuna göre, hangi resmi tarayacağını ona söylememiz gerekir. Aspose bir dosya yolu, bir `java.io.File` ya da hatta bir `java.awt.image.BufferedImage` kabul eder. Basitlik açısından bir yol kullanacağız:

```java
// Step 3: Load the high‑resolution image to be processed
ocrEngine.setImage("YOUR_DIRECTORY/high_res_photo.jpg");
```

`YOUR_DIRECTORY/high_res_photo.jpg` ifadesini test görüntünüzün gerçek konumuyla değiştirin. Görüntü kaynak klasörünüzdeyse, `getClass().getResource("/images/sample.png").getPath()` kullanabilirsiniz.

Yükleme neden önemlidir? Motor, büyük ölçüde GPU‑bağlı bir ön‑işleme adımı (eğrilik düzeltme, ikilileştirme) gerçekleştirir. Temiz, yüksek çözünürlüklü bir dosya sağlamak GPU'nun verimli çalışmasını sağlar ve **görüntüden metin tanıma** doğruluğunu artırır.

## Adım 4: Tanıma işlemini çalıştırın ve elde edilen dizeyi alın

GPU etkinleştirildi ve görüntü yüklendiğinde, son çağrı oldukça basittir:

```java
// Step 4: Run the recognition and retrieve the extracted text
String extractedText = ocrEngine.recognize().getText();
```

`recognize()` yöntemi GPU bitene kadar bloklanır, ardından `getText()` düz bir `String` döndürür. Aspose, CUDA çekirdeklerinde çalışan bir derin öğrenme modeli kullandığından gecikme, yalnızca CPU‑tabanlı OCR'dan çok daha azdır.

## Adım 5: Sonucu çıktı olarak alın

OCR çıktısını konsola yazdıralım, böylece çalıştığını doğrulayabilirsiniz:

```java
// Step 5: Output the GPU‑accelerated OCR result
System.out.println("GPU‑accelerated result:\n" + extractedText);
```

Her şey doğru bağlandıysa, transkribe edilmiş metin anında görünecektir. Orta seviye bir RTX 2060'da, 3000 × 2000 px bir görüntü bir saniyeden kısa sürede işlenir.

![recognize text from image using GPU Aspose OCR](/images/gpu-ocr-demo.png "GPU‑accelerated OCR demo")

*Görsel alt metni:* **görüntüden metin tanıma** – GPU OCR sonrası konsol çıktısının ekran görüntüsü.

## Beklenen çıktı

Örnek bir fişi tam programla çalıştırdığınızda aşağıdakine benzer bir çıktı alırsınız:

```
GPU‑accelerated result:
Item      Qty   Price
Apple      2    $1.20
Banana     5    $0.75
Total          $3.75
```

Gerçek metniniz kaynak görüntüye bağlı olarak farklılık gösterecektir, ancak yukarıdaki format motorun satır sonlarını ve sayıları doğru şekilde çıkardığını gösterir.

## Yaygın hatalar ve pratik ipuçları

| Sorun | Neden oluşur | Çözüm |
|-------|----------------|---------------|
| **GPU algılanmadı** | CUDA sürücüsü eksik veya JAR sürümü uyumsuz | En son NVIDIA sürücüsünü kurun, `nvidia-smi` çalıştığını doğrulayın ve Aspose OCR 23.12 veya daha yenisini kullanın |
| **Bellek yetersiz hatası** | Görüntü, sınırlı VRAM için çok büyük | `setGpuMemoryLimit` değerini artırın veya görüntüyü yüklemeden önce ölçeklendirin |
| **Garip karakterler** | Görüntü bulanık veya düşük kontrastlı | `ocrEngine.getPreprocessingSettings().setBinarization(true)` ile ön‑işleme yapın |
| **İlk çalıştırmada yavaş performans** | GPU bağlamı başlatma gecikmesi | Gerçek iş yükünden önce küçük bir dummy görüntü işleyerek motoru ısıtın |

Unutmayın, **set gpu memory limit** isteğe bağlıdır ancak 

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}