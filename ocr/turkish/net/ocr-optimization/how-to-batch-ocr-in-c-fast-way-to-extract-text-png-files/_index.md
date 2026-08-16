---
category: general
date: 2026-04-03
description: Aspose.OCR ile C#’ta toplu OCR nasıl yapılır öğrenin. Bu kılavuz, PNG
  görüntülerinden metin çıkarmayı ve görüntüleri verimli bir şekilde metne dönüştürmeyi
  gösterir.
draft: false
keywords:
- how to batch ocr
- extract text png
- convert images to text
- Aspose OCR
- C# parallel processing
language: tr
og_description: C#'ta toplu OCR yaparak PNG görüntülerinden metin çıkarmayı ve Aspose.OCR
  kullanarak görüntüleri metne dönüştürmeyi keşfedin. Tam kod dahil.
og_title: C#'ta Toplu OCR Nasıl Yapılır – Hızlı Rehber
tags:
- OCR
- C#
- Aspose
title: C#'ta Toplu OCR Nasıl Yapılır – PNG Dosyalarından Metin Çıkarma İçin Hızlı
  Yöntem
url: /tr/net/ocr-optimization/how-to-batch-ocr-in-c-fast-way-to-extract-text-png-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Toplu OCR Nasıl Yapılır – PNG Dosyalarından Metin Çıkarma İçin Hızlı Yöntem

Her dosya için döngü yazmadan bir klasördeki tüm ekran görüntülerinde **toplu OCR nasıl yapılır** diye merak ettiniz mi? Tek başınıza değilsiniz. Birçok projede—örneğin fatura dijitalleştirme veya taranmış makbuzların arşivlenmesi—onlarca, hatta yüzlerce PNG dosyasıyla karşılaşırsınız ve bu dosyaların metinlerinin çıkarılması gerekir. İyi haber? Aspose.OCR ile **extract text PNG** görüntülerini paralel olarak işleyebilir ve tüm süreci sadece birkaç C# satırıyla tamamlayabilirsiniz.

Bu öğreticide, toplu bir işlemci kullanarak **convert images to text** nasıl yapılacağını gösteren eksiksiz, çalıştırmaya hazır bir örnek üzerinden adım adım ilerleyeceğiz. Gereksinimleri ele alacağız, her satırın neden önemli olduğunu açıklayacağız ve ileride sıkça karşılaşabileceğiniz sorunlardan kaçınmanız için birkaç pro‑ipuçları da ekleyeceğiz.

## Önkoşullar

- **.NET 6.0** (veya daha yeni) makinenizde kurulu olmalıdır. Eski çalışma zamanları çalışabilir, ancak en yenisi daha iyi performans ve async desteği sağlar.
- **Aspose.OCR for .NET** paketi. NuGet üzerinden şu komutla alabilirsiniz: `dotnet add package Aspose.OCR`.
- İşlemek istediğiniz **PNG** görüntülerle dolu bir klasör. Kılavuz boyunca buna `YOUR_DIRECTORY` diye atıfta bulunacağız.
- Makul bir RAM miktarı—toplu OCR paralellik artırıldığında bellek yoğun olabilir, ancak `Environment.ProcessorCount` kullanmak bunu güvenli tutar.

> **Pro tip:** CI/CD hattındaysanız, ücretsiz denemenin 20 sayfa limitinden kaçınmak için Aspose lisans dosyasını bir gizli olarak ekleyin.

Şimdi, işe koyulalım.

## Adım 1: Toplu OCR İşlemcisini Kurun (Başlıkta Birincil Anahtar Kelime)

İhtiyacınız olan ilk şey `BatchOcrProcessor` örneğidir. Bu sınıf iş parçacığı mantığını soyutlar ve her görüntüyle ne yapmanız gerektiğine odaklanmanızı sağlar.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Create a batch OCR processor and tell it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };
```

**Neden önemli:**  
- `Engine = new OcrEngine()` her iş parçacığı için yeni bir OCR motoru sağlar, rekabeti önler.  
- `MaxDegreeOfParallelism = Environment.ProcessorCount` çekirdek sayısına otomatik olarak ölçeklenir, manuel ayar yapmadan en yüksek verimi elde etmenizi sağlar.

## Adım 2: İlerleme Olaylarına Bağlanın (Çıkarma Takibini Kolaylaştırır)

Yüzlerce dosya işlenirken ilerlemeyi görmek çok önemlidir. `ProgressChanged` olayı her dosya tamamlandığında tetiklenir ve durumu kaydetmenizi sağlar.

```csharp
        // Subscribe to progress updates so we know which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");
```

**Neden beğeneceksiniz:**  
- Gerçek zamanlı geri bildirim, uygulamanın takılıp takılmadığını merak etmenizi önler.  
- Duraklatma veya iptal etme ihtiyacınız olursa, `e.Current` ve `e.Total` değerlerini incelemek için zaten bir kanca vardır.

## Adım 3: Klasör Tarama ve Dosya Deseni Tanımlayın (Extract Text PNG)

Şimdi işlemciye nereleri tarayacağını ve hangi dosya türlerini alacağını söylüyoruz. `"*.png"` deseni sadece PNG görüntülerini işlediğimizden emin olur.

```csharp
        // Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"YOUR_DIRECTORY",          // folder containing the images
            "*.png",                    // file pattern
            (imagePath, ocrText) =>     // callback for each processed file
            {
                // Step 4 is inside this callback – see next section
            });
```

**Neden önemli:**  
- Glob deseni kullanmak kodu esnek tutar; daha sonra JPEG işlemek isterseniz `*.png` yerine `*.jpg` yapabilirsiniz.  
- Geri çağırma (callback) hem görüntü yolunu hem de tanınan metni alır, böylece sonraki adımda ne yapacağınız üzerinde tam kontrol sahibi olursunuz.

## Adım 4: Tanınan Metni Kaynağın Yanına Kaydedin (Convert Images to Text)

Geri çağırma içinde OCR çıktısını orijinal PNG'nin hemen yanında bir `.txt` dosyasına yazacağız. Bu, aşağı yönlü işleme için **convert images to text** yapmanın en basit yoludur.

```csharp
                // Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
```

**Neden yan yana bir `.txt` dosyası seçtik:**  
- İlişkiyi açık tutar—PNG'yi açın, TXT'yi açın, karşılaştırın.  
- Küçük ölçekli projelerde veritabanı veya ekstra depolama katmanına ihtiyaç yoktur.

## Adım 5: Dostane Bir Tamamlanma Mesajı ile Sonlandırın

Düzenli bir konsol mesajı, her şey bittiğinde size bildirir.

```csharp
        // Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

Programı çalıştırdığınızda aşağıdaki gibi bir çıktı göreceksiniz:

```
Processed 1/27: C:\Images\invoice1.png
Processed 2/27: C:\Images\invoice2.png
...
Batch processing completed.
```

Her PNG artık çıkarılan metni içeren bir kardeş `.txt` dosyasına sahip.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirildi)

Aşağıda, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Eksik bir parça yok—sadece `YOUR_DIRECTORY`'yi görüntülerinizin mutlak yolu ile değiştirin.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create a batch OCR processor and configure it to use all CPU cores
        var ocrBatch = new BatchOcrProcessor
        {
            Engine = new OcrEngine(),
            MaxDegreeOfParallelism = Environment.ProcessorCount
        };

        // Step 2: Subscribe to progress updates to see which file is being processed
        ocrBatch.ProgressChanged += (s, e) =>
            Console.WriteLine($"Processed {e.Current}/{e.Total}: {e.FilePath}");

        // Step 3: Run OCR on every PNG image in the target folder
        ocrBatch.ProcessFolder(
            @"C:\MyImages",          // folder containing the images
            "*.png",                // file pattern
            (imagePath, ocrText) => // callback for each processed file
            {
                // Step 4: Save the recognized text next to the image as a .txt file
                string txtPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(txtPath, ocrText);
            });

        // Step 5: Indicate that batch processing has finished
        Console.WriteLine("Batch processing completed.");
    }
}
```

### Beklenen Sonuç

- `C:\MyImages` içindeki her `image.png` için yanına bir `image.txt` dosyası oluşur.
- Konsol ilerleme satırları yazdırır, büyük toplu işlemleri izlemeyi kolaylaştırır.
- Manuel döngü veya iş parçacığı yönetimi yok—`BatchOcrProcessor` her şeyi halleder.

## Yaygın Sorular ve Kenar Durumlar

### Görüntülerim PNG değilse ne olur?

Sadece `ProcessFolder` içindeki ikinci argümanı `"*.jpg"` ya da `"*.*"` olarak değiştirin, böylece tüm dosyalar dahil olur. OCR motoru çoğu raster formatıyla çalışır.

### Bu ne kadar bellek tüketir?

`BatchOcrProcessor` her iş parçacığı başına bir görüntü yükler. `Environment.ProcessorCount` 8 çekirdek olarak ayarlıysa, aynı anda sekiz görüntü bellekte olur. OutOfMemory hatası alırsanız paralelliği azaltın:

```csharp
MaxDegreeOfParallelism = 4; // or any number that fits your machine
```

### OCR dilini özelleştirebilir miyim?

Kesinlikle. Motoru oluşturduktan sonra `Language` özelliğini ayarlayın:

```csharp
Engine = new OcrEngine { Language = Language.English };
```

Aspose birçok dili destekler; gerekirse uygun NuGet paketini ekleyin.

### Hata yönetimi nasıl yapılır?

Geri çağırmayı bir try/catch bloğuna sarın ve hataları kaydedin. İşlemci bir sonraki dosyaya devam eder, tek bir bozuk görüntünün tüm çalışmayı durdurmasını engeller.

```csharp
(imagePath, ocrText) =>
{
    try
    {
        string txtPath = Path.ChangeExtension(imagePath, ".txt");
        File.WriteAllText(txtPath, ocrText);
    }
    catch (Exception ex)
    {
        Console.Error.WriteLine($"Failed on {imagePath}: {ex.Message}");
    }
}
```

## Ölçeklendirme İçin Pro İpuçları

- **Klasörü bölün**: On binlerce dosyanız varsa, alt klasörlere ayırın ve birden fazla toplu işi sırasıyla çalıştırın.
- **Bulut VM kullanın**: Daha fazla çekirdeğe sahip bir makine (ör. 32‑core) işi çok daha hızlı bitirir. Sadece lisans limitlerini ayarlamayı unutmayın.
- **Metni sonradan işleyin**: Çıkarma sonrası fatura numaraları veya tarihleri çekmek için regex çalıştırmak isteyebilirsiniz. `.txt` dosyaları bu tür işlem hatları için mükemmel girdi olur.

## Sonuç

Artık **how to batch OCR** bir PNG dizini için, **extract text PNG** dosyaları ve **convert images to text** işlemlerini Aspose.OCR ile C# kullanarak yapabilecek sağlam, üretime hazır bir tarifiniz var. Örnek bağımsızdır, her satırın “neden”ini açıklar ve daha büyük iş yükleri veya farklı dosya türleriyle başa çıkmak için ipuçları içerir.

Bir sonraki adım için hazır mısınız? Geri çağırmayı sonuçları bir veritabanına itmek için değiştirin ya da OCR'den önce görüntü ön‑işleme (ör. eğikliği düzeltme) ekleyin. Desen güzel ölçeklenir, böylece karşılaştığınız herhangi bir toplu‑işleme senaryosuna uyarlayabilirsiniz.

Kodlamaktan keyif alın ve OCR işlem hatlarınız hızlı ve hatasız olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}