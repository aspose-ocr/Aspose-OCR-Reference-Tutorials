---
category: general
date: 2026-03-13
description: Aspose.OCR kullanarak tiff dosyalarından metin çıkarmayı öğrenirken,
  toplu OCR'ı hızlı ve güvenilir bir şekilde nasıl yapacağınızı öğrenin. Bu adım adım
  öğreticiyi izleyin.
draft: false
keywords:
- how to batch OCR
- extract text from tiff
- Aspose OCR batch processing
- C# OCR automation
- GPU accelerated OCR
language: tr
og_description: C#'ta toplu OCR yapmayı ve Aspose.OCR ile tiff dosyalarından metin
  çıkarmayı öğrenin. Bu rehber kurulum, kod ve en iyi uygulama ipuçlarını kapsar.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Tam Programlama Rehberi
tags:
- OCR
- C#
- Aspose
- Batch processing
title: C#'ta Toplu OCR Nasıl Yapılır – Tam Programlama Rehberi
url: /tr/net/ocr-optimization/how-to-batch-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta toplu OCR nasıl yapılır – Tam Programlama Kılavuzu

Hiç **toplu OCR nasıl yapılır** diye bir dağ gibi taranmış faturayı, her dosya için ayrı bir betik yazmadan işleyebileceğinizi merak ettiniz mi? Tek başınıza değilsiniz. Birçok gerçek‑dünya projesinde sorun OCR doğruluğu değil, genellikle TIFF olan görüntülerin devasa miktarıdır; bu görüntülerin aranabilir metne dönüştürülmesi gerekir.  

Bu öğreticide **toplu OCR nasıl yapılır** Aspose.OCR’nin `BatchProcessor` sınıfı ile gösterilirken, aynı zamanda **tiff'ten metin çıkarma** tek bir temiz çalışmada nasıl yapılır da öğreneceksiniz. Sonunda, tüm bir klasörü işleyen, isteğe bağlı GPU hızlandırmasından yararlanan ve düz metin sonuçlarını istediğiniz yere bırakan hazır bir konsol uygulamanız olacak.

## Gereksinimler

- **.NET 6+** (veya klasik çalışma zamanı tercih ediyorsanız .NET Framework 4.7.2)  
- **Aspose.OCR for .NET** – `dotnet add package Aspose.OCR` komutuyla NuGet paketini alabilirsiniz.  
- Okumak istediğiniz **TIFF** görüntülerinin bulunduğu bir klasör (öğreticide örnek olarak `Invoices` klasörü kullanılmıştır).  
- İsteğe bağlı: Hızı artırmak istiyorsanız DirectX 11 veya CUDA destekli bir GPU.  

Ek bir servis, bulut anahtarı yok—sadece yerel bir C# projesi ve Aspose kütüphanesi yeterli.

## Adım 1: Projeyi Oluşturun ve Aspose.OCR’yi Yükleyin

İlk olarak bir konsol uygulaması oluşturun.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Windows kullanıyorsanız ve GPU hızlandırması planlıyorsanız, en yeni grafik sürücüsünün yüklü olduğundan emin olun. Aksi takdirde `UseGpu = true` bayrağı otomatik olarak CPU’ya geçiş yapar.

## Adım 2: BatchProcessor Yapılandırmasını Oluşturun

Şimdi `BatchProcessor`’ı yapılandıracağız. Bu, **toplu OCR nasıl yapılır** sorusunun kalbidir—Aspose’a hangi dili beklediğinizi, hangi ön‑işleme filtrelerini uygulayacağını ve GPU kullanıp kullanmayacağını söylersiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 2: Configure the batch processor
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                // Primary language – English works for most invoices
                Language = Language.English,

                // Set to true if you have a compatible GPU; otherwise false
                UseGpu = true,

                // Optional pre‑processing to improve OCR accuracy
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),   // straightens tilted scans
                    new DespeckleFilter() // removes speckles and noise
                }
            };
```

**Bu ayarlar neden?**  
- `Language = Language.English` motorun İngilizce dil modelini kullanmasını sağlar; bu, genel modele göre çok daha yüksek doğruluk verir.  
- `UseGpu`, uygun bir GPU’da işleme süresini yarıya indirebilir, ancak bir dizüstü bilgisayarınızda GPU yoksa `false` bırakmak güvenlidir.  
- Filtre ardışıklığı, bir insanın yapacağı gibi: sayfayı düzleştirir ve lekeleri temizler, ardından OCR motoruna verir.

## Adım 3: İşlemciyi TIFF Klasörünüze Yönlendirin

**toplu OCR nasıl yapılır** sürecinin bir sonraki adımı, kütüphaneye kaynak dosyaların nerede olduğunu söylemektir. Joker karakterler desteklenir, böylece tek seferde tüm `.tif` dosyalarını alabilirsiniz.

```csharp
            // -------------------------------------------------
            // Step 3: Add the folder containing TIFF images
            // -------------------------------------------------
            // Replace YOUR_DIRECTORY with the actual path on your machine
            batchProcessor.AddFolder(@"C:\Data\Invoices", "*.tif");
```

> **Köşe durumu:** Görüntüleriniz karışık uzantılara sahipse (`.tiff`, `.tif`, `.png`), `AddFolder` metodunu birden çok kez çağırın ya da `*.*` kullanıp daha sonra kod içinde filtreleyin.

## Adım 4: OCR Sonuçlarının Nereye Gideceğini Belirleyin

“Çıkarılan metin nereye kaydedilir?” diye merak edebilirsiniz. Bu, **toplu OCR nasıl yapılır** sorusunun üçüncü ayağıdır—çıktı konumunu ve formatını tanımlamak. Düz metin dosyalarını orijinal dosyalarla aynı klasöre yan yana koyacağız.

```csharp
            // -------------------------------------------------
            // Step 4: Define output folder and format
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;
```

Eğer düz metin yerine JSON veya XML isterseniz, sadece `OutputFormat.PlainText` yerine `OutputFormat.Json` ya da `OutputFormat.Xml` kullanın. Kütüphane dönüşümü sizin için halleder.

## Adım 5: Toplu İşi Çalıştırın ve Sonuçları Raporlayın

Son olarak işi başlatın. `Execute` metodu, tüm dosyalar işlenene kadar bloklanır; ardından `ProcessedCount` ile başarıyı kontrol edebilirsiniz.

```csharp
            // -------------------------------------------------
            // Step 5: Execute the batch job
            // -------------------------------------------------
            batchProcessor.Execute();

            // Simple verification output
            Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
            Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
        }
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda konsol şu şekilde bir şey yazdırır:

```
Batch completed. Processed files: 42
Check C:\Data\Output for .txt files containing extracted text.
```

`Output` klasöründe, her kaynak TIFF için bir `.txt` dosyası bulacaksınız; dosya adı orijinal görüntünün adıyla aynı olacaktır (ör. `Invoice_001.txt`). Herhangi bir dosyayı açtığınızda ham OCR metnini göreceksiniz—bu, bir arama indeksi ya da sonraki veri‑çıkarma boru hattına beslemek için mükemmeldir.

## Yaygın Sorunlarla Baş Etme

### 1. GPU Kullanılamıyor

`UseGpu = true` ancak uyumlu bir cihaz bulunamazsa, Aspose sessizce CPU’ya geçer. Bunu açıkça yakalamak isterseniz `DeviceNotFoundException` istisnasını tutabilirsiniz:

```csharp
try
{
    batchProcessor.Execute();
}
catch (DeviceNotFoundException)
{
    Console.WriteLine("GPU not detected – switching to CPU mode.");
    batchProcessor.UseGpu = false;
    batchProcessor.Execute();
}
```

### 2. Aynı Klasörde TIFF Olmayan Dosyalar

Karışık bir klasörünüz varsa, programatik olarak filtreleyin:

```csharp
var tiffFiles = Directory.GetFiles(@"C:\Data\Invoices", "*.*")
                         .Where(f => f.EndsWith(".tif", StringComparison.OrdinalIgnoreCase) ||
                                     f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));

foreach (var file in tiffFiles)
    batchProcessor.AddFile(file);
```

### 3. Belleği Aşan Büyük Dosyalar

Devasa çok‑sayfalı TIFF’ler için akış (streaming) özelliğini etkinleştirin:

```csharp
batchProcessor.EnableMemoryManagement = true; // reduces RAM footprint
```

## **tiff'ten metin çıkarma** İçin Daha İyi Doğruluk İçin Pro İpuçları

- **Çözünürlük önemlidir** – 300 dpi veya daha yüksek hedefleyin. Daha düşük çözünürlükte OCR motoru karakterleri kaçırabilir.  
- **Renk vs. Gri Ton** – Renkli taramaları OCR’dan önce gri tonlamaya çevirin; `DeskewFilter` zaten bunu arka planda yapar, ancak ekstra hız için `ColorDepthReductionFilter` ekleyebilirsiniz.  
- **Son‑işleme** – Düz metin elde ettikten sonra bir imla denetleyicisi ya da regex temizliği çalıştırarak yaygın OCR hatalarını (ör. “0” ile “O” karışıklığı) düzeltin.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda derleyip çalıştırabileceğiniz tüm program yer alıyor. Yer tutucu yolları kendi dizinlerinizle değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
using System.Linq;

namespace BatchOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Configure the batch processor (how to batch OCR)
            // -------------------------------------------------
            BatchProcessor batchProcessor = new BatchProcessor
            {
                Language = Language.English,
                UseGpu = true, // set false if no GPU
                PreProcessingFilters = new FilterPipeline
                {
                    new DeskewFilter(),
                    new DespeckleFilter()
                },
                EnableMemoryManagement = true // helps with huge TIFFs
            };

            // -------------------------------------------------
            // Add source TIFF files
            // -------------------------------------------------
            string sourceFolder = @"C:\Data\Invoices";
            batchProcessor.AddFolder(sourceFolder, "*.tif");

            // -------------------------------------------------
            // Optional: add only TIFFs if folder contains other images
            // -------------------------------------------------
            var extraTiffs = Directory.GetFiles(sourceFolder, "*.*")
                                      .Where(f => f.EndsWith(".tiff", StringComparison.OrdinalIgnoreCase));
            foreach (var file in extraTiffs)
                batchProcessor.AddFile(file);

            // -------------------------------------------------
            // Define where results go
            // -------------------------------------------------
            batchProcessor.OutputFolder = @"C:\Data\Output";
            batchProcessor.OutputFormat = OutputFormat.PlainText;

            // -------------------------------------------------
            // Execute the batch job
            // -------------------------------------------------
            try
            {
                batchProcessor.Execute();
                Console.WriteLine($"\nBatch completed. Processed files: {batchProcessor.ProcessedCount}");
                Console.WriteLine("Check C:\\Data\\Output for .txt files containing extracted text.");
            }
            catch (DeviceNotFoundException)
            {
                Console.WriteLine("GPU not detected – falling back to CPU.");
                batchProcessor.UseGpu = false;
                batchProcessor.Execute();
                Console.WriteLine($"Batch completed (CPU). Processed files: {batchProcessor.ProcessedCount}");
            }
        }
    }
}
```

Derleyin ve çalıştırın:

```bash
dotnet run
```

Artık düzenli bir `.txt` dosya setiniz olacak—her biri **tiff'ten metin çıkarma** işleminin tam otomatik bir toplu süreç sonucudur.

## Sonuç

C#’ta **toplu OCR nasıl yapılır** sorusunu baştan sona ele aldık ve **tiff'ten metin çıkarma** dosyalarını verimli bir şekilde işlemek için ihtiyacınız olan her şeyi kapsadık. Özetle:

1. Tekrarlayan döngüler yazmaktan kaçınmak için Aspose.OCR’nin `BatchProcessor` ını kullanın.  
2. Daha yüksek doğruluk için ön‑işleme filtrelerini (deskew, despeckle) etkinleştirin.  
3. Mümkün olduğunda GPU hızlandırmasından yararlanın, ancak her zaman bir CPU geri dönüşü bulundurun.  
4. Sonuçları öngörülebilir bir klasör yapısında saklayın, böylece sonraki işler otomatik olarak bunları alabilir.

Bundan sonra şunları keşfedebilirsiniz:

- Düz metni bir **arama indeksi** (ör. Elasticsearch) içine besleyerek faturaları aranabilir hâle getirmek.  
- Çıktıyı **JSON** formatına dönüştürüp satır kalemlerini çıkaran bir makine‑öğrenme modeline beslemek.  
- Bozuk TIFF’ler veya izin sorunları için **hata yönetimi** eklemek.

Deneyin,

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}