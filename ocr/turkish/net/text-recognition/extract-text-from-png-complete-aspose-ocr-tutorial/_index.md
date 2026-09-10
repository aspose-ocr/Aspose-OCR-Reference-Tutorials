---
category: general
date: 2026-01-09
description: Aspose OCR ile PNG'den hızlıca metin çıkarın. Görüntü metnini nasıl okuyacağınızı
  öğrenin, OCR doğruluğunu artırın ve C#'ta temiz sonuçlar elde edin.
draft: false
keywords:
- extract text from png
- read image text
- improve ocr accuracy
- extract text from image
- aspose ocr tutorial
language: tr
og_description: Aspose OCR ile PNG'den hızlıca metin çıkarın. Görüntü metnini nasıl
  okuyacağınızı öğrenin, OCR doğruluğunu artırın ve C#'ta temiz sonuçlar elde edin.
og_title: PNG'den Metin Çıkarma – Tam Aspose OCR Öğreticisi
tags:
- Aspose OCR
- C#
- Image Processing
title: PNG'den Metin Çıkar – Tam Aspose OCR Öğreticisi
url: /tr/net/text-recognition/extract-text-from-png-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkarma – Tam Aspose OCR Öğreticisi

Hiç **PNG'den metin çıkar** gerekti ve sonuçlar anlamsız karakterlerle doluydu mu? Yalnız değilsiniz. Birçok gerçek dünya projesinde – faturalar, makbuzlar veya taranmış formlar – OCR çıktısının kalitesi otomasyon hatlarını belirleyebilir.  

Bu rehberde, Aspose OCR kullanarak görüntü metnini okumanın **adım‑adım** bir yolunu, OCR doğruluğunu **artırmak** için özel bir sözlük eklemeyi, gürültüyü temizlemeyi ve sonunda düzenli bir dize yazdırmayı göstereceğiz. Sonunda, PNG görüntülerinden güvenilir bir şekilde metin çıkaran, çalıştırmaya hazır bir C# konsol uygulamanız olacak.

> **Ne kazanacaksınız**  
> * Tam, çalıştırılabilir bir kod örneği.  
> * Özel bir sözlüğün neden önemli olduğunu anlama.  
> * Düşük kontrastlı taramalar gibi kenar durumlarını ele alma ipuçları.  

## Önkoşullar

- .NET 6 SDK veya daha yenisi (kod .NET 6 hedefli, ancak .NET 5 de çalışır).  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör.  
- İşlemek istediğiniz bir **PNG** görüntüsü – örneğin `invoice.png`.  
- **Aspose.OCR** NuGet paketi (`dotnet add package Aspose.OCR`).  

Ek yapılandırma dosyalarına gerek yok; her şey tek bir `.cs` dosyasında bulunur.

## 1. Adım – Aspose OCR'yi Kur ve Referans Ekle

İlk olarak, kütüphaneyi projenize ekleyin. Çözüm klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu tek satır, en son kararlı sürümü (Ocak 2026 itibarıyla sürüm 23.9) getirir. Paket, öğreticide boyunca kullanacağımız `OcrEngine` sınıfını içerir.

## 2. Adım – OCR Motorunu Başlat

`OcrEngine` örneği oluşturmak temeldir. Bunu, pikselleri yorumlamaya hazır bir tarayıcıyı açmak gibi düşünün.

```csharp
using Aspose.OCR;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

> **Pro ipucu:** Bir döngüde çok sayıda görüntü işleyecekseniz aynı `OcrEngine` örneğini yeniden kullanın. İç kaynakları önbelleğe alır ve sonraki çağrıları hızlandırır.

## 3. Adım – Özel Bir Sözlük ile Doğruluğu Artırma

Hazır OCR iyidir, ancak “Aspose”, “OCR” veya “SDK” gibi alan‑özel kelimelerde takılabilir. Bu terimleri bir **özel sözlüğe** eklemek, motorun bu dizeleri geçerli olarak kabul etmesini sağlar ve yanlış tanıma olasılığını azaltır.

```csharp
// Define domain‑specific terms that the engine should recognize
ocrEngine.CustomDictionary = new HashSet<string>
{
    "Aspose",
    "OCR",
    "SDK",
    "invoice"
};
```

### Özel bir sözlüğün neden yardımcı olduğu

- OCR'nin arkasındaki **istatistiksel modeller**, yaygın dil kalıplarına büyük ağırlık verir. Nadir kelimeler düşük olasılık alır ve benzer görünümlü karakterlerle değiştirilebilir.  
- Bunları açıkça listeleyerek modelin tahminini geçersiniz.  
- Özellikle **görüntü metnini okuma** içinde ürün kodları, kısaltmalar veya marka adları bulunan durumlarda kullanışlıdır.

## 4. Adım – PNG Dosyasından Metni Tanıma

Şimdi motoru görüntü yoluyla besliyoruz. `RecognizeImage` yöntemi, motorun eşleştiremediği bilinmeyen tokenları (ör. “#@!”) içeren ham bir dize döndürür.

```csharp
// Path to the PNG you want to process
string imagePath = @"YOUR_DIRECTORY/invoice.png";

// Perform OCR
string rawText = ocrEngine.RecognizeImage(imagePath);
```

> **Köşe durumu:** Dosya bulunamazsa, `RecognizeImage` bir `FileNotFoundException` fırlatır. Üretim kodu için çağrıyı bir try‑catch bloğuna sarın.

## 5. Adım – Sonucu `CleanText` ile Temizleme

Aspose OCR, “bilinmeyen” olarak işaretlediği karakterleri temizleyen bir yardımcı ile birlikte gelir. Bu adım, **görüntüden metin çıkarma** projelerinde, sonraki ayrıştırıcıların yalnızca alfanümerik ve temel noktalama işaretleri beklediği durumlarda kritiktir.

```csharp
// Remove unknown tokens and extra whitespace
string cleanedText = ocrEngine.CleanText(rawText);
```

`CleanText` yöntemi ayrıca satır sonlarını normalleştirir, çıktının veritabanlarında saklanmasını veya diğer hizmetlere aktarılmasını güvenli hâle getirir.

## 6. Adım – Temizlenmiş Metni Çıktılamak

Son olarak, sonucu gösterin veya saklayın. Bir konsol uygulamasında `Console.WriteLine` iş görür.

```csharp
Console.WriteLine("=== Cleaned OCR Output ===");
Console.WriteLine(cleanedText);
```

Programı çalıştırdığınızda, `invoice.png` içeriğini yansıtan düzenli bir metin bloğu görmelisiniz. Görüntü “Aspose” kelimesini içeriyorsa, özel sözlük bunun doğru şekilde görünmesini, “A5p0se” gibi bir şey yerine sağlamasını garantiler.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz tam `Program.cs` dosyasını aşağıda bulabilirsiniz:

```csharp
using Aspose.OCR;
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new OcrEngine();

        // 2️⃣ Add domain‑specific terms to improve OCR accuracy
        ocrEngine.CustomDictionary = new HashSet<string>
        {
            "Aspose",
            "OCR",
            "SDK",
            "invoice"
        };

        // 3️⃣ Path to your PNG file (adjust as needed)
        string imagePath = @"YOUR_DIRECTORY/invoice.png";

        try
        {
            // 4️⃣ Recognize raw text from the image
            string rawText = ocrEngine.RecognizeImage(imagePath);

            // 5️⃣ Clean up unknown tokens
            string cleanedText = ocrEngine.CleanText(rawText);

            // 6️⃣ Show the result
            Console.WriteLine("=== Cleaned OCR Output ===");
            Console.WriteLine(cleanedText);
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

**Beklenen çıktı** (PNG basit bir fatura içeriyorsa):

```
=== Cleaned OCR Output ===
Invoice #12345
Date: 01/08/2026
Total: $1,250.00
Thank you for your business!
```

Eğer garip semboller görürseniz, görüntü kalitesini tekrar kontrol edin veya özel sözlüğü daha fazla terim ekleyerek genişletin.

## Bonus: Düşük Kaliteli Taramalarla Baş Etme

Bazen PNG'ler 72 dpi'de taranır veya yoğun sıkıştırma artefaktları içerir. C#'tan çıkmadan **OCR doğruluğunu artırmak** için birkaç hızlı ipucu:

1. `SixLabors.ImageSharp` gibi bir kütüphane ile **görüntüyü ön‑işlemeye** alın – kontrastı artırın, gri tonlamaya dönüştürün veya gürültüyü azaltmak için hafif bir bulanıklık uygulayın.  
2. `OcrEngine` üzerindeki `Resolution` özelliğini ayarlayın (ör. `ocrEngine.Resolution = 300;`) motorun görüntüyü daha yüksek çözünürlükte işlemesini söylemek için.  
3. İngilizce dışı metinlerle çalışıyorsanız **dil paketlerini etkinleştirin** (`ocrEngine.Language = Language.English;`).  

Bu üç yaklaşım da `RecognizeImage` çağrısından önce eklenebilir.

## Sık Sorulan Sorular

- **Bu diğer görüntü formatlarıyla çalışır mı?**  
  Evet. `RecognizeImage` JPEG, BMP, TIFF ve hatta PDF (görüntü konteyneri olarak) kabul eder. Aynı adımlar geçerlidir.

- **Bir klasördeki birden fazla PNG'den metin çıkarabilir miyim?**  
  Kesinlikle. Temel mantığı `foreach (var file in Directory.GetFiles(folder, "*.png"))` döngüsüyle sarın ve her sonucu bir listeye kaydedin ya da ayrı dosyalara yazın.

- **Metin koordinatlarına ihtiyacım olursa ne yapmalıyım?**  
  Aspose OCR, sınırlama kutuları içeren `OcrResult` nesneleri de sağlar. Bu gelişmiş senaryo için `ocrEngine.RecognizeImageToResult(imagePath)` kullanın.

## Sonuç

Aspose OCR kullanarak **PNG dosyalarından metin çıkarma** için **tam, uçtan uca** bir çözüm üzerinden geçtik. Motoru başlatarak, ona bir **özel sözlük** vererek, ham çıktıyı temizleyerek ve birkaç yaygın sorunu ele alarak, kendi C# uygulamalarınızda **görüntü metnini okuyabilir** ve **OCR doğruluğunu artırabilirsiniz**.

Bir sonraki adıma hazır mısınız? PNG'yi taranmış bir makbuzla değiştirin, sözlüğe daha fazla alan‑özel kelime ekleyin veya çıktıyı otomatik fatura işleme için bir veritabanına entegre edin. Aspose OCR'yi .NET'in zengin ekosistemiyle birleştirdiğinizde sınır yoktur.

Kodlamaktan keyif alın ve OCR'niz her zaman kusursuz olsun! 

![Extract text from png example](/images/extract-text-from-png.png "extract text from png – Aspose OCR demo")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}