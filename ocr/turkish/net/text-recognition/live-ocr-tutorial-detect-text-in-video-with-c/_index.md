---
category: general
date: 2026-03-13
description: Canlı OCR öğreticisi, OCR dilini nasıl ayarlayacağınızı ve Aspose.OCR
  kullanarak gerçek zamanlı olarak metin video akışlarını nasıl algılayacağınızı gösterir.
  Adım adım rehberi izleyin.
draft: false
keywords:
- live ocr tutorial
- set OCR language
- detect text video
- Aspose OCR live processing
- real‑time text detection
language: tr
og_description: Canlı OCR öğreticisi, Aspose.OCR Live'ı C#'ta kullanarak OCR dilini
  nasıl ayarlayacağınızı ve metin video akışlarını nasıl algılayacağınızı açıklar.
  Tam kod dahil.
og_title: 'Canlı OCR Eğitimi: Videoda Gerçek Zamanlı Metin Algılama'
tags:
- OCR
- C#
- Aspose
- Video Processing
title: 'Canlı OCR Eğitimi: C# ile Videoda Metin Algılama'
url: /tr/net/text-recognition/live-ocr-tutorial-detect-text-in-video-with-c/
---

same structure.

Let's assemble.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Canlı OCR Öğreticisi: Video'da Metin Algılama C# ile

Hiç **canlı OCR öğreticisi**'ne ihtiyaç duydunuz mu ve gerçekten bir video akışında çalışıyor mu? Belki akıllı‑kamera uygulaması ya da gerçek‑zamanlı çeviri katmanı geliştiriyorsunuz ve “her kareden metni nasıl alırım?” sorusunda takılı kaldınız. İyi haber şu ki, tekerleği yeniden icat etmenize gerek yok. Bu rehberde **OCR dilini ayarlayan**, bir kameradan kareler yakalayan ve **canlı video** akışında metin algılayan tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Düşük gecikmeli senaryolar için özel olarak tasarlanmış Aspose.OCR’nin `LiveOcr` sınıfını kullanacağız. Bu makalenin sonunda, gördüğü ilk metni ekrana yazdırıp ardından çıkan bir konsol uygulamanız olacak—daha karmaşık işlem hatları için mükemmel bir başlangıç noktası.

## Önkoşullar

- .NET 6.0 SDK (veya herhangi bir yeni .NET sürümü)  
- Visual Studio 2022 veya VS Code (favori IDE’niz)  
- NuGet paketi `Aspose.OCR` (`dotnet add package Aspose.OCR` komutuyla kurun)  
- Bir webcam ya da `Bitmap` kareleri sağlayabilen herhangi bir video kaynağı  

Ek native kütüphanelere gerek yok; Aspose.OCR ihtiyacınız olan her şeyi içinde barındırır.

## Adım 1: Aspose.OCR'yi Kurun ve Ad Alanlarını Ekleyin

Herhangi bir kod yazmadan önce Aspose OCR kütüphanesinin referanslandığından emin olun. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Ardından, `Program.cs` dosyanızın en üstüne, kullanacağımız ad alanlarını ekleyin:

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System.Drawing;
using System.Threading;
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, IDE sınıf adlarını yazdıktan sonra `using` ifadelerini otomatik olarak önerecektir.

## Adım 2: LiveOcr Örneğini Oluşturun ve Yapılandırın

Öğreticinin kalbi `LiveOcr` nesnesidir. Hangi dili arayacağını ona söylememiz ve isteğe bağlı olarak doğruluğu artırmak için ön işleme filtreleri (örneğin eğrilik düzeltme) uygulamamız gerekir.

```csharp
// Step 2: Initialize LiveOcr with English language and a deskew filter
LiveOcr liveOcr = new LiveOcr
{
    // This is where we **set OCR language** to English.
    Language = Language.English,

    // Pre‑processing helps when the camera isn’t perfectly aligned.
    PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
};
```

Dil ayarlamanın nedeni nedir? OCR motorları dil‑özel sözlükler ve karakter modelleri kullanır; İngilizce belirtmek yanlış pozitifleri azaltır ve tanıma hızını artırır. Başka bir dile ihtiyacınız varsa, sadece `Language.English` yerine `Language.Spanish`, `Language.French` vb. değiştirin.

## Adım 3: Kameranızdan Kareleri Yakalayın

Gerçek bir projede yer tutucu yöntem `CaptureFrameFromCamera()`'ı gerçek yakalama mantığıyla değiştirirsiniz—belki `AForge.Video`, `OpenCvSharp` ya da Windows Media Capture API'si kullanarak. Bu öğretici kapsamında yöntemi soyut tutacağız, ancak `AForge` kullanarak hızlı bir örnek göstereceğiz.

```csharp
// Simple wrapper that returns a Bitmap from the default webcam.
// You can replace this with any library that gives you a Bitmap.
static Bitmap CaptureFrameFromCamera()
{
    // NOTE: This is a minimal example. In production you should
    // manage the video source lifecycle and dispose objects properly.
    var videoSource = new AForge.Video.DirectShow.VideoCaptureDevice(
        new AForge.Video.DirectShow.FilterInfoCollection(
            AForge.Video.DirectShow.FilterCategory.VideoInputDevice)[0].MonikerString);

    Bitmap frame = null;
    var waitHandle = new AutoResetEvent(false);

    videoSource.NewFrame += (sender, eventArgs) =>
    {
        frame = (Bitmap)eventArgs.Frame.Clone();
        waitHandle.Set(); // signal that we have a frame
    };

    videoSource.Start();
    waitHandle.WaitOne(1000); // wait up to 1 second for a frame
    videoSource.SignalToStop();
    videoSource.WaitForStop();

    return frame;
}
```

> **Köşe durum:** Kamera mevcut değilse, `CaptureFrameFromCamera` `null` dönecektir. Üretim kodunda buna her zaman karşı koruma ekleyin.

## Adım 4: Metin Bulunana Kadar Her Kareyi İşleyin

Şimdi sabit bir kare sayısı (veya süresiz) üzerinden döngü kuruyor ve her bitmap'i `LiveOcr.ProcessFrame`'e gönderiyoruz. Boş olmayan bir dize aldığımız anda, onu ekrana yazdırıp döngüden çıkıyoruz.

```csharp
// Step 4: Scan up to 100 frames or until text appears
for (int frameIndex = 0; frameIndex < 100; frameIndex++)
{
    Bitmap cameraFrame = CaptureFrameFromCamera();

    // Guard against a failed capture
    if (cameraFrame == null)
    {
        Console.WriteLine("Failed to capture a frame. Retrying...");
        Thread.Sleep(100);
        continue;
    }

    // Run OCR on the current frame
    string recognizedText = liveOcr.ProcessFrame(cameraFrame);

    // If we detected something, show it and stop
    if (!string.IsNullOrEmpty(recognizedText))
    {
        Console.WriteLine($"Detected text: {recognizedText}");
        break;
    }

    // Small pause to avoid hammering the CPU
    Thread.Sleep(30);
}
```

### Neden bir duraklama?

`Thread.Sleep(30)` kamera sürücüsüne nefes aldırır ve CPU kullanımını azaltır. Yüksek performanslı senaryolarda bunu daha gelişmiş bir kare hızı kontrolörüyle değiştirebilirsiniz.

## Adım 5: Her Şeyi Bir Konsol Uygulamasına Sarın

Hepsini bir araya getirerek, işte tam, kopyala‑yapıştır‑hazır program. Yeni bir konsol projesi (`dotnet new console`) içinde `Program.cs` olarak kaydedin ve `dotnet run` komutunu çalıştırın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Live;
using System;
using System.Drawing;
using System.Threading;

// Optional: using AForge for demo capture (install AForge.Video via NuGet)
// using AForge.Video.DirectShow;

class Program
{
    static void Main()
    {
        // Initialize LiveOcr – **set OCR language** to English
        LiveOcr liveOcr = new LiveOcr
        {
            Language = Language.English,
            PreProcessingFilters = new FilterPipeline { new DeskewFilter() }
        };

        Console.WriteLine("Starting live OCR… Press Ctrl+C to abort.");

        // Loop through frames – **detect text video** in real time
        for (int i = 0; i < 100; i++)
        {
            Bitmap frame = CaptureFrameFromCamera();

            if (frame == null)
            {
                Console.WriteLine("No frame captured, retrying...");
                Thread.Sleep(100);
                continue;
            }

            string text = liveOcr.ProcessFrame(frame);

            if (!string.IsNullOrEmpty(text))
            {
                Console.WriteLine($"Detected text: {text}");
                break; // stop after first successful detection
            }

            Thread.Sleep(30); // throttle loop
        }

        Console.WriteLine("Live OCR session ended.");
    }

    // -----------------------------------------------------------------
    // Replace this stub with your own capture logic.
    // -----------------------------------------------------------------
    static Bitmap CaptureFrameFromCamera()
    {
        // Placeholder implementation – returns a solid‑color bitmap.
        // In a real app you would pull frames from a webcam or video file.
        Bitmap dummy = new Bitmap(640, 480);
        using (Graphics g = Graphics.FromImage(dummy))
        {
            g.Clear(Color.Black);
            g.DrawString(DateTime.Now.ToString("hh:mm:ss"), 
                new Font("Arial", 24), Brushes.White, new PointF(10, 10));
        }
        return dummy;
    }
}
```

### Beklenen çıktı

Kamera okunabilir İngilizce metin (örneğin, basılı bir etiket) gördüğünde, aşağıdakine benzer bir çıktı göreceksiniz:

```
Starting live OCR… Press Ctrl+C to abort.
Detected text: OpenAI
Live OCR session ended.
```

Eğer görüşte hiçbir şey yoksa, döngü 100 yinelemeden sonra sona erecek ve “Live OCR session ended.” mesajını yazdıracak. İterasyon sayısını artırabilir veya `for` döngüsünü `while (true)` ile değiştirerek sonsuz izlemeye geçebilirsiniz.

## Yaygın Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|----------|--------|
| **Birden fazla dili aynı anda işleyebilir miyim?** | Evet. Çok dilli bir sözlük etkinleştirmek için `Language = Language.English | Language.Spanish;` (bit düzeyinde OR) şeklinde ayarlayın. |
| **Karelerim büyükse ve OCR yavaş çalışıyorsa ne yapmalıyım?** | `ProcessFrame`'i çağırmadan önce bitmap'i küçültün. Örnek: `Bitmap small = new Bitmap(frame, new Size(320, 240));` |
| **Aspose.OCR için lisansa ihtiyacım var mı?** | 30 güne kadar geçerli bir geçici değerlendirme lisansı yeterlidir. Üretim için, filigranı kaldırmak amacıyla bir lisans satın alın. |
| **Döndürülmüş metni nasıl ele alırım?** | `DeskewFilter` zaten küçük dönüşleri düzeltir. Aşırı açılar için, pipeline'a bir `RotateFilter` ekleyin. |
| **Bu yaklaşım çoklu iş parçacığı (thread) güvenli mi?** | `LiveOcr` örnekleri thread‑safe değildir. Her iş parçacığı için bir tane oluşturun ya da erişimi bir lock ile koruyun. |

## Öğreticiyi Genişletmek

Artık bir **canlı OCR öğreticisi** temeline sahipsiniz, aşağıdaki adımları düşünün:

1. **Bir UI'ye akış** – `Windows Forms` veya `WPF` kullanarak OCR sonuçları üstüne bindirilmiş canlı videoyu gösterin.  
2. **Toplu işleme** – kareleri bir kuyruğa gönderin ve daha yüksek verimlilik için OCR'yi arka plan çalışan havuzunda çalıştırın.  
3. **Dil tespiti** – `LiveOcr.Language`'ı anlık olarak değiştirmek için bir dil tanıma kütüphanesi entegre edin.  
4. **Sonuçları kalıcı hale getirme** – algılanan dizeleri analiz için bir veritabanına ya da CSV dosyasına yazın.  

Bu uzantıların her biri, ele aldığımız temel kavramlara dayanır: `LiveOcr`'ı başlatmak, **OCR dilini ayarlamak** ve gerçek zamanlı **video karelerinde metin algılamak**.

---

### TL;DR

- NuGet üzerinden Aspose.OCR'yi kurun.  
- `LiveOcr` nesnesi oluşturun, **OCR dilini ayarlayın** (örnekte İngilizce).  
- Kameradan `Bitmap` kareleri yakalayın.  
- Kareler üzerinde döngü kurun, `ProcessFrame`'i çağırın ve metin belirdiğinde durun.  
- Yukarıdaki tam program çalıştırılmaya hazırdır ve herhangi bir gerçek‑zamanlı metin‑algılama projesi için sağlam bir temel oluşturur.

Deneyin, ön işleme pipeline'ını ayarlayın ve uygulamanızın dünyayı bir karede bir kez okuyarak nasıl çalıştığını izleyin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}