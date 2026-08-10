---
category: general
date: 2026-06-03
description: Aspose.OCR kullanarak MP4 gibi video dosyalarından kareler çıkarma ve
  metin okuma işlemini gösteren video altyazı OCR öğreticisi.
draft: false
keywords:
- video subtitle ocr
- extract frames from video
- read text from video
- extract text from mp4
language: tr
og_description: Aspose.OCR ile video altyazı OCR'ını öğrenin. Videodan kareler çıkarın,
  videodan metin okuyun ve birkaç dakika içinde MP4'ten metin çıkarın.
og_title: C# ile Video Altyazı OCR – Adım Adım Rehber
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  headline: Video Subtitle OCR in C# – Complete Guide
  type: TechArticle
- description: Video subtitle OCR tutorial showing how to extract frames from video
    and read text from video files like MP4 using Aspose.OCR.
  name: Video Subtitle OCR in C# – Complete Guide
  steps:
  - name: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
    text: Decodes an MP4 (or any supported format) into individual `Bitmap` frames.
  - name: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
    text: Limits the OCR region to the subtitle band so the engine isn’t distracted
      by the whole picture.
  - name: Processes each frame with Aspose’s `VideoOcrProcessor`.
    text: Processes each frame with Aspose’s `VideoOcrProcessor`.
  - name: Prints the recognized subtitle text to the console.
    text: Prints the recognized subtitle text to the console.
  type: HowTo
tags:
- C#
- Aspose.OCR
- video-processing
title: C#'ta Video Altyazı OCR – Tam Kılavuz
url: /tr/net/text-recognition/video-subtitle-ocr-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Video Altyazı OCR – Tam Kılavuz

Hiç **video subtitle ocr**'a ihtiyaç duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. İster ders kayıtlarını dijitalleştiriyor, ister eğitim videolarından altyazı çekiyor, ister sadece videodan metin okumaya meraklı olun, bu öğretici size C# ve Aspose.OCR ile tam olarak nasıl yapılacağını gösteriyor.  

Önümüzdeki birkaç dakikada videodan kareler çıkaracağız, bu karelerde OCR çalıştıracağız ve sonunda altyazı metnini kare‑kare görüntüleyeceğiz. Sonunda **videodan metin okuma** yeteneğine sahip olacaksınız—MP4 dahil—ve üçüncü‑taraf araçlar aramak zorunda kalmayacaksınız.

## Ne Oluşturacaksınız

Küçük bir konsol uygulaması yapacağız ve bu uygulama:

1. Bir MP4'ü (veya desteklenen herhangi bir formatı) tek tek `Bitmap` karelerine çözecek.  
2. OCR bölgesini altyazı bandına sınırlayacak, böylece motor bütün resimle meşgul olmayacak.  
3. Her kareyi Aspose'un `VideoOcrProcessor`'ı ile işleyecek.  
4. Tanınan altyazı metnini konsola yazdıracak.

Süsleme yok, sadece gerçek bir projeye ekleyebileceğiniz uçtan uca çalışan bir örnek.

## Önkoşullar

- **.NET 6.0** veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).  
- **Aspose.OCR for .NET** – NuGet üzerinden kurun: `Install-Package Aspose.OCR`.  
- Bir video dosyası (MP4 harika çalışır).  
- Video karelerini çözmek için bir yol – demo bir yer tutucu yöntem kullanıyor, ama `Bitmap` nesneleri döndüren herhangi bir kütüphane (FFmpeg, OpenCV vb.) ile değiştirebilirsiniz.  

> Pro ipucu: Windows'ta `System.Drawing.Common` paketi `Bitmap` için sorunsuz çalışır. Linux/macOS'ta ise yerel `libgdiplus` bağımlılığına ihtiyacınız olacak.

## Adım 1 – Videodan Kareleri Çıkarma

İlk engel, hareketli bir resmi sabit görüntülere dönüştürmek. Aşağıdaki `GetVideoFrames` yöntemi kasıtlı olarak boş bırakıldı; favori çözücünüzle değiştirin. İşte verinin şeklini göstermek için FFmpeg‑Core kullanan hızlı bir taslak:

```csharp
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

/// <summary>
/// Extracts every frame from the supplied video file and yields it as a Bitmap.
/// You can swap this implementation for OpenCV, MediaToolkit, etc.
/// </summary>
static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
{
    // Create a temporary folder for the extracted PNGs
    string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
    Directory.CreateDirectory(tempDir);

    // FFmpeg command: -i input -vf fps=1 output_%04d.png (1 fps for demo)
    var startInfo = new ProcessStartInfo
    {
        FileName = "ffmpeg",
        Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
        RedirectStandardOutput = true,
        UseShellExecute = false,
        CreateNoWindow = true
    };
    Process ffmpeg = Process.Start(startInfo);
    ffmpeg.WaitForExit();

    foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
    {
        using var bmp = new Bitmap(file);
        // Clone the bitmap so the file can be deleted later
        yield return new Bitmap(bmp);
    }

    // Clean up
    Directory.Delete(tempDir, true);
}
```

> **Neden önemli:** Kareleri çıkarmak OCR motoruna statik bir görüntü verir, bu da doğrudan video akışından okumaya göre doğruluğu büyük ölçüde artırır.

## Adım 2 – VideoOcrProcessor'ı Ayarlama

Artık bir `Bitmap` dizimiz olduğuna göre, bunları Aspose.OCR'a verebiliriz. `VideoOcrProcessor`, **İlgi Bölgesi (ROI)** tanımlamamıza izin verir – genellikle çerçevenin üst ya da alt kısmında bulunan altyazılar için mükemmeldir.

```csharp
using Aspose.OCR.Video;
using System.Drawing;

// Create the processor and focus on the top 200 pixels (typical subtitle band)
var ocrProcessor = new VideoOcrProcessor
{
    // ROI = new Rectangle(x, y, width, height)
    Roi = new Rectangle(0, 0, 1920, 200)   // adjust width/height to your video resolution
};
```

> **ROI'yi sınırlamanın nedeni:** Resmin geri kalanını görmezden gelerek gürültüyü azaltır, işleme süresini kısaltır ve arka plan grafiklerinden kaynaklanan yanlış pozitifleri önler.

## Adım 3 – Kare Dizisi Üzerinde OCR Çalıştırma

İşlemci hazır olduğunda, kareleri beslemek tek satır kodla yapılır. `Process` metodu, her kareye karşılık gelen tanınan metni içeren `OcrResult` nesnelerinin bir enumerable'ını döndürür.

```csharp
IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

// Execute OCR on every extracted frame
IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);
```

> **Arka planda neler oluyor?** Aspose.OCR, her bitmap'i normalleştirir, sinir‑ağ‑tabanlı bir tanıyıcı çalıştırır ve ardından noktalama ve satır sonlarını iyileştirmek için çıktıyı post‑process eder.

## Adım 4 – Çıkarılan Metni Görüntüleme

Son olarak sonuçlar üzerinde döngü kurup her altyazı satırını yazdırıyoruz. Ayrıca bunları bir SRT dosyasına, veritabanına kaydedebilir ya da bir çeviri servisine gönderebilirsiniz.

```csharp
int frameIndex = 0;
foreach (var result in ocrResults)
{
    // result.Text contains the plain‑text subtitle for this frame
    Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
}
```

### Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde bağımsız bir konsol programı elde ederiz:

```csharp
using Aspose.OCR.Video;
using System;
using System.Collections.Generic;
using System.Drawing;
using System.Diagnostics;
using System.IO;

class VideoSubtitleOcrDemo
{
    static void Main()
    {
        // 1️⃣ Extract frames from the MP4 (replace with your own decoder)
        IEnumerable<Bitmap> videoFrames = GetVideoFrames(@"C:\Videos\lecture.mp4");

        // 2️⃣ Configure OCR – focus on the subtitle band
        var ocrProcessor = new VideoOcrProcessor
        {
            Roi = new Rectangle(0, 0, 1920, 200) // tweak for your video size
        };

        // 3️⃣ Run OCR across all frames
        IEnumerable<OcrResult> ocrResults = ocrProcessor.Process(videoFrames);

        // 4️⃣ Output the recognized subtitle text
        int frameIndex = 0;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"Frame {frameIndex++}: {result.Text}");
        }
    }

    // --------------------------------------------------------------------
    // Helper: extract one‑frame‑per‑second PNGs using FFmpeg.
    // Replace this with any library that can return Bitmap objects.
    // --------------------------------------------------------------------
    static IEnumerable<Bitmap> GetVideoFrames(string videoPath)
    {
        string tempDir = Path.Combine(Path.GetTempPath(), Guid.NewGuid().ToString());
        Directory.CreateDirectory(tempDir);

        var startInfo = new ProcessStartInfo
        {
            FileName = "ffmpeg",
            Arguments = $"-i \"{videoPath}\" -vf fps=1 \"{tempDir}\\frame_%04d.png\" -hide_banner -loglevel error",
            RedirectStandardOutput = true,
            UseShellExecute = false,
            CreateNoWindow = true
        };
        using var ffmpeg = Process.Start(startInfo);
        ffmpeg.WaitForExit();

        foreach (var file in Directory.GetFiles(tempDir, "frame_*.png"))
        {
            using var bmp = new Bitmap(file);
            yield return new Bitmap(bmp);
        }

        Directory.Delete(tempDir, true);
    }
}
```

**Beklenen çıktı (örnek)**  

```
Frame 0: Welcome to the Introduction to Machine Learning.
Frame 1: In this lecture we will cover...
Frame 2: ...
```

Eğer OCR belirli bir karede zorlanırsa boş bir string göreceksiniz – bu, ROI'yi ayarlamanız ya da kare çıkarma oranını artırmanız gerektiğine işaret eder.

## Yaygın Tuzaklar ve Çözümleri

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **Bozuk karakterler** | Düşük çözünürlüklü kareler veya yüksek sıkıştırma | Kareleri daha yüksek bitrate ile çıkarın, ya da OCR'dan önce bitmap'i upscale edin (`Bitmap.Clone(new Size(...), ...)`). |
| **Metin dönmüyor** | ROI aslında altyazı bandını kapsamıyor | Dikdörtgen koordinatlarını doğrulayın (ekran görüntüsü aracıyla ölçüm yapın). |
| **Performans darboğazı** | 30 fps'de her kareyi işlemek gereksiz | Çoğu altyazı akışı için 1‑2 fps'e down‑sample edin; yine de her altyazı değişimini yakalayabilirsiniz. |
| **FFmpeg bulunamadı** | `ffmpeg.exe` `PATH` içinde yok | `ProcessStartInfo.FileName` içinde tam yolu belirtin ya da FFmpeg'i global olarak kurun. |

## Çözümü Genişletmek

- **SRT'ye Dışa Aktarma** – zaman damgalarını OCR metniyle birleştirip SubRip dosyası yazın.  
- **Çok‑dilli destek** – `ocrProcessor.Language = OcrLanguage.Spanish` (veya desteklenen başka bir dil) ayarlayın.  
- **Gerçek‑zaman işleme** – diskten okumak yerine canlı akıştan kareleri doğrudan boru hattına yönlendirin.  

Tüm bu varyasyonlar hâlâ **videodan kare çıkarma**, **videodan metin okuma** ve **mp4'ten metin çıkarma** temel fikirleri etrafında döner.

## Sonuç

C# içinde tam bir **video subtitle ocr** iş akışını adım adım inceledik. Videodan kare çıkararak, OCR'ı altyazı bandına odaklayarak ve sonuçları yineleyerek MP4 gibi video dosyalarından güvenilir bir şekilde **metin okuyabilirsiniz**. Kod kopyala‑yapıştır için hazır ve modüler tasarımı sayesinde istediğiniz herhangi bir kare çözücüyü takas edebilirsiniz.

Sonraki adımlar? Sonuçları bir SRT dosyasına dışa aktarın, farklı ROI boyutlarıyla deney yapın ya da altyazıları çok‑dilli altyazılar için bir çeviri API'sine besleyin. Temel metin çıkarma becerilerini kavradıktan sonra sınır yok.

İyi kodlamalar, altyazılarınız her zaman kristal netliğinde olsun!

## Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanan ve yakından ilgili konuları kapsar. Her kaynak, adım adım açıklamalarla tam çalışan kod örnekleri içerir ve API özelliklerini daha iyi kavramanızı ve projelerinizde alternatif uygulama yaklaşımları keşfetmenizi sağlar.

- [Extract image text C# with language selection using Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)
- [Extract Text from Image Using Aspose.OCR .NET](/ocr/english/net/image-and-drawing-recognition/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}