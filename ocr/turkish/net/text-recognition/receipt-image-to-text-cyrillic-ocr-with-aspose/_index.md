---
category: general
date: 2026-04-01
description: Aspose OCR kullanarak bir fiş görüntüsünü metne dönüştürmeyi öğrenin.
  Bu kılavuz, Kiril alfabesi metnini nasıl çıkaracağınızı, OCR için görüntüyü nasıl
  yükleyeceğinizi ve Kiril karakterlerini verimli bir şekilde nasıl tanıyacağınızı
  gösterir.
draft: false
keywords:
- receipt image to text
- extract cyrillic text
- load image for ocr
- recognize cyrillic characters
- create OCR engine
language: tr
og_description: Aspose OCR ile bir fiş görüntüsünü metne dönüştürün. Kiril metnini
  çıkarmayı, OCR için görüntüyü yüklemeyi ve C#'ta Kiril karakterlerini tanımayı öğrenin.
og_title: Fiş görüntüsünü metne – Aspose ile Kiril OCR
tags:
- OCR
- C#
- Aspose
- Cyrillic
title: Fiş görüntüsünden metne – Aspose ile Kiril OCR
url: /tr/net/text-recognition/receipt-image-to-text-cyrillic-ocr-with-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# receipt image to text – Cyrillic OCR with Aspose

Hiç **fiş görüntüsünden metne** dönüştürmek istediğinizde karakterlerin tamamen Kiril alfabesinde olduğunu gördünüz mü? Bu konuda yalnız değilsiniz. Birçok perakende veya muhasebe uygulamasında fişler Rusça, Bulgarca ya da Sırpça karakterlerle gelir ve yine de temiz, aranabilir bir dize elde etmek istersiniz.  

Bu öğreticide **Kiril metnini** bir fiş fotoğrafından **nasıl çıkaracağınızı**, **görüntüyü OCR için nasıl yükleyeceğinizi** ve **Kiril karakterlerini** Aspose OCR kütüphanesiyle **nasıl tanıyacağınızı** adım adım göstereceğiz. Sonunda OCR sonucunu bir `.txt` dosyasına yazan çalıştırılabilir bir C# programına sahip olacaksınız.

## What You’ll Need

- **.NET 6** (veya herhangi bir yeni .NET sürümü) – kod .NET Framework 4.7+ üzerinde de çalışır.  
- **Aspose.OCR for .NET** NuGet paketi – `Install-Package Aspose.OCR`.  
- Kiril metin içeren bir örnek fiş görüntüsü (ör. `cyrillic_receipt.jpg`).  
- Bir geliştirme ortamı – Visual Studio, VS Code ya da Rider yeterli.  

Ek bir yerel bağımlılık gerekmez; Aspose dil modellerini içinde barındırır ve ağır işleri dahili olarak halleder.

## receipt image to text – Setting up the OCR Engine

İlk yapmamız gereken **OCR motoru** örneği oluşturmak ve hangi dili kullanacağımızı belirtmektir. Aspose bunu çok basit hâle getirir:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;   // language and resource handling
using System.Drawing;      // Image class
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        // Step 1: Instantiate the OCR engine
        var ocrEngine = new OcrEngine();

        // Step 2: Tell Aspose we want Cyrillic support
        ocrEngine.Language = Language.Cyrillic;

        // Optional: Pre‑load the model if you’ll run offline later
        // ResourceManager.Preload(Language.Cyrillic);
```

> **Pro tip:** Modeli önceden yüklemek, programı ilk kez çalıştırdığınızda bir ağ çağrısını önler; bu, masaüstü ya da gömülü senaryolar için kullanışlıdır.

## How to extract Cyrillic text – Loading the receipt image

Motor hazır olduğuna göre, **OCR için görüntüyü yüklememiz** gerekir. `System.Drawing.Image` sınıfı çoğu bitmap formatı için mükemmel çalışır.

```csharp
        // Step 3: Point to your receipt image
        string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

        // Step 4: Load the image inside a using block (ensures disposal)
        using (var image = Image.FromFile(imagePath))
        {
            // Step 5: Run the OCR process
            var recognitionResult = ocrEngine.Recognize(image);
```

Dosya bulunamazsa, `Image.FromFile` bir `FileNotFoundException` fırlatır. Üretim kodu için tüm işlemi bir `try…catch` bloğuna almak isteyebilirsiniz.

## Recognize Cyrillic characters – Getting the text out

`recognitionResult` nesnesi ham metni, güven skorlarını ve gerekirse sınırlama kutularını içerir. Basit bir “fiş görüntüsünden metne” dönüşümü için sadece `Text` özelliğini bir dosyaya yazıyoruz:

```csharp
            // Step 6: Write the extracted text to a .txt file
            string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
            File.WriteAllText(outputPath, recognitionResult.Text);

            // Quick verification: print to console
            Console.WriteLine("OCR completed. Extracted text:");
            Console.WriteLine(recognitionResult.Text);
        }
    }
}
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
OCR completed. Extracted text:
СЧЕТ № 12345
Дата: 01/04/2026
Товар      Кол-во   Цена
Хлеб       2        30,00
Молоко     1        45,00
Итого:               105,00
```

İşte aradığınız **fiş görüntüsünden metne** dönüşüm sonucu.

![fiş görüntüsünden metne örnek](receipt-ocr-example.png "Bir fiş görüntüsünün metne dönüştürülmesinin örneği")

*Görsel alt metni: Aspose OCR tarafından çıkarılan Kiril karakterlerini gösteren fiş görüntüsünden metne dönüşüm örneği.*

## Edge Cases & Common Questions

### What if the language model isn’t downloaded yet?

Aspose, `ocrEngine.Language = Language.Cyrillic;` satırını ilk kez ayarladığınızda gerekli modeli otomatik olarak indirir. Makinede internet yoksa, isteğe bağlı ön‑yükleme adımı başarısız olur. Bu durumda modeli manuel olarak sağlayın (Aspose belgelerine bakın) ya da cihazın `download.aspose.com` adresine erişebildiğinden emin olun.

### How do I handle multiple languages in the same receipt?

Virgül‑ayırmalı bir liste geçirebilirsiniz:

```csharp
ocrEngine.Language = Language.Cyrillic | Language.English;
```

Aspose, her iki dil setinden de karakter tanımaya çalışacaktır.

### My receipt is blurry – can I improve accuracy?

Aspose OCR temel görüntü ön‑işleme seçenekleri sunar:

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Sharpen = true,
    Binarize = true,
    Denoise = true
};
```

`Recognize` metodunu çağırmadan önce bunu uygulayın.

### What about large batch processing?

Tanıma döngüsünü bir `Parallel.ForEach` içinde sarın ve aynı `OcrEngine` örneğini yeniden kullanın (model yüklendikten sonra iş parçacığı‑güvenlidir). İş parçacığı‑güvenliği sorunlarıyla karşılaşırsanız motoru kilitlemeyi unutmayın.

## Full Working Example (All Steps Combined)

Aşağıda, isteğe bağlı ön‑yükleme ve temel hata yönetimini içeren, kopyala‑yapıştır‑hazır tam program yer almaktadır:

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using System;
using System.Drawing;
using System.IO;

class CyrillicDemo
{
    static void Main()
    {
        try
        {
            // Create OCR engine and select Cyrillic language
            var ocrEngine = new OcrEngine();
            ocrEngine.Language = Language.Cyrillic;

            // Optional: preload model for offline use
            // ResourceManager.Preload(Language.Cyrillic);

            // Path to the receipt image
            string imagePath = @"YOUR_DIRECTORY\cyrillic_receipt.jpg";

            // Verify the file exists
            if (!File.Exists(imagePath))
                throw new FileNotFoundException("Receipt image not found.", imagePath);

            using (var image = Image.FromFile(imagePath))
            {
                // Perform OCR
                var result = ocrEngine.Recognize(image);

                // Output path for extracted text
                string outputPath = @"YOUR_DIRECTORY\cyrillic.txt";
                File.WriteAllText(outputPath, result.Text);

                Console.WriteLine("✅ receipt image to text conversion succeeded.");
                Console.WriteLine("Extracted text saved to: " + outputPath);
                Console.WriteLine("\n--- Extracted Text ---\n");
                Console.WriteLine(result.Text);
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine("❌ An error occurred: " + ex.Message);
        }
    }
}
```

Programı (`dotnet run` komutunu proje klasöründen çalıştırarak) çalıştırın ve **fiş görüntüsünden metne** çıktısını içeren bir `.txt` dosyası elde edin.

## Conclusion

Artık Aspose OCR kullanarak **fiş görüntüsünden metne**—özellikle Kiril alfabesi için—tam bir uçtan uca çözümünüz var. **OCR motoru oluşturma**, **görüntüyü OCR için yükleme**, **Kiril metni çıkarma** ve **Kiril karakterlerini tanıma** işlemlerini sadece birkaç C# satırıyla gerçekleştirdik.  

Sonraki adımlar? Bir klasördeki birden çok fişi işleyin, doğruluğu artırmak için `ImagePreprocessor` ile deneyler yapın ya da OCR çıktısını otomatik muhasebe için bir veritabanıyla birleştirin. Başka alfabelerle çalışmanız gerekirse `

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}