---
category: general
date: 2026-03-21
description: C#'ta toplu OCR nasıl basitleştirilir—görüntülerden metin çıkarmayı,
  görüntüleri metne dönüştürmeyi ve dil ayarlarıyla OCR'yi metin olarak kaydetmeyi
  öğrenin.
draft: false
keywords:
- how to batch OCR
- extract text from images
- convert images to text
- save OCR as text
- set OCR language
language: tr
og_description: C#'ta toplu OCR nasıl yapılır, görüntülerden metin çıkarmanıza, görüntüleri
  metne dönüştürmenize ve OCR'yi metin olarak kaydetmenize, OCR dilini kolayca ayarlamanıza
  olanak tanır.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Hızlı Kılavuz
tags:
- OCR
- C#
- Aspose
title: C#'ta Toplu OCR Nasıl Yapılır – Görsellerden Metni Hızlıca Çıkar
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-fast/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Nasıl Yapılır – Görsellerden Metin Hızlıca Çıkar

Yüzlerce resmin bir klasörde biriktiği zaman **toplu OCR nasıl yapılır** diye hiç merak ettiniz mi? Yalnız değilsiniz—geliştiriciler sürekli olarak her dosya için bir döngü yazmadan görsellerden metin nasıl çıkarılır sorusunu soruyor.  İyi haber, Aspose.OCR size sadece birkaç C# satırıyla **görselleri metne dönüştürmek** için temiz, paralel‑hazır bir yol sunuyor.  

Bu öğreticide, **OCR'yi metin olarak kaydetme**, doğru dili seçme ve hızı artırmak için paralel işleme nasıl yapılır gösteren tam, çalıştırmaya hazır bir örnek üzerinden ilerleyeceğiz.  Sonunda, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir çözüm elde edeceksiniz.

## Gerekenler

- .NET 6 veya daha yeni (API .NET Core ve .NET Framework ile çalışır)
- Aspose.OCR for .NET (NuGet paketi `Aspose.OCR`)
- İşlemek istediğiniz resimlerin bulunduğu klasör (PNG, JPEG, TIFF, vb.)
- Paralel programlama hakkında biraz merak (opsiyonel, ama faydalı)

Ekstra hizmet yok, bulut anahtarı yok—sadece yerel olarak çalışan saf C# kodu.

---

![how to batch OCR workflow](placeholder.png){alt="toplu OCR iş akışı diyagramı"}

## Adım 1: Projeyi Kurun ve Aspose.OCR'yi Yükleyin

İlk olarak bir console uygulaması oluşturun (ya da mevcut birini kullanın) ve Aspose.OCR paketini ekleyin:

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **İpucu:** Visual Studio kullanıyorsanız, projeye sağ‑tıklayın → *Manage NuGet Packages* → *Aspose.OCR* aratın ve en son kararlı sürümü yükleyin.

Bu, `OcrBatchProcessor`, `OcrEngineSettings` ve `Language` enum’una erişmenizi sağlar.

## Adım 2: Giriş ve Çıkış Klasörlerini Tanımlayın

Toplu işlemci, kaynak görsellerin nerede olduğunu ve çıkarılan metin dosyalarının nereye yazılacağını bilmelidir.  Yolları mutlak ya da proje köküne göre göreceli tutun—kodunuzu çalıştırmadan önce klasörlerin var olduğundan emin olun.

```csharp
var inputPath  = @"C:\MyImages\BatchInput";
var outputPath = @"C:\MyImages\BatchResults";

// Ensure the output directory exists
if (!Directory.Exists(outputPath))
    Directory.CreateDirectory(outputPath);
```

> **Neden önemli:** Çıkış klasörü yoksa işlemci bir istisna fırlatır ve tüm toplu işlemi keser. Önceden oluşturmak sorunsuz bir çalışmayı garantiler.

## Adım 3: OCR Ayarlarını Yapılandırın (dil dahil)

İşte **OCR dilini** tüm toplu işlem için ayarladığınız yer.  Aspose.OCR onlarca dili destekler; İngilizce varsayılan, ancak `Language` enum değerini değiştirerek Fransızca, İspanyolca vb. diller seçebilirsiniz.

```csharp
var ocrSettings = new OcrEngineSettings
{
    Language = Language.English   // Change to Language.French, Language.Spanish, etc.
};
```

Farklı görseller için farklı diller işlemeniz gerekirse, bu ayarı dosya bazında daha sonra geçersiz kılabilirsiniz—daha fazla bilgi ileride.

## Adım 4: `OcrBatchProcessor` Nesnesini Oluşturun

Şimdi her şeyi bir araya getiriyoruz.  `OcrBatchProcessor`, giriş klasörünü, çıkış klasörünü, çıktı formatını, paralel seçenekleri ve az önce oluşturduğumuz ortak ayarları belirlemenizi sağlar.

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System.Threading.Tasks;

var batch = new OcrBatchProcessor
{
    InputFolder   = inputPath,
    OutputFolder  = outputPath,
    OutputFormat  = OcrOutputFormat.PlainText, // **save OCR as text** in .txt files
    ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 }, // up to 4 threads
    Settings = ocrSettings
};
```

> **Neden paralellik?**  Onlarca ya da yüzlerce görseliniz olduğunda, tek tek işlemek acı verici derecede yavaştır. `MaxDegreeOfParallelism` değerini 4 olarak ayarlamak, çalışma zamanının aynı anda dört CPU çekirdeğini kullanmasını sağlar ve tipik bir iş istasyonunda toplam süreyi büyük ölçüde azaltır.

## Adım 5: Toplu İşlemi Çalıştırın

İşlemci yapılandırıldıktan sonra yürütme tek bir metod çağrısıdır.  Kütüphane dosya taramasını, OCR’u ve sonuçların yazılmasını otomatik olarak halleder.

```csharp
batch.Execute();
Console.WriteLine("Batch OCR completed.");
```

Konsol *“Batch OCR completed.”* mesajını verdiğinde, `BatchResults` içinde her orijinal görselin yanına bir `.txt` dosyası bulacaksınız.  Her metin dosyası, kaynak görselden çıkarılan ham karakterleri içerir—**görsellerden metin çıkarma** için tam olarak ihtiyacınız olan şey.

### Beklenen Çıktı

```
C:\MyImages\BatchResults\image1.txt
C:\MyImages\BatchResults\image2.txt
...
```

Bu dosyalardan birini açtığınızda, görsel içeriğinin düz metin temsilini göreceksiniz.

## Adım 6: Sonuçları Doğrulayın (Opsiyonel)

Birkaç dosyayı iki kez kontrol etmek, OCR’un beklendiği gibi çalıştığından emin olmak için iyi bir alışkanlıktır.  Hızlı bir yol, her oluşturulan dosyanın ilk satırını okuyup konsola yazdırmaktır:

```csharp
foreach (var txtFile in Directory.GetFiles(outputPath, "*.txt"))
{
    var firstLine = File.ReadLines(txtFile).FirstOrDefault();
    Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
}
```

Eğer bozuk karakterler görürseniz, `Language` ayarını değiştirmeyi ya da görüntü kalitesini (ör. DPI artırma, gri tonlamaya çevirme) ayarlamayı düşünün.

## İleri Düzey Varyasyonlar ve Kenar Durumları

### 1. Dosya Başına Dil Geçersiz Kılmaları
Bazen bir toplu işlem çok dilli belgeler içerir.  Her görsel adını inceleyip anlık olarak bir dil atayabilirsiniz:

```csharp
batch.Settings = new OcrEngineSettings(); // default settings

batch.FileProcessing += (sender, args) =>
{
    if (args.FileName.Contains("_fr"))
        args.Settings.Language = Language.French;
    else if (args.FileName.Contains("_es"))
        args.Settings.Language = Language.Spanish;
    // otherwise keep the default (English)
};
```

### 2. Farklı Çıktı Formatları
Düz metin yerine aranabilir PDF’lere ihtiyacınız varsa, `OutputFormat` değerini değiştirin:

```csharp
batch.OutputFormat = OcrOutputFormat.SearchablePdf;
```

Bu, **görselleri metne dönüştürür** ve PDF konteyneri içinde orijinal düzeni korur.

### 3. Büyük Görselleri İşleme
Çok yüksek çözünürlüklü görseller bellek tüketimini artırabilir.  İşlemi hafif tutmak için görüntü küçültmeyi (down‑sampling) etkinleştirin:

```csharp
batch.Settings.Dpi = 300; // lowers internal processing DPI
```

### 4. Hata Günlüğü
Okunamayan dosyalar için işlemci istisna fırlatır.  `Execute` metodunu try/catch bloğuna alıp sorunlu dosya adlarını kaydedin:

```csharp
try
{
    batch.Execute();
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed on {ex.Data["FileName"]}: {ex.Message}");
}
```

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, kopyala‑yapıştır‑hazır tam program aşağıdadır:

```csharp
using Aspose.OCR.Batch;
using Aspose.OCR.Settings;
using System;
using System.IO;
using System.Linq;
using System.Threading.Tasks;

class Program
{
    static void Main()
    {
        // 1️⃣ Input & output locations
        var inputFolder  = @"C:\MyImages\BatchInput";
        var outputFolder = @"C:\MyImages\BatchResults";

        if (!Directory.Exists(outputFolder))
            Directory.CreateDirectory(outputFolder);

        // 2️⃣ OCR settings – set OCR language
        var ocrSettings = new OcrEngineSettings
        {
            Language = Language.English // change as needed
        };

        // 3️⃣ Configure the batch processor
        var batch = new OcrBatchProcessor
        {
            InputFolder    = inputFolder,
            OutputFolder   = outputFolder,
            OutputFormat   = OcrOutputFormat.PlainText, // **save OCR as text**
            ParallelOptions = new ParallelOptions { MaxDegreeOfParallelism = 4 },
            Settings       = ocrSettings
        };

        // 4️⃣ Run the batch job
        batch.Execute();

        // 5️⃣ Confirmation message
        Console.WriteLine("Batch OCR completed.");

        // 6️⃣ (Optional) Quick verification of a few results
        foreach (var txtFile in Directory.GetFiles(outputFolder, "*.txt").Take(5))
        {
            var firstLine = File.ReadLines(txtFile).FirstOrDefault();
            Console.WriteLine($"{Path.GetFileName(txtFile)} → {firstLine}");
        }
    }
}
```

Bunu `Program.cs` olarak kaydedin, projeyi derleyin ve `dotnet run` komutunu çalıştırın.  Konsolda tamamlandığını belirten bir çıktı göreceksiniz, ardından çıkarılan metnin kısa bir ön izlemesi görüntülenecek.

---

## Sonuç

Aspose.OCR kullanarak C#’ta **toplu OCR** nasıl yapılır, **görsellerden metin çıkarma**, **görselleri metne dönüştürme** ve **OCR'yi metin olarak kaydetme** konularını, içeriğinize uygun **OCR dili ayarlama** ile gösterdik.  Örnek tamamen işlevsel, hız için paralel işleme içeriyor ve dosya bazında dil geçersiz kılmaları ya da PDF çıktısı gibi ileri senaryolar için kancalar sunuyor.

Bir sonraki adıma hazır mısınız? `OcrOutputFormat.PlainText` yerine `SearchablePdf` kullanarak aranabilir PDF’ler üretmenin ne kadar kolay olduğunu deneyin.  Ya da çok çekirdekli bir makinede her bir milisaniyeyi sıkıştırmak için farklı `MaxDegreeOfParallelism` değerleriyle oynayın.

Sorun yaşarsanız, klasör yollarını iki kez kontrol edin, görsellerin okunabilir olduğundan emin olun ve dil enum’unun resimlerinizdeki metinle eşleştiğini doğrulayın.  İyi kodlamalar, OCR toplularınız hızlı ve doğru olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}