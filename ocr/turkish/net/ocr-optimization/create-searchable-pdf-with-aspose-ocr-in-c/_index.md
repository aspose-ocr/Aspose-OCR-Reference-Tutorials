---
category: general
date: 2026-04-01
description: Aspose OCR kullanarak C# ile aranabilir PDF oluşturun – taranmış PDF'yi
  dönüştürmeyi, PDF'ye OCR eklemeyi ve hızlı sonuçlar için GPU hızlandırmayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- convert pdf to searchable
- add OCR to pdf
- enable GPU acceleration
language: tr
og_description: C#'ta hızlıca aranabilir PDF oluşturun—taran PDF'yi dönüştürün, PDF'ye
  OCR ekleyin ve yüksek performanslı işleme için GPU hızlandırmasını etkinleştirin.
og_title: C#'ta Aspose OCR ile Aranabilir PDF Oluşturun
tags:
- Aspose OCR
- C#
- PDF processing
title: C# ile Aspose OCR kullanarak Aranabilir PDF Oluştur
url: /tr/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile C#’ta Aranabilir PDF Oluşturma

Hiç **aranabilir PDF** dosyalarını taranmış belgeler yığını üzerinden oluşturmanız gerekti mi? Tek başınıza değilsiniz—birçok ekip, yalnızca görüntü içeren PDF’leri metin‑aranabilir varlıklara dönüştürmekle uğraşıyor. İyi haber? Aspose OCR sayesinde **taranmış PDF**’yi sadece birkaç satır C# kodu ile tamamen aranabilir bir sürüme dönüştürebilirsiniz. Bu rehberde, OCR’yi PDF’e eklemekten **GPU hızlandırmayı etkinleştirmeye** kadar tüm süreci adım adım inceleyeceğiz.

Ayrıca **pdf’yi aranabilir** formata nasıl dönüştüreceğinizi gösterecek, **PDF’e OCR eklemenin** nedenlerini tartışacak ve büyük partilerle çalışırken pratik ipuçları sunacağız. Sonunda, herhangi bir belge yönetim sistemine bırakabileceğiniz aranabilir bir PDF üreten hazır bir konsol uygulamanız olacak.

---

## Gereksinimler

İlerlemeye başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **.NET 6.0** veya üzeri (API, .NET Framework ile de çalışır, ancak .NET 6+ önerilir).
- **Aspose.OCR for .NET** NuGet paketi (`Install-Package Aspose.OCR`).
- Girdi olarak kullanacağınız taranmış bir PDF dosyası (yalnızca görüntü içerikli).
- İsteğe bağlı: **GPU hızlandırmayı etkinleştirmek** istiyorsanız CUDA® yüklü bir GPU‑uyumlu makine.

Hepsi bu—ağır OCR motorları, harici hizmetler yok. Her şey yerel olarak çalışır.

---

## Aranabilir PDF Oluşturma – Adım‑Adım Genel Bakış

Aşağıda izleyeceğimiz yüksek‑seviye akış yer alıyor:

1. **OCR motorunu başlat** – Aspose’a hangi dili arayacağını ve GPU kullanıp kullanmayacağını söyle.
2. **Motoru taranmış PDF’nize yönlendir** – giriş ve çıkış yollarını tanımla.
3. **Dönüşümü çalıştır** – Aspose ağır işi yapar ve aranabilir bir PDF yazar.
4. **Sonucu doğrula** – çıktıyı aç ve bir metin araması dene.

Her adım kendi bölümünde açıklanmıştır, böylece ihtiyacınız olan kısımları seçebilirsiniz.

---

## Taranmış PDF’yi Aranabilir PDF’ye Dönüştürme

İlk yapmanız gereken `OcrEngine` örneği oluşturmaktır. Bu nesne, PDF’nizin içindeki raster görüntüleri okur ve metni çıkarır.

```csharp
using Aspose.OCR;
using System;

class PdfSearchableDemo
{
    static void Main()
    {
        // Step 1: Create and configure the OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English,
            // Optional: enable GPU for faster processing
            UseGpuAcceleration = true
        };

        // Step 2: Specify the input scanned PDF and the output searchable PDF paths
        string sourcePdfPath = @"C:\Docs\input.pdf";
        string searchablePdfPath = @"C:\Docs\output.pdf";

        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

        // Step 4: Notify the user where the searchable PDF was saved
        Console.WriteLine("Searchable PDF created at: " + searchablePdfPath);
    }
}
```

**Neden çalışıyor:** `ConvertToSearchablePdf` her sayfayı okur, raster içeriğe OCR uygular ve ardından orijinal görüntünün arkasına görünmez bir metin katmanı ekler. Sonuç, orijinal taranmış belgeye tamamen benzer görünür, ancak artık metni kopyalayabilir, seçebilir ve arayabilirsiniz.

---

## Aspose ile PDF’e OCR Ekleme

Zaten bir PDF’niz varsa ve **PDF’e OCR eklemek** istiyorsanız, tüm dosyayı dönüştürmek yerine aynı metodu çağırabilirsiniz—Aspose bu işlemi “OCR ekleme” olarak değerlendirir. Yukarıdaki kod zaten bunu yapıyor, ancak bir döngü içinde birden fazla dosyayı nasıl işleyebileceğinizi gösteren hızlı bir varyant:

```csharp
string[] pdfFiles = Directory.GetFiles(@"C:\Docs\Scanned", "*.pdf");
foreach (var file in pdfFiles)
{
    string output = Path.Combine(@"C:\Docs\Searchable", Path.GetFileNameWithoutExtension(file) + "_searchable.pdf");
    ocrEngine.ConvertToSearchablePdf(file, output);
    Console.WriteLine($"Processed {Path.GetFileName(file)} → {Path.GetFileName(output)}");
}
```

**İpucu:** Tüm batch için aynı `OcrEngine` örneğini tutun. Her seferinde yeniden oluşturmak, özellikle **GPU hızlandırmayı etkinleştiriyorsanız** gereksiz bir yük getirir.

---

## Daha Hızlı OCR İçin GPU Hızlandırmayı Etkinleştirme

GPU hızlandırma, büyük bir batch’te dakikalar kazanmanızı sağlar. Aspose OCR, arka planda NVIDIA CUDA’yı kullanır; sadece bir boolean bayrağını değiştirmeniz yeterlidir:

```csharp
ocrEngine.UseGpuAcceleration = true; // set to false if no compatible GPU
```

**Ne zaman kullanmalı:** PDF’leriniz 10 MB’den büyükse veya birkaç düzine dosyadan fazlasını işliyorsanız, GPU genellikle 2‑3 kat hız artışı sağlar. CUDA‑destekli bir GPU’su olmayan sıradan bir dizüstü bilgisayarda `false` bırakın—kütüphane otomatik olarak CPU’ya geçer.

**Yaygın tuzak:** Doğru CUDA sürücüsü sürümünün kurulu olmaması çalışma zamanı hatasına (`CudaException`) yol açar. Sürücünüzün Aspose’un beklediği sürümle eşleştiğinden emin olun (NuGet sayfasındaki sürüm notlarına bakın).

---

## Tam Çalışan Örnek (Tüm Adımlar Birleşik)

Aşağıda yeni bir .NET projesine kopyalayıp yapıştırabileceğiniz, bağımsız bir konsol uygulaması bulunuyor. Yardımcı yorumlar, hata yönetimi ve işlenen sayfa sayısını yazdıran bir son doğrulama adımı içerir.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class PdfSearchableDemo
{
    static void Main()
    {
        try
        {
            // 1️⃣ Initialize OCR engine – English language, GPU on if available
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.English,
                UseGpuAcceleration = true // set to false on non‑GPU machines
            };

            // 2️⃣ Define input and output paths
            string sourcePdfPath = @"C:\Docs\input.pdf";
            string searchablePdfPath = @"C:\Docs\output.pdf";

            // 3️⃣ Perform the conversion – this creates a searchable PDF
            ocrEngine.ConvertToSearchablePdf(sourcePdfPath, searchablePdfPath);

            // 4️⃣ Simple verification – count pages in the new file
            int pageCount = new Aspose.Pdf.Facades.PdfFileInfo(searchablePdfPath).NumberOfPages;
            Console.WriteLine($"✅ Searchable PDF created at: {searchablePdfPath}");
            Console.WriteLine($"📄 The new file contains {pageCount} pages.");

            // 5️⃣ Optional: open the file automatically (Windows only)
            // System.Diagnostics.Process.Start(new System.Diagnostics.ProcessStartInfo(searchablePdfPath) { UseShellExecute = true });
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
        }
    }
}
```

**Beklenen çıktı**

```
✅ Searchable PDF created at: C:\Docs\output.pdf
📄 The new file contains 12 pages.
```

`output.pdf`’yi herhangi bir PDF görüntüleyicide açın ve taranmış görüntülerde bulunan bir kelimeyi yazmayı deneyin. Metin vurgulanıyorsa, **aranabilir pdf oluşturma** işlemini başarıyla tamamlamışsınız demektir.

---

## Yaygın Tuzaklar ve Profesyonel İpuçları

| Sorun | Neden Oluşur | Çözüm / Önlem |
|-------|--------------|---------------|
| **GPU algılanmadı** | Eksik veya uyumsuz CUDA sürücüsü. | Aspose’un sürüm notlarında listelenen sürücüyü kurun; yedek olarak `UseGpuAcceleration = false` ayarlayın. |
| **Yanlış dil** | OCR varsayılan olarak İngilizce; diğer diller açıkça ayarlanmalı. | Dönüştürmeden önce `Language = Language.Spanish` (veya desteklenen herhangi bir enum) ayarlayın. |
| **Büyük PDF’lerde OutOfMemory** | Motor tüm sayfaları belleğe yüklüyor. | PDF’yi `ocrEngine.PageRange = new PageRange(1, 5)` gibi parçalar halinde işleyin. |
| **Çıktı dosyası bozuk** | Hedef klasörde yazma izni yok. | Uygulamayı yönetici olarak çalıştırın veya yazılabilir bir yol seçin. |
| **Metin katmanı aranamaz** | Görüntüleyici eski sürümü önbelleğe alıyor. | PDF görüntüleyiciyi yenileyin veya dosyayı yeniden açın. |

**Pro ipucu:** Tarama ve yerel PDF’lerin karışımıyla çalışıyorsanız, OCR çalıştırmadan önce her sayfanın `HasText` bayrağını (`PdfPageInfo.HasText`) kontrol edin. Bu, CPU döngülerini tasarruf ettirir ve zaten aranabilir olan sayfalarda çift OCR yapılmasını önler.

---

## Sonucu Programatik Olarak Doğrulama (İsteğe Bağlı)

Doğrulamayı otomatikleştirmek isterseniz, Aspose.PDF gizli metni çıkarabilir:

```csharp
using Aspose.Pdf;
using Aspose.Pdf.Text;

// Load the searchable PDF
Document doc = new Document(searchablePdfPath);
TextAbsorber absorber = new TextAbsorber();
doc.Pages.Accept(absorber);
string extracted = absorber.Text;

// Simple check – does the word "Invoice" appear?
if (extracted.Contains("Invoice"))
    Console.WriteLine("✅ OCR succeeded – 'Invoice' found.");
else
    Console.WriteLine("⚠️ OCR may have missed some text.");
```

Bu kod parçacığı, **pdf’yi aranabilir** formata dönüştürdüğünüzü, sadece bir görüntü katmanı eklemediğinizi kanıtlar.

---

## Görsel Örnek

![Create searchable PDF output example](https://example.com/images/searchable-pdf.png "Create searchable PDF using Aspose OCR")

*Alt metin:* **aranabilir pdf** örneği, öncesi (taranmış) ve sonrası (aranabilir) görünümü gösterir.

---

## Sonraki Adımlar & İlgili Konular

- **Batch işleme:** “PDF’e OCR ekleme” bölümündeki döngüyü bir Windows Service veya Azure Function içinde paketleyerek gece boyu işler haline getirin.
- **Gelişmiş dil desteği:** Karmaşık betik içeren belgeler için `ocrEngine.Language = Language.Multilingual` keşfedin.
- **OCR sonrası temizlik:** Aspose.PDF’nin `TextFragmentAbsorber` özelliğiyle yaygın OCR hatalarını (ör. “0” vs “O”) düzeltin.
- **Güvenlik

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}