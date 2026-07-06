---
category: general
date: 2026-05-06
description: Aspose OCR kullanarak C#'ta bir görüntüden aranabilir PDF oluşturun.
  PNG'yi PDF'ye dönüştürmeyi, görüntüden metin çıkarmayı ve aranabilir bir PDF üretmeyi
  öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- convert png to pdf
- ocr image to pdf
language: tr
og_description: Aspose OCR kullanarak C#'ta bir görüntüden aranabilir PDF oluşturun.
  Bu adım adım öğretici, png'yi pdf'ye dönüştürmeyi, görüntüden metin çıkarmayı ve
  aranabilir bir PDF üretmeyi gösterir.
og_title: Görüntüden Aranabilir PDF Oluşturma – C# Aspose OCR Rehberi
tags:
- Aspose
- C#
- OCR
- PDF
title: Görüntüden Aranabilir PDF Oluşturma – C# Aspose OCR Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-image-c-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma – C# Aspose OCR Kılavuzu

Hiç taranmış bir resimden **create searchable PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilemediniz mi? Belki bir PNG makbuzunuz, bir sözleşmenin JPEG'i ya da arama yapabileceğiniz bir PDF'e dönüştürmek istediğiniz herhangi bir bitmap dosyanız vardır. Bu, özellikle bir klasörde duran eski taramalarla uğraşırken yaygın bir sorundur.

İyi haber, Aspose OCR ile **convert image to PDF** yapabilir, gizli metni çıkarabilir ve tamamen aranabilir bir belge elde edebilirsiniz—bunun hepsi birkaç satır C# koduyla. Bu kılavuzda ayrıca **convert png to PDF**, **extract text from image** nasıl yapılacağını ve çok sayfalı TIFF'lerin işlenmesi gibi uç durumları da göstereceğiz. Sonuna geldiğinizde, herhangi bir .NET projesine ekleyebileceğiniz bağımsız bir çözümünüz olacak.

## Gereksinimler

- **.NET 6+** (kod .NET Framework 4.6+ üzerinde de çalışır)
- **Visual Studio 2022** veya tercih ettiğiniz herhangi bir IDE
- **Aspose.OCR** NuGet paketi (Aspose.PDF'yi otomatik olarak ekler)
- Aranabilir PDF'e dönüştürmek istediğiniz bir görüntü dosyası (PNG, JPEG, BMP, TIFF)

Ek lisans hilesi yok, harici hizmet yok—sadece tek bir NuGet referansı ve birkaç dakikalık kodlama.

## Adım 1: Aspose.OCR NuGet Paketini Yükleyin

İlk olarak, kütüphaneyi projenize ekleyin. Package Manager Console'u açın ve şu komutu çalıştırın:

```powershell
Install-Package Aspose.OCR
```

Bu tek komut, bağımlı olduğu **Aspose.OCR** ve **Aspose.Pdf** derlemelerini indirir, böylece hem görüntüyü okuyup hem de PDF yazmaya hazır olursunuz.

> **Pro tip:** .NET CLI kullanıyorsanız eşdeğeri `dotnet add package Aspose.OCR` komutudur.

## Adım 2: OCR Motorunu Başlatın

`OcrEngine` örneği oluşturmak, tüm OCR işlemlerinin kapısıdır. Bunu, resminize bakıp karakterleri “okumaya” başlayan bir beyin olarak düşünün.

```csharp
using Aspose.OCR;
using Aspose.Pdf;   // pulled in by the OCR package

// Create an OCR engine instance – this object holds configuration and state
var ocrEngine = new OcrEngine();
```

Merak edebilirsiniz, *neden doğrudan statik bir metod çağırmıyoruz?* Nesne‑yönelimli yaklaşım, ayarları (dil, çözünürlük vb.) daha sonra değiştirmenize izin verir, genel akışı değiştirmeden.

## Adım 3: Dönüştürmek İstediğiniz Görüntüyü Yükleyin

İşte burada, bitmap'i OCR motoruna vererek **convert image to PDF** işlemini yapıyoruz. `"YOUR_DIRECTORY/input.png"` ifadesini dosyanızın gerçek yolu ile değiştirin.

```csharp
// Load the source image (PNG, JPEG, BMP, or multi‑page TIFF)
ocrEngine.SetImage("YOUR_DIRECTORY/input.png");
```

Eğer bir **convert png to pdf** senaryonuz varsa, sadece PNG'ye işaret edin. Çok sayfalı TIFF'lerde, Aspose.OCR otomatik olarak her çerçeveyi ayrı bir sayfa olarak ele alır.

## Adım 4: OCR'ı Çalıştırın ve İsteğe Bağlı Metni Alın

`Recognize()` metodunu çalıştırmak işi halleder: resmi analiz eder, karakterleri algılar ve yapılandırılmış bir sonuç döndürür. Metni, günlük kaydı, arama indeksleme veya gösterim için saklayabilirsiniz.

```csharp
// Perform OCR – this extracts the textual content from the image
var ocrResult = ocrEngine.Recognize();

// Optional: show the extracted text in the console
Console.WriteLine("Extracted text:");
Console.WriteLine(ocrResult.Text);
```

> **Neden metin çıkarılıyor?** Son PDF'e gömecek olsak da, ham dizeyi elde tutmak doğrulama veya analiz için faydalı olabilir.

## Adım 5: Aranabilir Bir Belge İçin PDF Seçeneklerini Yapılandırın

Aspose.PDF, **CreateSearchablePdf** adlı özel bir `PdfSaveOptions` modu sağlar. Bu, kütüphaneye OCR metnini görüntünün arkasına görünmez bir katman olarak eklemesini söyler ve PDF'i aranabilir hâle getirir.

```csharp
// Prepare PDF save options – this tells Aspose to embed OCR text
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();
```

Eğer sadece görüntü içeren bir PDF'e (gizli metin olmadan) ihtiyacınız olursa, `PdfSaveOptions.CreatePdf()`'a geçebilirsiniz. Ancak amacımız—**create searchable PDF**—için aranabilir mod yıldızdır.

## Adım 6: Aranabilir PDF'i Disk'e Kaydedin

Şimdi her şeyi birleştiriyoruz. `SavePdf` metodu, görüntüyü ve gizli metni tek bir dosyaya yazar.

```csharp
// Save the searchable PDF file
ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

Console.WriteLine("Searchable PDF created successfully.");
```

Bu noktada, Adobe Reader'da açabileceğiniz, arama kutusuna bir kelime yazıp eşleşen konuma anında gidebileceğiniz bir **searchable PDF**'e sahipsiniz—görünür sayfa hâlâ orijinal görüntü olsa da.

## Tam Çalışan Örnek

Tüm parçaları bir araya getirerek, çalıştırmaya hazır bir konsol uygulaması burada. Yeni bir C# projesine kopyalayıp yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.OCR;
using Aspose.Pdf; // included automatically with Aspose.OCR

class Program
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        var ocrEngine = new OcrEngine();

        // Step 2: Load the image that contains the scanned document
        // Replace with your actual image path
        ocrEngine.SetImage("YOUR_DIRECTORY/input.png");

        // Step 3: Run the OCR process to extract text (optional but useful)
        var ocrResult = ocrEngine.Recognize();

        // Show extracted text – helpful for debugging
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("======================");

        // Step 4: Prepare to export the recognized content as a searchable PDF
        var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

        // Step 5: Save the searchable PDF to disk
        // Replace with your desired output path
        ocrEngine.SavePdf("YOUR_DIRECTORY/output.pdf", pdfOptions);

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created successfully.");
    }
}
```

### Beklenen Çıktı

Programı çalıştırdığınızda, konsol şu şekilde bir çıktı verir:

```
=== Extracted Text ===
Invoice #12345
Date: 2024‑04‑30
Total: $1,250.00
...
======================
Searchable PDF created successfully.
```

Ve `YOUR_DIRECTORY` içinde `output.pdf` dosyasını bulacaksınız. Açın, **Ctrl F** tuşlarına basın, “Invoice” yazın ve kelimeye doğrudan atlayın—sayfa düz bir tarama gibi görünse de.

## Yaygın Varyasyonları Ele Alma

### Birden Çok Görüntüyü Tek Seferde Dönüştürme

Eğer PNG'lerle dolu bir klasörünüz varsa ve tek bir aranabilir PDF istiyorsanız, dosyalar üzerinde döngü kurup her birini ayrı bir sayfa olarak ekleyin:

```csharp
var allImages = Directory.GetFiles("YOUR_DIRECTORY", "*.png");
var ocrEngine = new OcrEngine();
var pdfOptions = PdfSaveOptions.CreateSearchablePdf();

foreach (var imgPath in allImages)
{
    ocrEngine.SetImage(imgPath);
    ocrEngine.Recognize(); // extracts text for the current page
    ocrEngine.SavePdf("temp_page.pdf", pdfOptions);

    // Merge temp_page.pdf into the final document (omitted for brevity)
}
```

Ayrıca geçici PDF'leri tek bir son dosyada birleştirmek için Aspose.PDF'den `PdfFileEditor` kullanabilirsiniz.

### Düşük Çözünürlüklü Tarama ile Baş Etme

Görüntü DPI'sı 150'nin altında olduğunda OCR doğruluğu düşer. Görüntüyü OCR'a vermeden önce ölçeğini artırabilirsiniz:

```csharp
ocrEngine.ImageProcessingOptions.Dpi = 300; // forces 300 DPI for better recognition
```

### Belirli Bir Dil Seçme

Belgeniz İngilizce değilse, `Recognize()`'den önce dili ayarlayın:

```csharp
ocrEngine.Language = Language.Spanish; // or Language.French, etc.
```

Bu ayarlamalar, **extract text from image**'in farklı senaryolarda güvenilir çalışmasını sağlar.

## Görsel Sonuç

![Aspose OCR ile oluşturulan aranabilir PDF – create searchable PDF](https://example.com/images/searchable-pdf.png)

*Yukarıdaki ekran görüntüsü, görüntünün görüldüğü ancak metin katmanının aranabilir olduğu bir PDF'i gösterir.*

## Sonuç

Artık Aspose OCR ve C# kullanarak herhangi bir görüntüden **create searchable PDF** dosyaları oluşturmak için eksiksiz, üretim‑hazır bir tarifiniz var. **convert image to PDF**, **extract text from image** nasıl yapılacağını ve hatta **convert png to pdf** ve **ocr image to pdf** gibi uç durumları ele aldık. Kod tamamen bağımsızdır, herhangi bir .NET çalışma zamanında çalışır ve toplu işleme ya da özel dil desteğine genişletilebilir.

Sırada ne var? Bir filigran eklemeyi, PDF'i şifrelemeyi ya da çıkarılan metni Elasticsearch gibi bir arama indeksine beslemeyi deneyin. Olasılıklar sonsuzdur ve aynı desen—yükle → tanı → kaydet—her OCR‑tabanlı iş akışı için size iyi hizmet edecektir.

Herhangi bir sorunla karşılaşırsanız ya da paylaşacak ilginç bir kullanım senaryonuz varsa, aşağıya yorum bırakın. Kodlamaktan keyif alın ve o inatçı taramaları aranabilir altına dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}