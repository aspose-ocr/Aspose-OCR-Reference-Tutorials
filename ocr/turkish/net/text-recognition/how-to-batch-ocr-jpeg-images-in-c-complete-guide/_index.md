---
category: general
date: 2026-02-22
description: C# ile Aspose.OCR kullanarak JPEG görüntülerini toplu OCR nasıl yapılır.
  JPG'den metin çıkarma, JPG'yi txt'ye dönüştürme ve görüntüleri verimli bir şekilde
  toplu işleme öğrenin.
draft: false
keywords:
- how to batch ocr
- extract text from jpg
- convert jpg to txt
- batch process images
- c# ocr example
language: tr
og_description: C# ile Aspose.OCR kullanarak JPEG görüntüleri toplu OCR nasıl yapılır.
  Bu öğreticide jpg’den metin çıkarma, jpg’yi txt’ye dönüştürme ve görüntüleri dakikalar
  içinde toplu işleme yöntemlerini gösteriyoruz.
og_title: C# ile JPEG Görüntülerini Toplu OCR İşleme – Tam Kılavuz
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# ile JPEG Görüntüleri Toplu OCR – Tam Kılavuz
url: /tr/net/text-recognition/how-to-batch-ocr-jpeg-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta JPEG Görüntülerini Toplu OCR İşlemi – Tam Kılavuz

Her bir dosya için ayrı bir program yazmadan, resimlerle dolu bir klasörü **toplu OCR** yapmanın nasıl olduğunu hiç merak ettiniz mi? Bu rehberde, Aspose.OCR kullanarak JPEG dosyalarını **toplu OCR** yapmanın tam olarak nasıl yapılacağını göstereceğiz, böylece sadece birkaç satır kodla **jpg'den metin çıkarabilir** ve **jpg'yi txt'ye dönüştürebilirsiniz**.  

Bir dizindeki taranmış faturalarla karşı karşıya kaldığınızda ve “Daha hızlı bir yol olmalı” diye düşündüğünüzde, doğru yerdesiniz. Her adımı adım adım inceleyecek, her parçanın neden önemli olduğunu açıklayacak ve büyük toplularla başa çıkmak için birkaç profesyonel ipucu da ekleyeceğiz.

## Oluşturacağınız Şey

Bu öğreticinin sonunda, aşağıdakileri yapan küçük bir konsol uygulamanız olacak:

* Belirtilen bir dizinde `*.jpg` dosyalarını tarar.  
* Her görüntüyü Aspose OCR motorundan geçirir (eğer uygun bir kartınız varsa GPU‑hızlandırmalı).  
* Tanımlanan metni, orijinal resmin yanına yerleştirilen bir `.txt` dosyasına yazar.  

Harici hizmetler yok, manuel kopyala‑yapıştır yok—sadece saf C# ve güvenilir bir OCR kütüphanesi.

### Önkoşullar

* .NET 6.0 veya daha yenisi (kod .NET Framework 4.8'de de çalışır).  
* Visual Studio 2022 veya C# destekleyen herhangi bir editör.  
* Bir Aspose.OCR NuGet paketi (ücretsiz deneme testi için çalışır).  

Eğer bunlardan herhangi birine sahip değilseniz, şimdi durup kurun; rehberin geri kalanı bunların zaten yüklü olduğunu varsayar.

![Toplu OCR örneği](/images/how-to-batch-ocr.png "toplu ocr diyagramı")

## Adım 1: Aspose.OCR NuGet Paketini Yükleyin

İlk olarak, projenizin OCR kütüphanesine ihtiyacı var. Çözüm klasöründe bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Veya Visual Studio'da NuGet Paket Yöneticisi UI'sını kullanın. Bu, gerek duyduğunuz her şeyi, makineniz destekliyorsa GPU‑destekli ikili dosyaları da getirir.

> **Pro ipucu:** Bunu GPU'suz bir sunucuda çalıştırmayı planlıyorsanız, daha sonra `UseGpu = false` olarak ayarlayın; motor otomatik olarak CPU'ya geri dönecektir.

## Adım 2: OCR Motorunu Yapılandırın

`OcrEngine` oluşturmak ve yapılandırmak sihrin başladığı yerdir. Motora hangi dili bekleyeceğini, GPU kullanıp kullanmayacağını ve çıktının hangi formatta olması gerektiğini söyleyeceksiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// ...

// Step 2: Initialize and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // English works for most documents; change if you need another language.
    Language = Language.English,

    // Enable GPU for faster processing on supported hardware.
    UseGpu = true,

    // We only need plain text for our .txt files.
    OutputFormat = OutputFormat.Text
};
```

**Neden önemli?** `Language` ayarı, motorun karakter setlerini daraltabilmesi sayesinde doğruluğu artırır. `UseGpu`'yu etkinleştirmek, modern bir grafik kartında işleme süresini yarıya indirebilir; bu, **görüntüleri toplu işleme** yaparken gerçek bir avantajdır.

## Adım 3: Bir Klasördeki Tüm JPEG Dosyalarını Tanıyın

Şimdi Aspose'un ağır işi yapmasına izin veriyoruz. Statik `BatchProcessor.RecognizeFolder` metodu dizini dolaşır, eşleşen her dosyada OCR çalıştırır ve sonuçların bir koleksiyonunu döndürür.

```csharp
using System.Collections.Generic;

// ...

// Step 3: Run OCR on every *.jpg in the target directory
IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
    ocrEngine,
    @"C:\Images\Invoices",   // <-- replace with your folder path
    searchPattern: "*.jpg"); // Only JPEG files are processed
```

**Köşe durumları:** Klasör alt klasörler içeriyorsa, `SearchOption.AllDirectories` aşırı yüklemesini (veya manuel olarak yinelemeyi) ekleyerek hiçbir dosyayı kaçırmadığınızdan emin olabilirsiniz.

## Adım 4: Her Sonucu Uygun `.txt` Dosyasına Yazın

`OcrResult` nesneleri orijinal dosya yolunu ve tanınan metni içerir. Bunlar üzerinde döngü kurun, uzantıyı değiştirin ve çıktıyı yazın.

```csharp
using System.IO;

// ...

// Step 4: Persist OCR results as .txt files next to the source images
foreach (var result in ocrResults)
{
    // Change "image.jpg" → "image.txt"
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");

    // Save the extracted text
    File.WriteAllText(txtFilePath, result.Text);
}
```

Hepsi bu kadar—her JPEG artık yanına bir metin dosyası eklenmiş durumda; bu dosyayı sonraki süreçlere, arama indekslerine ya da sadece arşivlemeye besleyebilirsiniz.

## Adım 5: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Programı derleyin ve çalıştırın:

```bash
dotnet run
```

Klasörün `invoice1.jpg` ve `receipt2.jpg` içerdiğini varsayarsak, yanlarında `invoice1.txt` ve `receipt2.txt` dosyalarının belirdiğini görmelisiniz. `.txt` dosyalarından birini açın; ham OCR çıktısını göreceksiniz, örneğin:

```
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
Thank you for your business!
```

Metin bozuk görünüyorsa, kaynak görüntülerin yüksek kontrastlı olduğundan ve `Language` özelliğinin belge diline uygun olduğundan emin olun.

## Adım 6: İleri Düzey Ayarlamalar (İsteğe Bağlı)

### a) Düşük Kaliteli Taramalarla Başa Çıkma

Bazen JPEG'ler gürültülüdür. Görüntüleri Aspose.Imaging veya başka bir kütüphane ile ön işleme tabi tutabilirsiniz:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

// Example: increase contrast before OCR
using (var image = Image.Load(result.SourceFilePath))
{
    image.Contrast = 30; // boost contrast
    image.Save(result.SourceFilePath); // overwrite or save to temp file
}
```

### b) Toplu İşlemi Paralelleştirme

Eğer çok sayıda dosyanız ve çok çekirdekli bir CPU'nuz varsa, döngüyü `Parallel.ForEach` ile sarmalayın:

```csharp
Parallel.ForEach(ocrResults, result =>
{
    string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
    File.WriteAllText(txtFilePath, result.Text);
});
```

Sadece Aspose OCR motorunun kendisinin iş parçacığı güvenli olmadığını unutmayın; her iş parçacığı için ayrı bir `OcrEngine` örneği gerekir ya da eşzamanlı bir kuyruk kullanın.

### c) Günlükleme ve Hata Yönetimi

Sağlam bir çözüm, hataları kaydeder böylece daha sonra yeniden deneyebilirsiniz:

```csharp
try
{
    // OCR and write logic here
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {result.SourceFilePath}: {ex.Message}");
    // Optionally write to a log file
}
```

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, yeni bir Console App içine kopyalayıp yapıştırabileceğiniz tam program burada:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Collections.Generic;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create and configure the OCR engine
        var ocrEngine = new OcrEngine
        {
            Language = Language.English,
            UseGpu = true,
            OutputFormat = OutputFormat.Text
        };

        // 2️⃣ Recognize all JPEG images in the target folder
        IList<OcrResult> ocrResults = BatchProcessor.RecognizeFolder(
            ocrEngine,
            @"C:\Images\Invoices",   // <-- change to your directory
            searchPattern: "*.jpg");

        // 3️⃣ Write each OCR result to a matching .txt file
        foreach (var result in ocrResults)
        {
            string txtFilePath = Path.ChangeExtension(result.SourceFilePath, ".txt");
            File.WriteAllText(txtFilePath, result.Text);
        }

        Console.WriteLine("Batch OCR complete. Check the folder for .txt files.");
    }
}
```

Çalıştırın, konsol çıktısını izleyin ve ardından birkaç `.txt` dosyasını açarak **jpg'den metin çıkarma** adımının başarılı olduğunu doğrulayın.  

---

## Sonuç

Aspose.OCR kullanarak C#'ta JPEG görüntülerinin bir koleksiyonunu **toplu OCR** yapmayı, her resmi aranabilir bir `.txt` dosyasına dönüştürmeyi yeni yeni ele aldık. Çözüm kompakt, GPU‑bilinçli ve hata yönetimi, görüntü ön işleme ya da paralel yürütme için genişletmesi kolay.

Daha ileri gitmeye hazırsanız, aşağıdaki adımları düşünün:

* **Batch process images** diğer formatlarda (`*.png`, `*.tif`) `searchPattern`'ı değiştirerek.  
* Çıktıyı, anlık belge araması için Lucene.NET gibi tam metin arama motoru ile birleştirin.  
* OCR sonuçlarından doğrudan aranabilir PDF'ler üretmek için Aspose'un PDF dönüşüm özelliklerini keşfedin.  

Denemekten çekinmeyin—dili değiştirin, GPU'yu kapatın ya da metni bir veritabanına yönlendirin. Temel desen aynı kalır ve artık üzerine inşa edebileceğiniz sağlam bir temele sahipsiniz.

Kodlamaktan keyif alın, ve OCR boru hatlarınız her daim hızlı ve doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}