---
category: general
date: 2026-04-04
description: C#'ta Aspose.OCR ile toplu OCR nasıl yapılır. Görsellerden metin çıkarmayı,
  CSV özetlerini dışa aktarmayı ve toplu görüntü OCR'sini verimli bir şekilde yönetmeyi
  öğrenin.
draft: false
keywords:
- how to batch ocr
- extract text images
- how to export csv
- bulk image ocr
- batch ocr images
language: tr
og_description: Aspose.OCR ile C#’ta toplu OCR nasıl yapılır. Görsellerden metin çıkarma
  ve CSV özetleri dışa aktarma için tam çözümü edinin.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Tam Adım Adım Öğretici
tags:
- OCR
- C#
- Aspose
- Automation
title: C#'ta Toplu OCR Nasıl Yapılır – Büyük Miktarda Görüntü Metni Çıkarma İçin Tam
  Kılavuz
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-complete-guide-for-bulk-image-text-ext/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Toplu OCR Nasıl Yapılır – Tam Özellikli C# Öğreticisi

Hiç **toplu OCR** işlemini, her dosya için ayrı bir rutin yazmadan bir klasördeki tüm resimler için yapmayı düşündünüz mü? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—fatura işleme, taranmış kitapların arşivlenmesi veya makbuzların toplu dijitalleştirilmesi gibi—geliştiricilerin onlarca hatta binlerce görüntüden metin çıkarmak için hızlı ve güvenilir bir yola ihtiyacı vardır.  

Bu rehberde, Aspose.OCR kullanarak **toplu OCR nasıl yapılır**, **görüntülerden metin nasıl çıkarılır** ve **CSV özeti nasıl dışa aktarılır** gösteren, çalıştırmaya hazır tam bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir resim klasörünü alıp aranabilir metin dosyalarına dönüştüren ve işlemin bir CSV raporunu sağlayan tek bir C# programına sahip olacaksınız. Sır yok, sadece net kod ve pratik ipuçları.

## Öğrenecekleriniz

- Aspose.OCR motorunu İngilizce (veya desteklenen herhangi bir dil) için kurma.  
- Tek seferde bir klasördeki tüm görüntüleri işleme—toplu görüntü OCR’u için mükemmel.  
- Her OCR sonucunu bir `.txt` dosyası olarak kaydetme ve isteğe bağlı olarak her kaynak görüntünün adını ve çıkarılan metin uzunluğunu listeleyen bir CSV dosyası oluşturma.  
- Desteklenmeyen dosya türleri, boş klasörler ve Unicode karakterler gibi yaygın kenar durumlarını ele alma.  

**Önkoşullar** – .NET 6+ (veya .NET Framework 4.7.2+), Visual Studio 2022 veya tercih ettiğiniz herhangi bir IDE ve geçerli bir Aspose.OCR lisansı (deneme sürümü demo için yeterlidir) gerekir. Başka üçüncü‑taraf kütüphane gerekmez.

![how to batch ocr diagram](https://example.com/ocr-flow.png "how to batch ocr flow diagram")

## Adım 1: Aspose.OCR’u Yükleyin ve Yeni Bir Konsol Projesi Oluşturun

Başlamak için Aspose.OCR NuGet paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Visual Studio kullanıyorsanız proje üzerine sağ‑tıklayıp → *Manage NuGet Packages* → *Aspose.OCR* aratıp → yükleyebilirsiniz.

Yeni bir konsol uygulaması oluşturun (`dotnet new console -n BulkOcrDemo`) ve `Program.cs` dosyasını açın. Burası tüm kodlarımızın evi olacak.

## Adım 2: OCR Motorunu Başlatın – Doğru Dili Seçin

OCR motorunun hangi dili arayacağını bilmesi gerekir. İngilizce en yaygın olanıdır, ancak `Language.English` ifadesini değiştirerek İspanyolca, Fransızca vb. dillerle çalışabilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

// Step 2: Set up the OCR engine
OcrEngine ocrEngine = new OcrEngine
{
    // You can switch to Language.Spanish, Language.French, etc.
    Language = Language.English
};
```

**Neden önemli:** Dili belirtmek, motorun dil‑özel sözlük ve karakter setlerini uygulayabilmesi sayesinde doğruluğu artırır. Bunu atladığınızda, karakterleri yanlış yorumlayabilecek genel bir model elde edersiniz.

## Adım 3: Kaynak, Çıktı ve İsteğe Bağlı CSV Yollarını Tanımlayın

Üç klasöre ihtiyacımız var:

| Yol | Amaç |
|------|---------|
| `sourceFolder` | Orijinal görüntülerin bulunduğu yer. |
| `outputFolder` | Her OCR sonucunun (`.txt`) kaydedileceği yer. |
| `csvSummaryPath` | (İsteğe bağlı) Her görüntü adını ve çıkarılan metin uzunluğunu kaydeden bir CSV dosyası. |

```csharp
// Step 3: Folder locations – update these to match your environment
string sourceFolder = @"C:\OcrDemo\Images\Bulk";
string outputFolder = @"C:\OcrDemo\Output\BulkResults";
string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional
```

> **İpucu:** Platformlar arası uyumluluk için `Path.Combine` kullanın; doğru dizin ayırıcıyı otomatik ekler.

## Adım 4: Toplu İşlemciyi Çalıştırın

Aspose.OCR, işi kolaylaştıran bir `BatchProcessor` ile gelir. Desteklenen her görüntüyü (`.png`, `.jpg`, `.tif` vb.) tarar, OCR uygular ve sonucu yazar.

```csharp
// Step 4: Process the entire folder
BatchProcessor.ProcessFolder(
    sourceFolder: sourceFolder,
    outputFolder: outputFolder,
    engine: ocrEngine,
    csvSummaryPath: csvSummaryPath);
```

### Arkada Ne Oluyor?

1. **Dosya keşfi** – İşlemci `sourceFolder` içinde görüntü dosyalarını tarar.  
2. **OCR yürütmesi** – Her görüntü `ocrEngine`e beslenir.  
3. **Metin kaydetme** – Tanınan metin, aynı temel ada sahip bir `.txt` dosyasına `outputFolder` içinde yazılır.  
4. **CSV kaydı** – `csvSummaryPath` sağlanmışsa, işlemci şu satırı ekler: `ImageName,CharactersExtracted,ProcessingTimeMs`.  

## Adım 5: Hata Yönetimi ve Kenar‑Durum Desteği Ekleyin

Sağlam bir toplu iş, eksik dosyalar, desteklenmeyen formatlar ve boş dizinlerle başa çıkabilmelidir. İşlem çağrısını bir `try/catch` bloğuna sarın ve girdileri önce doğrulayın.

```csharp
try
{
    // Validate folders
    if (!Directory.Exists(sourceFolder))
        throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

    Directory.CreateDirectory(outputFolder); // ensures output exists

    // Optional: clean previous CSV
    if (File.Exists(csvSummaryPath))
        File.Delete(csvSummaryPath);

    // Run the batch
    BatchProcessor.ProcessFolder(
        sourceFolder: sourceFolder,
        outputFolder: outputFolder,
        engine: ocrEngine,
        csvSummaryPath: csvSummaryPath);

    Console.WriteLine("✅ Batch OCR completed successfully!");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"❌ An error occurred: {ex.Message}");
}
```

**Neden eklenmeli?** Doğrulama yapılmazsa program sessizce başarısız olabilir, boş bir çıktı klasörü bırakabilir ve nedenini size söylemez. Açık mesajlar hata ayıklamayı sorunsuz hâle getirir.

## Adım 6: Sonuçları Doğrulayın – Ne Beklemelisiniz

Çalışma tamamlandığında `outputFolder`ı açın. Her görüntü için bir `.txt` dosyası görmelisiniz:

```
C:\OcrDemo\Output\BulkResults\invoice_001.txt
C:\OcrDemo\Output\BulkResults\receipt_2023-03-15.txt
...
```

Her dosya, ham OCR çıktısını içerir—arama indekslerine, veri tabanlarına veya daha ileri NLP boru hatlarına besleyebileceğiniz düz metin.

`csvSummaryPath` sağladıysanız `summary.csv` dosyasını açın. Şuna benzer bir içerik göreceksiniz:

```
ImageName,CharactersExtracted,ProcessingTimeMs
invoice_001.png,1245,312
receipt_2023-03-15.jpg,378,98
...
```

CSV, raporlar oluşturmayı, anormal derecede kısa sonuçları (muhtemel tarama hataları) tespit etmeyi veya metrikleri izleme panolarına beslemeyi çok kolaylaştırır.

## Adım 7: Çözümü Genişletin – Yaygın Varyasyonlar

### 7.1 Çıktı Formatını Değiştirin

Düz `.txt` yerine PDF veya JSON isteyebilirsiniz. `BatchProcessor` size özel bir geri çağırma (callback) sağlamanıza izin verir:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    (imagePath, ocrResult) =>
    {
        // Example: save as JSON
        var json = System.Text.Json.JsonSerializer.Serialize(new { Text = ocrResult.Text });
        string jsonPath = Path.ChangeExtension(Path.Combine(outputFolder,
                              Path.GetFileNameWithoutExtension(imagePath)), ".json");
        File.WriteAllText(jsonPath, json);
    });
```

### 7.2 Birden Çok Dil İşleyin

Klasörünüz karışık‑dilli belgeler içeriyorsa, görüntü başına dili algılayabilir veya iki geçiş yapabilirsiniz:

```csharp
ocrEngine.Language = Language.Spanish; // first pass
BatchProcessor.ProcessFolder(...);
ocrEngine.Language = Language.English; // second pass
BatchProcessor.ProcessFolder(...);
```

### 7.3 Bozuk Dosyaları Zarifçe Atlayın

Döngü içinde bir filtre ekleyin (veya bir koşul kabul eden aşırı yüklemeyi kullanın) ve istisna fırlatan dosyaları yok sayın:

```csharp
BatchProcessor.ProcessFolder(
    sourceFolder,
    outputFolder,
    ocrEngine,
    csvSummaryPath,
    filter: path => !Path.GetFileName(path).StartsWith("ignore_"));
```

## Tam Çalışan Örnek

Aşağıda yeni bir konsol projesine kopyalayıp‑yapıştırabileceğiniz tam `Program.cs` bulunmaktadır. Klasör yollarını kendi ortamınıza göre değiştirin.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BulkOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine – set language to English
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English
            };

            // 2️⃣ Define folders – adjust these for your environment
            string sourceFolder = @"C:\OcrDemo\Images\Bulk";
            string outputFolder = @"C:\OcrDemo\Output\BulkResults";
            string csvSummaryPath = Path.Combine(outputFolder, "summary.csv"); // optional

            try
            {
                // 3️⃣ Validate folders
                if (!Directory.Exists(sourceFolder))
                    throw new DirectoryNotFoundException($"Source folder not found: {sourceFolder}");

                Directory.CreateDirectory(outputFolder); // creates if missing

                // 4️⃣ Clean previous CSV (optional)
                if (File.Exists(csvSummaryPath))
                    File.Delete(csvSummaryPath);

                // 5️⃣ Run the batch OCR
                BatchProcessor.ProcessFolder(
                    sourceFolder: sourceFolder,
                    outputFolder: outputFolder,
                    engine: ocrEngine,
                    csvSummaryPath: csvSummaryPath);

                Console.WriteLine("✅ Batch OCR completed successfully!");
                Console.WriteLine($"📂 Text files are in: {outputFolder}");
                Console.WriteLine($"📄 CSV summary (if requested) at: {csvSummaryPath}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"❌ An error occurred during batch OCR: {ex.Message}");
            }
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
✅ Batch OCR completed successfully!
📂 Text files are in: C:\OcrDemo\Output\BulkResults
📄 CSV summary (if requested) at: C:\OcrDemo\Output\BulkResults\summary.csv
```

Oluşturulan `.txt` dosyalarından birini açın; çıkarılan metni görmeli ve daha ileri işleme hazır olmalıdır.

## Sık Sorulan Sorular

**PDF girişleriyle çalışır mı?**  
Aspose.OCR, PDF sayfalarını önce görüntülere dönüştürürseniz (ör. Aspose.PDF kullanarak) işleyebilir. Toplu işlemci yalnızca raster görüntü formatlarını arar.

**10.000 görüntüyü işlemem gerekirse?**  
Yerleşik `BatchProcessor` her dosyayı tek tek akış halinde işler, böylece bellek kullanımı düşük kalır. Çok büyük iş yükleri için alt klasörleri paralel işleyebilirsiniz, ancak OCR CPU‑ağır bir işlemdir—makinenizin çekirdek sayısına dikkat edin.

**OCR doğruluk ayarlarını değiştirebilir miyim?**  
Evet. `ocrEngine` `Resolution` ve `PreprocessOptions` gibi özellikler sunar. Bunları ayarlamak düşük kalite taramalarda sonuçları iyileştirebilir, ancak hız pahasına olur.

**Aspose.OCR’u üretimde nasıl lisanslarım?**  
Lisans dosyanızı (`Aspose.OCR.lic`) çalıştırılabilir dizine koyun ve başlangıçta yükleyin:

```csharp
var license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Sonuç

Artık C# kullanarak **toplu OCR nasıl yapılır** konusunda **tam, üretime hazır bir çözüme** sahipsiniz. Bu öğreticide Aspose.OCR’un kurulumu, motorun başlatılması, bir klasörün tamamen işlenmesi ve CSV özetinin dışa aktarılması gibi tüm adımları ele aldık.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}