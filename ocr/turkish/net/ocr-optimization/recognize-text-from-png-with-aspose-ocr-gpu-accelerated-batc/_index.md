---
category: general
date: 2026-04-01
description: Aspose OCR'de GPU cihaz kimliğini ayarlayarak ve GPU hızlandırmasını
  etkinleştirerek png dosyalarından metni hızlı bir şekilde tanımayı öğrenin. Adım
  adım C# rehberi.
draft: false
keywords:
- recognize text from png
- set gpu device id
- Aspose OCR GPU
- batch OCR C#
- OCR performance tips
language: tr
og_description: GPU cihaz kimliğini ayarlayarak png dosyalarından metni hızlı bir
  şekilde tanıyın. Aspose OCR ile GPU hızlandırmasını etkinleştirmek için bu kapsamlı
  C# rehberini izleyin.
og_title: png'den metin tanıma – GPU Hızlandırmalı Aspose OCR Öğreticisi
tags:
- C#
- OCR
- GPU
- Aspose
title: Aspose OCR ile png'den metin tanıma – GPU Hızlandırmalı Toplu Demo
url: /tr/net/ocr-optimization/recognize-text-from-png-with-aspose-ocr-gpu-accelerated-batc/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# png'den metin tanıma – Tam C# GPU Hızlandırmalı Toplu Öğretici

Hiç **png'den metin tanıma** ihtiyacı duydunuz mu ama sürecin ağrılı derecede yavaş olduğunu gördünüz mü? Yalnız değilsiniz. Çoğu geliştirici basit bir OCR çağrısıyla başlar, ardından bir klasörde onlarca ekran görüntüsü olduğunda bir salyangoz gibi ilerleyen bir konsola bakar.  

İyi haber? Aspose OCR, ağır işleri grafik kartınıza devredebilir ve sadece birkaç satırla **gpu cihaz kimliğini ayarlayarak** istediğiniz GPU'yu seçebilirsiniz. Bu rehberde, bir klasörden tüm PNG dosyalarını alıp GPU hızlandırmayı etkinleştiren, ilk GPU'yu seçen ve her dosya için karakter sayısını yazdıran tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

Sonunda, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir programınız olacak ve GPU'yu etkinleştirmenin neden önemli olduğunu, kenar durumlarını nasıl ele alacağınızı ve daha iyi performans için neleri ayarlamanız gerektiğini anlayacaksınız.

## Gereksinimler

- **.NET 6.0** veya daha yenisi (kod .NET Core ile de derlenir).  
- **Aspose.OCR** NuGet paketi – `dotnet add package Aspose.OCR` komutuyla kurun.  
- CUDA uyumlu bir GPU'ya (genellikle NVIDIA) ve uygun sürücüye sahip bir makine.  
- İşlemek istediğiniz **PNG** görüntülerle dolu bir klasör.  

Eğer bunlardan herhangi biri size yabancı geliyorsa, panik yapmayın. Aşağıdaki adımlar ihtiyacınız olan tam komutları içerir ve ayrıca bir GPU bulunmadığında ne yapmanız gerektiğini de ele alacağız.

## Adım 1: OCR Motorunu Başlatma ve GPU Hızlandırmayı Etkinleştirme  

İlk yapmanız gereken bir `OcrEngine` örneği oluşturmak ve GPU desteğini açmaktır. Bu bayrak, Aspose'a altında yerel CUDA kütüphanelerini kullanmasını söyler.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Initialise the OCR engine
        var ocrEngine = new OcrEngine();

        // Enable GPU acceleration – huge speed boost for large batches
        ocrEngine.UseGpuAcceleration = true;
```

**Neden önemli:** `UseGpuAcceleration` olmadan, her görüntü CPU'da işlenir ve bu, özellikle yüksek çözünürlüklü PNG'ler için kat kat daha yavaş olabilir. Bayrağı etkinleştirmek ayrıca motorun daha sonra belirli bir GPU cihazını kabul etmeye hazır olmasını sağlar.

## Adım 2: GPU Cihaz Kimliğini Ayarlama (Opsiyonel ama Tavsiye Edilir)  

İş istasyonunuzda birden fazla GPU varsa, hangisini kullanacağınıza karar verebilirsiniz. Cihaz kimlikleri **0**'dan başlar, yani `0` ilk GPU'yu, `1` ikinci GPU'yu vb. seçer.

```csharp
        // Optional: Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id
```

**Pro ipucu:** Paylaşımlı bir sunucuda çalışırken, GPU cihaz kimliğini açıkça ayarlamak işinizin diğer süreçlerden kaynak çalmasını önleyebilir. Bu satırı atlayarsanız, Aspose varsayılan cihazı seçecektir; bu genellikle tek GPU kurulumları için yeterlidir.

## Adım 3: Toplu Klasörünüzdeki Tüm PNG Dosyalarını Toplama  

Sonra OCR uygulamak istediğiniz tüm PNG'leri bulmamız gerekiyor. `Directory.GetFiles` yöntemi bu işi yapar.

```csharp
        // Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // <-- replace with your path
            "*.png",                  // only PNG files
            System.IO.SearchOption.TopDirectoryOnly);
```

**Kenar durumu:** Klasör boşsa, `imageFiles` boş bir dizi olacaktır. Bunu daha sonra dostça bir mesajla ele alacağız.

## Adım 4: Her Görüntüyü İşleme ve Tanınan Karakter Sayısını Çıktı Olarak Verme  

Şimdi temel döngü. Her PNG için `Recognize` metodunu çağırır, ardından dosya adını ve çıkarılan metnin uzunluğunu yazdırırız.

```csharp
        // Verify we actually found files
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

**Gördükleriniz:**  
```
invoice1.png → 342 chars
receipt_2023.png → 127 chars
screenshot.png → 0 chars
```

Bir görüntü metin içermiyorsa, sayı `0` olacaktır. Bu, tamamen grafik olan ekran görüntüleri için tamamen normaldir.

## Adım 5: Programı Çalıştırma ve GPU Kullanımını Doğrulama  

Dosyayı derleyin (`dotnet build`) ve çalıştırın (`dotnet run`). Konsol kayarken, GPU izleme aracınızı (örneğin NVIDIA Smi) açarak her görüntü için GPU kullanımının kısa bir artışını görebilirsiniz. Eğer herhangi bir aktivite görmezseniz, şunları iki kez kontrol edin:

1. CUDA sürücüsünün yüklü olduğundan emin olun.  
2. `UseGpuAcceleration` değerinin `true` olduğundan emin olun.  
3. Doğru `GpuDeviceId`'nin fiziksel bir GPU ile eşleştiğini kontrol edin.

GPU mevcut değilse, Aspose otomatik olarak CPU'ya geçer, ancak hız avantajını kaybedersiniz.

## Yaygın Varyasyonlar ve İpuçları  

| Durum | Ne Değiştirilmeli |
|-----------|----------------|
| **Farklı görüntü formatı** (ör. JPEG) | Arama desenini `*.jpg` veya `*.*` olarak değiştirin; Aspose hâlâ metni tanıyacaktır. |
| **Toplu boyut çok büyük** (binlerce dosya) | Bellek baskısını önlemek için parçalar halinde işleyin: `imageFiles`'ı daha küçük dizilere bölün. |
| **Gerçek metne, sadece uzunluğa değil, ihtiyacınız var** | `WriteLine` içinde `ocrResult.Text.Length` yerine `ocrResult.Text` kullanın. |
| **Grafiksiz (headless) bir sunucuda çalıştırma** | Sunucunun GPU sürücüsü olduğundan emin olun; aksi takdirde gereksiz hatalardan kaçınmak için `UseGpuAcceleration = false` ayarlayın. |
| **Birden fazla GPU, yükü dengelemek istiyor** | `foreach` içinde `ocrEngine.GpuDeviceId = i % gpuCount` döngüsüyle cihazları döndürün. |

## Beklenen Çıktı ve Doğrulama  

Her şey çalıştığında, konsol her dosya adını ardından karakter sayısını yazdırır, önceki gibi. Gerçek OCR çıktısını iki kez kontrol etmek için metni geçici olarak dökebilirsiniz:

```csharp
Console.WriteLine($"{Path.GetFileName(imagePath)} → {ocrResult.Text}");
```

Büyük toplular için bu satırı kaldırmayı veya yorum satırı yapmayı unutmayın; binlerce satır yazdırmak terminalinizi boğabilir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU‑specific namespace
using System;

class GpuBatchDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine and enable GPU acceleration
        var ocrEngine = new OcrEngine();
        ocrEngine.UseGpuAcceleration = true;

        // Step 2: (Optional) Choose the GPU device – 0 selects the first GPU
        ocrEngine.GpuDeviceId = 0;   // <-- set gpu device id

        // Step 3: Retrieve all PNG images from the batch folder
        string[] imageFiles = System.IO.Directory.GetFiles(
            @"YOUR_DIRECTORY\Batch",   // replace with your folder path
            "*.png",
            System.IO.SearchOption.TopDirectoryOnly);

        // Guard clause if no files are found
        if (imageFiles.Length == 0)
        {
            Console.WriteLine("No PNG files found in the specified folder.");
            return;
        }

        // Step 4: Process each image and display the recognised character count
        foreach (var imagePath in imageFiles)
        {
            var ocrResult = ocrEngine.Recognize(imagePath);
            Console.WriteLine($"{System.IO.Path.GetFileName(imagePath)} → {ocrResult.Text.Length} chars");
        }
    }
}
```

`GpuBatchDemo.cs` olarak kaydedin, `dotnet add package Aspose.OCR` komutunu çalıştırın, ardından `dotnet run`. GPU hızlandırması sayesinde her PNG için karakter sayılarının neredeyse anında göründüğünü göreceksiniz.

## Sonuç  

Artık **png dosyalarından metin tanıma** işlemini GPU hızlandırmasını etkinleştirerek ve Aspose OCR'de **gpu cihaz kimliğini ayarlayarak** verimli bir şekilde yapabileceğinizi biliyorsunuz. Tam, kopyala‑yapıştır programı klasör keşfini, kenar durumu kontrollerini yönetir ve OCR performansı hakkında anlık geri bildirim sağlar.

Sonraki adımlar? Engellemesiz işlem gerekiyorsa `Recognize` çağrısını `ocrEngine.RecognizeAsync` ile değiştirin veya Aspose'un sağladığı farklı görüntü ön işleme seçenekleriyle (ör. ikilileştirme) deney yapın. OCR sonuçlarını bir veritabanına veya tam metin arama çözümü için bir arama indeksine de aktarabilirsiniz.

Çok sayfalı PDF'leri nasıl ele alacağınızla ilgili sorularınız mı var, ya da Aspose OCR'yi Tesseract ile karşılaştırmak mı istiyorsunuz? Bir yorum bırakın veya **batch OCR C#**, **OCR performans ipuçları** ve **GPU‑tabanlı görüntü işleme** konularındaki diğer öğreticilerimize göz atın. Kodlamanın tadını çıkarın!  

![GPU hızlandırmasıyla png dosyalarından tanınan karakter sayısını gösteren konsol çıktısı](image-placeholder.png "png'den metin tanıma çıktısı örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}