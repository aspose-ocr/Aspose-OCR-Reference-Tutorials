---
category: general
date: 2026-02-13
description: Aspose.OCR kullanarak görüntüden aranabilir PDF oluşturun. Görüntüyü
  PDF'ye dönüştürmeyi, görüntüden metin çıkarmayı, PDF'ye yazı tipleri eklemeyi ve
  PNG'den metin tanımayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- embed fonts in pdf
- recognize text from png
language: tr
og_description: Aspose.OCR ile görüntüden aranabilir PDF oluşturun. Bu kılavuz, görüntüyü
  PDF'ye dönüştürmeyi, yazı tiplerini gömmeyi ve PNG'den metni zahmetsizce çıkarmayı
  gösterir.
og_title: Görüntüden Aranabilir PDF Oluşturma – Adım Adım C# Öğreticisi
tags:
- C#
- OCR
- Aspose
- PDF generation
title: Görüntüden Aranabilir PDF Oluşturma – Tam C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma – Tam C# Rehberi

Hiç taranmış bir PNG'den **aranabilir PDF** oluşturmanız gerekti ama nereden başlayacağınızı bilmiyor muydunuz? Yalnız değilsiniz. Birçok projede—fatura dijitalleştirme veya eski kılavuzları arşivleme gibi—bir resmi gerçekten arayabileceğiniz bir PDF'ye dönüştürebilmek oyunu değiştiren bir özellik.  

Bu öğreticide **görüntüyü PDF'ye dönüştürme**, **görüntüden metin çıkarma**, gerekli yazı tiplerini gömme ve sonunda tamamen aranabilir bir PDF dosyası elde etme adımlarını adım adım göstereceğiz. Belirsiz referanslar yok, sadece bugün Visual Studio'ya kopyalayıp yapıştırabileceğiniz tam, çalıştırılabilir bir örnek.

> **Ne elde edeceksiniz:** `input.png` dosyasını okuyan, OCR çalıştıran, yazı tiplerini gömen, orijinal raster görüntüyü arka plan olarak tutan ve `output.pdf` dosyasını yazan bir C# konsol uygulaması. Sonunda her satırın *neden* önemli olduğunu ve kendi senaryolarınız için nasıl ayarlayabileceğinizi anlayacaksınız.

---

## Önkoşullar

- .NET 6.0 SDK veya daha yenisi (kod .NET Framework 4.7+ ile de çalışır).  
- Aspose.OCR for .NET – NuGet üzerinden alabilirsiniz (`Install-Package Aspose.OCR`).  
- Kontrol ettiğiniz bir klasörde bulunan örnek PNG görüntüsü (`input.png`).  
- C# konsol projeleri hakkında temel bilgi (eğer hiç oluşturmadıysanız, Visual Studio → **Create a new project** → **Console App** → **C#** yolunu izleyin).

> **İpucu:** Aspose ücretsiz bir deneme lisansı sunar; `.lic` dosyasını çalıştırılabilir dosyanızın yanına koymanız yeterli, kütüphane filigran olmadan çalışır.

## Adım 1: OCR Motorunu Kurun – PNG'den Metin Tanıma

İlk olarak, PNG dosyasındaki karakterleri gerçekten okuyabilen bir OCR motoruna ihtiyacımız var. Aspose.OCR bunu oldukça basit hâle getiriyor.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

// Initialize the OCR engine with English language support
OcrEngine ocrEngine = new OcrEngine
{
    // Primary language – you can add more if needed
    Language = OcrLanguage.English
};
```

**Neden önemli:**  
`Language` ayarı, motorun hangi karakter setini bekleyeceğini belirtir. Bunu atlayarsanız motor, aksanlı karakterleri veya sayıları yanlış yorumlayabilecek genel bir moda geçer. Çok dilli belgeler için `OcrLanguage.English | OcrLanguage.French` gibi virgülle ayrılmış bir liste verebilirsiniz.

## Adım 2: Görüntüyü Yükleyin ve Tanıyın – Görüntüden Metin Çıkarma

Motor hazır olduğuna göre, işlemek istediğimiz PNG'yi ona veriyoruz.

```csharp
// Path to the source image; adjust as needed
string inputPath = @"YOUR_DIRECTORY/input.png";

// Perform OCR – this populates the engine's internal text representation
ocrEngine.RecognizeImage(inputPath);
```

**Arka planda neler oluyor?**  
`RecognizeImage` bitmap'i tarar, metin bloklarını belirler ve sonucu `ocrEngine` içinde saklar. Sadece ham dizeye ihtiyacınız varsa daha sonra `ocrEngine.Text`'e erişebilirsiniz, ancak aranabilir bir PDF için dönüşümü Aspose'a bırakacağız.

> **Köşe durumu:** PNG'niz çok büyükse (10 MB üzerindeyse) bellek tükenebilir. Bu durumda önce görüntüyü yeniden boyutlandırmayı veya veriyi akış olarak göndermek için `OcrEngine.RecognizeImage(Stream)` kullanmayı düşünün.

## Adım 3: PDF Dışa Aktarım Seçeneklerini Yapılandırın – PDF'e Yazı Tipi Gömme

Aranabilir bir PDF, yazı tipleri gömülmemişse işe yaramaz; belge, gerekli tipografileri olmayan makinelerde bozuk görünür. Aspose bu ayarı basit bir seçenek nesnesiyle kontrol etmemizi sağlar.

```csharp
// Define how the searchable PDF should be built
SearchablePdfOptions pdfOptions = new SearchablePdfOptions
{
    // Guarantees the PDF renders correctly everywhere
    EmbedFonts = true,

    // Keeps the original raster image as a visual background
    KeepOriginalImage = true
};
```

**Neden yazı tipleri gömülür?**  
`EmbedFonts` `true` olduğunda PDF, yazı tipi verisini dosyanın içinde taşır. Bu, Chrome, Adobe Reader veya bir mobil uygulama gibi herhangi bir görüntüleyicinin, hedef sistemde font bulunmasa bile metni tam olarak istediği gibi göstermesini sağlar.

**`KeepOriginalImage` değerini `false` ne zaman ayarlamalısınız?**  
Sadece çıkarılan metni istiyor ve daha küçük bir dosya istiyorsanız, bu seçeneği kapatmak arka plan görüntüsünü kaldırır ve “temiz” sadece metin içeren bir PDF oluşturur.

## Adım 4: Aranabilir PDF Olarak Dışa Aktarın – Görüntüyü PDF'ye Dönüştürün

OCR sonuçları ve PDF seçenekleri hazır olduğunda, tek satırlık bir komutla aranabilir PDF'i diske yazdırıyoruz.

```csharp
// Destination path for the generated PDF
string outputPath = @"YOUR_DIRECTORY/output.pdf";

// Export the OCR result as a searchable PDF
ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created.");
```

**Gördükleriniz:**  
`output.pdf` dosyasını herhangi bir görüntüleyicide açtığınızda metni seçebilir, kopyalayabilir ve `Ctrl + F` ile PNG'de sadece pikseller olarak bulunan kelimeleri arayabilirsiniz.

## Tam Çalışan Örnek

Aşağıda hemen derleyip çalıştırabileceğiniz tam program yer alıyor. `YOUR_DIRECTORY` kısmını `input.png` dosyanızın bulunduğu klasörle değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine – set language to English
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Recognize text from the PNG image
        string inputPath = @"YOUR_DIRECTORY/input.png";
        ocrEngine.RecognizeImage(inputPath);

        // 3️⃣ Prepare PDF options – embed fonts & keep raster background
        SearchablePdfOptions pdfOptions = new SearchablePdfOptions
        {
            EmbedFonts = true,
            KeepOriginalImage = true
        };

        // 4️⃣ Export to a searchable PDF file
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ExportToSearchablePdf(outputPath, pdfOptions);

        // 5️⃣ Notify the user
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Konsolda beklenen çıktı:**

```
Searchable PDF created.
```

`output.pdf` dosyasını açın ve `input.png` içinde bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin. Eğer vurgulanıyorsa, **görüntüden aranabilir pdf oluşturma** işlemini başarıyla tamamlamışsınız demektir.

## Yaygın Sorular & Profesyonel İpuçları

### “Bir çalıştırmada birden fazla görüntüyü işleyebilir miyim?”

Kesinlikle. Tanıma ve dışa aktarma mantığını bir döngü içinde sarabilirsiniz, örneğin `Directory.GetFiles(..., "*.png")` kullanarak. Her PDF'e benzersiz bir ad vermeyi unutmayın, örneğin `Path.GetFileNameWithoutExtension(img) + ".pdf"`.

### “Belgem hem İngilizce hem de İspanyolca metin içeriyorsa ne yapmalıyım?”

Dil özelliğini birleşik bir bayrak olarak ayarlayın:

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

Aspose, her iki alfabeden karakterleri algılamaya çalışacaktır.

### “PDF dosyası çok büyük—nasıl küçültebilirim?”

İki hızlı yöntem:

1. `pdfOptions.KeepOriginalImage = false` ayarıyla raster arka planı kaldırın.  
2. `pdfOptions.ImageCompression = ImageCompression.Jpeg;` (bu özelliği eklemeniz gerekir) kullanarak gömülü görüntüyü sıkıştırın.

### “Üretim ortamında lisansa ihtiyacım var mı?”

Deneme sürümü test için yeterlidir, ancak ticari dağıtımda bir lisans satın almalı ve uygulamanızın başında kaydetmelisiniz:

```csharp
Aspose.OCR.License license = new Aspose.OCR.License();
license.SetLicense("Aspose.OCR.lic");
```

## Çözümü Genişletmek

Artık **aranabilir PDF oluşturma** konusunu bildiğinize göre, şunları eklemek isteyebilirsiniz:

- **Filigran ekleme** – OCR sonrası `PdfDocument` (Aspose.PDF) kullanarak üzerine metin yerleştirin.  
- **PDF'leri toplu işleme** – birden fazla aranabilir PDF'i `PdfFileEditor` ile tek bir dosyada birleştirin.  
- **Azure Blob Storage ile bütünleştirme** – görüntü ve PDF akışlarını doğrudan buluttan okuyup yazarak yerel dosya I/O'sunu ortadan kaldırın.

Bu uzantıların her biri aynı modeli izler: OCR sonucunu alın, sonraki kütüphaneyi yapılandırın ve işlemleri zincirleyin.

## Sonuç

Aspose.OCR ve C# kullanarak bir PNG görüntüsünden **aranabilir PDF** oluşturmayı öğrendiniz. OCR motorunu başlatıp metni tanıdıktan, `SearchablePdfOptions` ile **PDF'e yazı tiplerini gömerek** dışa aktarma adımlarını izleyerek, hem görsel olarak orijinaliyle aynı hem de tamamen aranabilir bir dosya elde ettiniz.  

Şimdi toplu dönüşümler, farklı diller veya daha sıkı sıkıştırma gibi denemeler yapabilirsiniz—iş akışınıza en uygun olanı seçin. Sorunlarla karşılaşırsanız Aspose forumları ve API dokümantasyonu iyi kaynaklardır, ancak yukarıdaki temel adımlar tipik kullanım senaryolarının %90'ını kapsar.

Kodlamanın tadını çıkarın, PDF'leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}