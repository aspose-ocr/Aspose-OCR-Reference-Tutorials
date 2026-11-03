---
category: general
date: 2026-03-07
description: C# kullanarak PNG dosyalarından metin çıkarın. Görüntüyü metne dönüştürmeyi
  C# ile öğrenin ve taranmış görüntülerden metni hızlıca okuyun.
draft: false
keywords:
- extract text from png
- convert image to text c#
- read text from scanned images
- how to run ocr on images
language: tr
og_description: C# kullanarak PNG dosyalarından metin çıkarın. Bu kılavuz, görüntüyü
  C# ile metne dönüştürmeyi ve Aspose OCR ile taranmış görüntülerden metin okumayı
  gösterir.
og_title: C#'ta PNG'den Metin Çıkarma – Tam OCR Rehberi
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'ta PNG'den Metin Çıkarma – Tam OCR Rehberi
url: /tr/net/text-recognition/extract-text-from-png-in-c-full-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkarma C# – Tam OCR Rehberi

Hiç **PNG'den metin çıkarmak** gerekti ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—çoğu geliştirici, taranmış grafikler veya ekran görüntüleriyle ilk karşılaştıklarında bu duvara çarpar ve bunların aranabilir metin haline gelmesi gerekir. İyi haber? Birkaç satır C# ve Aspose OCR ile herhangi bir PNG'yi anında düzenlenebilir string'lere dönüştürebilirsiniz.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: diskteki PNG'leri bulmaktan, OCR görevlerini paralel olarak başlatmaya, her sonucun düzenli bir önizlemesini göstermeye kadar. Sonuna geldiğinizde **convert image to text C#** tarzında nasıl **görüntüyü metne dönüştüreceğinizi**, **tarama görüntülerinden metin okuma** konusunda nasıl verimli olacağınızı ve UI iş parçacığınızı yormadan **run OCR on images** en iyi yolunu göreceksiniz.

## Gereksinimler

- .NET 6.0 veya daha yeni (kod .NET Core ve .NET Framework'te de çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- İşlemek istediğiniz *.png* dosyalarıyla dolu bir klasör  
- Tercih ettiğiniz herhangi bir IDE (Visual Studio, VS Code, Rider…)

Ek bir yapılandırma gerekmez; kütüphane PNG, JPEG, TIFF gibi tüm formatları çözmek için gereken her şeyi içerir.

## Adım 1: Tüm PNG Dosyalarını Bulun – “Extract Text from PNG” Başlıyor

İlk olarak OCR çalıştırmak istediğimiz her PNG'yi bulmamız gerekiyor. `Directory.GetFiles` kullanmak hızlı ve güvenilirdir.

```csharp
// Step 1: Find all PNG images in the input folder
string[] imageFiles = Directory.GetFiles("YOUR_DIRECTORY", "*.png");

// Quick sanity check – throw if nothing was found
if (imageFiles.Length == 0)
    throw new FileNotFoundException("No PNG files found in the specified folder.");
```

*Neden önemli:* Dizini bir kez taramak, geri kalan işlem hattını basit tutar ve erken kontrol, daha sonra hata ayıklaması zor olabilecek sessiz bir “çıktı yok” durumunu önler.

## Adım 2: Paralel OCR Görevlerini Başlatın – Verimli bir şekilde **run OCR on images**

OCR'yi sıralı çalıştırmak birkaç dosya için yeterlidir, ancak gerçek dünyadaki projeler genellikle onlarca ya da yüzlerce dosyayla uğraşır. Görüntü başına bir `Task` başlatarak CPU'yu meşgul tutarız, kütüphane ise ağır işini yapar.

```csharp
// Step 2: Prepare a list to hold OCR tasks (one per image)
var ocrTasks = new List<Task<string>>();

// Step 3: Launch a parallel task for each image
foreach (var filePath in imageFiles)
{
    ocrTasks.Add(Task.Run(() =>
    {
        // Load the image and run OCR
        var engine = new OcrEngine();
        engine.Image = ImageStream.FromFile(filePath);
        engine.Recognize();
        return engine.Text;          // This is the extracted string
    }));
}
```

*Pro ipucu:* `Task.Run` işi iş parçacığı havuzuna devreder, bu da UI'nizin (varsa) yanıt vermeye devam etmesi anlamına gelir. Bir sunucuda iseniz, aynı desen çekirdekler arasında güzel bir şekilde ölçeklenir.

## Adım 3: Tüm Görevleri Bekleyin – Sonuçları Toplayın

Şimdi her OCR işleminin bitmesini bekliyoruz. `Task.WhenAll` orijinal dosya sırasına uyan bir dizi döndürür, böylece sonuçları dosya adlarıyla eşleştirmek kolay olur.

```csharp
// Step 4: Await all tasks and gather the recognized texts
string[] ocrResults = await Task.WhenAll(ocrTasks);
```

*Köşe durum notu:* Tek bir görüntü hata verirse (bozuk dosya, desteklenmeyen format) tüm `WhenAll` istisna fırlatır. İç `Task.Run`'ı try/catch ile sarabilir ve hata toleransı gerekiyorsa boş bir string ya da tanılayıcı mesaj döndürebilirsiniz.

## Adım 4: Önizleme Göster – **convert image to text C#** çıktısını doğrulayın

Hızlı bir önizleme, verileri başka bir yere kaydetmeye başlamadan OCR'nin çalıştığını doğrulamanıza yardımcı olur.

```csharp
// Step 5: Show a short preview of each result
for (int i = 0; i < ocrResults.Length; i++)
{
    string fileName = Path.GetFileName(imageFiles[i]);
    string preview = ocrResults[i].Length > 100
        ? ocrResults[i][..100] + "..."
        : ocrResults[i];
    Console.WriteLine($"{fileName}: {preview}");
}
```

Tipik konsol çıktısı şu şekildedir:

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
```

Eğer önizleme anlamsız karakterler gösteriyorsa, görüntü kalitesini iki kez kontrol edin veya ön işleme (ör. ikileştirme) düşünün – ancak çoğu temiz PNG için Aspose OCR ilk denemede doğru sonucu verir.

## Opsiyonel: Sonuçları CSV'ye Kaydedin – Gerçek Dünya Kullanım Durumu

Çoğu proje, çıkarılan metni yapılandırılmış bir formatta ihtiyaç duyar. Aşağıda dosya adını ve tam OCR metnini bir CSV dosyasına yazan küçük bir yardımcı bulunmaktadır.

```csharp
string csvPath = Path.Combine("YOUR_DIRECTORY", "ocr-results.csv");
using var writer = new StreamWriter(csvPath);
writer.WriteLine("FileName,ExtractedText");

for (int i = 0; i < imageFiles.Length; i++)
{
    string escaped = ocrResults[i].Replace("\"", "\"\"");
    writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
}
Console.WriteLine($"All results saved to {csvPath}");
```

Artık CSV'yi Excel, Power BI veya **read text from scanned images** bekleyen herhangi bir downstream sisteme aktarabilirsiniz.

## Sık Sorulan Sorular

**PNG'lerim çok büyük (5 MB'den fazla) olursa ne olur?**  
Aspose OCR büyük görüntüleri otomatik olarak alt örnek alarak bellek kullanımını makul tutar, ancak `engine.Image = ImageStream.FromFile(filePath).Resize(2000, 0);` ile genişliği 2000 px olarak sınırlayıp en boy oranını koruyarak manuel olarak yeniden boyutlandırabilirsiniz.

**Bunu Linux'ta çalıştırabilir miyim?**  
Evet. Aspose OCR çapraz platformdur; sadece yerel bağımlılıkların (`libgdiplus` gibi bazı dağıtımlarda) kurulu olduğundan emin olun.

**OCR dili varsayılan olarak İngilizce mi?**  
Doğru. Başka bir dile ihtiyacınız varsa, `engine.Language = OcrLanguage.French;` (veya desteklenen herhangi bir enum) şeklinde `Recognize()` çağırmadan önce ayarlayın.

**PNG içeren şifre korumalı PDF'leri nasıl ele alırım?**  
Önce PDF sayfalarını görüntülere dönüştürün (Aspose PDF veya başka bir kütüphane kullanarak), ardından bu PNG'leri aynı işlem hattına besleyin. **how to run OCR on images** prensibi değişmez.

## Tam Çalışan Örnek (Async Main)

Aşağıda bir konsol projesine kopyalayıp yapıştırabileceğiniz bağımsız bir program var. Yukarıdaki tüm parçaları ve giriş klasörünü doğrulayan küçük bir yardımcı içerir.

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;

class Program
{
    static async Task Main()
    {
        // -------------------------------------------------
        // 1️⃣ Locate PNGs – the heart of “extract text from png”
        // -------------------------------------------------
        const string folder = @"YOUR_DIRECTORY";   // <-- change this
        if (!Directory.Exists(folder))
        {
            Console.WriteLine($"Folder not found: {folder}");
            return;
        }

        string[] imageFiles = Directory.GetFiles(folder, "*.png");
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to do.");
            return;
        }

        // -------------------------------------------------
        // 2️⃣ Fire off OCR tasks – best way to “run OCR on images”
        // -------------------------------------------------
        var ocrTasks = new List<Task<string>>();
        foreach (var filePath in imageFiles)
        {
            ocrTasks.Add(Task.Run(() =>
            {
                var engine = new OcrEngine();
                engine.Image = ImageStream.FromFile(filePath);
                engine.Recognize();
                return engine.Text;
            }));
        }

        // -------------------------------------------------
        // 3️⃣ Await results
        // -------------------------------------------------
        string[] ocrResults = await Task.WhenAll(ocrTasks);

        // -------------------------------------------------
        // 4️⃣ Show previews
        // -------------------------------------------------
        for (int i = 0; i < ocrResults.Length; i++)
        {
            string fileName = Path.GetFileName(imageFiles[i]);
            string preview = ocrResults[i].Length > 100
                ? ocrResults[i][..100] + "..."
                : ocrResults[i];
            Console.WriteLine($"{fileName}: {preview}");
        }

        // -------------------------------------------------
        // 5️⃣ Optional: write CSV – perfect for “read text from scanned images”
        // -------------------------------------------------
        string csvPath = Path.Combine(folder, "ocr-results.csv");
        using var writer = new StreamWriter(csvPath);
        writer.WriteLine("FileName,ExtractedText");
        for (int i = 0; i < imageFiles.Length; i++)
        {
            string escaped = ocrResults[i].Replace("\"", "\"\"");
            writer.WriteLine($"\"{Path.GetFileName(imageFiles[i])}\",\"{escaped}\"");
        }

        Console.WriteLine($"✅ OCR complete – results saved to {csvPath}");
    }
}
```

**Beklenen çıktı** (iki PNG için örnek):

```
invoice-001.png: Invoice Number: 2025-07-14   Date: 07/14/2025   Total: $1,250.00...
receipt-202.png: Thank you for your purchase!   Order #12345   Amount: $89.99...
✅ OCR complete – results saved to C:\MyImages\ocr-results.csv
```

## Sonuç

C# kullanarak **PNG'den metin çıkarma** dosyaları için ihtiyacınız olan her şeyi ele aldık. Dosyaları bulmaktan, paralel OCR görevlerini başlatmaya, string'leri önizlemeye ve CSV'ye kaydetmeye kadar—bu rehber **convert image to text C#** senaryoları için üretim hazır bir desen sunar.  

Bir sonraki adıma hazırsanız, aynı işlem hattına JPEG veya TIFF dosyalarını da beslemeyi deneyin, farklı OCR dilleriyle deney yapın veya sonuçları bir arama indeksine bağlayarak **read text from scanned images** anında okuyun.  

Köşe durumları, performans ayarı veya lisanslama hakkında sorularınız mı var? Bir yorum bırakın ya da Aspose topluluğuna mesaj gönderin—iyi kodlamalar!

![PNG'den metin çıkarma örneği](extract-text-png.png "Aspose OCR kullanarak PNG'den metin çıkarma")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}