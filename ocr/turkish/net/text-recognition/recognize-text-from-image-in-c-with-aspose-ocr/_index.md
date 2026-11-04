---
category: general
date: 2026-02-22
description: C#'ta Aspose OCR kullanarak görüntüden metin tanıma. PNG'den metin çıkarma,
  görüntüyü metne dönüştürme ve lisanslama için gömülü kaynağı okuma adım adım rehberi.
draft: false
keywords:
- recognize text from image
- extract text from png
- convert image to text
- read embedded resource c#
- perform ocr on image
language: tr
og_description: Aspose OCR ile görüntüden metni anında tanıyın. PNG'den metin çıkarmayı,
  görüntüyü metne dönüştürmeyi ve sorunsuz lisanslama için gömülü kaynağı C#'ta okumayı
  öğrenin.
og_title: C#'de görüntüden metin tanıma – Tam Aspose OCR Öğreticisi
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# ile Aspose OCR kullanarak görüntüden metin tanıma
url: /tr/net/text-recognition/recognize-text-from-image-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose OCR kullanarak görüntüden metin tanıma

Görüntüden metin tanıma ihtiyacınız oldu ama C#’ta nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—çoğu geliştirici OCR ile ilk karşılaştıklarında aynı duvara çarpar. Bu öğreticide, **png’den metin çıkarma**, **görüntüyü metne dönüştürme** ve lisanslama için **embedded resource c#** okuma gibi işlemleri sorunsuz bir şekilde yapmanızı sağlayacak çalışan bir çözüme doğrudan dalacağız.

Gömülü bir Aspose OCR lisansını yüklemekten son string’i konsola yazdırmaya kadar her şeyi ele alacağız. Sonunda, herhangi bir .NET projesine ekleyip hemen çalıştırabileceğiniz bağımsız bir programınız olacak.

## Gereksinimler

- **.NET 6+** (kod .NET Framework’te de derlenebilir, ancak .NET 6 güncel LTS’dir)
- **Aspose.OCR for .NET** NuGet paketi (sürüm 23.9 veya daha yeni)
- Açık ve okunaklı İngilizce metin içeren bir **örnek PNG** resmi
- Projenize *Embedded Resource* olarak eklenmiş bir **Aspose OCR lisans dosyası** (`Aspose.OCR.lic`)

Eğer bu maddeler size yabancı geliyorsa endişelenmeyin—her adımda nasıl kuracağınızı açıklayacağız.

## Adım 1: Embedded Resource C# Lisansını Okuma  

OCR motorunun çalışabilmesi için Aspose geçerli bir lisansa ihtiyaç duyar. `.lic` dosyasını gömülü kaynak olarak saklamak, dosyanın kaynak kontrolüne sızmasını önler ve dağıtımı sorunsuz hâle getirir.

```csharp
using System;
using System.Reflection;
using Aspose.OCR;

class Program
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Load the embedded Aspose OCR license
        // ------------------------------------------------------------
        var assembly = Assembly.GetExecutingAssembly();

        // The resource name follows the folder hierarchy in the project.
        // Adjust "MyApp.Resources.Aspose.OCR.lic" if yours differs.
        using (var licenseStream = assembly.GetManifestResourceStream(
               "MyApp.Resources.Aspose.OCR.lic"))
        {
            if (licenseStream == null)
            {
                Console.Error.WriteLine(
                    "License file not found. Make sure it's marked as Embedded Resource.");
                return;
            }

            var license = new License();
            license.SetLicenseFromStream(licenseStream);
        }

        // Continue with OCR steps...
```

**Neden önemli:**  
Lisansı gömmek, kaynak kontrolünde yanlışlıkla ifşa olmasını engeller ve dosyanın derlenmiş DLL ile birlikte taşınmasını garantiler. Akış `null` ise program erken sonlanır—bu bizim ilk savunma kontrolümüzdür.

## Adım 2: OCR Motorunu Başlatma (Görüntüde OCR Çalıştırma)  

Lisans yüklendiğine göre bir `OcrEngine` örneği oluşturabiliriz. Dilimizi İngilizce olarak ayarlayacağız çünkü örnek PNG bu dili kullanıyor.

```csharp
        // ------------------------------------------------------------
        // 2️⃣ Initialise the OCR engine – this is where we perform OCR on image
        // ------------------------------------------------------------
        var ocrEngine = new OcrEngine
        {
            Language = Language.English   // change to Language.French etc. if needed
        };
```

**İpucu:** `Language` enum’u 30’dan fazla dili destekler. Değiştirmek sadece `Language.Spanish` gibi bir değer atamak kadar basittir. Çok‑dilli algılama ihtiyacınız olursa ayrı motorlar oluşturabilir veya `ocrEngine.AutoDetectLanguage = true` (daha yeni Aspose sürümlerinde mevcut) kullanabilirsiniz.

## Adım 3: PNG Görüntüyü Yükleme (PNG’den Metin Çıkarma)  

Aspose OCR, `System.Drawing.Image` yerine kendi `Image` sınıfını kullanır. Dosya yolunu gösterebilir ya da isterseniz bir `Stream` verebilirsiniz.

```csharp
        // ------------------------------------------------------------
        // 3️⃣ Load the image – this is the step where we extract text from png
        // ------------------------------------------------------------
        const string imagePath = "YOUR_DIRECTORY/sample.png";

        if (!System.IO.File.Exists(imagePath))
        {
            Console.Error.WriteLine($"Image not found at {imagePath}");
            return;
        }

        var image = Image.Load(imagePath);
```

**Köşe durumu:** PNG’niz alfa kanalı (şeffaf arka plan) içeriyorsa Aspose boşlukları yanlış yorumlayabilir. Hızlı bir çözüm, resmi `ImageProcessor` ile düzleştirerek ön işlemektir; ancak çoğu taranmış belge için varsayılan yükleyici yeterlidir.

## Adım 4: Tanıma İşlemini Çalıştırma (Görüntüyü Metne Dönüştürme)  

Motor ve görüntü hazır olduğunda gerçek OCR çağrısı tek bir satırdır. Sonuç nesnesi ham string’i ve bir güven puanını verir.

```csharp
        // ------------------------------------------------------------
        // 4️⃣ Recognise the image – this is where we convert image to text
        // ------------------------------------------------------------
        var ocrResult = ocrEngine.Recognize(image);

        // Optional: check confidence (0‑100)
        Console.WriteLine($"Confidence: {ocrResult.Confidence}%");
```

**Güven puanının önemi:**  
Düşük bir güven (%70’in altında gibi) genellikle bulanık tarama ya da desteklenmeyen bir fonta işaret eder. Üretimde farklı bir OCR motoruna geçiş yapabilir veya kullanıcıdan yeniden tarama isteyebilirsiniz.

## Adım 5: Tanınan Metni Çıktı Alma  

Son olarak çıkarılan string’i ekrana yazdırın. Gerçek bir uygulamada bunu bir veritabanına, JSON dosyasına ya da bir arama indeksine gönderebilirsiniz.

```csharp
        // ------------------------------------------------------------
        // 5️⃣ Output the recognised text – the final result of recognize text from image
        // ------------------------------------------------------------
        Console.WriteLine("\n--- Recognised Text ---");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Beklenen Konsol Çıktısı

```
Confidence: 96%
--- Recognised Text ---
Hello, world!
This is a sample PNG used for OCR testing.
```

Yukarıdaki metni (veya benzerini) görüyorsanız tebrikler—Aspose OCR ile **görüntüden metin tanıma** işlemini başarıyla tamamladınız!

## Yaygın Tuzaklar ve Çözümleri  

| Belirti | Muhtemel Neden | Çözüm |
|---------|----------------|------|
| `License not set` hatası | Lisans dosyası gömülmemiş ya da kaynak adı yanlış | `Build Action = Embedded Resource` olduğundan emin olun ve tam nitelikli adı iki kez kontrol edin |
| Boş çıktı | Görüntü DPI’sı düşük (150’nin altında) | PNG’yi en az 150 DPI’ye yeniden örnekleyerek Aspose’a besleyin |
| Bozuk karakterler | Yanlış dil seçilmiş | `ocrEngine.Language` değerini doğru `Language` enum’una ayarlayın |
| Büyük görüntülerde `OutOfMemoryException` | 10 MB+ bir PNG doğrudan yükleniyor | `Image.Load(stream, maxWidth: 2000, maxHeight: 2000)` ile anlık küçültme yapın |

## Pro İpucu: Toplu İşleme  

Birden çok **görüntüden metin tanıma** dosyasını toplu olarak işlemek istiyorsanız, temel mantığı bir `foreach` döngüsü içinde sarın ve aynı `OcrEngine` örneğini yeniden kullanın. Motoru yeniden kullanmak, yerel kütüphanelerin bellekte kalması sayesinde dosya başına birkaç milisaniye tasarruf sağlar.

```csharp
var images = System.IO.Directory.GetFiles("YOUR_DIRECTORY", "*.png");
foreach (var path in images)
{
    var img = Image.Load(path);
    var result = ocrEngine.Recognize(img);
    Console.WriteLine($"{path} → {result.Text.Trim()}");
}
```

## Sonraki Adımlar  

- **Ön işleme ince ayarı** – kontrastı artırmak veya gürültüyü kaldırmak için `ImageProcessor` deneyin.  
- **Diğer çıktı formatlarını keşfedin** – `ocrResult.GetWords()` size sınırlayıcı kutular verir, UI’da metni vurgulamak için kullanışlıdır.  
- **Azure Cognitive Services** ile birleştirin; bulut tabanlı el yazısı desteği gerekiyorsa.

Tüm bu uzantılar aynı temel deseni izler: lisansı yükle, motoru oluştur, bir görüntü besle ve metni oku.

![Screenshot of console showing recognized text from image](/images/ocr-result.png "recognize text from image result screenshot")

## Sonuç  

C# ile Aspose OCR kullanarak **görüntüden metin tanıma** nasıl yapılır konusunu baştan sona, üretim‑hazır bir örnekle ele aldık. Gömülü kaynak lisansını okumaktan PNG yüklemeye, OCR çalıştırmaya ve sonucu yazdırmaya kadar her adımı kapsadık.

Artık birkaç düzine satır kodla **png’den metin çıkarma**, **görüntüyü metne dönüştürme** ve lisanslama için **embedded resource c#** okuma işlemlerini gerçekleştirebilirsiniz. Farklı diller, daha büyük görüntü topluları ya da çıktıyı kendi belge‑işleme hattınıza entegre etme konusunda özgürce denemeler yapın. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}