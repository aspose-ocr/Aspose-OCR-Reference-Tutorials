---
category: general
date: 2026-02-11
description: Aspose OCR kullanarak C#'ta çok sayfalı bir TIFF üzerinde OCR nasıl çalıştırılır
  öğrenin. TIFF'i metne dönüştürün, TIFF'ten metin çıkarın ve görüntüden metni hızlıca
  tanıyın.
draft: false
keywords:
- how to run OCR
- recognize text from image
- convert tiff to text
- extract text from tiff
- perform OCR on image
language: tr
og_description: Aspose OCR kullanarak C#'de çok sayfalı TIFF üzerinde OCR nasıl çalıştırılır.
  TIFF'i metne dönüştürme, TIFF'ten metin çıkarma ve görüntüden metin tanıma için
  adım adım rehber.
og_title: Çok Sayfalı TIFF Görüntülerinde OCR Nasıl Çalıştırılır – Tam C# Öğreticisi
tags:
- OCR
- C#
- Aspose
- TIFF
title: Aspose OCR ile Çok Sayfalı TIFF Görüntülerinde OCR Nasıl Çalıştırılır – C#
  Rehberi
url: /tr/net/text-recognition/how-to-run-ocr-on-multi-page-tiff-images-with-aspose-ocr-c-g/
---

careful with bullet indentation and line breaks.

Let's write.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Çok Sayfalı TIFF Görüntülerinde OCR Nasıl Çalıştırılır

Birden fazla sayfa içeren taranmış bir TIFF üzerinde **OCR'nin nasıl çalıştırılacağını** hiç merak ettiniz mi? Yalnız değilsiniz—birçok geliştirici eski belgelerden aranabilir metin çıkarmaya çalışırken bu soruna takılıyor. İyi haber? Aspose OCR ile sadece birkaç satır C# kodu kullanarak görüntü dosyalarından metin tanıyabilir ve indeksleme ya da daha fazla işleme hazır, düz birleştirilmiş metin elde edersiniz.

Bu öğreticide, Aspose OCR paketini kurmaktan çok sayfalı bir TIFF'i yüklemeye, TIFF'i metne dönüştürmeye ve sonunda çıkarılan içeriği görüntülemeye kadar tüm iş akışını adım adım inceleyeceğiz. Sonunda **TIFF dosyalarından metin çıkarabilir**, **görüntüden metin tanıyabilir** ve hatta bir toplu işte onlarca dosya için süreci otomatikleştirebileceksiniz. Sihir yok, sadece net ve pratik adımlar.

## Neler Öğreneceksiniz

- Aspose OCR motorunu İngilizce dil tanıması için nasıl yapılandıracağınızı.  
- `OcrEngine` sınıfını kullanarak **TIFF'i metne dönüştürmek** için gereken tam kodu.  
- Çok sayfalı görüntüleri nasıl ele alacağınız ve her sayfanın doğru şekilde ayrıldığından nasıl emin olacağınız ipuçları.  
- Yaygın tuzaklar (ör. eksik yerel bağımlılıklar) ve bunlardan nasıl kaçınılacağı.  

**Önkoşullar** – .NET 6 veya daha yeni bir sürüm, Visual Studio (veya herhangi bir C# editörü) ve otomatik kaynak indirme özelliği için bir internet bağlantısına ihtiyacınız olacak. Hepsi bu; ek yerel kütüphanelerle uğraşmayacaksınız.

---

## Step 1 – Install Aspose OCR NuGet Package

**Görüntü dosyalarında OCR gerçekleştirebilmek** için önce kütüphaneyi projenize eklemelisiniz.

```bash
dotnet add package Aspose.OCR
```

> **İpucu:** Visual Studio içinde çalışıyorsanız, projeye sağ tıklayıp → *Manage NuGet Packages* → “Aspose.OCR” aratıp *Install* düğmesine tıklayabilirsiniz.

Paket ihtiyacınız olan her şeyi içerir ve `AutomaticResourceDownload = true` ayarı sayesinde motor, dil paketlerini anlık olarak indirir.

---

## Step 2 – Initialize the OCR Engine (How to Run OCR)

Paket yüklendikten sonra bir `OcrEngine` örneği oluşturup yapılandırıyoruz. Bu, senaryomuzda **OCR'nin nasıl çalıştırılacağı** konusunun kalbidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;   // For Image class
using System;

// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English,          // Recognize English text
    AutomaticResourceDownload = true,        // Auto‑download language data
    OutputFormat = OcrOutputFormat.Text      // Get plain concatenated text
};
```

**Neden önemli:** `Language` ayarı, motorun hangi karakter setini bekleyeceğini belirtirken, `AutomaticResourceDownload` dil dosyalarını manuel olarak sunucuya koyma zahmetinden sizi kurtarır. `OutputFormat` olarak `Text` seçmek, **TIFF'i metne dönüştürmek** işlemleri için mükemmel, basit bir string elde etmemizi sağlar.

---

## Step 3 – Load the Multi‑Page TIFF (Recognize Text from Image)

Bir TIFF, her biri bir sayfayı temsil eden birçok çerçeve (frame) içerebilir. `System.Drawing.Image` sınıfı bu işlemi bizim için soyutlar.

```csharp
// Step 3: Load the multi‑page image to be processed
using (var image = Image.FromFile("YOUR_DIRECTORY/multi_page.tiff"))
{
    // Step 4: Run OCR on the image
    var ocrResult = ocrEngine.Recognize(image);

    // Step 5: Display the extracted text
    Console.WriteLine(ocrResult.Text);
}
```

> **Dosya aynı klasörde değilse ne olur?** Tam mutlak bir yol sağlayın ya da `AppContext.BaseDirectory` ile `Path.Combine` kullanın.  
> **Bellek kullanımı hakkında ne söyleyebiliriz?** `using` ifadesi, işlem sonrası görüntüyü serbest bırakır ve sızıntıları önler—bu, onlarca büyük TIFF'i toplu işleyince kritik bir özelliktir.

`Recognize` çağrısı, TIFF içindeki her sayfayı otomatik olarak dolaşır ve sonuçları satır sonlarıyla birleştirir. Bu yüzden `ocrResult.Text` çıktısını bastığınızda her sayfanın ayrı bir satırda göründüğünü fark edeceksiniz.

---

## Step 4 – Full Working Example (All Steps in One File)

Aşağıda, tamamen çalışır durumda bir konsol uygulaması örneği bulacaksınız. Yeni bir .NET konsol projesine kopyalayıp **F5** tuşuna basmanız yeterli.

```csharp
// File: Program.cs
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace TiffOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Configure the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.English,
                AutomaticResourceDownload = true,
                OutputFormat = OcrOutputFormat.Text
            };

            // 2️⃣ Load your multi‑page TIFF (replace with your actual path)
            const string tiffPath = @"YOUR_DIRECTORY\multi_page.tiff";

            if (!System.IO.File.Exists(tiffPath))
            {
                Console.WriteLine($"File not found: {tiffPath}");
                return;
            }

            // 3️⃣ Perform OCR
            using (var image = Image.FromFile(tiffPath))
            {
                var result = ocrEngine.Recognize(image);

                // 4️⃣ Output the extracted text
                Console.WriteLine("=== OCR RESULT ===");
                Console.WriteLine(result.Text);
                Console.WriteLine("==================");
            }

            // Keep console open
            Console.WriteLine("Press any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
=== OCR RESULT ===
Page 1: The quick brown fox jumps over the lazy dog.
Page 2: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
...
==================
Press any key to exit...
```

Her sayfa, `OcrOutputFormat.Text` çerçeveler arasına satır sonu eklediği için kendi satırında görüntülenir. Farklı bir ayırıcıya ihtiyacınız olursa, `result.Text` üzerinde `String.Replace` ile sonradan işleme yapabilirsiniz.

---

## Step 5 – Handling Common Edge Cases

### 5.1 Large TIFF Files  
Gigabayt boyutundaki TIFF'lerle çalışırken tüm dosyayı belleğe yüklemek sorun yaratabilir. Bir çözüm, her çerçeveyi ayrı ayrı işlemek:

```csharp
using (var image = Image.FromFile(tiffPath))
{
    for (int i = 0; i < image.GetFrameCount(FrameDimension.Page); i++)
    {
        image.SelectActiveFrame(FrameDimension.Page, i);
        var pageResult = ocrEngine.Recognize(image);
        Console.WriteLine($"--- Page {i + 1} ---");
        Console.WriteLine(pageResult.Text);
    }
}
```

### 5. Non‑English Documents  
İspanyolca veya Fransızca gibi dillerde **görüntüden metin tanımak** istiyorsanız sadece `Language` özelliğini değiştirin:

```csharp
ocrEngine.Language = OcrLanguage.Spanish; // or OcrLanguage.French
```

Aspose, uygun dil kaynaklarını otomatik olarak indirir.

### 5. Saving the Output  
Genellikle **TIFF'i metne dönüştürüp** sonucu bir `.txt` dosyasına kaydetmek istersiniz:

```csharp
System.IO.File.WriteAllText("output.txt", ocrResult.Text);
```

Ayrıca çıktıyı `String.Split(Environment.NewLine)` ile sayfalara ayırıp her dilimi ayrı bir dosyaya yazabilirsiniz.

---

## Pro Tips & Gotchas

- **AutomaticResourceDownload** uygulamayı ilk çalıştırdığınızda devreye girer; sonraki çalıştırmalar çevrim dışı gerçekleşir.  
- Bozuk karakterler görürseniz, `Language` ayarını tekrar kontrol edin; uyumsuz dil paketleri hatalı tanıma neden olur.  
- TIFF'lere rasterleştirilmiş PDF'ler için `ocrEngine.Dpi` değerini (varsayılan 300) artırmak doğruluğu artırabilir.  
- `Image.FromFile` her zaman bir `using` bloğu içinde kullanılmalı; aksi takdirde dosya kilitlenir ve sonradan silinip taşınamaz.

---

## Frequently Asked Questions

**S: Tek sayfalı TIFF'lerde de çalışır mı?**  
C: Kesinlikle. Motor tek çerçeveli bir TIFF'i aynı şekilde işler; sadece bir satır metin elde edersiniz.

**S: PNG veya JPEG dosyalarını da aynı şekilde işleyebilir miyim?**  
C: Evet—dosya uzantısını değiştirmeniz yeterli. `Recognize` metodu, herhangi bir `System.Drawing.Image` formatını kabul eder.

**S: OCR sonucunu düz metin yerine PDF olarak almak istersem ne yapmalıyım?**  
C: `OutputFormat = OcrOutputFormat.Pdf` olarak ayarlayın, `ocrResult` PDF bayt dizisini içerecek ve diske yazılabilir.

---

## Conclusion

Artık Aspose OCR kullanarak C# içinde çok sayfalı TIFF dosyalarında **OCR'nin nasıl çalıştırılacağı** konusunda eksiksiz, uçtan uca bir çözümünüz var. Motoru yapılandırıp, görüntüyü yükleyip `Recognize` metodunu çağırarak **TIFF dosyalarından metin çıkarabilir**, **TIFF'i metne dönüştürebilir** ve **görüntüden metin tanıyabilirsiniz**; tüm bunlar sadece birkaç satır kodla mümkün. Dil, çıktı formatı veya çerçeve‑çerçeve işleme gibi ayarları kendi toplu iş ihtiyaçlarınıza göre özgürce değiştirebilirsiniz.

Bir sonraki adıma hazır mısınız? Bu yaklaşımı bir klasör‑izleyici servisiyle birleştirerek **görüntü dosyalarında OCR otomatik olarak** çalıştırabilir, çıktıyı anında bir arama indeksine entegre edebilir ve tam metin arama özelliği ekleyebilirsiniz. Olasılıklar sınırsız, ve az önce gördüğünüz kod sağlam bir temel oluşturuyor.

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da GitHub üzerinden bana ulaşın. İyi kodlamalar, ve inatçı TIFF'leri aranabilir metne dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}