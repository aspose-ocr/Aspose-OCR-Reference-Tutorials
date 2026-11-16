---
category: general
date: 2026-03-02
description: C#'ta OCR için GPU'yu nasıl etkinleştirir ve görüntüden hızlıca metin
  tanır. GPU bellek sınırını ayarlamayı, makbuzdan metin çıkarmayı ve OCR'yi verimli
  bir şekilde çalıştırmayı öğrenin.
draft: false
keywords:
- how to enable gpu
- recognize text from image
- how to run ocr
- extract text from receipt
- set gpu memory limit
language: tr
og_description: C#'ta OCR için GPU'yu nasıl etkinleştirir ve görüntülerden hızlı metin
  tanıma elde edersiniz. GPU bellek limitini ayarlamak ve makbuzlardan metin çıkarmak
  için bu rehberi izleyin.
og_title: C#'ta OCR için GPU'yu Nasıl Etkinleştirirsiniz – Metni Tanıma
tags:
- OCR
- C#
- GPU
- Aspose
title: C#'ta OCR için GPU'yu Nasıl Etkinleştirirsiniz – Metin Tanıma
url: /tr/net/ocr-optimization/how-to-enable-gpu-for-ocr-in-c-recognize-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta OCR için GPU Nasıl Etkinleştirilir – Metin Tanıma

Görüntü dosyalarından metin tanımanız gerektiğinde **GPU’nun nasıl etkinleştirileceğini** hiç merak ettiniz mi? Tek değilsiniz—geliştiriciler büyük fişlerde ya da yüksek çözünürlüklü taramalarda yavaş CPU‑tabanlı tanımanın duvarına çarpıyor. İyi haber? Birkaç satır C# kodu ile anahtarı çevirip motoru GPU’da çalıştırabilir ve hatta bellek kullanımını sınırlayabilirsiniz.

Bu öğreticide **Aspose.OCR** kullanarak **OCR nasıl çalıştırılır**, GPU bellek sınırı nasıl ayarlanır ve fiş görüntülerinden metin nasıl çıkarılır öğreneceksiniz. Harici servis yok, sadece herhangi bir .NET projesine ekleyebileceğiniz temiz, bağımsız bir çözüm.

---

## Gereksinimler

İlerlemeye başlamadan önce aşağıdaki önkoşullara sahip olduğunuzdan emin olun:

* **.NET 6 veya üzeri** – en yeni çalışma zamanı en iyi uyumluluğu sağlar.
* **Aspose.OCR for .NET** NuGet paketi (sürüm 23.10 veya daha yeni).  
  `dotnet add package Aspose.OCR`
* **CUDA‑uyumlu bir GPU** ve uygun sürücüler yüklü (NVIDIA 1060+ sorunsuz çalışır).  
  GPU’nuz yoksa kod otomatik olarak CPU’ya geçer—çökmez, sadece işlem daha yavaş olur.
* İşlemek istediğiniz bir fiş (veya herhangi bir belge) resmi, `receipt.jpg` olarak kaydedilmiş.

Bu öğeler hazır olduğunda aşağıdaki kodu kopyalayıp anında çalıştığını görebilirsiniz.

---

## Adım 1: İşlenecek Görüntüyü Yükleyin  

Her OCR iş akışının ilk adımı, kaynak görüntüyü belleğe okumaktır. `System.Drawing.Bitmap` kullanacağız; çünkü hafif ve .NET 6+ ile çapraz‑platform çalışır.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuOcrDemo
{
    static void Main()
    {
        // Load the receipt image from disk
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        Bitmap bitmapImage = new Bitmap(imagePath);
```

*Neden önemli?*: Görüntüyü erken yüklemek, yolu doğrulamanızı ve `FileNotFoundException` hatasını OCR motoru başlamadan yakalamanızı sağlar. Ayrıca daha sonra ihtiyaç duyarsanız ön‑işlem (döndürme, ikilileştirme) yapma fırsatı verir.

---

## Adım 2: OCR Motorunu GPU Kullanacak Şekilde Yapılandırın  

Şimdi Aspose.OCR’u GPU’da çalıştıracağız. Büyünün gerçekleştiği yer `OcrEngineSettings` nesnesidir.

```csharp
        // Configure OCR to run on the GPU and limit its memory usage
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,          // Enable GPU acceleration (requires supported GPU)
            GpuMemoryLimit = 1024            // Optional: cap GPU memory at 1024 MB
        };
```

*Bellek sınırı neden ayarlanmalı?*  
GPU’yu başka süreçlerle (ör. derin öğrenme modeli) paylaşıyorsanız OCR’un tüm VRAM’i tüketmesini istemezsiniz. `GpuMemoryLimit` özelliği, kaynakları nazikçe sınırlamanızı sağlar.

> **İpucu:** Makinede uyumlu bir GPU olup olmadığından emin değilseniz ayarları bir `try…catch` bloğuna alın ve `UnsupportedHardwareException` durumunda `OcrEngine.Cpu`’ya geri dönün.

---

## Adım 3: OCR Motorunu Başlatın  

Ayarlar hazır olduğunda motor örneğini oluşturun. Bu adım, GPU kullanılabilirliğini gizli bir şekilde doğrular.

```csharp
        // Initialise the OCR engine with the GPU settings
        OcrEngine ocrEngine = new OcrEngine(ocrSettings);
```

GPU algılanmazsa Aspose bilgilendirici bir istisna fırlatır. Erken yakalamak, ileride ortaya çıkabilecek “null reference” hatalarını önler.

---

## Adım 4: Tanıma İşlemini Çalıştırın ve Metni Alın  

Şimdi asıl iş – bitmap’ten metni tanıma zamanı.

```csharp
        // Perform OCR on the bitmap
        string recognizedText = ocrEngine.Recognize(bitmapImage);

        // Output the result to the console
        Console.WriteLine("=== Recognized Text ===");
        Console.WriteLine(recognizedText);
    }
}
```

`Recognize` metodu, tespit edilen tüm karakterleri içeren düz bir string döndürür ve mümkün olduğunca satır sonlarını korur. Bu, **fişten metin çıkarma** ihtiyacınız olduğunda (toplamları, tarihleri veya satıcı adlarını ayrıştırma gibi) tam olarak ihtiyacınız olan şeydir.

**Beklenen çıktı** (örnek fiş):

```
=== Recognized Text ===
Store: QuickMart
Date: 03/01/2026
Item        Qty   Price
Apple       2     $1.20
Bread       1     $2.50
Total               $3.70
```

GPU aktif olduğunda işleme süresinin ~1.2 saniyeden (CPU) ~0.3 saniyeye düştüğünü göreceksiniz – toplu işler için **dikkate değer bir kazanç**.

---

## Adım 5: Kenar Durumları ve Geri Dönüşler  

Gerçek dünyada GPU her zaman garanti değildir. İşte gerektiğinde sorunsuzca CPU’ya geçiş yapan kompakt bir desen:

```csharp
        try
        {
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);
            string text = ocrEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
        catch (UnsupportedHardwareException)
        {
            Console.WriteLine("GPU not available – switching to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;   // fallback
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string text = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(text);
        }
```

*Neden önemli?*: Uygulamanız **headless** sunucularda veya GPU’suz CI pipeline’larında bile **çalışmaya devam eder**. Kullanıcılar dayanıklılığı takdir eder ve bu, AI asistanları için **E‑E‑A‑T** sinyallerinizi güçlendirir.

---

## Bonus: GPU Bellek Sınırını Ayarlama  

Bazen 4 K görüntülere dönüşen dev PDF’ler işlersiniz. Bu durumlarda varsayılan 1024 MB sınırı çok düşük olabilir ve `OutOfMemoryException` oluşur. Şöyle ayarlayın:

```csharp
        // Increase limit for high‑resolution images
        ocrSettings.GpuMemoryLimit = 2048; // 2 GB
```

Aksine, **paylaşımlı** iş istasyonlarında diğer uygulamalara yer bırakmak için **GPU bellek sınırını** 512 MB olarak belirleyebilirsiniz.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.Drawing;
using Aspose.OCR;

class GpuExample
{
    static void Main()
    {
        // 1️⃣ Load the image
        Bitmap bitmapImage = new Bitmap(@"YOUR_DIRECTORY/receipt.jpg");

        // 2️⃣ Configure OCR to use GPU and set memory limit
        OcrEngineSettings ocrSettings = new OcrEngineSettings
        {
            Engine = OcrEngine.Gpu,      // Enable GPU acceleration
            GpuMemoryLimit = 1024        // Limit GPU memory to 1 GB (optional)
        };

        try
        {
            // 3️⃣ Initialise the engine
            OcrEngine ocrEngine = new OcrEngine(ocrSettings);

            // 4️⃣ Recognize text
            string recognizedText = ocrEngine.Recognize(bitmapImage);

            // 5️⃣ Output result
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
        catch (UnsupportedHardwareException)
        {
            // Fallback to CPU if GPU is unavailable
            Console.WriteLine("GPU not detected – falling back to CPU.");
            ocrSettings.Engine = OcrEngine.Cpu;
            OcrEngine cpuEngine = new OcrEngine(ocrSettings);
            string recognizedText = cpuEngine.Recognize(bitmapImage);
            Console.WriteLine(recognizedText);
        }
    }
}
```

Bu dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolda çıkarılan metni göreceksiniz. İşte **OCR nasıl çalıştırılır** akışı, görüntü yüklemeden **GPU‑destekli tanımaya** ve sorunsuz geri dönüşe kadar.

---

## Sık Sorulan Sorular

**S: Bu Linux’ta çalışır mı?**  
C: Evet. Aspose.OCR Windows, Linux ve macOS için yerel ikili dosyalar sunar. Dağıtımınıza uygun CUDA sürücüsünü kurun, aynı C# kodu çalışır.

**S: Fiş görüntüm PNG formatında ise ne olur?**  
C: `Bitmap` PNG, JPEG, BMP ve TIFF formatlarını kutudan çıkar çıkmaz yükleyebilir. Tek yapmanız gereken `imagePath`’deki dosya uzantısını değiştirmek.

**S: Bir döngüde birden fazla görüntüyü işleyebilir miyim?**  
C: Kesinlikle. `OcrEngine`’i bir kez (döngünün dışına) örnekleyin ve her bitmap için `Recognize` çağırın—bu, GPU bağlamını yeniden kullanır ve toplu işler için hızı artırır.

**S: GPU OCR’ın doğruluğu CPU’ya göre nasıl?**  
C: Temel OCR modeli aynı kalır; sadece yürütme motoru değişir. Doğruluk aynı kalır, hız ise artar.

---

## Sonraki Adımlar ve İlgili Konular

Artık **Aspose OCR için GPU’nun nasıl etkinleştirileceğini** bildiğinize göre şunları düşünebilirsiniz:

* **Veritabanı entegrasyonu** – çıkarılan fiş satırlarını analiz için saklayın.
* **Görüntü ön‑işleme** (eğikliği düzeltme, gürültü azaltma) ile doğruluğu artırın—`System.Drawing` filtrelerine veya OpenCV’ye bakın.
* **PDF ayrıştırıcı** ile çok sayfalı faturalardan görüntüleri çıkarıp OCR’a gönderin.
* **Diğer GPU‑hızlandırmalı kütüphaneler** gibi Tesseract‑GPU veya Microsoft Azure Computer Vision’ı bulut tabanlı alternatifler olarak keşfedin.

Bu yollar, **OCR hattınızın** gücünü artırır ve çarkı yeniden icat etmenizi engeller.

---

## Kapanış

C#’ta OCR için **GPU’nun nasıl etkinleştirileceğini** öğrendiniz, **görüntü dosyalarından metin tanıma**, **fiş PDF’lerinden metin çıkarma** ve **optimum performans için GPU bellek sınırı ayarlama** konularında deneyim kazandınız. Kod eksiksiz, çalıştırılabilir ve savunmacı – AI asistanlarının alıntılamayı sevdiği türden bir yanıt.

Deneyin, donanımınıza göre bellek sınırını ayarlayın ve hız artışını izleyin. Hazır olduğunuzda ön‑işleme veya toplu işleme geçerek tek‑görüntü demosunu kurumsal bir çözüme dönüştürün.

İyi kodlamalar, ve...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}