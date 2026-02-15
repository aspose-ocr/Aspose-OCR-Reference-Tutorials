---
category: general
date: 2026-02-14
description: Aspose OCR kullanarak aranabilir PDF oluşturun ve PDF'ye yazı tiplerini
  gömün. Görüntüyü PDF'ye OCR'lamak, görüntüden metni tanımak ve taranmış görüntüyü
  C#'ta PDF'ye dönüştürmeyi öğrenin.
draft: false
keywords:
- create searchable pdf
- embed fonts in pdf
- ocr image to pdf
- recognize text from image
- convert scanned image to pdf
language: tr
og_description: Aspose OCR ile C#'ta aranabilir PDF oluşturun. Bu kılavuz, PDF'ye
  yazı tiplerini gömmeyi, görüntüyü OCR ile PDF'ye dönüştürmeyi ve taranmış görüntüyü
  PDF'ye çevirirken PDF/A‑2b uyumluluğunu sağlamayı gösterir.
og_title: Aranabilir PDF Oluştur – Tam Aspose OCR Öğreticisi
tags:
- Aspose OCR
- C#
- PDF/A‑2b
- Document Automation
title: Aspose OCR ile Aranabilir PDF Oluşturma – Adım Adım Kılavuz
url: /tr/net/text-recognition/create-searchable-pdf-with-aspose-ocr-step-by-step-guide/
---

text and title should be translated. But URL stays same.

So alt: "Diagram showing the flow from scanned image → OCR engine → PDF/A‑2b with embedded fonts" => "Tarama görüntüsünden → OCR motoruna → gömülü fontlarla PDF/A‑2b'ye akışı gösteren diyagram"

Title: "create searchable pdf workflow" => "aranabilir pdf iş akışı"

Now TL;DR section: translate bullet points.

Make sure to keep code placeholders unchanged.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aranabilir PDF Oluşturma – Tam Aspose OCR Öğreticisi

Hiç taranmış bir TIFF'ten **aranabilir PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilmiyor muydunuz? Yalnız değilsiniz. Birçok ofis iş akışında **görüntüden metin tanıma** ve PDF içinde fontları gömmek, özellikle arşivleme için PDF/A‑2b uyumluluğunu karşılamanız gerektiğinde kritik bir özelliktir.  

Bu öğreticide tam olarak bunu yapan bir uygulamalı çözümü adım adım inceleyeceğiz: taranmış bir görüntüyü alacağız, üzerine OCR çalıştıracağız ve fontların gömülü olduğu tamamen aranabilir bir PDF oluşturacağız. Sonunda **ocr image to pdf**, **convert scanned image to pdf** nasıl yapılır ve uzun vadeli okunabilirlik için font gömmenin neden önemli olduğunu öğreneceksiniz.

## Gereksinimler

- .NET 6+ (veya .NET Framework 4.7.2+) ve bir C# IDE (Visual Studio, Rider veya VS Code)
- Aspose.OCR for .NET NuGet paketi (`Aspose.OCR` ve `Aspose.OCR.Pdf`)
- Referans verebileceğiniz bir klasöre yerleştirilmiş örnek bir taranmış görüntü (`input.tif`)
- C# konsol uygulamalarıyla temel aşinalık

> **Pro ipucu:** PDF/A‑2b hedefliyorsanız, en yeni Aspose.OCR sürümüne sahip olduğunuzdan emin olun; eski sürümler `PdfAStandard` enum'ını içermeyebilir.

## Adım 1 – Projeyi Kurun ve Aspose OCR'yi Yükleyin

Yeni bir konsol projesi oluşturun ve gerekli NuGet paketlerini ekleyin:

```bash
dotnet new console -n SearchablePdfDemo
cd SearchablePdfDemo
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Pdf
```

> **Neden önemli:** `Aspose.OCR.Pdf` paketini yüklemek, **embed fonts in PDF** ve ek üçüncü‑taraf kütüphanelerine ihtiyaç duymadan PDF/A uyumluluğu sağlayan PDF‑özel uzantıları getirir.

## Adım 2 – OCR Motorunu Başlatın

`Engine` sınıfı Aspose OCR'nin kalbidir. Bir kez başlatmak, **recognize text from image** dahil tüm OCR özelliklerine erişmenizi sağlar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;

// Initialize the OCR engine – this loads language data and prepares the engine.
var ocrEngine = new Engine();
```

Birçok görüntüyü toplu iş olarak işleyecekseniz, motoru tüm çalışma süresi boyunca canlı tutun; tekrar tekrar oluşturmak gereksiz yük getirir.

## Adım 3 – Taranmış Görüntünüzü Yükleyin

Aspose OCR akışlarla çalışır, bu yüzden TIFF dosyasını bir `ImageStream` içinde sarmalayacağız. Bu adım, daha sonra **convert scanned image to PDF** yapacağımız yerdir.

```csharp
// Replace the path with the location of your scanned TIFF.
var imagePath = @"C:\Docs\input.tif";
var imageStream = ImageStream.FromFile(imagePath);
```

> **Kenar durumu:** Bazı tarayıcılar çok sayfalı TIFF'ler üretir. `ImageStream.FromFile` varsayılan olarak ilk sayfayı okur. Çok sayfalı dosyaları işlemek için `imageStream.Pages` üzerinde döngü kurup her birini ayrı ayrı işleyin.

## Adım 4 – PDF Kaydetme Seçeneklerini Yapılandırın (Fontları Gömme & PDF/A‑2b)

Fontları gömmek, oluşturulan PDF'nin herhangi bir cihazda aynı görünmesini garanti ederken, PDF/A‑2b uyumluluğu yasal arşivleme gereksinimlerini karşılar.

```csharp
var pdfSaveOptions = new PdfSaveOptions
{
    // PDF/A‑2b ensures long‑term preservation.
    PdfAStandard = PdfAStandard.PdfA2b,
    // Embedding fonts is crucial for searchable PDFs that render correctly everywhere.
    EmbedFonts = true
};
```

Burada ayrıca görüntü sıkıştırmasını ayarlayabilir veya özel bir yazar adı belirleyebilirsiniz, ancak yukarıdaki iki ayar **create searchable pdf** iş akışı için en önemlisidir.

## Adım 5 – OCR'yi Gerçekleştirip Aranabilir PDF/A‑2b Belgesi Olarak Kaydedin

Şimdi sihir gerçekleşiyor. `RecognizeToPdf` yöntemi görüntü akışı üzerinde OCR çalıştırır ve PDF/A‑2b standartlarına uygun aranabilir bir PDF yazar.

```csharp
// Output path for the searchable PDF.
var outputPath = @"C:\Docs\output.pdf";

// Run OCR and generate the PDF.
ocrEngine.RecognizeToPdf(imageStream, outputPath, pdfSaveOptions);

Console.WriteLine("PDF/A‑2b document created at: " + outputPath);
```

`output.pdf` dosyasını Adobe Acrobat Reader'da açtığınızda metni seçip kopyalayabildiğinizi fark edeceksiniz – bu, **create searchable pdf** sonucunun bir göstergesidir.

## Adım 6 – Sonucu Doğrulayın (İsteğe Bağlı ama Tavsiye Edilir)

Kısa bir tutarlılık kontrolü, fontların gerçekten gömülü olduğunu ve PDF'nin PDF/A‑2b uyumlu olduğunu teyit etmenize yardımcı olur.

```csharp
using Aspose.Pdf; // Requires Aspose.PDF NuGet if you want to inspect the file

var pdfDoc = new Document(outputPath);
bool fontsEmbedded = pdfDoc.IsFontsEmbedded; // Returns true if fonts are embedded
bool isPdfA = pdfDoc.ValidatePdfA(PdfAConformance.PdfA2b); // Validates PDF/A‑2b compliance

Console.WriteLine($"Fonts embedded: {fontsEmbedded}");
Console.WriteLine($"PDF/A‑2b compliance: {isPdfA}");
```

Eğer kontrol başarısız olursa, `PdfSaveOptions` ayarlarını tekrar gözden geçirin ve en yeni Aspose OCR sürümünü kullandığınızdan emin olun.

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|----------|--------|
| **Bir çok sayfalı PDF'yi doğrudan OCR'leyebilir miyim?** | Evet. PDF'yi `Aspose.Pdf` ile yükleyin → her sayfayı bir görüntüye dönüştürün → döngü içinde her görüntüyü `RecognizeToPdf`'ye besleyin. |
| **Taranmış görüntüm düşük çözünürlükte ise ne olur?** | OCR doğruluğu 300 dpi altında düşer. Motoru beslemeden önce görüntüyü (dpi artırma, lekeleri temizleme) ön‑işleme yapmayı düşünün. |
| **Aspose OCR için lisansa ihtiyacım var mı?** | Ücretsiz deneme sürümü 5 sayfaya kadar çalışır. Üretim ortamında bir lisans, değerlendirme filigranını kaldırır ve tam özellikleri açar. |
| **OCR dilini nasıl değiştiririm?** | `ocrEngine.Language = Language.English;` ya da desteklenen herhangi bir dil enum'ı ile `RecognizeToPdf` çağrısından önce ayarlayın. |
| **Aranabilir PDF'ler için font gömme zorunlu mu?** | Zorunlu değil, ancak fontlar gömülmezse orijinal fonta sahip olmayan sistemlerde metin yanlış görünebilir ve “aranabilir” deneyimi bozulur. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda `Program.cs` dosyasına yapıştırabileceğiniz, yukarıdaki tüm adımları ve doğrulama bloğunu içeren eksiksiz program yer alıyor.

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;
using Aspose.Pdf; // For verification – add Aspose.PDF via NuGet if needed

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize the OCR engine
        var ocrEngine = new Engine();

        // 2️⃣ Load the scanned image (change the path as needed)
        var imagePath = @"C:\Docs\input.tif";
        var imageStream = ImageStream.FromFile(imagePath);

        // 3️⃣ Configure PDF save options – embed fonts & PDF/A‑2b compliance
        var pdfSaveOptions = new PdfSaveOptions
        {
            PdfAStandard = PdfAStandard.PdfA2b,
            EmbedFonts = true
        };

        // 4️⃣ Recognize text and save as searchable PDF/A‑2b
        var outputPath = @"C:\Docs\output.pdf";
        ocrEngine.RecognizeToPdf(imageStream, outputPath, pdfSaveOptions);
        Console.WriteLine("PDF/A‑2b document created at: " + outputPath);

        // 5️⃣ Verify embedding and compliance (optional)
        var pdfDoc = new Document(outputPath);
        bool fontsEmbedded = pdfDoc.IsFontsEmbedded;
        bool isPdfA = pdfDoc.ValidatePdfA(PdfAConformance.PdfA2b);
        Console.WriteLine($"Fonts embedded: {fontsEmbedded}");
        Console.WriteLine($"PDF/A‑2b compliance: {isPdfA}");
    }
}
```

Programı `dotnet run` ile çalıştırın. Her şey doğru kurulduysa, PDF'nin oluşturulduğunu, fontların gömülü olduğunu ve dosyanın PDF/A‑2b doğrulamasını geçtiğini belirten bir konsol çıktısı göreceksiniz.

## Sonraki Adımlar – İş Akışını Genişletme

Artık **create searchable pdf** dosyaları oluşturabildiğinize göre şu geliştirmeleri düşünebilirsiniz:

- **Toplu işleme** – bir klasördeki TIFF'ler üzerinde döngü kurarak her OCR sonucunu tek bir PDF'ye ekleyin.
- **Özel meta veriler** – `PdfSaveOptions.Metadata` kullanarak PDF'ye yazar, başlık ve anahtar kelimeler ekleyin.
- **Görüntü ön‑işleme** – düşük kaliteli taramaları iyileştirmek için OpenCV veya ImageSharp entegre edin.
- **Alternatif çıktılar** – OCR sonuçlarını düz metin, DOCX veya HTML olarak dışa aktararak sonraki iş akışlarına yönlendirin.

Bu fikirlerin her biri, **ocr image to pdf**, **recognize text from image** ve **embed fonts in pdf** temel kavramları üzerine inşa edilerek sağlam bir belge‑otomasyon hattı oluşturur.

---

![Tarama görüntüsünden → OCR motoruna → gömülü fontlarla PDF/A‑2b'ye akışı gösteren diyagram](https://example.com/flow-diagram.png "aranabilir pdf iş akışı")

*Görsel alt metni: aranabilir pdf iş akışı diyagramı, OCR, font gömme ve PDF/A‑2b çıktısını gösterir.*

---

### TL;DR

- `Engine`'i başlatın.
- `ImageStream.FromFile` ile taranmış TIFF'i yükleyin.
- Fontları gömmek ve PDF/A‑2b zorunluluğunu etkinleştirmek için `PdfSaveOptions` ayarlayın.
- **create searchable pdf** oluşturmak için `RecognizeToPdf`'yi çağırın.
- Gerekirse font gömme ve uyumluluğu doğrulayın.

İşte bu kadar. Artık **convert scanned image to pdf** yaparken metnin aranabilir olduğundan ve belgenin geleceğe dayanıklı olduğundan emin olabilirsiniz. Kodlamanın tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}