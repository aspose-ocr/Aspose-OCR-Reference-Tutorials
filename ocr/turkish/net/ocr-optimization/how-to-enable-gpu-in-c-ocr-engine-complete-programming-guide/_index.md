---
category: general
date: 2026-06-06
description: C# OCR motorunda GPU'yu nasıl etkinleştirir ve görüntüden metni hızlıca
  tanırsınız. OCR nasıl yapılır, OCR için görüntü nasıl yüklenir ve OCR motoru C#
  dakikalar içinde nasıl kullanılır öğrenin.
draft: false
keywords:
- how to enable gpu
- how to perform ocr
- recognize text from image
- load image for ocr
- use ocr engine c#
language: tr
og_description: C# OCR motorunda GPU'yu nasıl etkinleştirirsiniz. Bu öğreticide OCR
  nasıl yapılır, OCR için görüntü nasıl yüklenir ve OCR motoru C# kullanarak görüntüden
  metin nasıl tanınır gösterilmektedir.
og_title: C# OCR Motorunda GPU'yu Etkinleştirme – Adım Adım Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to enable GPU in a C# OCR engine and quickly recognize text from
    image. Learn how to perform OCR, load image for OCR, and use OCR engine C# in
    minutes.
  headline: How to Enable GPU in C# OCR Engine – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- C#
- GPU
title: C# OCR Motorunda GPU'yu Etkinleştirme – Tam Programlama Rehberi
url: /tr/net/ocr-optimization/how-to-enable-gpu-in-c-ocr-engine-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# OCR Motorunda GPU'yu Etkinleştirme – Tam Programlama Rehberi

C# içinde bir OCR iş yükü çalıştırırken **GPU'yu nasıl etkinleştirirsiniz** diye hiç merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler yüksek çözünürlüklü taramalarla özellikle yavaş CPU‑only işleme duvarına çarpıyorlar.  

İyi haber? GPU hızlandırmasını açmak çocuk oyuncağı ve bir kez çalışır hale geldiğinde **OCR gerçekleştirebilir**, **OCR için görüntü yükleyebilir** ve **görüntüden metin tanıyabilirsiniz** anında. Bu rehberde, doğru paketleri kurmaktan son metni yazdırmaya kadar her adımı, kodu temiz ve çalıştırılabilir tutarak anlatacağız.

Ayrıca birkaç “ya böyle olursa” senaryosuna da değineceğiz: Birden fazla GPU'nuz varsa ne olur? Görüntü formatı desteklenmiyorsa ne olur? Sonunda **GPU'yu nasıl etkinleştirirsiniz** ve güvenebileceğiniz sonuçları alırsınız gösteren sağlam, üretim‑hazır bir kod parçasına sahip olacaksınız.

## Önkoşullar

- .NET 6.0 veya daha yeni (örnek, kısalık için üst‑seviye ifadeler kullanıyor)
- GPU'yu destekleyen bir OCR kütüphanesi (ör. *MyOcrLib* – kendi sağlayıcınızın ad alanıyla değiştirin)
- En az bir CUDA‑uyumlu GPU ve yüklü sürücüler
- Referans alabileceğiniz bir örnek görüntü (JPEG/PNG) bir klasörde

Eğer bunlardan birini kaçırdıysanız, en son NVIDIA sürücüsünü indirin ve NuGet paketini ekleyin:

```bash
dotnet add package MyOcrLib --version 2.3.1
```

Şimdi, derinlemesine inceleyelim.

## Adım 1: C# OCR Motorunuzda GPU'yu Nasıl Etkinleştirirsiniz

İlk yapmanız gereken, motorun yapılandırma nesnesindeki GPU anahtarını açmak. Çoğu modern OCR SDK'sı, `GpuEnabled`, `GpuDeviceId` ve isteğe bağlı olarak ekstra hız elde etmek için hassasiyet modunu ayarlayabileceğiniz bir `Config` özelliği sunar.

```csharp
// Create the OCR engine instance
var ocrEngine = new MyOcrLib.OcrEngine();

// Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;                     // Turn on GPU mode
ocrEngine.Config.GpuDeviceId = 0;                       // Choose the first GPU (0‑based index)
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16; // Optional: lower precision for less memory usage
```

**Neden önemli:** GPU hızlandırması ağır matris hesaplamalarını CPU'dan alıp grafik işlemciye taşır, binlerce pikseli paralel olarak işleyebilir. Orta seviye bir RTX 3060'da CPU‑only moda kıyasla 3‑5× hız artışı görebilirsiniz.

> **Pro ipucu:** Birden fazla GPU'nuz varsa, yükü kartlar arasında dengelemek için `GpuDeviceId = 1` (veya daha yüksek) ile deney yapın.

## Adım 2: C#'ta OCR İçin Görüntü Yükleme

Motor bir şey okuyabilmesi için ona bir görüntü akışı vermeniz gerekir. SDK genellikle `ImageStream.FromFile` gibi bir yardımcı sunar. Yolun doğru ve dosyanın erişilebilir olduğundan emin olun.

```csharp
// Load the image you want to process
ocrEngine.Image = MyOcrLib.ImageStream.FromFile(@"C:\OCRSamples\sample1.jpg");

// Quick sanity check – ensure the image was loaded
if (ocrEngine.Image == null)
{
    Console.WriteLine("Failed to load image. Check the file path and format.");
    return;
}
```

**Köşe durumu:** Bazı kütüphaneler CMYK JPEG'lerde takılır. Bir istisna alırsanız, önce `System.Drawing` ya da `ImageSharp` kullanarak görüntüyü RGB'ye dönüştürün.

## Adım 3: Dil Ayarlama ve OCR Gerçekleştirme

Çoğu OCR motoru hangi dil modelinin kullanılacağını bilmek zorundadır. İngilizce birçok pakette varsayılan olsa da, tek bir enum değişikliğiyle Fransızca, İspanyolca vb. diller seçilebilir.

```csharp
// Choose the language for recognition
ocrEngine.Language = OcrLanguage.English; // Change to OcrLanguage.Spanish for Spanish text
```

Şimdi tanıma hattını çalıştırıyoruz. İşte **OCR nasıl yapılır** sorusunun somut bir çağrıya dönüşmesi.

```csharp
// Run the OCR process – this will automatically use the GPU because we enabled it earlier
var ocrResult = ocrEngine.Recognize();
```

Çağrı `null` dönerse ya da bir istisna fırlatırsa, GPU sürücülerinin güncel olduğundan ve model dosyalarının beklenen dizinde bulunduğundan iki kez kontrol edin.

## Adım 4: Görüntüden Metin Tanıma ve Sonucu Çıktı Alma

`Recognize` metodu genellikle bir `Text` özelliği ve her satır için güven skorları içeren bir nesne döndürür. Düz metni konsola yazdıralım.

```csharp
// Output the recognized text
if (ocrResult?.Text != null)
{
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("OCR failed to produce any text.");
}
```

**Gördükleriniz:** Temiz bir taranmış sayfa için çıktı neredeyse kusursuz olmalı. Karakter bozulması fark ederseniz, görüntü DPI'sını (300 dpi ideal bir nokta) artırmayı ya da daha yüksek doğruluk için `GpuPrecision`'ı `Float32`'ye geri döndürmeyi düşünün.

### Beklenen Konsol Çıktısı (örnek)

```
=== OCR Output ===
The quick brown fox jumps over the lazy dog.
```

## Adım 5: Yaygın Tuzaklar & Performans İpuçları

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| **GPU kullanılmıyor** (CPU kullanımı yükseliyor) | `GpuEnabled` `false` bırakıldı veya sürücü eksik | `ocrEngine.Config.GpuEnabled`'in `true` olduğundan emin olun ve `nvidia-smi` ile süreci kontrol edin |
| **Bellek yetersiz hatası** | Çok büyük bir görüntüde `Float16` kullanmak | `GpuPrecision.Float32`'ye geçin veya görüntüyü beslemeden önce küçültün |
| **Düşük doğruluk** | Yanlış dil modeli veya düşük DPI | `ocrEngine.Language`'i doğru ayarlayın ve görüntünün ≥300 dpi olduğundan emin olun |
| **Çok sayfalı PDF'lerde çökme** | Motor tek bir görüntü bekliyor | Her sayfa için bir `ImageStream` oluşturarak döngüye alın |

**Ek ipucu:** UI'nizin yanıt vermesini istiyorsanız OCR çağrısını bir `Task.Run` içinde sarın. GPU işi ayrı bir iş parçacığında çalışır, ancak .NET iş parçacığı havuzu yine de engellenir; bu yüzden dışarıya aktarın.

```csharp
var ocrResult = await Task.Run(() => ocrEngine.Recognize());
```

## Adım 6: Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, bir konsol uygulamasına bırakabileceğiniz, `using` yönergeleri, hata yönetimi ve pencere kapanmadan önce çıktıyı görebilmeniz için `Console.ReadKey()` içeren bütünleşik bir program bulunuyor.

```csharp
using System;
using MyOcrLib;               // Replace with the actual namespace of your OCR library
using MyOcrLib.Enums;        // For GpuPrecision and OcrLanguage

// ------------------------------------------------------------
// How to Enable GPU, Load Image, Perform OCR, and Get Text
// ------------------------------------------------------------
var ocrEngine = new OcrEngine();

// 1️⃣ Enable GPU acceleration
ocrEngine.Config.GpuEnabled = true;
ocrEngine.Config.GpuDeviceId = 0;                 // First GPU
ocrEngine.Config.GpuPrecision = GpuPrecision.Float16;

// 2️⃣ Load the image for OCR
string imagePath = @"C:\OCRSamples\sample1.jpg";
ocrEngine.Image = ImageStream.FromFile(imagePath);

if (ocrEngine.Image == null)
{
    Console.WriteLine("❌ Unable to load image. Check the path.");
    return;
}

// 3️⃣ Set language (how to perform OCR)
ocrEngine.Language = OcrLanguage.English;

// 4️⃣ Run OCR – this uses the GPU because we enabled it
var ocrResult = ocrEngine.Recognize();

if (ocrResult?.Text != null)
{
    Console.WriteLine("\n=== Recognized Text ===");
    Console.WriteLine(ocrResult.Text);
}
else
{
    Console.WriteLine("\n⚠️ OCR returned no text.");
}

// Keep console open
Console.WriteLine("\nPress any key to exit...");
Console.ReadKey();
```

Programı `dotnet run` ile çalıştırın; çıkarılan metnin konsola yazdırıldığını görmelisiniz. `imagePath`'i farklı bir dosyayla değiştirirseniz aynı hat hattı çalışır—sadece gerekirse dili ayarlamayı unutmayın.

## Sonuç

**GPU'yu nasıl etkinleştirirsiniz** konusunda C# OCR motorunda neler yapmanız gerektiğini, **OCR için görüntü nasıl yüklenir**, **OCR nasıl gerçekleştirilir** ve `OCR engine C#` API'sı ile **görüntüden metin nasıl tanınır** konularını adım adım gösterdik. Sondaki tam örnek her şeyi bir araya getiriyor, böylece kopyalayıp yapıştırarak GPU'nun metin çıkarımınızı anında hızlandırmasını izleyebilirsiniz.

Bir sonraki seviyeye hazır mısınız? Bir `Parallel.ForEach` döngüsüyle bir grup görüntüyü işleyin, farklı `GpuPrecision` ayarlarıyla deney yapın ya da çok dilli bir modele geçerek uygulamanızın yeteneklerini genişletin.  

Herhangi bir sorunla karşılaşırsanız ya da geliştirme fikirleriniz varsa yorum bırakın—mutlu kodlamalar!  

![GPU etkinleştirilmiş OCR boru hattını gösteren diyagram – nasıl gpu etkinleştirilir](/images/ocr-gpu-setup.png "Diagram showing GPU‑enabled OCR pipeline – how to enable gpu")

---


## Sonra Ne Öğrenmelisiniz?


Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayalı olarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini ustalaşmanız ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmeniz için adım adım açıklamalarla tam çalışan kod örnekleri içerir.

- [How to OCR Image – Perform OCR on Image in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [How to Use Aspose to Recognize Image from Stream in OCR Image Recognition](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to Set Threshold Value in OCR Image Recognition](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}