---
category: general
date: 2026-03-20
description: Aspose OCR ve ePub kütüphanelerini kullanarak taranmış bir sayfadan ePub
  nasıl oluşturulur. Görüntüden metin çıkarma, jpg’den metin tanıma ve görüntüyü ePub’a
  dönüştürmeyi öğrenin.
draft: false
keywords:
- how to create epub
- extract text from image
- recognize text from jpg
- convert image to epub
- extract text from scan
language: tr
og_description: Aspose OCR kullanarak taranmış bir sayfadan ePub nasıl oluşturulur.
  Görüntüden metin çıkarın, jpg’den metni tanıyın ve görüntüyü dakikalar içinde ePub’a
  dönüştürün.
og_title: Tarama Görüntülerinden ePub Nasıl Oluşturulur – Tam C# Öğreticisi
tags:
- C#
- Aspose
- OCR
- ePub
title: Taranmış Görüntülerden ePub Oluşturma – Adım Adım Kılavuz
url: /tr/net/text-recognition/how-to-create-epub-from-scanned-images-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tarama Görüntülerinden ePub Oluşturma – Tam C# Öğreticisi

Bir kitap sayfasının fotoğrafından **ePub nasıl oluşturulur** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici eski kağıt kitapları dijital ePub dosyalarına dönüştürmek zorunda, ancak süreç çoğu zaman resmi olmayan bir bulmacayı birleştirmek gibi hissettirir.  

İyi haber? Aspose OCR ve Aspose ePub ile görüntüden metin çıkarabilir, jpg'den metin tanıyabilir ve görüntüyü sadece birkaç satır kodla ePub'a dönüştürebilirsiniz. Bu rehberde tüm iş akışını adım adım inceleyecek, her adımın neden önemli olduğunu açıklayacak ve size çalıştırmaya hazır bir kod örneği sunacağız.

## Gereksinimler

- **.NET 6+** (veya herhangi bir yeni .NET çalışma zamanı)
- **Aspose.OCR** NuGet paketi  
- **Aspose.Epub** NuGet paketi  
- Temiz, okunabilir metin içeren bir taranmış görüntü (`.jpg` veya `.png`)  
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir IDE  

Harici hizmetler, API anahtarları yok—sadece saf cihaz içi işleme.

## Adım 1 – Projeyi Kurun ve Paketleri Yükleyin

Başlamak için yeni bir konsol uygulaması oluşturun:

```bash
dotnet new console -n ImageToEpubDemo
cd ImageToEpubDemo
```

Ardından iki Aspose kütüphanesini ekleyin:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Epub
```

> **Pro ipucu:** Paketlerinizi güncel tutun. Mart 2026 itibarıyla OCR için en son kararlı sürüm `23.9.0`, ePub için `23.7.0`'dır. Daha yeni sürümler genellikle büyük taramalar için performans artışı sağlar.

## Adım 2 – OCR Motorunu Başlatın (Görüntüden Metin Çıkarma)

OCR motoru **görüntüden metin çıkarma** işleminin kalbidir. Hangi dili arayacağını ona söylersiniz; çoğu durumda İngilizce yeterlidir, ancak Fransızca, Almanca vb. dillerle değiştirebilirsiniz.

OCR motorunu aşağıdaki gibi başlatabilirsiniz:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialise OCR engine and set language
using var ocrEngine = new OcrEngine
{
    Language = Language.English   // change if you need another language
};
```

Neden dili ayarlamalısınız? OCR algoritmaları doğruluğu artırmak için dil modelleri kullanır. Yanlış modeli beslemek, özellikle aksan işaretlerinde bozuk çıktıya yol açabilir.

## Adım 3 – Taranmış JPG'yi Yükleyin ve Tanıma Yapın (JPG'den Metin Tanıma)

Şimdi taranmış sayfayı içeren resmi yüklüyoruz. `Image.FromFile` çağrısı çoğu yaygın format için çalışır (`.jpg`, `.png`, `.bmp`).

Resmi aşağıdaki gibi yükleyip tanıma işlemini gerçekleştirebilirsiniz:

```csharp
using System.Drawing;   // for Image class

// Load the scanned page – replace with your actual file path
var sourceImage = Image.FromFile(@"C:\Temp\book_page.jpg");

// Run OCR – this returns an OcrResult containing the plain text
var ocrResult = ocrEngine.Recognize(sourceImage);

// Optional: Inspect the raw text in the console
Console.WriteLine("---- OCR Output ----");
Console.WriteLine(ocrResult.Text);
```

Görüntü gürültülü ise, ön işleme (kontrast artırma, eğikliği düzeltme) yapmayı düşünün. Aspose OCR, eşik değerlerini ayarlayabileceğiniz bir `RecognitionOptions` nesnesi kabul eder, ancak çoğu temiz tarama için varsayılan ayarlar yeterlidir.

## Adım 4 – Yeni bir ePub Kitabı Oluşturun ve Meta Verileri Doldurun (Görüntüyü ePub'a Dönüştürme)

Metni elde ettikten sonra bir `EpubBook` nesnesi oluştururuz. Bu nesne nihai ePub dosyasını temsil eder ve istediğiniz meta verileri—başlık, yazar, dil vb.—ayarlayabilirsiniz.

Yeni bir ePub kitabı oluşturup meta verileri ayarlamak için:

```csharp
using Aspose.Epub;

// Initialise a fresh ePub container
var epubBook = new EpubBook
{
    Title  = "Scanned Book",
    Author = "Unknown",
    Language = "en"
};
```

Dili ayarlamak, e‑okuyucuların metni doğru görüntülemesine yardımcı olur ve erişilebilirliği artırır.

## Adım 5 – Tanınan Metni İçeren Bir Bölüm Ekleyin

Bir ePub temelde XHTML bölümlerinin bir koleksiyonudur. Burada basit bir metin bölümü oluşturuyoruz, ancak aynı zamanda resimler, CSS veya bir içerik tablosu da ekleyebilirsiniz.

Basit bir metin bölümü eklemek için aşağıdaki kodu kullanabilirsiniz:

```csharp
using Aspose.Epub.Models;

// Build a chapter from the OCR output
var textChapter = new EpubTextChapter
{
    Title   = "Page 1",
    Content = ocrResult.Text   // the raw text from step 3
};

// Attach the chapter to the book
epubBook.Chapters.Add(textChapter);
```

> **Neden metin bölümü?**  
> Sadece metin bölümleri dosya boyutunu küçültür ve çoğu cihazda anında aranabilir olur. Orijinal düzeni korumanız gerekiyorsa, orijinal resmi ayrı bir bölüm olarak ekleyebilir veya metnin yanına gömebilirsiniz.

## Adım 6 – ePub Dosyasını Kaydedin (Son Çıktı)

Son satır ePub dosyasını diske yazar. Yazma izniniz olan bir konum seçin.

ePub dosyasını kaydetmek için:

```csharp
// Save the ePub – adjust the path as needed
string outputPath = @"C:\Temp\scanned_book.epub";
epubBook.Save(outputPath);

Console.WriteLine($"✅ ePub saved to {outputPath}");
```

`scanned_book.epub` dosyasını Calibre, Apple Books veya herhangi bir ePub okuyucusunda açtığınızda, çıkarılan metni içeren *Page 1* başlıklı tek bir bölüm göreceksiniz.

### Beklenen Sonuç

Tam programı çalıştırdığınızda aşağıdakine benzer bir çıktı almanız gerekir:

```
---- OCR Output ----
Chapter One
It was the best of times, it was the worst of times...
...
✅ ePub saved to C:\Temp\scanned_book.epub
```

ePub dosyasını açtığınızda aynı paragrafı temiz ve kaydırılabilir bir sayfada göreceksiniz.

## Tam Çalışan Örnek

Aşağıda eksiksiz, bağımsız bir program yer alıyor. `Program.cs` dosyasına kopyalayıp **Run** tuşuna basın.

```csharp
// Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Epub;
using Aspose.Epub.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialise OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image (replace with your own path)
        var sourceImage = Image.FromFile(@"C:\Temp\book_page.jpg");

        // 3️⃣ Recognise text – this is where we extract text from image
        var ocrResult = ocrEngine.Recognize(sourceImage);
        Console.WriteLine("---- OCR Output ----");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create ePub book and set metadata
        var epubBook = new EpubBook
        {
            Title    = "Scanned Book",
            Author   = "Unknown",
            Language = "en"
        };

        // 5️⃣ Build a chapter using the recognised text
        var textChapter = new EpubTextChapter
        {
            Title   = "Page 1",
            Content = ocrResult.Text
        };
        epubBook.Chapters.Add(textChapter);

        // 6️⃣ Save the ePub file
        string outputPath = @"C:\Temp\scanned_book.epub";
        epubBook.Save(outputPath);
        Console.WriteLine($"✅ ePub saved to {outputPath}");
    }
}
```

Bunu `dotnet run` ile çalıştırın. Her şey doğru ayarlandıysa, dağıtıma hazır bir ePub elde edeceksiniz.

## Yaygın Sorular ve Kenar Durumları

### OCR karakterleri kaçırırsa ne olur?

- **Görüntü kalitesini kontrol edin** – bulanık veya düşük çözünürlüklü taramalar hatalara yol açar. En az 300 dpi hedefleyin.
- **`RecognitionOptions` kullanın** – ikilileştirme eşiklerini ayarlamak için.
- **Sonradan işleyin** – çıktıyı bir yazım denetleyicisi (ör. `NHunspell`) ile işleyerek belirgin yazım hatalarını temizleyin.

### Birden fazla sayfa ekleyebilir miyim?

Kesinlikle. Yükleme‑tanıma‑bölüm adımlarını bir döngü içinde sarabilirsiniz:

```csharp
foreach (var file in Directory.GetFiles(@"C:\Temp\Scans", "*.jpg"))
{
    var img = Image.FromFile(file);
    var result = ocrEngine.Recognize(img);
    epubBook.Chapters.Add(new EpubTextChapter
    {
        Title   = Path.GetFileNameWithoutExtension(file),
        Content = result.Text
    });
}
```

### Orijinal taranmış görüntüyü ePub içinde nasıl tutarım?

Bir `EpubImageChapter` oluşturun (veya resmi bir XHTML bölümüne gömün). Bu, görsel bütünlüğü korurken hâlâ aranabilir metin sağlar.

```csharp
var imgBytes = File.ReadAllBytes(@"C:\Temp\book_page.jpg");
var imgChapter = new EpubImageChapter
{
    Title   = "Page 1 (Image)",
    Content = imgBytes,
    MediaType = "image/jpeg"
};
epubBook.Chapters.Add(imgChapter);
```

### Oluşturulan ePub tüm okuyucularla uyumlu mu?

Aspose ePub, modern okuyucuların çoğu tarafından desteklenen EPUB 3.2 spesifikasyonunu izler. Daha eski cihazları hedefliyorsanız, EPUB 2'ye düşürmeniz gerekebilir—Aspose bunun için bir `SaveAsEpub2` aşırı yüklemesi sağlar.

## Üretim‑Hazır Uygulamalar İçin İpuçları

1. **Hata yönetimi** – OCR ve dosya I/O işlemlerini try/catch blokları içinde sarın; kullanıcıya anlamlı mesajlar gösterin.
2. **Bellek yönetimi** – Büyük toplular çok RAM tüketebilir. `Image` nesnelerini hemen serbest bırakın (`img.Dispose()`).
3. **Paralel işleme** – Onlarca sayfa için OCR'ı hızlandırmak amacıyla `Parallel.ForEach` kullanmayı düşünün (Aspose OCR iş parçacığı‑güvenlidir).
4. **Meta veri zenginleştirme** – `Publisher`, `ISBN` ve `CoverImage` alanlarını doldurun; bunlar e‑kitap kütüphanelerinde bulunabilirliği artırır.
5. **Test** – Üretilen ePub'ı `epubcheck` gibi araçlarla doğrulayarak dağıtımdan önce yapısal sorunları yakalayın.

## Sonuç

Aspose OCR ve Aspose ePub kullanarak taranmış bir resimden **ePub nasıl oluşturulur** konusunu ele aldık, **görüntüden metin çıkarma** işlemini gösterdik, **jpg'den metin tanıma** nasıl yapılır gösterdik ve sonucu temiz bir **görüntüyü epub'a dönüştürme** iş akışına dönüştürdük.  

Yukarıdaki eksiksiz kod örneğiyle, okunabilir herhangi bir taramayı anında aranabilir bir ePub'a dönüştürebilir, Kindle, Apple Books veya diğer okuyucular için hazır hâle getirebilirsiniz.  

Şimdi, öğreticiyi genişletmeyi deneyin: bir içerik tablosu ekleyin, orijinal taramaları resim olarak gömün veya çok dilli kitaplar için dil‑özel bir OCR modeli entegre edin. Sınır yok—iyi kodlamalar!

--- 

*İş akışını gösteren görsel (alt metin: “tarama görüntüsünden epub oluşturma Aspose OCR ve ePub kütüphaneleri kullanarak”)*  
![tarama görüntüsünden epub oluşturma Aspose OCR ve ePub kütüphaneleri kullanarak](https://example.com/placeholder-image.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}