---
category: general
date: 2026-01-02
description: Aspose OCR ve GPU desteği kullanarak PNG üzerinde OCR'ı hızlıca çalıştırın.
  Görüntüden metin tanımayı, metni görüntüden çıkarmayı ve GPU bellek sınırını ayarlamayı
  öğrenin.
draft: false
keywords:
- run OCR on PNG
- recognize text from image
- extract text from image
- how to extract text
- set GPU memory limit
language: tr
og_description: PNG üzerinde OCR'ı verimli bir şekilde çalıştırmak için Aspose OCR
  ve GPU hızlandırmadan yararlanın. Bu öğreticide, görüntüden metin tanıma, görüntüden
  metin çıkarma ve GPU bellek kullanımını kontrol etme yöntemlerini gösteriyoruz.
og_title: GPU ile PNG üzerinde OCR çalıştırma – Tam C# Rehberi
tags:
- OCR
- C#
- GPU
title: GPU ile PNG üzerinde OCR çalıştırma – Tam C# Kılavuzu
url: /tr/net/ocr-optimization/run-ocr-on-png-with-gpu-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# GPU ile PNG Üzerinde OCR Çalıştırma – Tam C# Rehberi

Hiç **PNG üzerinde OCR çalıştırmak** istediğinizde performans sorunlarıyla takıldınız mı? Tek değilsiniz. Gerçek dünyadaki birçok iş akışında tek bir yüksek çözünürlüklü PNG, yalnızca CPU kullanan bir OCR motorunu yavaşlatabilir ve hızlı bir arama olması gereken işlem bir dakikalık beklemeye dönüşebilir.  

İyi haber şu ki Aspose OCR, **görüntüden metin tanıma** işlemini çok daha kısa sürede yapmanızı sağlayan GPU uzantılarına sahiptir. Bu öğreticide, C# kullanarak **PNG üzerinde OCR çalıştırma**, **görüntüden metin çıkarma** ve **GPU bellek sınırını ayarlama** konularını adım adım göstereceğiz.

Ayrıca her adımın “nasıl” ve “neden” yönlerini de ele alacağız, böylece sadece bir kopyala‑yapıştır kod parçası değil, sağlam bir zihinsel model elde edeceksiniz.

## Öğrenecekleriniz

- Aspose OCR’ın GPU desteğini kullanmak için gereken ön koşullar.  
- Bir PNG’yi `Bitmap` olarak yükleyip OCR motoruna besleme.  
- Optimum performans için `GpuDevice` ve `GpuMemoryLimitMb` yapılandırması.  
- **Görüntüden metin tanıma** ve düz metin sonucunu alma.  
- Düşük bellekli GPU’lar veya çok sayfalı PNG’ler gibi yaygın kenar durumlarını ele alma ipuçları.  

Bu rehberin sonunda **PNG üzerinde OCR** işlemini GPU hızıyla çalıştırabilecek ve OCR işlerinin bellek ayak izini güvenle kontrol edebileceksiniz.

![GPU hızlandırmalı PNG üzerinde OCR çalıştırma diyagramı](run-ocr-on-png-diagram.png "run OCR on PNG örneği")

## Ön Koşullar

Başlamadan önce şunların kurulu olduğundan emin olun:

1. .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile de çalışır).  
2. CUDA desteğine sahip bir NVIDIA GPU (örnek cihaz indeksi 0 olarak ayarlanmıştır).  
3. Aspose.OCR NuGet paketi ve GPU uzantıları (`Aspose.OCR.Extensions`).  
4. Projenizden referans verebileceğiniz bir klasörde bulunan örnek PNG (`input.png`).  

Bu maddeler size yabancı geliyorsa endişelenmeyin—ilgili alternatifleri not edeceğiz.

---

## 1. Adım – Aspose OCR ve GPU Uzantılarını Yükleyin

İlk iş olarak doğru kütüphaneler olmadan kod derlenmez.

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Extensions
```

`Aspose.OCR.Extensions` paketi, GPU hızlandırması için gerekli yerel CUDA ikili dosyalarını içerir.  
*İpucu:* GPU’su olmayan bir makinede de projeyi derleyebilirsiniz; daha sonra `PreferGpu = false` olarak ayarlamanız yeterli.

---

## 2. Adım – İşlemek İstediğiniz PNG’yi Yükleyin

Şimdi **PNG üzerinde OCR çalıştırma** işlemini `Bitmap` içine yükleyerek yapacağız. Bu adım basit ama bir not düşmekte fayda var: `Bitmap` bir dosya yolu bekler, bu yüzden yolun çalıştırılabilir dosyanıza göre doğru olduğundan emin olun.

```csharp
using System.Drawing;        // Bitmap handling
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

// ...

// Step 2: Load the PNG image
string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory, "YOUR_DIRECTORY", "input.png");
Bitmap imageBitmap = new Bitmap(imagePath);
```

PNG çok büyükse (örneğin bir kenarı > 5000 px ise), GPU belleğini tüketmemek için önce ölçeklendirmek isteyebilirsiniz. Bu noktada **GPU bellek sınırını ayarlama** seçeneği devreye girer.

---

## 3. Adım – OCR Motorunu GPU Kullanımı İçin Oluşturup Yapılandırın

İşte öğreticinin kalbi: OCR motorunu **görüntüden metin tanıma** için GPU ile yapılandırmak. İki özellik kritik:

- `GpuDevice` – kullanılacak CUDA cihazını seçer.  
- `GpuMemoryLimitMb` – motorun ayırabileceği GPU bellek miktarını sınırlar.

```csharp
// Step 3: Initialize OCR engine with GPU settings
OcrEngine ocrEngine = new OcrEngine()
{
    // Pick the first CUDA device (index 0)
    GpuDevice = GpuDeviceInfo.GetDevice(0),

    // Optional: limit GPU memory consumption (in MB)
    GpuMemoryLimitMb = 2048   // Adjust based on your GPU's VRAM
};
```

**Bellek sınırı neden ayarlansın?** Bazı GPU’lar belleği ekranla paylaşır veya aynı anda birden fazla iş yükü çalıştırır. Sınır koyarak, özellikle paralel olarak birçok PNG işlediğinizde bellek yetersizliği hatalarını önlersiniz.

---

## 4. Adım – Tanıma Seçeneklerini Tanımlayın (Dil & GPU Tercihi)

`RecognitionOptions` nesnesi, motorun hangi dili arayacağını ve **GPU tercih et** ayarının küçük görüntülerde bile kullanılmasını belirler. Çoğu İngilizce belge için bu yeterlidir, ancak `Language.English` yerine başka desteklenen yerel ayarları da seçebilirsiniz.

```csharp
// Step 4: Set recognition options
RecognitionOptions recognitionOptions = new RecognitionOptions
{
    Language = Language.English,
    PreferGpu = true // Force GPU path even for smaller images
};
```

Eğer **görüntüden metin çıkarma** işlemini İngilizce dışındaki bir dilde yapmak isterseniz, sadece `Language` enum’unu değiştirin. Kütüphane kutudan çıkar çıkmaz onlarca dili destekler.

---

## 5. Adım – OCR’u Çalıştırın ve Sonucu Alın

Her şey bağlandıktan sonra, **PNG üzerinde OCR çalıştırma** işlemini tek bir satır kodla gerçekleştirebilir ve zengin bir sonuç nesnesi elde edebilirsiniz.

```csharp
// Step 5: Perform OCR
OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

// Output the extracted text
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

`OcrResult` sadece düz metni (`ocrResult.Text`) değil, aynı zamanda güven skorlarını, sınırlayıcı kutuları ve hatta vurgulanmış kelimelerle orijinal görüntüyü içerir—hata ayıklama veya çıkarımı görselleştirme ihtiyacınız varsa çok işe yarar.

**Beklenen çıktı** (örnek PNG “Hello World” yazıyorsa):

```
=== OCR Output ===
Hello World
```

Metin bozuk görünüyorsa, PNG’nin bozulmadığını ve GPU bellek sınırının görüntü boyutu için çok düşük olmadığını kontrol edin.

---

## 6. Adım – Kenar Durumları ve En İyi Uygulama İpuçları

### Düşük Bellekli GPU’lar

`CudaException: out of memory` gibi bir istisna alırsanız, `GpuMemoryLimitMb` değerini düşürün veya PNG’yi işlemden önce parçalara bölün. Parçalama işlemi `Graphics.DrawImage` ile bir `Bitmap` kopyası üzerinde yapılabilir.

### Toplu İşlemde Birden Fazla PNG

Bir klasördeki PNG’leri işlerken aynı `OcrEngine` örneğini yeniden kullanın—tek sefer başlatmak GPU bağlam geçişlerini azaltır.

```csharp
foreach (var file in Directory.GetFiles("images", "*.png"))
{
    using var bmp = new Bitmap(file);
    var result = ocrEngine.Recognize(bmp, recognitionOptions);
    Console.WriteLine($"{Path.GetFileName(file)}: {result.Text}");
}
```

### CPU’ya Geri Dönüş

GPU mevcut değilse sadece `PreferGpu = false` olarak ayarlayın. Motor, kodda başka bir değişiklik yapmadan otomatik olarak CPU’ya geçiş yapar.

```csharp
recognitionOptions.PreferGpu = false; // Safe CPU path
```

---

## Tam Çalışan Örnek

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam program yer alıyor. Yukarıdaki tüm adımları ve birkaç güvenlik kontrolünü içeriyor.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Extensions; // GPU support extensions

class GpuExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Load the PNG image
        // -------------------------------------------------
        string imagePath = Path.Combine(AppDomain.CurrentDomain.BaseDirectory,
                                         "YOUR_DIRECTORY", "input.png");

        if (!File.Exists(imagePath))
        {
            Console.Error.WriteLine($"File not found: {imagePath}");
            return;
        }

        using Bitmap imageBitmap = new Bitmap(imagePath);

        // -------------------------------------------------
        // Step 2: Initialize OCR engine with GPU settings
        // -------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine()
        {
            GpuDevice = GpuDeviceInfo.GetDevice(0), // First CUDA device
            GpuMemoryLimitMb = 2048                  // Adjust as needed
        };

        // -------------------------------------------------
        // Step 3: Set recognition options
        // -------------------------------------------------
        RecognitionOptions recognitionOptions = new RecognitionOptions
        {
            Language = Language.English,
            PreferGpu = true // Force GPU even for small images
        };

        // -------------------------------------------------
        // Step 4: Perform OCR
        // -------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(imageBitmap, recognitionOptions);

        // -------------------------------------------------
        // Step 5: Output the extracted text
        // -------------------------------------------------
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolda çıkarılan metni göreceksiniz.

---

## Sonuç

Aspose OCR’ın GPU uzantılarını kullanarak **PNG üzerinde OCR çalıştırma**, **görüntüden metin tanıma** ve **GPU bellek sınırını ayarlama** konularını gösterdik. `GpuDevice` ve `GpuMemoryLimitMb` ayarlarıyla uygulamanızı hızlı ve kararlı tutabilir, hatta düşük donanımlı GPU’larda bile sorunsuz çalıştırabilirsiniz.

İleride şunları deneyebilirsiniz:

- Başka dillerle çalışmak (`Language.French`, `Language.Spanish`).  
- OCR adımını daha büyük bir belge‑işleme hattına entegre etmek.  
- Çıkarılan ham metni düzeltmek için yazım denetimi veya varlık çıkarımı gibi son‑işlem eklemek.  

Unutmayın, önemli olan sadece kod değil, her ayarın neden önemli olduğunu anlamaktır. **GPU bellek sınırını ayarlamayı** ve gerektiğinde CPU’ya geri dönmeyi bildiğinizde, ölçeklenebilir OCR çözümleri oluşturabilirsiniz.

Belirli bir PNG boyutu, çok sayfalı TIFF’ler veya GPU hatalarıyla ilgili sorularınız mı var? Aşağıya yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}