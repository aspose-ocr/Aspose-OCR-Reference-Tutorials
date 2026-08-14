---
category: general
date: 2026-02-28
description: Görselleri dikey olarak birleştirerek C#'ta aranabilir PDF oluşturun.
  Görselleri dikey olarak nasıl yığacağınızı öğrenin ve taranmış sayfaları Aspose
  OCR ile PDF'ye dönüştürün.
draft: false
keywords:
- create searchable pdf
- combine images vertically
- how to stack images vertically
- convert scanned pages pdf
language: tr
og_description: Görselleri dikey olarak birleştirerek C#'ta aranabilir PDF oluşturun.
  Bu kılavuz, görselleri dikey olarak istiflemeyi ve taranmış sayfaları Aspose OCR
  kullanarak PDF'ye dönüştürmeyi gösterir.
og_title: C#'ta Aranabilir PDF Oluştur – Görüntüleri Dikey Olarak Birleştir
tags:
- Aspose OCR
- C#
- PDF generation
title: C# ile Aranabilir PDF Oluşturma – Görüntüleri Dikey Olarak Birleştirme
url: /tr/net/text-recognition/create-searchable-pdf-in-c-combine-images-vertically/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Aranabilir PDF Oluşturma – Görüntüleri Dikey Olarak Birleştirme

Bir avuç taranmış PNG'den **aranabilir PDF** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz. Birçok belge‑otomasyon projesinde en büyük sorun, bir dizi görüntü dosyasını indeksleyebileceğiniz ve paylaşabileceğiniz tek, düzenli, aranabilir PDF'e dönüştürmektir.  

Bu öğreticide, **görüntüleri dikey olarak yığmanın**, **görüntüleri dikey olarak birleştirmenin** ve sonunda Aspose.OCR’un GPU‑hızlandırmalı motorunu kullanarak **taran sayfaları PDF'e dönüştürmenin** nasıl yapılacağını gösteren eksiksiz, hemen çalıştırılabilir bir örnek üzerinden ilerleyeceğiz. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz bağımsız bir programınız olacak.

> **Neler Öğreneceksiniz**
> - GPU desteğiyle bir OCR motoru başlatmak.
> - Görüntü topluluğunu paralel olarak işlemek.
> - **Görüntüleri dikey olarak birleştirerek** çok sayfalı bir taramayı taklit etmek.
> - Aranabilir bir PDF ve sonraki analizler için ayrıntılı bir JSON raporu dışa aktarmak.

## Önkoşullar

- .NET 6+ (kod .NET 6, .NET 7 veya .NET 8 ile derlenir)
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)
- `ProcessingMode.Gpu` ayarını tutmak istiyorsanız GPU‑destekli bir makine (CPU geri dönüşü de çalışır)
- Birkaç taranmış PNG/JPEG dosyasının bulunduğu bir klasör (demoda `page1.png`, `page2.png`, `page3.png` kullanılır)

Harici hizmet yok, gizli yapılandırma dosyası yok—sadece saf C#.

## Adım 1 – OCR Motorunu **Aranabilir PDF Oluşturmak** İçin Kurma

İlk olarak bir `OcrEngine` oluşturur, GPU hızlandırmasını etkinleştirir, dili İngilizce olarak seçer ve birkaç ön işleme filtresi ekleriz. Bu filtreler, eğik sayfaları düzleştirerek (`DeskewFilter`) ve gürültüyü kaldırarak (`DenoiseFilter`) doğruluğu artırır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;
using System.Collections.Generic;
using System.Drawing;

class AllInOneDemo
{
    static void Main()
    {
        // Initialize OCR engine – this is the heart of creating a searchable PDF
        var ocrEngine = new OcrEngine
        {
            ProcessingMode = ProcessingMode.Gpu,   // Switch to CPU if no GPU
            Language = OcrLanguage.English
        };
        // Pre‑processing improves OCR quality
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseFilter());
```

**Neden önemli:** OCR motoru metin tanımanın ağır işini yapar. `ProcessingMode.Gpu`'yu etkinleştirmek, modern bir grafik kartında tanıma süresini yarıya indirebilir, filtreler ise aksi takdirde bozuk çıktı üretebilecek yaygın tarama artefaktlarını azaltır.

## Adım 2 – **Taran Sayfaları PDF'e Dönüştürmek** İçin Bir Toplu İşlemciyi Verimli Şekilde Yapılandırma

Her sayfayı tek tek işlemek birkaç görüntü için yeterli olabilir, ancak gerçek dünyadaki projeler genellikle onlarca ya da yüzlerce sayfa içerir. Aspose.OCR’un `OcrBatchProcessor`ı, tanıma işlemlerini paralel olarak çalıştırmamıza olanak tanır ve **taran sayfaları pdf'e dönüştürme** adımını büyük ölçüde hızlandırır.

```csharp
        // Set up batch processor – ideal for converting many scanned pages to PDF
        var batchProcessor = new OcrBatchProcessor
        {
            MaxDegreeOfParallelism = 2,          // Adjust based on CPU/GPU cores
            Language = OcrLanguage.English,
            ProcessingMode = ProcessingMode.Gpu
        };

        // List the image files you want to turn into a searchable PDF
        List<string> imageFiles = new()
        {
            "YOUR_DIRECTORY/page1.png",
            "YOUR_DIRECTORY/page2.png",
            "YOUR_DIRECTORY/page3.png"
        };
```

**Pro ipucu:** Sadece CPU kullanan bir sistemde iseniz, `ProcessingMode = ProcessingMode.Cpu` olarak ayarlayın. Toplu işlemci hâlâ `MaxDegreeOfParallelism` değerine saygı gösterecek, böylece makineyi aşırı yüklememek için ayarlayabilirsiniz.

## Adım 3 – Toplu İşlemde OCR'ı Çalıştırma ve Sonuçları Toplama

Şimdi gerçekten metni tanıyoruz. `Recognize` yöntemi, orijinal görüntüyü ve çıkarılan metni içeren `OcrResult` nesnelerinin bir listesini döndürür.

```csharp
        // Run OCR on all images at once
        List<OcrResult> ocrResults = batchProcessor.Recognize(imageFiles);
```

Bu noktada **aranabilir PDF oluşturmak** için ihtiyacınız olan her şeye sahipsiniz: görüntüler (hafızada hâlâ) ve ilişkili metin katmanları.

## Adım 4 – **Görüntüleri Dikey Olarak Birleştir** ve Aranabilir PDF Oluştur

Çoğu taranmış belge çok sayfalı PDF'lerdir, bu yüzden tek tek sayfa görüntülerini fiziksel bir yığını taklit eden uzun bir görüntüde birleştirmemiz gerekir. Aspose.OCR bu amaç için `Image.CombineVertical` sağlar.

```csharp
        // Stitch the page images into one tall image – this is how we **combine images vertically**
        using var combinedImage = Image.CombineVertical(
            ocrResults.ConvertAll(r => r.Image));

        // Finally, create a searchable PDF from the combined image
        ocrEngine.RecognizeToPdf(combinedImage, "YOUR_DIRECTORY/combined_searchable.pdf");
```

Ortaya çıkan dosya (`combined_searchable.pdf`), her sayfa görüntüsünün altında seçilebilir, aranabilir metin içerir—tarama kaynaklarından **aranabilir PDF oluşturmak** için tam olarak ihtiyacınız olan şey.

![Aranabilir PDF oluşturma örneği](/images/create-searchable-pdf.png "aranabilir pdf oluşturma örneği")

*Görsel alt metni: aranabilir metin içeren birleştirilmiş PDF'i gösteren bir örnek.*

**Neden dikey yığma?** Birçok OCR kütüphanesi her görüntüyü ayrı bir sayfa olarak ele alır. Görüntüleri yığıp, PDF'in sayfa sırasını korurken tüm belge için tek bir OCR geçişinden yararlanırız.

## Adım 5 – İlk Sayfa İçin Ayrıntılı JSON Dışa Aktar (İleri İş Akışları İçin Harika)

Bazen bir PDF'den daha fazlasına ihtiyacınız olur; belki OCR verilerini bir veritabanına ya da makine‑öğrenimi hattına beslemek istersiniz. Aspose.OCR, her `OcrResult` nesnesini JSON olarak serileştirmenize olanak tanır ve sınırlama kutuları, güven skorları ve daha fazlasını korur.

```csharp
        // Dump the first page’s OCR result to pretty‑printed JSON
        string jsonOutput = ocrResults[0].ToJson(prettyPrint: true);
        Console.WriteLine("--- JSON for first page ---");
        Console.WriteLine(jsonOutput);
    }
}
```

**Beklenen JSON snippet (kısaltılmış):**

```json
{
  "Text": "Sample scanned text …",
  "Confidence": 0.97,
  "Blocks": [
    {
      "Text": "Header",
      "BoundingBox": { "X": 15, "Y": 10, "Width": 480, "Height": 30 }
    }
    // …
  ]
}
```

Artık bu JSON'u herhangi bir sonraki sisteme besleyebilirsiniz—metni Elasticsearch'te indeksliyor olun ya da özel bir analiz panosuna gönderiyor olun.

---

## **Görüntüleri Dikey Olarak Yığma** Nasıl Yapılır – Kısa Bir Özet

Aspose olmadan **görüntüleri dikey olarak nasıl yığacağınızı** merak ediyorsanız, `System.Drawing` kullanarak yeni bir bitmap oluşturabilir ve her sayfayı sırayla çizebilirsiniz. Ancak, Aspose'un yerleşik `Image.CombineVertical` işlevi DPI, piksel formatı ve bellek yönetimini sizin için halleder, bu da onu üretim kodu için en güvenilir seçenek yapar.

### Alternatif: `System.Drawing` Kullanımı (sadece merak için)

```csharp
int totalHeight = 0;
int maxWidth = 0;
foreach (var img in ocrResults)
{
    totalHeight += img.Image.Height;
    maxWidth = Math.Max(maxWidth, img.Image.Width);
}
var canvas = new Bitmap(maxWidth, totalHeight);
using var g = Graphics.FromImage(canvas);
int offset = 0;
foreach (var img in ocrResults)
{
    g.DrawImage(img.Image, 0, offset);
    offset += img.Image.Height;
}
canvas.Save("combined_manual.png");
```

Manuel yaklaşım çalışır, ancak otomatik DPI yönetimi ve sonucu doğrudan `RecognizeToPdf`'a besleme kolaylığını kaybedersiniz. Çok özel bir ihtiyacınız yoksa `CombineVertical` ile kalın.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

| Sorun | Neden Oluşur | Çözüm |
|-------|----------------|-----|
| **Out‑of‑memory errors** yüksek çözünürlüklü taramaları düzine düzine işlerken | Her görüntü PDF yazılana kadar bellekte kalır | `Image` nesnelerini işiniz bittiğinde hemen (`using` blokları) serbest bırakın veya birleştirmeden önce görüntüleri küçültün |
| **Garbage text** OCR sonrası | Eğimli taramalar veya düşük kontrast | `DeskewFilter` ve `DenoiseFilter`'i tutun; gerekirse `ContrastFilter` eklemeyi düşünün |
| **Missing searchable layer** | `RecognizeToPdf` yerine `Recognize` kullanıldı | Birleştirilmiş görüntü üzerinde `ocrEngine.RecognizeToPdf` çağırdığınızdan emin olun |
| **GPU fallback fails** uygun sürücüler olmayan makinelerde | `ProcessingMode.Gpu` bir istisna fırlatır | Motor oluşturmayı try/catch içinde sarın ve `ProcessingMode.Cpu`'ya geri dönün |

## Sonraki Adımlar – İş Akışını Genişletme

Artık **aranabilir PDF oluşturmayı** bildiğinize göre, şunları yapmak isteyebilirsiniz:

- `Directory.GetFiles` ve bir `foreach` döngüsü kullanarak **tüm klasörleri toplu işleyin**.
- Birleştirmeden önce her sayfaya **filigran ekleyin** (`Aspose.Imaging`'den `ImageProcessor` kullanarak).
- Daha sonra sayfa başına PDF'lere ihtiyacınız olursa **aranabilir PDF'i tek tek sayfalara bölün** (`Aspose.PDF`'den `PdfDocument.Split`).
- **Azure Blob Storage** ile entegrasyon sağlayarak görüntüleri buluttan çekin ve son PDF'i geri gönderin.

Bu uzantıların tümü doğal olarak aynı temel kavramları içerir: OCR kurulumu, görüntü işleme ve PDF dışa aktarımı.

---

## Sonuç

C#'ta taranmış görüntüler koleksiyonundan **aranabilir PDF oluşturmak** için ihtiyacınız olan her şeyi ele aldık. GPU‑destekli bir `OcrEngine` başlatarak, `OcrBatchProcessor` ile paralel bir toplu işlem çalıştırarak, **görüntüleri dikey olarak birleştirerek** ve sonunda `RecognizeToPdf` çağırarak, arşivleme veya indeksleme için hazır, düzenli ve aranabilir bir belge elde edersiniz. Ek JSON dışa aktarımı, OCR sonuçlarına tam görünürlük sağlar ve analizler ya da özel iş akışları için kapılar açar.

Deneyin, farklı filtrelerle oynayın ve belge‑otomasyon hattınızın çok daha sorunsuz hale geldiğini izleyin. Herhangi bir sorunla karşılaşırsanız yorum bırakın—iyi kodlamalar!

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}