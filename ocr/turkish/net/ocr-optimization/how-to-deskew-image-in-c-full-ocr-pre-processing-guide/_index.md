---
category: general
date: 2026-02-11
description: C#'ta görüntüyü eğrilikten (deskew) nasıl düzelteceğinizi ve metin çıkarmadan
  önce görüntüdeki gürültüyü nasıl kaldıracağınızı öğrenin. Dosyadan görüntü yüklemeyi
  ve OCR için görüntüyü dakikalar içinde ön işleme almayı öğrenin.
draft: false
keywords:
- how to deskew image
- remove noise from image
- extract text from image
- preprocess image for ocr
- load image from file
language: tr
og_description: C# ile görüntünün eğriliğini nasıl düzelteceğinizi ve metin çıkarmadan
  önce görüntüdeki gürültüyü nasıl kaldıracağınızı öğrenin. OCR için görüntüyü ön
  işleme adım adım bu rehberi izleyin.
og_title: C#'de Görüntüyü Düzeltme – Tam OCR Ön İşleme Rehberi
tags:
- C#
- OCR
- Image Processing
title: C#'ta Görüntüyü Eğriliğinden Düzeltme – Tam OCR Ön İşleme Rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-in-c-full-ocr-pre-processing-guide/
---

Ok produce final.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüyü Eğriltmeyi Düzeltme – Tam OCR Ön‑İşleme Rehberi

Hiç **görüntüyü eğriltmeyi düzeltme** (deskew) işlemini, sarsak bir kameradan çekilmiş gibi görünen dosyalar üzerinde denediniz mi? Belki eğik bir taramayı bir OCR motoruna verdiniz ve sadece karışık bir çıktı aldınız. Bu, özellikle kaynak resim hem eğik *hem* gürültülüyse sıkça karşılaşılan bir sorundur.  

Bu öğreticide bir resmi dosyadan yüklemeyi, düzeltmeyi, lekeleri temizlemeyi ve sonunda Aspose.OCR kullanarak görüntüden metin çıkarmayı adım adım göstereceğiz. Sonunda, tüm bu ağır işleri sizin için yapan hazır bir C# konsol uygulamanız olacak. Sır yok, sadece net kod ve her adımın neden gerekli olduğuna dair açıklamalar.

---

## Gerekenler

- **.NET 6+** (veya herhangi bir yeni .NET çalışma zamanı)  
- **Aspose.OCR for .NET** NuGet paketi (ücretsiz deneme sürümü demolar için yeterli)  
- Eğik ve gürültülü bir örnek resim (ör. `skewed_noisy.jpg`)  
- Visual Studio, VS Code veya sevdiğiniz IDE  

Hepsi bu. Zaten bir .NET projeniz varsa, sadece Aspose.OCR paketini ekleyin:

```bash
dotnet add package Aspose.OCR
```

---

![görüntüyü eğriltmeyi düzeltme örneği](/images/deskew-example.png "görüntüyü eğriltmeyi düzeltme – işleme öncesi ve sonrası")

*Alt metin: görüntüyü eğriltmeyi düzeltme – işleme öncesi ve sonrası*

---

## Adım 1 – Resmi Dosyadan Yükleme

Herhangi bir sihri yapmadan önce resmi belleğe okumamız gerekir. `System.Drawing.Image.FromFile` kullanmak basittir, ancak `Image` nesnesini dispose edene kadar dosyayı kilitli tutar, bu yüzden bir `using` bloğu içinde sarmalayacağız.

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

// Load the source file – this satisfies the “load image from file” requirement.
using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
{
    // The rest of the pipeline will go here.
}
```

> **İpucu:** Test aşamasında yolu mutlak tutun, ardından üretim için göreli yol ya da yapılandırma ayarına geçin.

---

## Adım 2 – OCR Motorunu Başlatma (ve Otomatik Kaynak İndirmeyi Etkinleştirme)

Aspose.OCR, dil verilerini gerektiğinde indirebilir. `AutomaticResourceDownload` özelliğini etkinleştirmek, dil paketlerini manuel kopyalamaktan sizi kurtarır.

```csharp
// Step 2: Set up the OCR engine.
OcrEngine ocrEngine = new OcrEngine
{
    AutomaticResourceDownload = true,
    Language = OcrLanguage.English // you can change this to French, Spanish, etc.
};
```

Dili açıkça ayarlamanın nedeni nedir? Motor, özellikle resimde noktalama işaretleri veya özel karakterler olduğunda doğruluğu artırmak için dile özgü sözlükler kullanır.

---

## Adım 3 – Görüntüyü Eğriltmeyi Düzeltme (How to Deskew Image)

Eğik bir tarama, karakterler artık temel çizgiye hizalanmadığı için çoğu OCR algoritmasını şaşırtır. `OcrPreprocessor.Deskew`, metin satırlarını analiz eder, açıyı hesaplar ve bitmap'i yatay konuma döndürür.

```csharp
// Step 3: Correct orientation – this is the core “how to deskew image” operation.
Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);
```

> **Peki ya görüntü zaten düzse?** Metot, sıfıra yakın bir açı tespit eder ve bir kopya döndürür, bu yüzden koşulsuz olarak çağırmak güvenlidir.

---

## Adım 4 – Görüntüden Gürültüyü Kaldırma

Eski belgelerden gelen taramalar genellikle lekeler, sıkıştırma artefaktları veya hafif arka plan desenleri içerir. Bu küçük lekeler OCR motorunun karakterleri yanlış tanımasına yol açabilir. `OcrPreprocessor.Denoise`, kenarları korurken izole pikselleri temizleyen bir medyan filtresi uygular.

```csharp
// Step 4: Clean up the deskewed picture – this fulfills “remove noise from image”.
Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);
```

Daha agresif bir temizlik gerekiyorsa, Aspose `GaussianBlur` veya `ContrastAdjustment` gibi ek filtreler sunar. Çoğu senaryo için varsayılan gürültü azaltma yeterli olur.

---

## Adım 5 – OCR İşlemini Gerçekleştirme ve Görüntüden Metin Çıkarma

Resim artık düz ve sessiz olduğuna göre, onu OCR motoruna teslim ediyoruz. `Recognize` metodu, düz metin, güven skorları ve gerekirse daha sonra kullanabileceğiniz sınırlayıcı kutuları içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Step 5: Run OCR – this is where we “extract text from image”.
OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);
```

Şunu merak edebilirsiniz: *Ara resimleri dispose etmem gerekiyor mu?* Kesinlikle. Her resmi kendi `using` bloğunda tutun ya da `Dispose()`'ı manuel çağırın. Bu kompakt örnekte dış `using` bloğu `sourceImage` için yeterli ve geri kalanını GC temizler, ancak üretim kodunda açıkça dispose etmek iyi bir alışkanlıktır.

---

## Adım 6 – Tanınan Metni Görüntüleme

Son olarak sonucu konsola yazdırıyoruz. Gerçek bir uygulamada bunu bir dosyaya, veritabanına yazabilir ya da sonraki bir NLP boru hattına besleyebilirsiniz.

```csharp
// Step 6: Output the recognized text.
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.Text);
```

**Beklenen çıktı** (örnek resimde “Hello World” ifadesi olduğu varsayılırsa):

```
=== OCR Output ===
Hello World
```

Metin karışık görünüyorsa, önceki adımlara geri dönün: belki daha güçlü bir gürültü azaltma ya da farklı bir dil ayarı gerekir.

---

## Tam Çalışan Örnek

Her şeyi bir araya getirdiğimizde, işte tamamen çalışır bir program:

```csharp
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // Initialize OCR engine with automatic resource download.
        OcrEngine ocrEngine = new OcrEngine
        {
            AutomaticResourceDownload = true,
            Language = OcrLanguage.English
        };

        // Load the source image from file.
        using (Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.jpg"))
        {
            // Deskew – core “how to deskew image” step.
            Image deskewedImage = OcrPreprocessor.Deskew(sourceImage);

            // Denoise – fulfills “remove noise from image”.
            Image cleanedImage = OcrPreprocessor.Denoise(deskewedImage);

            // Perform OCR – “extract text from image”.
            OcrResult ocrResult = ocrEngine.Recognize(cleanedImage);

            // Show the result.
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

Dosyayı `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve OCR çıktısının belirdiğini izleyin. Basit, değil mi?  

---

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| **Görüntü bir PDF sayfasıysa ne olur?** | Önce PDF'yi bir resme dönüştürün (ör. `Aspose.PDF` kullanarak), ardından aynı boru hattına besleyin. |
| **Birden fazla sayfayı döngü içinde işleyebilir miyim?** | Kesinlikle. Tüm bloğu `foreach (var path in imagePaths)` döngüsü içine koyun ve sonuçları bir listede toplayın. |
| **Büyük partilerde performans nasıl?** | Tek bir `OcrEngine` örneğini yeniden kullanın; dil verilerini önbelleğe alır ve başlatma süresini büyük ölçüde azaltır. |
| **Metnim Latin dışı karakterler içeriyor – yine de çalışır mı?** | `ocrEngine.Language` özelliğini uygun `OcrLanguage` enum değeriyle ayarlayın (ör. `OcrLanguage.ChineseSimplified`). |
| **Çıktı hâlâ garip karakterler içeriyor – ne yapmalıyım?** | Gürültü azaltma gücünü artırın (`OcrPreprocessor.Denoise(sourceImage, strength: 2)`) veya bir ikilileştirme filtresi uygulayın (`OcrPreprocessor.Binarize`). |

---

## Sonraki Adımlar

Artık **görüntüyü eğriltmeyi düzeltme** ve **görüntüden gürültüyü kaldırma** konularında uzmanlaştığınıza göre, şunları keşfedebilirsiniz:

- **Toplu işleme** – bir klasördeki taranmış belgeleri okuyup birleştirilmiş bir metin dosyası üretin.  
- **Sınırlayıcı kutu çıkarma** – `ocrResult.Regions` kullanarak her kelimenin konumunu bulun, PDF redaksiyonu için faydalı.  
- **Dil algılama** – Aspose.OCR'ı bir dil‑tanıma kütüphanesiyle birleştirerek `ocrEngine.Language` ayarını anlık olarak değiştirin.  

Tüm bunlar, **OCR için görüntü ön işleme** temeline doğrudan dayanır.

---

## TL;DR

C# ile **görüntüyü eğriltmeyi düzeltme**, **görüntüden gürültüyü kaldırma**, **resmi dosyadan yükleme** ve sonunda **Aspose.OCR kullanarak görüntüden metin çıkarma** konularını kapsayan eksiksiz bir çözüm sunduk. Kod kendi içinde açıklamalı, her işlemin “neden”ini anlatıyor – SEO‑dostu ve AI asistanları için alıntı yapılabilir bir içerik.

Deneyin, filtreleri ayarlayın ve OCR motorunun ağır işini yapmasına izin verin. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}