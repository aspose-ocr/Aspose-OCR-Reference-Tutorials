---
category: general
date: 2026-03-17
description: C#'da Aspose OCR kullanarak PNG'den metin çıkarın. Görüntüden metin okumayı,
  fiş OCR işlemesini ve GPU hızlandırmalı bir OCR motoru oluşturmayı öğrenin.
draft: false
keywords:
- extract text from png
- read text from image
- ocr receipt image
- process receipt ocr
- create ocr engine
language: tr
og_description: Aspose OCR kullanarak PNG'den metin çıkarın. Bu kılavuz, görüntüden
  metin okuma, fiş OCR işleme ve OCR motorunu verimli bir şekilde oluşturma yöntemlerini
  gösterir.
og_title: PNG'den Metin Çıkar – Görüntüden OCR ile Metin Oku
tags:
- OCR
- CSharp
- Aspose
title: PNG'den Metin Çıkar – Görüntüden OCR ile Metin Oku
url: /tr/net/text-recognition/extract-text-from-png-read-text-from-image-with-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkar – Görüntüden Metin Okuma (OCR)

Hiç **PNG'den metin çıkarmak** gerekti ve hangi kütüphanenin güvenilir sonuçlar vereceğinden emin olmadınız mı? Tek başınıza değilsiniz—geliştiriciler sürekli olarak “Makbuz gibi görüntü dosyalarından özel bir sinir ağı yazmadan metni nasıl okurum?” sorusunu soruyor. İyi haber, Aspose OCR sizin için zor kısmı hallediyor ve hatta hız artışı için GPU'yu da çalıştırabilirsiniz.

Bu öğreticide **makbuz OCR işleme** için ihtiyacınız olan her şeyi adım adım göstereceğiz; NuGet paketinin kurulumu, PNG dosyanızı anlayan bir OCR motoru oluşturma gibi. Sonunda, bir makbuz görüntüsünü okuyan, tanınan metni konsola yazdıran ve motoru farklı senaryolar için nasıl ayarlayacağınızı gösteren bağımsız bir konsol uygulamanız olacak. Harici dokümanlar yok, sadece saf kod ve net açıklamalar.

## Önkoşullar

- .NET 6.0 SDK (veya herhangi bir güncel .NET sürümü)  
- Visual Studio 2022 veya C# uzantılarına sahip VS Code  
- En son sürücüye sahip desteklenen bir NVIDIA GPU (isteğe bağlı, ancak GPU modu için önerilir)  
- The **Aspose.OCR** NuGet package (`dotnet add package Aspose.OCR`)  

GPU'nuz yoksa, örneği CPU modunda da çalıştırabilirsiniz—GPU yapılandırma satırlarını atlayın yeter.

## Adım 1: Aspose.OCR'ı Kurun ve Projeyi Ayarlayın

İlk olarak, yeni bir konsol projesi oluşturun ve Aspose OCR kütüphanesini ekleyin.

```bash
dotnet new console -n ReceiptOcrDemo
cd ReceiptOcrDemo
dotnet add package Aspose.OCR
```

Neden önemli: `Aspose.OCR` paketi OCR motorunu, görüntü yükleyicileri ve isteğe bağlı GPU desteğini bir arada sunar. NuGet üzerinden eklemek, en son kararlı sürümü (Mart 2026 itibarıyla 23.10) almanızı sağlar.

## Adım 2: Ad Alanlarını İçe Aktarın ve OCR Motorunu Oluşturun

Şimdi **Program.cs** dosyasını açın ve gerekli `using` yönergelerini ekleyin. Ardından motoru örnekleyin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // Optional: Enable GPU acceleration if a compatible GPU is present
            // This dramatically speeds up processing of high‑resolution PNGs
            ocrEngine.Config.EngineMode = EngineMode.Gpu;   // <-- primary way to "process receipt ocr" fast
            ocrEngine.Config.GpuDeviceId = 0; // selects the first GPU in the system

            // The rest of the code follows...
```

**Pro ipucu:** GPU'suz makinelerde `System.DllNotFoundException` alırsanız, `EngineMode` ve `GpuDeviceId` ayarlayan iki satırı yorum satırı haline getirin. Motor otomatik olarak CPU'ya geçecektir.

## Adım 3: Metin Çıkarmak İstediğiniz PNG Görüntüsünü Yükleyin

Aspose OCR, görüntüleri doğrudan dosya yolundan, akıştan veya hatta bayt dizisinden okuyabilir. Bu demo için yerel bir makbuz görüntüsü yükleyeceğiz.

```csharp
            // Step 3: Load the image (replace the path with your own PNG file)
            string imagePath = @"C:\Images\receipt.png";

            // Validate the file exists to avoid runtime surprises
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }

            // Load the image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Eksik dosyaya karşı nasıl koruma sağladığımıza dikkat edin. Gerçek dünyadaki uygulamalarda sadece çıkmak yerine kullanıcı dostu bir UI mesajı göstermek muhtemeldir.

## Adım 4: OCR Tanıma İşlemini Gerçekleştirin

Gerçek metin çıkarma tek bir metod çağrısıyla gerçekleşir. Motor, ham dize, güven puanları ve düzen bilgilerini içeren bir `OcrResult` nesnesi döndürür.

```csharp
            // Step 4: Run the OCR process
            OcrResult ocrResult = ocrEngine.Recognize();

            // Check if the engine succeeded
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }
```

`ocrResult.Text`'i kontrol etmemizin nedeni: bazen düşük kaliteli PNG boş bir dize döndürür ve kullanıcıya sessizce hiçbir şey çıkarmak yerine bunu bildirmek daha iyidir.

## Adım 5: Tanınan Metni Çıktılayın

Son olarak, çıkarılan dizeyi konsola yazdırın. Ayrıca bir dosyaya, veritabanına yazabilir veya başka bir servise besleyebilirsiniz.

```csharp
            // Step 5: Display the recognized text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Programı çalıştırdığınızda (`dotnet run`) aşağıdakine benzer bir çıktı görmelisiniz:

```
=== Extracted Text from PNG ===
Store: Coffee Corner
Date: 03/15/2026
Item      Qty   Price
Latte      2    $5.40
Muffin     1    $2.30
Total            $7.70
=== End of Output ===
```

Bu, Aspose OCR ile **PNG dosyalarından metin çıkarma** için **tam çözümdür** ve makbuz gibi görüntü dosyalarından **metin okuma** konusunda yeni şeyler öğrendiniz.

## Opsiyonel: OCR Motorunu İnce Ayar (İleri Düzey)

Belirli yazı tipleri veya gürültülü arka planlar için daha yüksek doğruluk gerekiyorsa, bu ayarları değiştirmenizi öneririz:

```csharp
// Enable language detection (default is English)
ocrEngine.Config.Language = Language.English;

// Turn on automatic image preprocessing (deskew, binarization)
ocrEngine.Config.EnableImagePreprocessing = true;

// Set a confidence threshold if you only want high‑certainty results
ocrEngine.Config.ConfidenceThreshold = 0.75f;
```

Bu ince ayarlar, bazı taramaların mükemmel olmadığı toplu işlerde **makbuz OCR işleme** yaparken özellikle faydalıdır.

## Yaygın Tuzaklar ve Nasıl Önlenir

| Sorun | Neden Oluşur | Çözüm |
|-------|--------------|------|
| **GPU sürücü eksik** | Motor CUDA'yı yüklemeye çalışıyor ancak DLL bulunamıyor. | En son NVIDIA sürücüsünü kurun veya `EngineMode.Gpu` satırını kaldırarak CPU moduna geçin. |
| **Yanlış görüntü yolu** | Dosya bulunamazsa `ImageStream.FromFile` bir istisna fırlatır. | Her zaman yolu doğrulayın (Bkz. Adım 3) veya çapraz platform güvenliği için `Path.Combine` kullanın. |
| **Bulanık makbuzlarda düşük güven** | OCR motoru karakterleri ayırt edemiyor. | `EnableImagePreprocessing`'i etkinleştirin ve isteğe bağlı olarak görüntü DPI'sını artırın. |
| **Uzun süren hizmetlerde bellek sızıntısı** | Her `OcrEngine` yönetilmeyen kaynak tutar. | Kullanım sonrası motoru serbest bırakın: `using var ocrEngine = new OcrEngine();` |

## Tam Çalışan Örnek (Kopyala‑Yapıştır)

Aşağıda `Program.cs` içine ekleyebileceğiniz **tam program** bulunuyor. Tüm opsiyonel ince ayarlar, kolay etkinleştirme için yorum satırı olarak eklenmiştir.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;

namespace ReceiptOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Create OCR engine
            using var ocrEngine = new OcrEngine();

            // Enable GPU acceleration if you have a supported card
            ocrEngine.Config.EngineMode = EngineMode.Gpu;
            ocrEngine.Config.GpuDeviceId = 0;

            // Optional fine‑tuning (uncomment as needed)
            //ocrEngine.Config.Language = Language.English;
            //ocrEngine.Config.EnableImagePreprocessing = true;
            //ocrEngine.Config.ConfidenceThreshold = 0.75f;

            // Load PNG image
            string imagePath = @"C:\Images\receipt.png";
            if (!System.IO.File.Exists(imagePath))
            {
                Console.WriteLine($"Error: File not found – {imagePath}");
                return;
            }
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR
            OcrResult ocrResult = ocrEngine.Recognize();

            // Verify result
            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("No text could be recognized.");
                return;
            }

            // Output the extracted text
            Console.WriteLine("=== Extracted Text from PNG ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine("=== End of Output ===");
        }
    }
}
```

Kaydedin, `dotnet run` çalıştırın ve makbuzun içeriğinin konsola yazdırıldığını göreceksiniz.

![png'den metin çıkarma örneği](receipt.png "png'den metin çıkarma örneği")

*Yukarıdaki görüntü, kodun işleyebileceği örnek bir makbuz PNG'sini gösterir.*

## Özet

Aspose OCR kullanarak **PNG dosyalarından metin çıkarma** yöntemini, **görüntü dosyalarından metin okuma** gösterimini ve opsiyonel GPU hızlandırması içeren tam bir **makbuz OCR işleme** hattını ele aldık. Kendi **OCR motorunuzu** oluşturarak yapılandırma, performans ve hata yönetimi üzerinde tam kontrol elde edersiniz.

## Sonra Neler Keşfedebiliriz?

- **Toplu işleme**: PNG makbuzların bulunduğu bir klasörü döngüye alıp her sonucu bir CSV dosyasına yazın.  
- **Azure Functions ile entegrasyon**: Bu konsol uygulamasını görüntü yüklemelerini kabul eden sunucusuz bir uç noktaya dönüştürün.  
- **Çok‑dilli destek**: `Language.English` yerine `Language.Spanish` kullanın veya özel sözlükler ekleyin.  
- **Son‑işleme**: Ham OCR dizesinden toplam tutar, tarih veya vergi kimliği gibi alanları çıkarmak için düzenli ifadeler kullanın.

Denemekten çekinmeyin—OCR, doğru ayarları bildiğinizde şaşırtıcı derecede esnek bir araçtır. Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın veya daha derinlemesine bilgi için Aspose OCR API referansına bakın.

Kodlamanın tadını çıkarın ve inatçı PNG makbuzları aranabilir metne dönüştürmenin keyfini yaşayın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}