---
category: general
date: 2026-06-03
description: Aspose.OCR kullanarak PDF üzerinde OCR gerçekleştirin ve taranmış PDF'yi
  aranabilir PDF'ye dönüştürün. PDF'den metin tanımayı ve dakikalar içinde aranabilir
  PDF'ler oluşturmayı öğrenin.
draft: false
keywords:
- perform OCR on PDF
- recognize text from PDF
- how to create searchable PDF
- convert scanned PDF to searchable PDF
- convert image to searchable PDF
language: tr
og_description: PDF üzerinde OCR gerçekleştir ve anında aranabilir bir PDF oluştur.
  Bu eğitim, Aspose.OCR kullanarak PDF'den metin tanımanın adım adım nasıl yapılacağını
  gösterir.
og_title: PDF'de OCR Yapın – Tam C# Rehberi
schemas:
- author: Aspose
  dateModified: '2026-06-03'
  description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  headline: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  type: TechArticle
- description: Perform OCR on PDF and convert scanned PDF to searchable PDF using
    Aspose.OCR. Learn how to recognize text from PDF and create searchable PDFs in
    minutes.
  name: Perform OCR on PDF with Aspose.OCR – Complete C# Guide
  steps:
  - name: 1. Large Files & Memory Management
    text: If you’re processing PDFs larger than 100 MB, consider using `OcrEngineSettings.MemoryLimit`
      to cap memory usage. Additionally, process pages in batches to avoid `OutOfMemoryException`.
  - name: 2. Language Support
    text: 'By default Aspose.OCR assumes English. To recognize other languages, set
      the `Language` property:'
  - name: 3. Multi‑Threaded Scenarios
    text: '`OcrEngine` is **not** thread‑safe. If you need parallel processing, create
      a separate engine per thread.'
  - name: 4. Debugging OCR Accuracy
    text: 'You can extract the plain text from `ocrResult` for debugging:'
  - name: 5. Licensing Gotchas
    text: 'When you run the evaluation version, Aspose adds a watermark to the output
      PDF. Register your license early in the application:'
  type: HowTo
- questions:
  - answer: Absolutely. Replace `OcrImage.FromFile("input.pdf")` with the path to
      your image file. The engine will rasterize the image and embed the OCR layer
      just the same.
    question: Can I use this to convert a single image (PNG/JPEG) to a searchable
      PDF?
  - answer: The engine will overlay the OCR text on top of existing content, so native
      text stays selectable while scanned pages become searchable.
    question: What if my PDF has both scanned pages and native text?
  - answer: 'Accuracy hinges on source quality. Clean, high‑resolution scans (>300
      dpi) give >95 % accuracy. For noisy documents, enable `PreprocessSettings` (deskew,
      despeckle) before calling `Recognize`. --- ## Next Steps – Extending Your OCR
      Toolkit Now that you can **recognize text from PDF** and **convert s'
    question: How accurate is the OCR?
  type: FAQPage
tags:
- Aspose
- OCR
- C#
- PDF
title: Aspose.OCR ile PDF'de OCR Yapın – Tam C# Rehberi
url: /tr/net/text-recognition/perform-ocr-on-pdf-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR ile PDF Üzerinde OCR Yapma – Tam C# Kılavuzu

Hiç **PDF üzerinde OCR nasıl yapılır** diye merak ettiniz mi, komut satırı araçlarıyla uğraşmadan? Yalnız değilsiniz. İster faturaları dijitalleştiriyor, eski raporları arşivliyor, ister taranmış bir sözleşmenin aranabilir bir versiyonuna ihtiyacınız olsun, sabit bir PDF'i gerçekten arayabileceğiniz bir şeye dönüştürmek oyunu değiştiriyor.

Bu kılavuzda, Aspose.OCR for .NET kullanarak taranmış PDF'lerden (ve hatta düz görüntülerden) **aranabilir PDF** dosyaları oluşturmayı adım adım göstereceğiz. Sonunda, birkaç satır C# kodu ile **PDF'den metin tanıma** yapabilecek ve her adımın nedenini anlayarak çözümü kendi projelerinize uyarlayabileceksiniz.

> **Hızlı özet:** Tüm süreç üç adıma indirgenir—OCR motorunu başlatmak, kaynağı (PDF veya görüntü) beslemek ve aranabilir PDF çıktısını kaydetmek. Hadi başlayalım.

---

## Gereksinimler

Başlamadan önce şunların olduğundan emin olun:

| Gereklilik | Neden Önemli |
|------------|--------------|
| **.NET 6.0+** (veya .NET Framework 4.6+) | Aspose.OCR modern çalışma zamanlarını hedefler; eski sürümler API güncellemelerini kaçırabilir. |
| **Aspose.OCR for .NET** NuGet paketi | `OcrEngine` sınıfını ve PDF işleme yardımcılarını sağlar. |
| **Geçerli bir Aspose lisansı** (veya ücretsiz deneme) | Lisans olmadan 30‑günlük deneme sınırı ve filigranlarla karşılaşırsınız. |
| **Aranabilir hâle getirmek istediğiniz taranmış PDF** (veya bir görüntü dosyası) | OCR için kaynak belge budur. |
| **Visual Studio 2022** (veya herhangi bir C# editörü) | Hata ayıklamayı kolaylaştırır, ancak herhangi bir IDE de çalışır. |

Kütüphaneyi aşağıdaki NuGet komutuyla kurabilirsiniz:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** CI pipeline'ında çalışıyorsanız, lisans dosyasını derleme artefaktlerine ekleyin ve çalışma zamanında yükleyin; böylece yolları sabit kodlamaktan kaçınmış olursunuz.

---

## PDF Üzerinde OCR Yapma – Aspose.OCR'ı Kurma

İlk olarak yeni bir `OcrEngine` örneğine ihtiyacımız var. Bunu, belgenizi okuyacak beyin olarak düşünün.

```csharp
// Step 1: Create an OCR engine instance
var ocrEngine = new OcrEngine();
```

Neden her seferinde yeni bir örnek? Motor, belge bazında değişebilen (dil ayarları gibi) yapılandırmaları tutar. Her çalıştırmada yeni bir örnek oluşturmak temiz bir başlangıç sağlar ve işler arasında karışıklığı önler.

---

## Aranabilir PDF Oluşturma – Şifreleme Ayarları (İsteğe Bağlı)

PDF'niz korumalıysa, motorun sayfaları okuyabilmesi için şifreyi belirtmeniz gerekir:

```csharp
// Step 2: (Optional) Provide the password if the PDF is protected
ocrEngine.Settings.PdfPassword = "mySecret";
```

Korunan bir dosyada bu adımı atlamak `PdfPasswordException` hatasına yol açar. Koruma durumundan emin değilseniz her zaman try‑catch bloğu içinde yakalayın.

---

## Taranmış PDF'yi Aranabilir PDF'ye Dönüştürme – Kaynağı Yükleme

Aspose.OCR, PDF, TIFF, JPEG vb. dosyaları saran `OcrImage` soyutlamasını kullanır. İşte taranmış bir PDF'yi belleğe almanın yolu:

```csharp
// Step 3: Load the scanned PDF that will be converted to a searchable PDF
var sourcePdf = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");
```

Arka planda, `FromFile` her sayfayı OCR motorunun işleyebileceği raster görüntülere dönüştürür. Çok sayfalı bir PDF'niz varsa, motor otomatik olarak tüm sayfalar üzerinde döner.

---

## PDF'den Metin Tanıma – OCR'i Çalıştırma

Şimdi öğreticinin özü: motoru metni tanıması ve aranabilir bir PDF üretmesi için yönlendirin.

```csharp
// Step 4: Perform OCR and request a searchable PDF as the output format
var ocrResult = ocrEngine.Recognize(sourcePdf, OutputFormat.SearchablePdf);
```

`OutputFormat.SearchablePdf` motorun, orijinal taranmış görüntülerin üzerine görünmez bir metin katmanı eklemesini söyler. Ortaya çıkan PDF, taramanın görsel bütünlüğünü korurken tamamen aranabilir hâle gelir—uygulama denetimlerinde tam ihtiyacınız olan şey.

---

## Görüntüyü Aranabilir PDF'ye Dönüştürme – Sonucu Kaydetme

Son olarak ikili veriyi diske yazın:

```csharp
// Step 5: Save the resulting searchable PDF to disk
File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", ocrResult.Binary);
Console.WriteLine("Searchable PDF created.");
```

`Binary` özelliği ham PDF baytlarını tutar. Bir API geliştiriyorsanız, bunları doğrudan bir web yanıtına da akıtabilirsiniz.

---

![Diagram showing the OCR conversion flow to create searchable PDF](https://example.com/ocr-flow.png "Perform OCR on PDF flow diagram")
*Görsel alt metni: PDF üzerinde OCR akış diyagramı, taranmış bir PDF'nin aranabilir PDF'ye nasıl dönüştüğünü gösterir.*

---

## Kenar Durumları ve Pratik İpuçları

### 1. Büyük Dosyalar ve Bellek Yönetimi
100 MB'den büyük PDF'ler işliyorsanız, `OcrEngineSettings.MemoryLimit` ile bellek kullanımını sınırlamayı düşünün. Ayrıca `OutOfMemoryException` almamak için sayfaları partiler halinde işleyin.

```csharp
ocrEngine.Settings.MemoryLimit = 512; // MB
```

### 2. Dil Desteği
Varsayılan olarak Aspose.OCR İngilizce kabul eder. Başka dilleri tanımak için `Language` özelliğini ayarlayın:

```csharp
ocrEngine.Settings.Language = Language.French; // or Language.Multilingual
```

### 3. Çoklu İş Parçacıklı Senaryolar
`OcrEngine` **thread‑safe** değildir. Paralel işleme ihtiyacınız varsa, her iş parçacığı için ayrı bir motor oluşturun.

### 4. OCR Doğruluğunu Hata Ayıklama
Hata ayıklama amacıyla `ocrResult`'tan düz metni çıkarabilirsiniz:

```csharp
string plainText = ocrResult.Text;
Console.WriteLine(plainText);
```

Çıktı bozuk görünüyorsa, kaliteyi artırmak için `PreprocessSettings` (ör. deskew, despeckle) ile deney yapın.

### 5. Lisans Tuşları
Değerlendirme sürümünü çalıştırdığınızda Aspose çıktıya bir filigran ekler. Lisansı uygulamanın başında kaydedin:

```csharp
var license = new License();
license.SetLicense("Aspose.OCR.lic");
```

---

## Tam Çalışan Örnek – Baştan Sona

Aşağıda, yukarıdaki tüm ipuçlarını içeren, çalıştırılmaya hazır tam program yer alıyor. Yeni bir console projesine kopyalayıp yapıştırabilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class PdfOcrDemo
{
    static void Main()
    {
        // Load license (replace with your actual license file)
        var license = new License();
        license.SetLicense("Aspose.OCR.lic");

        // 1️⃣ Initialize OCR engine
        var ocrEngine = new OcrEngine();

        // Optional: set PDF password if needed
        // ocrEngine.Settings.PdfPassword = "mySecret";

        // Optional: tweak memory usage for large files
        ocrEngine.Settings.MemoryLimit = 1024; // MB

        // 2️⃣ Load scanned PDF (or image) – adjust path as required
        var source = OcrImage.FromFile("YOUR_DIRECTORY/input.pdf");

        // 3️⃣ Perform OCR – ask for a searchable PDF output
        var result = ocrEngine.Recognize(source, OutputFormat.SearchablePdf);

        // 4️⃣ Save the searchable PDF
        string outputPath = Path.Combine("YOUR_DIRECTORY", "output.pdf");
        File.WriteAllBytes(outputPath, result.Binary);

        Console.WriteLine($"Searchable PDF created at: {outputPath}");
    }
}
```

**Beklenen çıktı:** Çalıştırdıktan sonra, dosya konumunu belirten bir konsol satırı göreceksiniz. `output.pdf` dosyasını herhangi bir PDF görüntüleyicide açın; orijinal taramada bulunan bir kelimeyi yazmayı deneyin. Metin vurgulanıyorsa, **PDF üzerinde OCR yaptınız** ve aranabilir bir belge oluşturdunuz demektir.

---

## Sıkça Sorulan Sorular

**S: Tek bir görüntüyü (PNG/JPEG) aranabilir PDF'ye dönüştürebilir miyim?**  
C: Kesinlikle. `OcrImage.FromFile("input.pdf")` ifadesini görüntü dosyanızın yolu ile değiştirin. Motor aynı şekilde görüntüyü rasterleştirir ve OCR katmanını ekler.

**S: PDF'im hem taranmış sayfalar hem de yerel metin içeriyorsa ne olur?**  
C: Motor, mevcut içeriğin üzerine OCR metnini bindirir; yerel metin seçilebilir kalırken taranmış sayfalar aranabilir hâle gelir.

**S: OCR ne kadar doğru?**  
C: Doğruluk kaynak kalitesine bağlıdır. Temiz, yüksek çözünürlüklü taramalar (>300 dpi) %95'in üzerinde doğruluk sağlar. Gürültülü belgeler için `PreprocessSettings` (deskew, despeckle) etkinleştirerek kaliteyi artırın.

---

## Sonraki Adımlar – OCR Araç Setinizi Genişletme

Artık **PDF'den metin tanıma** ve **taranmış PDF'yi aranabilir PDF'ye dönüştürme** konularını başardığınıza göre, aşağıdaki konulara göz atabilirsiniz:

- **Toplu işleme**: Bir klasördeki PDF'leri döngüyle işleyip otomatik olarak aranabilir sürümler oluşturun.  
- **Metin çıkarma**: `ocrResult.Text`'i bir arama indeksi (ör. Elasticsearch) için kullanın.  
- **Özel dil paketleri**: Aspose'tan ek dil verileri indirerek Asya scriptlerini destekleyin.  
- **PDF/A uyumluluğu**: OCR çıktısını Aspose.PDF ile birleştirerek arşiv‑hazır PDF'ler üretin.  

Bu konular, temel adımlara dayanır; böylece çözümünüzü rahatça genişletebilirsiniz.

---

## Özet

Aspose.OCR kullanarak **PDF üzerinde OCR yapma**, taranmış PDF'leri tam anlamıyla aranabilir PDF'lere dönüştürme ve hatta düz görüntüleri aynı şekilde işleme konularını gösterdik. Kod

## Bir Sonraki Öğrenmeniz Gerekenler


Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayanan ve ilgili konuları derinlemesine ele alan örnekler sunar. Her kaynak, adım adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece API özelliklerini daha iyi kavrayabilir ve projelerinizde alternatif yaklaşımları keşfedebilirsiniz.

- [Recognize PDF Text – OCR Operations with Aspose.OCR for Java](/ocr/english/java/ocr-operations/)
- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Convert Images to PDF C# – Save Multipage OCR Result](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}