---
category: general
date: 2026-02-14
description: Aspose OCR'i C#'ta kullanarak görüntüdeki eğimi nasıl kaldıracağınızı,
  OCR için görüntüyü nasıl ön işleme yapacağınızı, görüntüdeki gürültüyü nasıl azaltacağınızı
  ve görüntüden metin nasıl çıkaracağınızı öğrenin.
draft: false
keywords:
- remove skew from image
- preprocess image for ocr
- reduce noise in image
- extract text from image
- recognize text from document
language: tr
og_description: Görüntüdeki eğikliği kaldırın, OCR için görüntüyü ön işleme tabi tutun
  ve Aspose OCR kullanarak adım adım bir C# öğreticisiyle görüntüden metin çıkarın.
og_title: Görüntüdeki Eğimi Kaldır – Tam OCR Ön İşleme Rehberi
tags:
- OCR
- CSharp
- ImageProcessing
title: Görüntüdeki Eğimi Kaldır – Tam OCR Ön İşleme Rehberi
url: /tr/net/skew-angle-calculation/remove-skew-from-image-complete-ocr-pre-processing-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Eğimi Kaldırma – Tam OCR Ön İşleme Kılavuzu

Bir OCR motoruna vermeden önce **remove skew from image** yapmanız gerektiğinde hiç oldu mu? Tek başınıza değilsiniz—taratılmış belgeler, makbuz fotoğrafları veya ekran görüntüleri sık sık eğik gelir ve bu küçük açı metin tanımasını sabote edebilir.  

İyi haber? Birkaç Aspose OCR filtresiyle görüntüyü düzleştirebilir, gürültüyü azaltabilir, kontrastı artırabilir ve ardından **extract text from image** tek bir akıcı boru hattında gerçekleştirebilirsiniz. Bu kılavuzda, eğik bir resmi yüklemekten **recognize text from document** yapıp sonucu yazdırmaya kadar tüm süreci adım adım inceleyeceğiz.

---

## Oluşturacağınız Şey

Bu öğreticinin sonunda, aşağıdaki özelliklere sahip çalışan bir C# konsol uygulamanız olacak:

1. `DeskewFilter` kullanarak **Removes skew from image**.
2. `DenoiseFilter` ile **Reduces noise in image**.
3. Kontrastı artırarak **Preprocesses image for OCR**.
4. Aspose OCR’nin `Engine`i aracılığıyla **Recognizes text from document**.
5. **Extracts text from image** ve konsolda görüntüler.

Harici hizmet yok, sadece Aspose OCR NuGet paketi ve birkaç satır kod.

---

## Önkoşullar

- .NET 6.0 SDK veya daha yeni (kod .NET Core ve .NET Framework ile de çalışır).  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör.  
- Aspose.OCR for .NET yüklü (`dotnet add package Aspose.OCR`).  
- Referans alabileceğiniz bir klasöre yerleştirilmiş örnek bir görüntü (`skewed_noisy.jpg`).

Bu şartlar sağlandıysa, başlayalım.

---

## Adım 1: Kaynak Görüntüyü Yükleyin

İlk olarak temizlemek istediğimiz dosyaya işaret eden bir `ImageStream` oluşturmamız gerekiyor.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source image that needs cleaning
ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Why this matters:** `ImageStream` temel bitmap’i soyutlayarak Aspose filtrelerinin ham piksel verisiyle uğraşmadan çalışmasını sağlar.

---

## Adım 2: Ön İşleme Boru Hattı Oluşturun (Remove Skew & Reduce Noise)

Her filtreyi ayrı ayrı çağırmak yerine, Aspose bunları bir `ImageProcessingPipeline` içinde zincirlemenize izin verir. Bu, kodu düzenli tutar ve işlemlerin doğru sırayla gerçekleşmesini sağlar.

```csharp
// Create a pipeline and add desired filters
var processingPipeline = new ImageProcessingPipeline()
    .AddFilter(new DeskewFilter())                     // Remove skew
    .AddFilter(new DenoiseFilter())                    // Reduce noise
    .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)
```

### Sıralamanın Önemi

1. **Deskew first** – Görüntüyü denoise etmeden önce düzleştirmek, gürültü filtresinin eğik kenarları artefakt olarak algılamasını önler.  
2. **Denoise second** – Resim düz olduğunda algoritma sinyal ile gren arasını daha iyi ayırabilir.  
3. **Contrast boost last** – Görüntü temizlendikten sonra kontrastı artırmak, OCR okunurluğunu maksimize ederken gürültüyü artırmaz.

---

## Adım 3: Boru Hattını Uygulayın ve Temizlenmiş Görüntüyü Alın

Şimdi orijinal akışa karşı boru hattını çalıştırıyoruz.

```csharp
// Apply the pipeline to obtain a cleaned image
ImageStream cleanedImage = processingPipeline.Apply(sourceImage);
```

Bu noktada görüntü düzleştirilmiş, gürültüsü azaltılmış ve kontrastı artırılmış durumda—OCR için mükemmel.

---

## Adım 4: OCR Motorunu Başlatın ve Metni Tanıyın

Parlak bir görüntümüz olduğuna göre, artık Aspose OCR’ye besleyebiliriz.

```csharp
// Initialise the OCR engine
Engine ocrEngine = new Engine();

// Recognise text from the cleaned image
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

> **Tip:** Dil‑spesifik ayarlama gerekiyorsa, `Engine` bir `Language` özelliği kabul eder (ör. `ocrEngine.Language = Language.English;`). Çoğu Latin‑tabanlı belge için varsayılan ayar yeterlidir.

---

## Adım 5: Çıkarılan Metni Görüntüleyin

Kısa bir `Console.WriteLine` sonucu gösterir.

```csharp
// Output the extracted text
Console.WriteLine(ocrResult.Text);
```

Programı çalıştırdığınızda `skewed_noisy.jpg` dosyasının metin içeriğinin terminale temiz, okunaklı ve sonraki işlemlere hazır bir şekilde yazdırıldığını görmelisiniz.

---

## Tam Çalışan Örnek

Aşağıda tamamen kopyala‑yapıştır hazır program yer alıyor. `Program.cs` olarak kaydedin, `YOUR_DIRECTORY` kısmını gerçek yol ile değiştirin ve `dotnet run` komutunu çalıştırın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace ImageOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Load the source image that needs cleaning
            ImageStream sourceImage = ImageStream.FromFile("YOUR_DIRECTORY/skewed_noisy.jpg");

            // Step 2: Create an image‑processing pipeline and add desired filters
            var processingPipeline = new ImageProcessingPipeline()
                .AddFilter(new DeskewFilter())                     // Remove skew
                .AddFilter(new DenoiseFilter())                    // Reduce noise
                .AddFilter(new ContrastBoostFilter { Level = 30 });// Boost contrast (0‑100)

            // Step 3: Apply the pipeline to obtain a cleaned image
            ImageStream cleanedImage = processingPipeline.Apply(sourceImage);

            // Step 4: Initialise the OCR engine and recognize text from the cleaned image
            Engine ocrEngine = new Engine();
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Step 5: Display the extracted text
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Beklenen çıktı** (basit bir makbuz örneği):

```
=== Extracted Text ===
Store: Coffee Corner
Date: 02/12/2026
Item          Qty   Price
Latte          2    $5.80
Croissant      1    $2.50
Total                $8.30
```

Çıktı bozuk görünüyorsa, görüntü yolunun doğru olduğundan ve kaynak dosyanın gerçekten okunabilir metin içerdiğinden emin olun.

---

## Yaygın Sorular ve Kenar Durumları

### Görüntü hafif bir eğim yerine 90° döndürülmüşse ne olur?

`DeskewFilter` küçük açıları (±15°) işler. Tam dönüşler için, deskew adımından önce `new RotateFilter { Angle = 90 }` çağırın.

### Görüntüm PNG formatında—herhangi bir değişiklik olur mu?

Hayır. `ImageStream.FromFile` formatı otomatik algılar, bu yüzden PNG, JPEG, BMP veya TIFF aynı şekilde çalışır.

### Gürültü azaltma gücünü nasıl ayarlayabilirim?

`DenoiseFilter` bir `Strength` özelliği (0‑100) sunar. Yüksek değerler daha fazla gren temizler ancak ince detayları bulanıklaştırabilir. Metin ağırlıklı belgeler için 30‑50 civarında değerlerle deneme yapın.

### Bir dosya topluluğunu işlemek istiyorum—boru hattını yeniden kullanabilir miyim?

Kesinlikle. `processingPipeline`ı bir kez oluşturup ardından her dosya için döngüye sokun:

```csharp
foreach (var path in Directory.GetFiles("batch_folder", "*.jpg"))
{
    var src = ImageStream.FromFile(path);
    var cleaned = processingPipeline.Apply(src);
    var result = ocrEngine.Recognize(cleaned);
    // Save or log result.Text
}
```

Aynı `Engine` örneğini yeniden kullanmak da performansı artırır.

---

## Üretim‑Hazır OCR için Pro İpuçları

- **Cache the pipeline**: Filtreleri tekrar tekrar örneklemek yüksek hacimli senaryolarda maliyetli olabilir.  
- **Set OCR language**: `ocrEngine.Language = Language.Spanish;` gibi ayarlar, İngilizce dışı belgeler için kullanılabilir.  
- **Handle empty results**: İlerlemeye geçmeden önce her zaman `ocrResult.Text?.Length > 0` kontrol edin.  
- **Log intermediate images**: `cleanedImage`ı diske kaydetmek (`cleanedImage.Save("debug.png");`) filtre parametrelerini ince ayar yapmanıza yardımcı olur.

---

## Sonuç

Aspose OCR’nin güçlü filtre boru hattını kullanarak **remove skew from image**, **reduce noise in image** ve **preprocess image for OCR** işlemlerini nasıl gerçekleştireceğimizi, ardından **recognize text from document** ve **extract text from image** adımlarını gösterdik. Tüm iş akışı 50 satırın altında C# kodu ile gerçekleşir ve toplu işleme, özel dil modelleri veya ek filtreler için kolayca genişletilebilir.

Bir sonraki adıma hazır mısınız? Siyah‑beyaz çıktı zorlamak için bir `BinarizeFilter` ekleyin ya da farklı `ContrastBoostFilter` seviyeleriyle deneme yaparak tanıma doğruluğuna etkisini görün. Boru hattıyla ne kadar çok oynarsanız, her filtrenin temiz bir OCR sonucuna nasıl katkı sağladığını o kadar iyi anlarsınız.

İyi kodlamalar, ve görüntüleriniz her zaman düz kalsın!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}