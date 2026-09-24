---
category: general
date: 2026-02-14
description: C#'ta OCR kullanarak PNG dosyalarından metni hızlıca nasıl çıkarılır?
  Toplu OCR görüntülerini öğrenin, birden fazla görüntüyü işleyin ve tek bir rehberde
  Aspose OCR C#'ı kullanın.
draft: false
keywords:
- how to use OCR
- extract text png
- batch OCR images
- process multiple images
- aspose OCR c#
language: tr
og_description: C#'ta Aspose OCR C# ile OCR nasıl kullanılır. Bu öğreticide PNG dosyalarından
  metin çıkarma, toplu OCR görüntüleri ve birden fazla görüntüyü verimli bir şekilde
  işleme gösterilmektedir.
og_title: C#'da OCR Nasıl Kullanılır – Toplu PNG Metin Çıkarma
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'de OCR Nasıl Kullanılır – Aspose OCR ile PNG Görüntülerini Toplu İşleme
url: /tr/net/text-recognition/how-to-use-ocr-in-c-batch-process-png-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Aspose OCR ile PNG Görüntülerini Toplu İşleme

Hiç **OCR nasıl kullanılır** sorusunu, her bir PNG dosyası için ayrı bir rutin yazmadan metin çıkarmak için düşündünüz mü? Yalnız değilsiniz. Birçok geliştirici, özellikle görüntüler bir klasörde durduğunda ve her dosya için OCR motorunu çalıştırmanız gerektiğinde, **PNG'den metin çıkarma** işlemini ölçekli bir şekilde yaparken zorlanıyor.

Bu rehberde, **toplu OCR görüntüleri**, **birden fazla görüntüyü paralel olarak işleme** ve güçlü **Aspose OCR C#** kütüphanesini kullanan tam, çalıştırmaya hazır bir çözümü adım adım inceleyeceğiz. Sonunda, istediğiniz sayıda PNG'yi okuyup metnini çıkaran ve sonuçları konsola yazdıran tek bir çalıştırılabilir dosyanız olacak – sadece birkaç satır kodla.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework ile de çalışır)  
- Geçerli bir Aspose.OCR for .NET lisansı (veya ücretsiz deneme) – lisansı Aspose web sitesinden alabilirsiniz.  
- Okumak istediğiniz PNG dosyalarını içeren bir klasör.  
- Visual Studio 2022 (veya herhangi bir C# uyumlu IDE).  

`Aspose.OCR` dışındaki ek NuGet paketlerine ihtiyaç yoktur.

## Adım 1: OCR Nasıl Kullanılır – Aspose OCR Motorunu Başlatma

İlk olarak bir `Engine` sınıfı örneğine ihtiyacınız var. Bu nesne, altındaki OCR teknolojisini soyutlar ve donanımınıza ve lisansınıza bağlı olarak CPU ya da GPU üzerinde çalışabilir.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

// Create an OCR engine (CPU by default; GPU can be enabled via EngineSettings if licensed)
var ocrEngine = new Engine();
```

*Bu neden önemlidir:* Motoru bir kez başlatıp tüm iş parçacıkları arasında yeniden kullanmak bellek tasarrufu sağlar ve OCR modellerinin tekrar tekrar yüklenmesinden kaynaklanan gecikmeyi önler. Ayrıca tüm görüntüler için tutarlı ayarlar garantilenir.

## Adım 2: PNG'den Metin Çıkarma – Görüntü Yollarını Toplama

Şimdi bir dosya yolu koleksiyonuna ihtiyacımız var. Gerçek bir projede klasörü dinamik olarak okuyabilirsiniz, ancak açıklık olması açısından birkaç örnek dosyayı listeleyeceğiz.

```csharp
// List the PNG files you want to process
var imagePaths = new List<string>
{
    "YOUR_DIRECTORY/img1.png",
    "YOUR_DIRECTORY/img2.png",
    "YOUR_DIRECTORY/img3.png"
};
```

*İpucu:* `YOUR_DIRECTORY` ifadesini görüntülerinizin mutlak ya da göreli yolu ile değiştirin. Eğer onlarca dosyanız varsa, manuel listeyi `Directory.GetFiles("YOUR_DIRECTORY", "*.png")` ile değiştirebilirsiniz.

## Adım 3: Toplu OCR Görüntüleri – Paralelde Tanıma Çalıştırma

Görüntüleri birbiri ardına işlemek basit ama yavaştır. `Parallel.ForEach` kullanarak **birden fazla görüntüyü** aynı anda işleyebilir, çok çekirdekli CPU'lardan faydalanabiliriz.

```csharp
// Helper method that performs the parallel recognition
static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
{
    var resultsBag = new ConcurrentBag<OcrResult>();

    Parallel.ForEach(paths, path =>
    {
        // Load the image stream (Aspose handles various formats)
        var image = ImageStream.FromFile(path);
        // Perform OCR
        OcrResult result = engine.Recognize(image);
        // Store the result safely for later use
        resultsBag.Add(result);
    });

    return resultsBag.ToArray();
}

// Execute the parallel OCR
var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);
```

*Neden paralel?* Her OCR çağrısı CPU‑yoğun ancak bağımsızdır, bu yüzden aynı anda çalıştırmak toplam çalışma süresini özellikle 4 çekirdek ve üzeri makinelerde büyük ölçüde azaltır.

## Adım 4: Birden Fazla Görüntüyü İşleme – Çıkarılan Metni Görüntüleme

Artık bir `OcrResult` nesne koleksiyonumuz olduğuna göre, bunlar üzerinde döngü kurup tanınan metni yazdırabiliriz. Normalde çıktıyı bir veritabanına kaydeder ya da dosyalara yazarız, ancak konsol çıktısı örneği kısa tutar.

```csharp
int index = 1;
foreach (var result in ocrResults)
{
    Console.WriteLine($"--- Image {index++} ---");
    Console.WriteLine(result.Text);
}
```

**Beklenen konsol çıktısı (örnek):**

```
--- Image 1 ---
Hello world! This is the first image.
--- Image 2 ---
Invoice #12345
Total: $250.00
--- Image 3 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
```

Herhangi bir görüntü yüklenemezse Aspose bir istisna fırlatır; `engine.Recognize` çağrısını bir try/catch bloğuna sararak hataları kaydedebilir ve bütün toplu işlemin durmasını önleyebilirsiniz.

## Adım 5: Tam Çalışan Örnek – Tüm Parçalar Bir Arada

Aşağıda yeni bir C# konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. `using` ifadelerinden son çıktı döngüsüne kadar her şey dahil.

```csharp
using System;
using System.Collections.Generic;
using System.Collections.Concurrent;
using System.Threading.Tasks;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // Step 1: Initialize the OCR engine
        var ocrEngine = new Engine();

        // Step 2: Define the PNG files to process
        var imagePaths = new List<string>
        {
            "YOUR_DIRECTORY/img1.png",
            "YOUR_DIRECTORY/img2.png",
            "YOUR_DIRECTORY/img3.png"
        };

        // Step 3: Run OCR in parallel
        var ocrResults = RecognizeImagesInParallel(ocrEngine, imagePaths);

        // Step 4: Output the recognized text
        int index = 1;
        foreach (var result in ocrResults)
        {
            Console.WriteLine($"--- Image {index++} ---");
            Console.WriteLine(result.Text);
        }
    }

    // Helper method for parallel OCR
    static IReadOnlyList<OcrResult> RecognizeImagesInParallel(Engine engine, IEnumerable<string> paths)
    {
        var resultsBag = new ConcurrentBag<OcrResult>();

        Parallel.ForEach(paths, path =>
        {
            try
            {
                var image = ImageStream.FromFile(path);
                OcrResult result = engine.Recognize(image);
                resultsBag.Add(result);
            }
            catch (Exception ex)
            {
                // Log the error but keep the batch running
                Console.Error.WriteLine($"Error processing {path}: {ex.Message}");
            }
        });

        return resultsBag.ToArray();
    }
}
```

### Örneği Çalıştırma

1. Visual Studio'da yeni bir **Console App** projesi oluşturun.  
2. **Aspose.OCR** NuGet paketini ekleyin (`Install-Package Aspose.OCR`).  
3. `YOUR_DIRECTORY` ifadesini PNG dosyalarınızı tutan klasörün yolu ile değiştirin.  
4. Derleyin ve çalıştırın – çıkarılan metnin konsola yazdırıldığını görmelisiniz.

## Pro İpuçları & Kenar Durumları

- **GPU hızlandırma:** Uyumlu bir GPU ve lisanslı Aspose OCR varsa, motoru oluşturmadan önce `EngineSettings` ile etkinleştirin. Bu, her görüntü için saniyeler kazanmanızı sağlar.  
- **Büyük dosyalar:** 10 MB'den büyük görüntüler için önce ölçek küçültme yaparak bellek baskısını azaltın.  
- **Dil desteği:** Varsayılan olarak motor İngilizce kabul eder. `engine.Language = Language.French;` (veya desteklenen başka bir dil) ayarlayarak İngilizce dışı metinlerde doğruluğu artırabilirsiniz.  
- **Hata yönetimi:** Paralel döngüdeki `try/catch`, bozuk bir dosyanın tüm toplu işlemi durdurmasını engeller. Hataları daha sonra incelemek için bir dosyaya da kaydedebilirsiniz.  
- **Sonuç depolama:** Yazdırmak yerine `result.Text` değerini `File.WriteAllText(Path.ChangeExtension(path, ".txt"))` kullanarak bir `.txt` dosyasına yazabilirsiniz.

## Sonuç

Artık **C#'ta OCR nasıl kullanılır** ve **PNG dosyalarından metin çıkarma**, **görüntüleri toplu OCR** ve **birden fazla görüntüyü verimli bir şekilde işleme** konusunda tam bir çözüme sahipsiniz. Çözüm tamamen bağımsız, paralel çalışıyor ve yüzlerce ya da binlerce dosyayı minimum değişiklikle işleyebilecek şekilde genişletilebilir.

Bir sonraki adıma hazır mısınız? Konsol çıktısını bir CSV raporuna dönüştürmeyi deneyin, GPU hızlandırmayı test edin ya da OCR metnini bir arama indeksine besleyin. Olasılıklar sınırsızdır ve temel desen—bir kez başlat, paralel çalış, hataları nazikçe yönet—her türlü görüntü‑işleme hattında size hizmet edecektir.

İyi kodlamalar, OCR işleriniz hızlı ve hatasız olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}