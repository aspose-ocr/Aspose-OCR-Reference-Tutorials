---
category: general
date: 2026-02-19
description: Aspose.OCR ile C#'ta toplu OCR nasıl yapılır öğrenin. Bu kılavuz, görüntülerden
  metin çıkarmayı ve görüntüleri verimli bir şekilde txt'ye dönüştürmeyi gösterir.
draft: false
keywords:
- how to batch ocr
- extract text from images
- convert images to txt
- Aspose OCR batch processing
- C# image to text conversion
language: tr
og_description: C#'ta Aspose.OCR ile toplu OCR nasıl yapılır. Görüntülerden metin
  çıkarın ve birkaç kolay adımda görüntüleri txt'ye dönüştürün.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Hızlı Görüntüden Metne Dönüşüm
tags:
- OCR
- C#
- Aspose
title: C#'ta Toplu OCR Nasıl Yapılır – Görsellerden Metni Hızlıca Çıkarın
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-images-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Nasıl Yapılır – Tam Adım‑Adım Kılavuz

Hiç **bir klasördeki tüm resimleri toplu olarak OCR** yapmanın, her dosya için ayrı bir program yazmadan nasıl mümkün olduğunu merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, onlarca—hatta binlerce—tarama sayfası, fiş veya ekran görüntüsünden metin çıkarmaları gerektiğinde bir çıkmaza giriyor. İyi haber? Aspose.OCR ile tüm süreci otomatikleştirebilir, **resimlerden metin çıkarabilir** ve **resimleri txt'ye dönüştürebilirsiniz** sadece birkaç satır kodla.

Bu öğreticide, bir OCR toplu işlemcisini nasıl kuracağınızı, ön işleme ayarlarını nasıl yapacağınızı, paralellik yönetimini nasıl ele alacağınızı ve her sonucu bir `.txt` dosyasına nasıl yazacağınızı gösteren, çalıştırmaya hazır tam bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir konsol uygulamanız olacak.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework'te de çalışır)
- Aspose.OCR for .NET NuGet paketi (`Aspose.OCR`)  
- İşlemek istediğiniz görüntü dosyalarıyla dolu bir klasör (`.png`, `.jpg` vb.)
- Makul bir RAM miktarı; demo 4 paralel iş parçacığı kullanıyor ancak ihtiyaca göre ayarlayabilirsiniz

Harici hizmetler, gizli yapılandırma dosyaları yok—sadece bugün derleyip çalıştırabileceğiniz saf C# kodu.

![Diagram illustrating how to batch ocr processing flow](/images/how-to-batch-ocr-flow.png "how to batch ocr flow diagram")

## Adım 1: Aspose.OCR'ı Yükleyin ve Projeyi Hazırlayın

İlk olarak, Aspose.OCR paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Neden önemli: Aspose.OCR OCR motorunu, dil verilerini ve ön işleme yardımcılarını içinde barındırır, böylece üçüncü‑taraf ikili dosyalara ihtiyacınız olmaz. Paket yüklendikten sonra yeni bir konsol uygulaması oluşturun (veya mevcut birine kodu ekleyin) ve gerekli ad alanlarını içe aktarın:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;
```

Bu `using` ifadeleri, toplu işlemci sınıflarına ve kullanışlı I/O yardımcılarına erişmenizi sağlar.

## Adım 2: OCR Toplu İşlemcisini Yapılandırın

Şimdi `OcrBatchProcessor` nesnesini oluşturup hangi dili arayacağını, görüntüleri nasıl temizleyeceğini ve kaç iş parçacığıyla paralel çalışacağını belirleyeceğiz. Bu, **toplu OCR nasıl yapılır** sorusunun verimli cevabıdır.

```csharp
// Step 2: Create and configure the OCR batch processor
var ocrBatch = new OcrBatchProcessor
{
    // Language selection – English is the most common, but you can change it
    Language = Language.English,

    // Preprocessing improves accuracy; Deskew removes rotation
    Preprocessing = new PreprocessingOptions
    {
        Deskew = DeskewAdvanced.Enable()
    },

    // Parallelism – adjust based on your CPU/GPU capabilities
    MaxDegreeOfParallelism = 4
};
```

**Deskew (eğim düzeltme) neden etkinleştirilmeli?** Birçok taranmış belge tam olarak hizalanmamış olur; deskew algoritması bunları düz bir tabana döndürür ve tanıma oranlarını %10‑15 artırabilir.

## Adım 3: Sonuç Geri Çağrısını Bağlayarak Metin Dosyalarını Kaydedin

Toplu işlemci, işlediği her görüntü için bir olay yayar. `ResultProcessed` olayına abone olarak her OCR sonucunu bir `.txt` dosyasına yazacağız—yani **resimleri txt'ye dönüştürmek** anında gerçekleşecek.

```csharp
// Step 3: Register a callback to save each OCR result as a text file
ocrBatch.ResultProcessed += (sender, args) =>
{
    // Change the original file extension to .txt
    string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");

    // Write the recognized text to the new file
    File.WriteAllText(txtPath, args.Result.Text);

    // Inform the console for debugging / progress monitoring
    Console.WriteLine($"Processed: {args.ImagePath}");
};
```

Kısa bir ipucu: Orijinal klasör yapısını korumak isterseniz, `txtPath` değişkenini alt klasörleri veya ayrı bir çıktı dizinini içerecek şekilde değiştirebilirsiniz.

## Adım 4: Görüntü Klasörünüzde Toplu İşlemi Başlatın

Kalan tek şey, **görüntülerden metin çıkarma** ihtiyacı duyduğunuz klasörü işlemciye göstermek. `ProcessFolder` yöntemi alt klasörleri de rekürsif olarak tarar, böylece tüm tarama ağacını bir kerede bırakıp kütüphanenin geri kalanını halletmesini sağlayabilirsiniz.

```csharp
// Step 4: Run the batch on all image files in the target folder
ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
```

Programı çalıştırdığınızda aşağıdaki gibi bir konsol çıktısı göreceksiniz:

```
Processed: C:\Path\To\Your\Images\invoice1.png
Processed: C:\Path\To\Your\Images\receipt_2024.jpg
...
```

Her görüntünün yanında, çıkarılan metni içeren bir `.txt` dosyası oluşur.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, `Program.cs` dosyasına kopyalayıp yapıştırabileceğiniz tam program aşağıdadır:

```csharp
using Aspose.OCR;
using Aspose.OCR.Batch;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR batch processor
        var ocrBatch = new OcrBatchProcessor
        {
            Language = Language.English,
            Preprocessing = new PreprocessingOptions
            {
                Deskew = DeskewAdvanced.Enable()
            },
            // Step 2: Define the level of parallelism (adjust for your CPU/GPU)
            MaxDegreeOfParallelism = 4
        };

        // Step 3: Register a callback to save each OCR result as a text file
        ocrBatch.ResultProcessed += (sender, args) =>
        {
            string txtPath = Path.ChangeExtension(args.ImagePath, ".txt");
            File.WriteAllText(txtPath, args.Result.Text);
            Console.WriteLine($"Processed: {args.ImagePath}");
        };

        // Step 4: Run the batch on all image files in the target folder
        ocrBatch.ProcessFolder(@"C:\Path\To\Your\Images");
    }
}
```

### Beklenen Çıktı

- Kaynak dizindeki her `*.png` veya `*.jpg` için yanına karşılık gelen bir `*.txt` dosyası oluşturulur.
- Konsol, dosya başına bir satır yazarak anlık geri bildirim sağlar.
- Bir görüntü okunamazsa (bozuk dosya, desteklenmeyen format) Aspose.OCR bir hata kaydeder ancak kalan dosyaları işlemeye devam eder—bu, toplu motorun yerleşik dayanıklılığı sayesinde mümkün olur.

## Yaygın Sorular & Kenar Durumları

### PDF'leri görüntüler yerine işlemek istersem ne yapmalıyım?

Aspose.OCR PDF sayfalarını dahili olarak görüntüye dönüştürebilir, ancak önce PDF'yi raster görüntülere (ör. Aspose.PDF kullanarak) çevirmeniz gerekir. PNG'lere sahip olduğunuzda aynı toplu kod değişiklik yapmadan çalışır.

### Dili anlık olarak değiştirebilir miyim?

Evet. `Language` özelliği, herhangi bir `Language` enum değerini (İspanyolca, Fransızca, Çince vb.) kabul eder. Çok dilli belgeleriniz varsa, dil başına iki geçiş yapmayı veya `Language.AutoDetect` kullanmayı düşünebilirsiniz.

### İşlemi sadece belirli dosya türleriyle sınırlamak istiyorum, nasıl yaparım?

`ProcessFolder` isteğe bağlı bir `SearchOption` ve `string[] extensions` parametresi alır. Örnek:

```csharp
ocrBatch.ProcessFolder(@"C:\Images", new[] { ".png", ".tif" });
```

### GPU hızlandırması mümkün mü?

Aspose.OCR, `OcrEngine` yapılandırmasıyla GPU'yu destekler, ancak toplu işlemcinin `MaxDegreeOfParallelism` hâlâ eşzamanlılık için ana ayardır. Uyumlu bir GPU'nuz varsa, `OcrBatchProcessor` oluşturulmadan önce motor ayarlarında GPU'yu etkinleştirin.

### Çok büyük klasörlerle (on binlerce dosya) nasıl başa çıkılır?

- `MaxDegreeOfParallelism` değerini dikkatli artırın; çok fazla iş parçacığı bellek tüketimini artırabilir.
- Çıktıyı ayrı bir klasöre yönlendirerek dağınıklığı önleyin.
- Bellek şişmesini engellemek için logları periyodik olarak diske boşaltın.

## Yüksek Kaliteli OCR İçin Uzman İpuçları

- **DPI Önemlidir**: 300 DPI veya üzerindeki görüntüler en yüksek doğruluğu verir. Taramalarınız daha düşük DPI ise, işleme başlamadan önce bikübik filtreyle ölçeklendirmeyi düşünün.
- **Gürültü Azaltma**: Kaynak görüntüler grenliyse `Preprocessing.NoiseRemoval` özelliğini açın.
- **Dosya Adlandırma**: Dosya adlarını kısa ve alfanümerik tutun; özel karakterler geri çağırma yolu mantığını karıştırabilir.
- **Loglama**: Üretim ortamları için `Console.WriteLine` yerine `Serilog` gibi bir logger kullanın.

## Sonraki Adımlar

**Toplu OCR** konusundaki ustalığınızla şimdi şunları yapabilirsiniz:

- **Görüntülerden metin çıkarma** ve çıktıyı bir arama indeksi (ör. Elasticsearch) içine besleyerek tam metin araması sağlama.
- **Resimleri txt'ye dönüştürme** ardından doğal dil işleme (NLP) ile belgeleri otomatik sınıflandırma.
- **Farklı dil paketleri** veya sektöre özgü terimler için özel sözlükler deneme.

İşleme sonrası konularla ilgileniyorsanız, “OCR çıktısını düzenli ifadelerle ayrıştırma” veya “OCR sonuçlarını bir SQL veritabanına kaydetme” üzerine öğreticilere göz atın.

---

**Kodlamanın tadını çıkarın!** Paralelliği ayarlayın, daha fazla ön işleme adımı ekleyin veya sürekli izleme için tüm süreci bir Windows servisine sarın. Aspose.OCR'ın toplu yeteneklerini biraz .NET yaratıcılığıyla birleştirdiğinizde, sınır yoktur.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}