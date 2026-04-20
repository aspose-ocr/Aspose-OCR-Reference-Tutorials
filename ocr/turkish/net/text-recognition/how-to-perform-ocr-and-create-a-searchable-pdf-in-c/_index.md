---
category: general
date: 2026-02-14
description: TIFF veya bir görüntüde OCR nasıl uygulanır ve OCR kullanarak PDF'yi
  aranabilir bir PDF'ye dönüştürürsünüz—adım adım C# rehberi.
draft: false
keywords:
- how to perform OCR
- convert pdf using OCR
- make searchable pdf
- tiff to searchable pdf
- searchable pdf from image
language: tr
og_description: Görsellerde OCR nasıl yapılır, OCR kullanarak PDF nasıl dönüştürülür
  ve Aspose OCR ile aranabilir bir PDF nasıl oluşturulur, kısa bir C# öğreticisinde
  keşfedin.
og_title: C#'ta OCR Nasıl Yapılır ve Aranabilir PDF Nasıl Oluşturulur
tags:
- OCR
- C#
- Aspose
- PDF conversion
title: C#'ta OCR Nasıl Yapılır ve Aranabilir PDF Oluşturulur
url: /tr/net/text-recognition/how-to-perform-ocr-and-create-a-searchable-pdf-in-c/
---

as is.

Make sure we keep bullet lists formatting.

Now produce final output with all translated content and unchanged shortcodes.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile OCR Nasıl Yapılır ve Aranabilir PDF Oluşturulur

Tarama belgesi üzerinde **perform OCR** (OCR gerçekleştirmek) yapmanız gerektiğinde, sonucu aranabilir bir PDF'ye nasıl dönüştüreceğinizi bilemediğiniz oldu mu? Yalnız değilsiniz—birçok geliştirici, eski TIFF arşivleri veya yalnızca görüntü içeren PDF'lerle çalışırken bu engelle karşılaşıyor. İyi haber? Birkaç satır C# ve Aspose.OCR kütüphanesiyle, bir TIFF'i ya da herhangi bir görüntüyü birkaç saniye içinde tamamen aranabilir bir PDF'ye dönüştürebilirsiniz.

Bu öğreticide, bilmeniz gereken her şeyi adım adım göstereceğiz: kütüphaneyi kurmaktan, çok sayfalı bir TIFF'i yüklemeye, `RecognizeToPdf` metodunu çağırmaya kadar, böylece **convert PDF using OCR** ve **make searchable PDF** dosyalarını oluşturabilir ve kullanıcılarınızın gerçekten arama yapabileceği PDF'ler elde edebilirsiniz. Sonunda, bir görüntü kaynağından aranabilir PDF üreten, çalıştırmaya hazır bir konsol uygulamanız olacak.

## Önkoşullar

- **.NET 6.0** veya üzeri (kod .NET Framework 4.7+ üzerinde de çalışır).
- Geçerli bir **Aspose.OCR** lisansı veya geçici bir değerlendirme anahtarı (ücretsiz deneme testi için yeterlidir).
- **NuGet** paket yöneticisine sahip Visual Studio 2022 (veya tercih ettiğiniz herhangi bir editör).
- `input.tif` adlı bir giriş dosyası, kontrol ettiğiniz bir klasöre yerleştirilmiş olmalı—çok sayfalı TIFF'ler doğrudan çalışır.

> **Pro tip:** Windows kullanıyorsanız, TIFF'i derlenmiş `.exe` dosyasının bulunduğu klasöre kopyalayarak yol ile ilgili sorunlardan kaçının.

## Adım 1: Aspose.OCR NuGet Paketini Yükleyin

Proje klasörünüzü bir terminalde açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu, en son kararlı sürümü (Şubat 2026 itibarıyla 23.10) indirir ve tüm gerekli bağımlılıkları ekler. Geri yükleme tamamlandığında, Solution Explorer'da **Dependencies** altında `Aspose.OCR` listelendiğini göreceksiniz.

## Adım 2: Minimal Bir Konsol Uygulaması Oluşturun

Henüz bir projeniz yoksa yeni bir konsol projesi oluşturun:

```bash
dotnet new console -n OcrSearchablePdfDemo
cd OcrSearchablePdfDemo
```

Otomatik oluşturulan `Program.cs` dosyasını **Adım 3**'te gösterilen tam kodla değiştirin. Program şunları yapacak:

1. OCR motorunu örnekleyecek.
2. Kaynak görüntüyü (veya çok sayfalı TIFF'i) yükleyecek.
3. OCR çalıştırıp çıktıyı doğrudan aranabilir bir PDF'ye yazacak.
4. Kullanıcıya işlemin başarılı olduğunu bildirecek.

## Adım 3: Tam Çalışan Kod – Görüntüden Aranabilir PDF'ye

Aşağıda **tam** kaynak dosyası yer alıyor. `Program.cs` içine kopyalayıp yapıştırın. Açıklayıcı yorumlar, gözden kaçabilecek kısımları açıklıyor.

```csharp
using System;
using Aspose.OCR;          // Core OCR namespace
using Aspose.OCR.Image;   // Provides ImageStream helpers

namespace OcrSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣ Initialise the OCR engine.
            // -------------------------------------------------
            // The Engine class is the entry point for all OCR operations.
            // You can optionally pass a license object here if you have one.
            var ocrEngine = new Engine();

            // -------------------------------------------------
            // 2️⃣ Load the source image.
            // -------------------------------------------------
            // ImageStream.FromFile supports TIFF, PDF, JPEG, PNG, etc.
            // For multi‑page TIFFs the stream automatically contains all pages.
            string inputPath = "YOUR_DIRECTORY/input.tif";
            var imageStream = ImageStream.FromFile(inputPath);

            // -------------------------------------------------
            // 3️⃣ Perform OCR and write a searchable PDF.
            // -------------------------------------------------
            // RecognizeToPdf does the heavy lifting:
            // • It runs the OCR engine on every page.
            // • It embeds the extracted text as an invisible layer.
            // • The visual appearance of the original image is preserved.
            string outputPath = "YOUR_DIRECTORY/searchable.pdf";
            ocrEngine.RecognizeToPdf(imageStream, outputPath);

            // -------------------------------------------------
            // 4️⃣ Inform the user.
            // -------------------------------------------------
            Console.WriteLine("Searchable PDF created at: " + outputPath);
        }
    }
}
```

**Gördükleriniz:** Programı çalıştırdıktan sonra hedef klasörde `searchable.pdf` adlı bir dosya oluşur. Adobe Reader ya da herhangi bir PDF görüntüleyicide açın ve orijinal TIFF'te bulunan bir kelimeyi aramayı deneyin. Metin anında bulunmalı, böylece bir görüntüden **made searchable PDF** (aranabilir PDF) oluşturduğunuzu kanıtlar.

### Uygulamayı Çalıştırma

```bash
dotnet run
```

Her şey doğru ayarlandıysa şu çıktıyı alacaksınız:

```
Searchable PDF created at: YOUR_DIRECTORY/searchable.pdf
```

PDF'yi açın, `Ctrl+F` tuşlarına basın, kaynaktan bir kelime yazın ve vurgunun doğru konuma atladığını izleyin.

## Adım 4: Yaygın Varyasyonlar ve Kenar Durumları

### Normal Bir PDF'yi (yalnızca görüntü) Aranabilir PDF'ye Dönüştürme

Kaynağınız metin yerine taranmış görüntüler içeren bir PDF ise, aynı yöntemi kullanabilirsiniz—sadece `ImageStream` kaynağını değiştirin:

```csharp
var pdfStream = ImageStream.FromFile("YOUR_DIRECTORY/input.pdf");
ocrEngine.RecognizeToPdf(pdfStream, "YOUR_DIRECTORY/searchable_from_pdf.pdf");
```

Bu, ekstra kod eklemeden **convert pdf using OCR** senaryosunu karşılar.

### Büyük Çok Sayfalı Belgelerle Başa Çıkma

Birkaç yüz sayfayı aşan belgeler için şunları düşünün:

- **Bellek limitlerini artırma** (`Engine.MemoryLimit = 2_000; // MB`).
- **Parçalar halinde işleme**: sayfaların bir alt kümesini yükleyin, ara PDF'ler yazın, ardından bir PDF kütüphanesi (ör. Aspose.PDF) ile birleştirin.

### İngilizce Dışındaki Dillerle Çalışma

Aspose.OCR, kutudan çıkar çıkmaz birçok dili destekler. Tanımadan önce dili ayarlayın:

```csharp
ocrEngine.Language = OcrLanguage.French; // or OcrLanguage.Spanish, etc.
```

Eğer Latin dışı bir alfabede **tiff to searchable pdf** ihtiyacınız varsa, uygun dil paketinin yüklü olduğundan emin olun.

### Çıktı PDF Boş Çıktıysa Ne Yapmalı?

- Giriş dosyasının bozuk olmadığını doğrulayın.
- OCR motorunun geçerli bir lisansa sahip olduğundan emin olun—değerlendirme modu sayfa limitleri getirebilir.
- Görüntü çözünürlüğünün en az 300 dpi olduğundan kontrol edin; daha düşük çözünürlükler düşük tanıma kalitesine yol açabilir.

## Adım 5: Sonucu Programatik Olarak Doğrulama (İsteğe Bağlı)

Bazen PDF'in gerçekten bir metin katmanı içerdiğini doğrulamak isteyebilirsiniz. Metni çıkarmak için Aspose.PDF'yi kullanabilirsiniz:

```csharp
using Aspose.Pdf;

var pdfDoc = new Document("YOUR_DIRECTORY/searchable.pdf");
string extracted = pdfDoc.Pages[1].ExtractText();
Console.WriteLine("First page text snippet: " + extracted.Substring(0, 100));
```

`extracted` boş değilse, **made searchable pdf** işlemini başarıyla tamamlamışsınız.

## Sonuç

TİFF (veya herhangi bir görüntü) üzerinde **how to perform OCR** konusunu ve sorunsuz bir şekilde **convert PDF using OCR** yaparak **searchable PDF** (aranabilir PDF) oluşturmayı ele aldık; bu PDF yerel bir belge gibi davranır. Temel adımlar şunlardır:

1. Aspose.OCR'ı kurun.  
2. `Engine`'i başlatın.  
3. Görüntüyü `ImageStream` ile yükleyin.  
4. `RecognizeToPdf`'yi çağırın.

Bundan sonra dil ayarları, büyük toplu işleme deneyebilir ya da çıktıyı diğer PDF manipülasyon görevleriyle birleştirebilirsiniz. Aynı desen **tiff to searchable pdf**, **searchable pdf from image** ve hatta taranmış PDF'ler için de çalışır.

Bir sonraki meydan okumaya hazır mısınız? OCR'ı bir web API'sine entegre ederek kullanıcıların taramaları yükleyip anında aranabilir PDF'ler almasını sağlayın, ya da `OcrEngine`'in gelişmiş ayarlarıyla el yazısı notlarda OCR'ı keşfedin. Olanaklar sınırsız—iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}