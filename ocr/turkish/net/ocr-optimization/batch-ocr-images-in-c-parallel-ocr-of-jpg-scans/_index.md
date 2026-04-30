---
category: general
date: 2026-04-29
description: Aspose OCR'i C# ile kullanarak görüntüleri hızlı bir şekilde toplu OCR'leyin.
  JPG dosyalarından metin çıkarmayı, taramalardan metin okumayı ve görüntü listesini
  paralel olarak işlemeyi öğrenin.
draft: false
keywords:
- batch OCR images
- extract text from jpg
- read text from scans
- parallel OCR processing
- process image list
language: tr
og_description: Aspose OCR ile görüntüleri hızlıca toplu OCR yapın. Bu kılavuz, jpg
  dosyalarından metin çıkarmayı, taramalardan metin okumayı ve bir görüntü listesini
  paralel olarak işlemeyi gösterir.
og_title: C# ile Toplu OCR Görüntüleri – JPG Taramalarının Paralel OCR'ı
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#'ta Toplu OCR Görüntüleri – JPG Taramalarının Paralel OCR'ı
url: /tr/net/ocr-optimization/batch-ocr-images-in-c-parallel-ocr-of-jpg-scans/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Görüntüleri – JPG Taramalarının Paralel OCR'u

Ever needed to **batch OCR images** but weren’t sure how to scale the work across multiple files? You’re not alone—developers often hit a wall when they try to read text from scans one by one. The good news is that with Aspose OCR you can **extract text from jpg** files, **read text from scans**, and **process image list** items in parallel with just a few lines of C#.

Bu öğreticide, tam olarak nasıl yapılacağını gösteren eksiksiz, doğrudan çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, JPEG taramaları içeren bir klasörü tanıyan, her sayfanın metnini yazdıran ve her işlemin ne kadar sürdüğünü bildiren bağımsız bir konsol uygulamanız olacak. Takip etmeniz gereken dış belgeler yok, yarım kalmış kod parçacıkları yok—sadece Visual Studio'ya ekleyip çalıştırabileceğiniz tam bir çözüm.

## İhtiyacınız Olanlar

- **.NET 6.0** veya daha yenisi (kod .NET Framework 4.6+ üzerinde de derlenir)
- **Aspose.OCR** NuGet paketi (`Install-Package Aspose.OCR`)
- İşlemek istediğiniz birkaç JPG veya taranmış görüntü dosyası
- İstediğiniz herhangi bir IDE; ben Visual Studio 2022 kullanıyorum, ancak VS Code da sorunsuz çalışır

Hepsi bu. NuGet paketine zaten sahipseniz, hazırsınız.

## Adım 1 – OCR Motorunu Başlatma (Toplu OCR Görüntüleri Kurulumu)

İlk yaptığımız şey bir `OcrEngine` örneği oluşturmak ve hangi dili arayacağını ona söylemektir. Çoğu durumda İngilizce yeterlidir, ancak `OcrLanguage.English`'i desteklenen herhangi bir dil ile değiştirebilirsiniz.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create the OCR engine and set the language to English
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };
```

*Neden önemli:* Motoru bir kez başlatıp tüm görüntülerde yeniden kullanmak, dosya başına yeni bir örnek oluşturmaktan çok daha verimlidir. Ayrıca Aspose'un iç kaynakları paylaşmasına izin verir; bu da **parallel OCR processing** için gereklidir.

## Adım 2 – Görüntü Listesini Oluşturma (Görüntü Listesini İşleme)

Sonra, toplu tanıyıcıya beslemek istediğimiz dosya yolu koleksiyonunu tanımlıyoruz. Bu listeyi `Directory.GetFiles` ile dinamik olarak oluşturabilirsiniz, ancak açıklık açısından birkaç girişi sabit kodlayacağız.

```csharp
        // Step 2: Define the image files that will be processed
        var imagePaths = new List<string>
        {
            @"YOUR_DIRECTORY/page1.jpg",
            @"YOUR_DIRECTORY/page2.jpg",
            @"YOUR_DIRECTORY/page3.jpg"
        };
```

*Tip:* Binlerce taramanız varsa, tüm listeyi bir kerede belleğe yüklememek için `Directory.EnumerateFiles` ve `*.jpg` gibi bir filtre kullanmayı düşünün.

## Adım 3 – Toplu Tanıma Çalıştırma (Paralel OCR İşleme)

Şimdi işin özü geliyor: `BatchRecognize` çağrısı. Metot, Aspose'un kaç iş parçacığı oluşturacağını kontrol eden bir `maxDegreeOfParallelism` argümanı alır. Varsayılan olarak dört iş parçacığı kullanır, ancak CPU'nuzda daha fazla çekirdek varsa bunu artırabilirsiniz.

```csharp
        // Step 3: Run batch recognition (4 parallel threads by default)
        var recognitionResults = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);
```

*Arka planda neler oluyor?* Aspose `imagePaths` koleksiyonunu parçalar, her parçayı ayrı bir iş parçacığına verir ve sonuçları birleştirir. Bu, **extract text from jpg** dosyalarından metin çıkarmanın, aynı anda ele alınabilecek bir **process image list** olduğunda en verimli yoludur.

## Adım 4 – Sonuçları Görüntüleme (Taramalardan Metin Okuma)

Son olarak `recognitionResults` koleksiyonunda döngü kurar ve her dosyanın metnini ve işleme süresini yazdırırız. `OcrResult` nesnesi ayrıca kaynak dosya adını verir; bu, çıktıyı kaydetmeniz veya loglamanız gerektiğinde yardımcı olur.

```csharp
        // Step 4: Output the results for each image
        foreach (var result in recognitionResults)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

**Beklenen çıktı (örnek):**

```
File: C:\Scans\page1.jpg
Time: 1.34s
The quick brown fox jumps over the lazy dog.
----------------------------------------
File: C:\Scans\page2.jpg
Time: 1.27s
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
----------------------------------------
File: C:\Scans\page3.jpg
Time: 1.41s
Invoice #12345
Total: $1,250.00
----------------------------------------
```

Her bloğun dosya adını, OCR süresini ve çıkarılan metni nasıl gösterdiğine dikkat edin. Bu, üretim hattında **reading text from scans** yaparken tam olarak ihtiyacınız olan bilgidir.

## Yaygın Kenar Durumlarını Ele Alma

| Situation | What to Watch For | Quick Fix |
|-----------|-------------------|-----------|
| **Dosya eksik** | `FileNotFoundException` `BatchRecognize` içinde fırlatılır | Yolları `imagePaths`'e eklemeden önce `File.Exists` ile doğrulayın. |
| **Desteklenmeyen format** | Aspose yalnızca raster görüntüleri (JPG, PNG, BMP, TIFF) işler. | Önce PDF'leri görüntülere dönüştürün (Aspose.PDF kullanın) veya bu dosyaları atlayın. |
| **Bellek baskısı** | Çok büyük görüntüler, birden fazla iş parçacığı çalıştığında RAM'i tüketebilir. | `maxDegreeOfParallelism` değerini düşürün veya OCR'dan önce görüntüleri yeniden boyutlandırın. |
| **İngilizce dışı metin** | Dil İngilizce olarak ayarlandığında diğer yazı sistemleri göz ardı edilir. | `Language = OcrLanguage.French` olarak değiştirin (veya çok dilli bir kombinasyon). |

Bu ipuçları, özellikle kullanıcı yüklemelerinden veya taranmış bir arşivden gelen **processing an image list** yaparken toplu işinizi sağlam tutar.

## Pro İpucu – Paralellik Ayarlama

Bunu 8 çekirdekli bir makinede çalıştırıyorsanız, paralelliği 6 ya da 8'e çıkarın ve hızın arttığını izleyin. Ancak, her iş parçacığının bitmap için de bellek tükettiğini unutmayın. Genel bir kural:

```csharp
int cores = Environment.ProcessorCount;
int maxThreads = Math.Max(1, cores - 1); // leave one core free for UI/OS
```

`maxThreads` değerini `BatchRecognize` içine yerleştirerek dinamik, makine‑bilincine sahip bir yapılandırma elde edebilirsiniz.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlemeye hazır tam program yer alıyor. `YOUR_DIRECTORY` ifadesini JPG taramalarınızı içeren yol ile değiştirmeniz yeterli.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // 1️⃣ Initialise the OCR engine – English language
        var ocrEngine = new OcrEngine
        {
            Config = { Language = OcrLanguage.English }
        };

        // 2️⃣ Build the list of image files to process
        var imagePaths = new List<string>();
        string folder = @"C:\Scans"; // <-- change this
        foreach (var file in Directory.EnumerateFiles(folder, "*.jpg"))
        {
            imagePaths.Add(file);
        }

        if (imagePaths.Count == 0)
        {
            Console.WriteLine("No JPG files found in the specified folder.");
            return;
        }

        // 3️⃣ Run batch OCR – let the library use 4 threads (adjust as needed)
        var results = ocrEngine.BatchRecognize(
            imagePaths,
            maxDegreeOfParallelism: 4);

        // 4️⃣ Output each result
        foreach (var result in results)
        {
            Console.WriteLine($"File: {result.SourceFile}");
            Console.WriteLine($"Time: {result.ProcessingTime.TotalSeconds:F2}s");
            Console.WriteLine(result.Text);
            Console.WriteLine(new string('-', 40));
        }
    }
}
```

> **Not:** `using System.IO;` satırı `Directory` yardımcı sınıfı için gereklidir. Kod, JPG bulunamazsa dostça bir mesaj yazdırır, sessiz bir hatayı önler.

## Sonuç

Temiz bir **batch OCR images** iş akışı, **extract text from jpg** dosyalarından metin çıkaran, **reads text from scans** yapan ve **parallel OCR processing** kullanarak **process an image list** verimli bir şekilde işleyen bir örnek gösterdik. Tam, çalıştırılabilir örnek, motoru nasıl kuracağınızı, dosya koleksiyonunu nasıl besleyeceğinizi ve sonuçları nasıl yöneteceğinizi tam olarak gösteriyor—bütün bunları bellek kullanımını ve iş parçacığı sayısını kontrol altında tutarak.

Bir sonraki adıma hazır mısınız? Dili Fransızcaya değiştirin, PDF‑to‑image dönüşümü ekleyin veya OCR metnini bir veritabanına kaydedin. Desen aynı kalır: bir kez başlatın, bir liste besleyin ve Aspose'un paralel olarak ağır işi yapmasına izin verin.

Sorularınız mı var ya da kendi ayarlamalarınızı paylaşmak mı istiyorsunuz? Aşağıya bir yorum bırakın, iyi kodlamalar!

![Batch OCR images processing flow](https://example.com/placeholder.png "Diagram illustrating batch OCR images workflow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}