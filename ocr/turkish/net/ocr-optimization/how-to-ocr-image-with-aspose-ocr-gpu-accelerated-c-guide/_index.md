---
category: general
date: 2026-02-17
description: Aspose OCR'ı GPU üzerinde kullanarak görüntüyü OCR yapmayı öğrenin. Görüntüden
  metin tanıma, yüksek çözünürlüklü görüntü yükleme, GPU cihaz kimliğini ayarlama
  ve Aspose kullanarak metin çıkarma için adım adım kod.
draft: false
keywords:
- how to ocr image
- recognize text from image
- load high resolution image
- set gpu device id
- extract text using aspose
language: tr
og_description: Aspose OCR ile GPU’da görüntüyü OCR nasıl yapılır. Görüntüden metni
  tanımak, yüksek çözünürlüklü görüntüyü yüklemek, GPU cihaz kimliğini ayarlamak ve
  Aspose kullanarak metni çıkarmak için tam C# öğreticisini izleyin.
og_title: Aspose OCR ile Görüntüyü OCR'lamak – GPU Hızlandırmalı C# Rehberi
tags:
- Aspose OCR
- C#
- GPU acceleration
title: Aspose OCR ile Görüntüyü OCR'lamak – GPU Hızlandırmalı C# Kılavuzu
url: /tr/net/ocr-optimization/how-to-ocr-image-with-aspose-ocr-gpu-accelerated-c-guide/
---

besides image placeholder and maybe code blocks placeholders. Keep them unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Görüntü OCR'ı – GPU Hızlandırmalı C# Kılavuzu

Dosya devasa, 300 DPI tarama olduğunda ve saniyeler içinde sonuçlara ihtiyacınız olduğunda **görüntüyü OCR'lamak** merak ettiniz mi? Tek başınıza değilsiniz—geliştiriciler özellikle yüksek çözünürlüklü resimlerde yavaş CPU‑only OCR motorlarıyla sürekli mücadele ediyor. İyi haber? Aspose OCR, GPU'nuzu kullanmanıza olanak tanıyarak işleme süresini büyük ölçüde kısaltırken doğruluğu yüksek tutar.

Bu öğreticide, **görüntüden metni tanır**, **yüksek çözünürlüklü görüntüyü yükle**, **GPU cihaz kimliğini ayarla** ve sonunda **Aspose kullanarak metni çıkar** adımlarını içeren tam, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir programınız olacak.

## Gerekenler

- **.NET 6.0** veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır)
- **Aspose.OCR for .NET** NuGet paketi (sürüm 23.11 veya daha yeni)
- CUDA 11+ destekli bir GPU‑aktif makine (isteğe bağlı ama önerilir)
- OCR yapmak istediğiniz yüksek çözünürlüklü JPEG/PNG (ör. `highres_scan.jpg`)

Eğer bunlardan birine sahip değilseniz, NuGet paketini şu şekilde alın:

```bash
dotnet add package Aspose.OCR
```

Ek native kütüphanelere gerek yok; Aspose, CUDA çalışma zamanını sizin için paketler.

![görüntüyü OCR'lama diyagramı](image-placeholder.png "GPU hızlandırmalı OCR hattını gösteren diyagram – görüntüyü OCR'lama")

## Adım 1: OCR Motorunu Oluştur ve GPU Cihaz Kimliğini Ayarla  

İlk yapmanız gereken, Aspose'a GPU üzerinde çalışmasını söylemektir. İşte **GPU cihaz kimliğini ayarla** devreye girer—birden fazla GPU'nuz varsa iş yükünüze uygun olanı seçebilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine with GPU processing mode
var ocrEngine = new OcrEngine(new OcrEngineSettings
{
    ProcessingMode = ProcessingMode.Gpu, // Enable GPU acceleration
    GpuDeviceId = 0                     // Choose GPU #0 (change if you have several)
});
```

> **Neden önemli:** GPU işleme, ağır görüntü‑analiz işini paralel çekirdeklere devrederek tipik taramalarda 3‑5× hız artışı sağlar. `GpuDeviceId` ayarlamazsanız, Aspose varsayılan olarak ilk cihazı kullanır; bu tek‑GPU sistemler için yeterlidir.

## Adım 2: Yüksek Çözünürlüklü Görüntüyü Yükle  

Sonra, **yüksek çözünürlüklü görüntüyü yükle** verilerini OCR motorunun anlayacağı bir formata aktarırız. Aspose, dosyayı gereksiz dönüşümler olmadan belleğe okuyan `ImageStream.FromFile` sağlar.

```csharp
// Path to your high‑resolution scan (300 DPI or more)
string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";

// Load the image; ImageStream handles large files efficiently
var image = ImageStream.FromFile(imagePath);
```

> **Tip:** Görüntünüz bir bulut kovasında bulunuyorsa, doğrudan bir `Stream` de besleyebilirsiniz—sadece `FromFile` yerine `FromStream(yourStream)` kullanın. Motor yine yüksek çözünürlüklü bir kaynak olarak kabul eder.

## Adım 3: Görüntüden Metni Tanı  

Motor hazır ve resim yüklendiğine göre, **görüntüden metni tanı** yapabiliriz. `Recognize` metodu, düz metin, güven skorları ve gerekirse daha sonra kullanabileceğiniz sınırlama kutuları içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Perform OCR; this call is where the GPU does its magic
OcrResult recognitionResult = ocrEngine.Recognize(image);

// For debugging, you can also inspect recognitionResult.Regions
```

> **Köşe durumu:** Görüntü çok karanlık ya da çok gürültülüyse, `Recognize` çağırmadan önce ön‑işleme (ör. kontrast artırma) yapmayı düşünün. Aspose bir `Preprocess` API'si sunar, ancak çoğu temiz tarama için varsayılan yeterlidir.

## Adım 4: Aspose Kullanarak Metni Çıkar ve Görüntüle  

Son olarak, **Aspose kullanarak metni çıkar** ve sonucu `Text` özelliğinden okuyarak konsola yazdırıyoruz. İsterseniz bir dosyaya ya da veritabanına da yazabilirsiniz.

```csharp
// Output the plain‑text result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognitionResult.Text);
```

**Beklenen çıktı** (taralı bir fatura örneği):

```
=== OCR Output ===
Invoice #12345
Date: 2024‑12‑01
Total: $1,254.00
Thank you for your business!
```

Eğer bozuk karakterler görürseniz, görüntünün gerçekten yüksek çözünürlüklü olduğundan ve `OcrEngineSettings` içinde doğru dilin ayarlandığından emin olun (ör. `Language = Language.English`).

## Tam Çalışan Örnek  

Hepsini bir araya getirerek, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program aşağıdadır:

```csharp
// ------------------------------------------------------------
// Full OCR example – Aspose OCR with GPU acceleration
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine for GPU
        var ocrEngine = new OcrEngine(new OcrEngineSettings
        {
            ProcessingMode = ProcessingMode.Gpu, // GPU acceleration
            GpuDeviceId = 0                      // Change if you have multiple GPUs
        });

        // 2️⃣ Load a high‑resolution image
        string imagePath = @"YOUR_DIRECTORY/highres_scan.jpg";
        var image = ImageStream.FromFile(imagePath);

        // 3️⃣ Recognize text from the image
        OcrResult result = ocrEngine.Recognize(image);

        // 4️⃣ Extract and display the plain text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(result.Text);
    }
}
```

Programı `dotnet run` ile çalıştırın. İyi bir GPU’da, 5 MB, 300 DPI bir tarama için bile OCR sonucunu bir saniyenin altında görebilirsiniz.

## Yaygın Sorular ve Pro İpuçları  

### GPU'm yoksa ne olur?  
`ProcessingMode = ProcessingMode.Cpu` ayarlayarak Aspose OCR'ı hâlâ CPU üzerinde kullanabilirsiniz. API aynı kalır; sadece performans değişir.

### Birden fazla dili nasıl yönetirim?  
`OcrEngineSettings` içinde `Language = Language.Multilingual` (veya `Language.French` gibi belirli bir enum) ekleyin. Aspose uygun dil paketlerini otomatik olarak yükler.

### PDF'leri doğrudan işleyebilir miyim?  
Evet—Aspose OCR önce PDF'lerden görüntüleri çıkarır, ardından her sayfada OCR çalıştırır. Aynı `OcrEngine` ile `Aspose.PDF`'yi birleştirerek sorunsuz bir akış elde edersiniz.

### `GpuDeviceId`'yi ne zaman ayarlamalıyım?  
Sunucunuz hem görüntü‑işleme hem de makine‑öğrenme iş yüklerini çalıştırıyorsa, OCR için GPU 1'i (`GpuDeviceId = 1`) ayırıp GPU 0'ı çıkarım görevleri için boş bırakabilirsiniz.

### Gürültülü taramalarda doğruluğu nasıl artırırım?  
Görüntüyü ön‑işleme yapın:  
```csharp
image = image.AdjustContrast(1.2f).ApplyThreshold(0.5f);
```
Bu yöntemler Aspose’un görüntü‑işleme yardımcı araçlarının bir parçasıdır.

## Sonuç  

Artık **görüntüyü OCR'lamak** için Aspose OCR'ı GPU hızlandırmasıyla nasıl kullanacağınızı, **görüntüden metni tanı**, **yüksek çözünürlüklü görüntüyü yükle**, **GPU cihaz kimliğini ayarla** ve sonunda **Aspose kullanarak metni çıkar** adımlarını temiz, üretim‑hazır bir C# programında biliyorsunuz.

Kodu birkaç farklı dosyada deneyin—bulanık bir fiş, parlak bir broşür ya da el yazısı bir not. Dil ayarları ve ön‑işleme adımlarıyla oynayarak doğruluğun nasıl değiştiğini görün.

Sonraki adımda **batch processing** (tarama klasörünü döngüye alarak) ya da OCR sonucunu **search index**'e entegre ederek hızlı belge geri getirme üzerine çalışabilirsiniz. Her iki konu da burada ele alınan kavramların doğal bir uzantısıdır ve mükemmel takip projeleridir.

İyi kodlamalar, OCR hatlarınız hızlı ve kusursuz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}