---
category: general
date: 2026-03-17
description: OCR ile taranmış PDF'yi dönüştürerek hızlıca aranabilir PDF oluşturun.
  OCR nasıl çalıştırılır, PDF'den metin nasıl çıkarılır ve daha fazlasını öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr to searchable pdf
- extract text from pdf
- how to run ocr
language: tr
og_description: Tarayıcıyla taranmış belgelerden aranabilir PDF oluşturun. Bu kılavuz,
  taranmış PDF'yi nasıl dönüştüreceğinizi, OCR çalıştıracağınızı ve C# kullanarak
  metni nasıl çıkaracağınızı gösterir.
og_title: Aranabilir PDF Oluştur – Tam C# OCR Öğreticisi
tags:
- OCR
- PDF
- C#
- .NET
title: Taranmış dosyalardan aranabilir PDF oluşturma – Adım adım C# rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-scanned-files-step-by-step-c-guid/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aranabilir PDF Oluşturma – Tam C# Öğreticisi

Hiç **create searchable PDF**'i bir yığın taranmış sayfadan oluşturmanız gerekti mi? Belki eski sözleşmeleri dijitalleştiriyorsunuzdur ya da PDF'lerinizin Windows Gezgini'nde aranabilir olmasını istiyorsunuzdur. Her iki durumda da, **convert scanned pdf**'i gerçekten arayabileceğiniz bir şeye nasıl dönüştürebileceğinizi merak ediyor olabilirsiniz.  

İyi haber? Birkaç C# satırı ve bir OCR motoru ile, herhangi bir görüntü‑tabanlı PDF'yi tamamen aranabilir bir PDF'ye dönüştürebilirsiniz—harici hizmetlere gerek yok. Bu öğreticide, kütüphaneyi kurmaktan metin çıkarmaya kadar tüm süreci adım adım göstereceğiz ve her adımın “neden”ini ele alacağız, böylece arka planda neler olduğunu gerçekten anlayacaksınız.  

> **Quick answer:** sadece `PdfConversionMode = PdfConversionMode.SearchablePdf` ayarlayın, taranmış dosyayı besleyin, `Recognize()` çağırın ve sonucu kaydedin.  

Aşağıda, bugün çalışır hale getirmek için ihtiyacınız olan her şeyi bulacaksınız.

---

## İhtiyacınız Olanlar

| Gereksinim | Neden Önemli |
|------------|--------------|
| .NET 6 or later (or .NET Framework 4.7+) | Kullanacağımız OCR SDK'sı bu çalışma zamanlarını hedef alır. |
| Visual Studio 2022 (or any C# IDE) | Hata ayıklamayı ve NuGet yönetimini zahmetsiz hale getirir. |
| A NuGet‑compatible OCR library (e.g., **Aspose.OCR** or **Tesseract.NET**) | `OcrEngine` sınıfını kodda gösterildiği gibi sağlar. |
| A scanned PDF file to test with | Test etmek için bir taranmış PDF dosyası |
|  | Bunu aranabilir bir PDF'ye dönüştüreceğiz. |

Zaten bir projeniz varsa, OCR paketini Package Manager Console üzerinden ekleyin:

```powershell
Install-Package Aspose.OCR
```

*(\`Aspose.OCR\`'ı seçtiğiniz kütüphane ile değiştirin; gösterdiğimiz API oldukça genel bir yapıya sahiptir.)*

## Adım‑Adım Uygulama

Her adımın altında, kopyalayıp‑yapıştırabileceğiniz tam C# kodunu ve satırın **neden** var olduğuna dair kısa bir açıklamayı bulacaksınız.

### Adım 1: OCR Motorunu Başlatma  

Motoru oluşturmak, tanıma işlemi için tüm yapılandırma ve durumu tuttuğu için yaptığınız ilk şeydir.

```csharp
using Aspose.OCR;          // <-- OCR library namespace
using System.IO;           // needed for file handling

// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

> **Pro tip:** Birden fazla dosya için tek bir `OcrEngine` örneğini yeniden kullanmak, özellikle büyük toplu işlemlerde bellek tüketimini azaltır.

### Adım 2: Motoru Aranabilir PDF İçin Yapılandırma  

Motor, düz metin, görüntü veya aranabilir PDF çıktısı verebilir. Doğru modu ayarlamak, kütüphaneye orijinal sayfa görüntülerinin arkasına görünmez bir metin katmanı eklemesini söyler.

```csharp
// Step 2: Tell the engine to produce a searchable PDF
ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
```

*Why?* Bu bayrak olmadan OCR çalışması size sadece tanınan metnin bir `string`ini verir; orijinal sayfa düzenine hâlâ ihtiyacınız varsa bu kullanışlı değildir.

### Adım 3: Taranmış Belgeyi Yükleme  

Çoğu OCR SDK'sı bir `Image` veya `ImageStream` kabul eder. Burada, bir PDF dosyasını okuyup her sayfayı bir görüntü olarak işleyen bir yardımcı kullanıyoruz.

```csharp
// Step 3: Load the scanned PDF you want to convert
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\scanned.pdf");
```

> **Köşe durumu:** PDF'niz karışık raster ve vektör sayfalar içeriyorsa, bazı motorlar vektör sayfaları atlayabilir. Bu durumda, OCR motoruna beslemeden önce PDF'yi görüntülere (ör. Ghostscript kullanarak) önceden dönüştürün.

### Adım 4: OCR Tanımasını Çalıştırma  

`Recognize()` çağrısı ağır işi yapar—metin tespiti, dil modelleme ve PDF oluşturma hepsi arka planda gerçekleşir.

```csharp
// Step 4: Run OCR; the result includes the searchable PDF object
var ocrResult = ocrEngine.Recognize();
```

Eğer **extract text from pdf**'i de çıkarmanız gerekiyorsa, `ocrResult.Text` üzerinden alabilirsiniz:

```csharp
string extractedText = ocrResult.Text;   // plain text version
```

### Adım 5: Aranabilir PDF'yi Kaydetme  

Son olarak, çıktıyı diske yazın. `PdfDocument` özelliği, görünmez bir metin katmanı içeren tam bir PDF tutar.

```csharp
// Step 5: Persist the searchable PDF
ocrResult.PdfDocument.Save(@"C:\Docs\searchable.pdf");
```

`searchable.pdf`'i Adobe Reader veya Edge'de açtığınızda, Bul kutusuna bir kelime yazıp doğrudan eşleşen konuma atlayabileceksiniz—tıpkı yerel bir PDF gibi.

## Sonucu Doğrulama

1. Herhangi bir PDF görüntüleyicide oluşturulan dosyayı açın.  
2. **Ctrl + F** tuşlarına basın ve taranmış sayfalarda bulunduğundan emin olduğunuz bir kelime yazın.  
3. Görüntüleyici terimi vurguluyorsa, **create searchable pdf** işlemini başarıyla gerçekleştirdiniz.

Eğer hiçbir şey bulunamazsa, kaynak PDF'nin gerçekten okunabilir metin içerdiğini iki kez kontrol edin (bazı taramalar o kadar düşük çözünürlükte ki OCR hiçbir şeyi tanıyamaz). OCR'den önce DPI'yi artırmak (ör. `ocrEngine.Config.Dpi = 300`) genellikle yardımcı olur.

## Yaygın Tuzaklar ve Çözüm Yolları

| Belirti | Muhtemel neden | Çözüm |
|---------|----------------|-------|
| Boş aranabilir PDF | `PdfConversionMode` varsayılan (sadece görüntü) olarak bırakıldı | Set `PdfConversionMode = PdfConversionMode.SearchablePdf`. |
| Bozuk karakterler | Yanlış dil modeli | `ocrEngine.Config.Language = Language.English;` (veya uygun dil). |
| Büyük dosyalarda yavaş işleme | Motor her sayfa için yeniden başlatılıyor | Aynı `OcrEngine` örneğini yeniden kullanın veya kütüphane destekliyorsa çoklu iş parçacığını etkinleştirin. |
| Dönüştürmeden sonra metin aranabilir değil | Girdi PDF'si sadece vektör (raster görüntü yok) | PDF sayfalarını önce görüntülere dönüştürün (ör. `PdfRenderer` from Aspose.PDF). |

## Bonus: Aranabilir PDF'den Doğrudan Metin Çıkarma  

Bazen indeksleme veya analiz için ham metne ihtiyaç duyarsınız. `ocrResult` zaten size `Text` sağladığından PDF'yi tekrar açmayı atlayabilirsiniz. Ancak, daha sonra yalnızca PDF dosyanız varsa, bir PDF metin çıkarıcı kullanın:

```csharp
using Aspose.Pdf;   // PDF library for reading

var pdfDoc = new Document(@"C:\Docs\searchable.pdf");
var textAbsorber = new TextAbsorber();
pdfDoc.Pages.Accept(textAbsorber);
string fullText = textAbsorber.Text;
```

Artık **extract text from pdf**'i OCR'yi yeniden çalıştırmadan elde ettiniz—birçok dosya işlediğinizde kullanışlı bir kısayol.

## Tam Çalışan Örnek (Tüm Adımlar Tek Dosyada)

```csharp
// ------------------------------------------------------------
// Full C# example: Convert a scanned PDF into a searchable PDF
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.Pdf;               // For optional text extraction
using Aspose.Pdf.Text;          // TextAbsorber class

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Configure for searchable PDF output
            ocrEngine.Config.PdfConversionMode = PdfConversionMode.SearchablePdf;
            // Optional: set language and DPI for better accuracy
            ocrEngine.Config.Language = Language.English;
            ocrEngine.Config.Dpi = 300;

            // 3️⃣ Load the scanned document (replace path as needed)
            string inputPath = @"C:\Docs\scanned.pdf";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 4️⃣ Run OCR – this creates both PDF and plain‑text results
            var ocrResult = ocrEngine.Recognize();

            // 5️⃣ Save the searchable PDF
            string outputPath = @"C:\Docs\searchable.pdf";
            ocrResult.PdfDocument.Save(outputPath);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");

            // 🎉 Bonus: Extract plain text without opening the PDF again
            string extractedText = ocrResult.Text;
            Console.WriteLine("\n--- Extracted Text Preview ---");
            Console.WriteLine(extractedText.Substring(0,
                Math.Min(300, extractedText.Length)) + "...");

            // Optional: Verify by re‑reading the PDF
            var pdfDoc = new Document(outputPath);
            var absorber = new TextAbsorber();
            pdfDoc.Pages.Accept(absorber);
            Console.WriteLine("\nText extracted from saved PDF:");
            Console.WriteLine(absorber.Text.Substring(0,
                Math.Min(300, absorber.Text.Length)) + "...");
        }
    }
}
```

**Beklenen çıktı** (kısaltılmış olarak):

```
Searchable PDF saved to: C:\Docs\searchable.pdf

--- Extracted Text Preview ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit...

Text extracted from saved PDF:
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

Eğer aynı kod parçacığını iki kez görürseniz, OCR başarılı olmuş ve PDF artık aranabilir bir metin katmanı içeriyor demektir.

## Sonraki Adımlar ve İlgili Konular

- **Batch processing:** Taranmış PDF'lerin bulunduğu bir klasörü döngüye alarak, aynı `OcrEngine` örneğini yeniden kullanıp verimliliği artırın.  
- **Language detection:** Çok dilli arşivler için, dosya meta verilerine göre `ocrEngine.Config.Language`'ı dinamik olarak değiştirin.  
- **PDF/A compliance:** Bazı sektörler arşiv PDF'leri gerektirir; SDK'nız destekliyorsa `PdfConversionMode = PdfConversionMode.SearchablePdfA` ayarlayın.  
- **Performance tuning:** Büyük işler için hızı artırmak amacıyla `ocrEngine.Config.UseParallelProcessing = true` (varsa) ile deneyler yapın.  

Bunların hepsi, **how to run OCR**'ı verimli bir şekilde çalıştırma ve **create searchable pdf** dosyalarının anında indekslenebilir olma temel kavramı üzerine inşa edilmiştir.

## Sonuç

Artık herhangi bir taranmış belgeyi **create searchable pdf** başyapıtına dönüştürmek için eksiksiz, üretim‑hazır bir tarife sahipsiniz. OCR motorunu yapılandırarak, kaynağı yükleyerek, tanıma çalıştırarak ve sonucu kaydederek tüm süreci—ham görüntüden aranabilir, metin‑çıkartılabilir PDF'ye—tamamladınız.  

Kendi dosyalarınızla deneyin, DPI veya dil ayarlarını değiştirin ve siz...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}