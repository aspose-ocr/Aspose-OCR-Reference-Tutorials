---
category: general
date: 2026-03-23
description: Aspose OCR kullanarak görüntüden aranabilir PDF oluşturun. Yüksek sıkıştırmalı
  TIFF'i PDF'ye dönüştürmeyi ve dakikalar içinde görüntü metnini tanımayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- high compression pdf
- recognize image text
- searchable pdf from image
language: tr
og_description: Aspose OCR ile görüntüden aranabilir PDF oluşturun. Bu öğreticide
  TIFF'i PDF'ye dönüştürme, aranabilir bir metin katmanı ekleme ve yüksek sıkıştırma
  uygulama gösterilmektedir.
og_title: Görüntüden Aranabilir PDF Oluşturma – Tam C# Rehberi
tags:
- Aspose OCR
- C#
- PDF generation
title: Görüntüden Aranabilir PDF Oluşturma – Tam C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-image-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma – Tam C# Kılavuzu

Tarayıcıdan bir belgeyi **create searchable pdf** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici TIFF taramalarını aranabilir PDF'lere dönüştürürken aynı sorunla karşılaşıyor. İyi haber? Aspose OCR ile **convert tiff to pdf** yapabilir, üzerine gizli bir metin katmanı ekleyebilir ve **high compression pdf** seçenekleriyle dosya boyutunu bile sıkıştırabilirsiniz, hepsi birkaç satır C# koduyla.

Bu öğreticide tüm süreci adım adım inceleyeceğiz: doğru NuGet paketlerini kurmaktan, bir TIFF görüntüsü yüklemeye, metnini tanımaya ve sonunda aranabilir bir PDF dışa aktarmaya kadar. Sonunda **recognize image text** yapan çalıştırılabilir bir konsol uygulamanız olacak ve indeksleme için hazır, kompakt, aranabilir bir PDF üretecek. Ekstra araçlar yok, manuel OCR adımları yok—sadece temiz kod ve biraz açıklama.

## Gereksinimler ve İhtiyacınız Olanlar

- **.NET 6+** (or .NET Framework 4.6+). API her iki platformda da çalışır, ancak .NET 6 size en yeni çalışma zamanı iyileştirmelerini sunar.  
- **Visual Studio 2022** veya tercih ettiğiniz herhangi bir IDE.  
- **Aspose.OCR** ve **Aspose.OCR.Gpu** NuGet paketleri (GPU paketi isteğe bağlıdır ancak desteklenen donanımlarda tanıma hızını artırır).  
- Kontrol ettiğiniz bir klasöre yerleştirilmiş örnek bir TIFF dosyası (ör., `invoice.tif`).  

Bu öğelere zaten sahipseniz, harika—bir sonraki adıma geçin. Yoksa, aşağıdaki kurulum adımı her şeyi kapsayacak.

## Adım 1: Aspose OCR Paketlerini Kurun

Başlamak için, projenizin klasörünü bir terminalde açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.OCR.Gpu
```

Bu komutlar hem temel OCR motorunu hem de GPU hızlandırma kütüphanesini çeker. İkincisi zorunlu değildir; motor uyumlu bir GPU bulamazsa CPU moduna geri dönecektir.

> **Pro tip:** Üretim ortamını hedeflerken, beklenmedik kırılma değişikliklerinden kaçınmak için `csproj` dosyanızda paket sürümlerini kilitleyin.

## Adım 2: Proje İskeletini Oluşturun

Yeni bir konsol uygulaması oluşturun (eğer henüz yoksa):

```bash
dotnet new console -n PdfExportDemo
cd PdfExportDemo
```

Otomatik oluşturulan `Program.cs` dosyasını daha sonra gösterilecek tam kodla değiştirin. Program şunları yapacak:

1. GPU desteğiyle bir `OcrEngine` başlatır.  
2. TIFF görüntüsünü yükler.  
3. OCR çalıştırır ve başarısızlıkta zarif bir şekilde durur.  
4. **PdfExportOptions**'ı aranabilir bir katman ve **high compression** için yapılandırır.  
5. Çıktı dosyasını yazar.

## Adım 3: Tam Kodu Yazın (Tam Örnek)

Aşağıda *tam* kaynak dosyası yer alıyor. `Program.cs` içine kopyalayıp yapıştırın. Yorumlar, her satırın “ne” değil, “neden” olduğunu açıklar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Export;
using System;

class PdfExport
{
    static void Main()
    {
        // ------------------------------------------------------------
        // 1️⃣ Initialise OCR engine with GPU acceleration.
        //    GpuMode.Enabled tells Aspose to use the GPU if one is present.
        //    If no compatible GPU exists, the engine automatically falls back
        //    to CPU mode—no extra code required.
        // ------------------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine(GpuMode.Enabled))
        {
            // ------------------------------------------------------------
            // 2️⃣ Load the source image.
            //    ImageStream.FromFile supports many formats; here we use TIFF.
            // ------------------------------------------------------------
            string inputPath = @"YOUR_DIRECTORY\invoice.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // ------------------------------------------------------------
            // 3️⃣ Perform OCR recognition.
            //    Recognize() returns false if the engine cannot read the image.
            //    Exiting early prevents us from creating an empty PDF.
            // ------------------------------------------------------------
            if (!ocrEngine.Recognize())
            {
                Console.WriteLine("OCR failed – check the image path and format.");
                return;
            }

            // ------------------------------------------------------------
            // 4️⃣ Configure PDF export options.
            //    IncludeTextLayer = true adds an invisible, searchable text layer.
            //    CompressionLevel = High reduces file size dramatically.
            // ------------------------------------------------------------
            PdfExportOptions pdfExportOptions = new PdfExportOptions
            {
                IncludeTextLayer = true,
                CompressionLevel = PdfCompression.High
            };

            // ------------------------------------------------------------
            // 5️⃣ Save the searchable PDF.
            //    The output will be a compact, searchable PDF ready for indexing.
            // ------------------------------------------------------------
            string outputPath = @"YOUR_DIRECTORY\invoice.pdf";
            ocrEngine.Save(outputPath, pdfExportOptions);
            Console.WriteLine($"Searchable PDF saved to: {outputPath}");
        }
    }
}
```

### Bunun Neden Çalıştığı

- **GPU acceleration** modern kartlarda tanıma süresini saniyelerden milisaniyelere düşürebilir—toplu işleme için kullanışlıdır.  
- **IncludeTextLayer** OCR‑türetilen metni görünmez şekilde gömer, PDF görüntüleyicilerin belgeyi görselini değiştirmeden aramasını sağlar.  
- **High compression** görüntü akışında Flate (ZIP) sıkıştırması kullanır, kayıpsızdır ancak dosya boyutunu büyük ölçüde küçültür—binlerce faturayı arşivlemek için idealdir.

## Adım 4: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Proje klasörünün içinde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet run
```

Her şey doğru kurulduysa, şunu göreceksiniz:

```
Searchable PDF saved to: YOUR_DIRECTORY\invoice.pdf
```

`invoice.pdf` dosyasını herhangi bir PDF okuyucusunda (Adobe Acrobat, Edge veya bir tarayıcı) açın. Orijinal TIFF'te bulunduğunu bildiğiniz bir kelimeyi aramayı deneyin—ör., “Total”. Görüntünün bir parçası olmasına rağmen görüntüleyici kelimeyi vurgulamalıdır. Bu, bir **searchable pdf**'in özelliğidir.

### Beklenen Dosya Boyutu

Tipik bir taranmış fatura (≈300 KB TIFF) `PdfCompression.High` uygulandıktan sonra genellikle **~80 KB**'a küçülür. Tam boyut, görüntünün karmaşıklığına bağlıdır, ancak belirgin bir azalma fark edeceksiniz.

## Adım 5: Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Ne Ayarlanmalı | Neden |
|-----------|----------------|-----|
| **GPU yok** | `new OcrEngine(GpuMode.Enabled)` ifadesini `new OcrEngine(GpuMode.Disabled)` ile değiştirin | Motorun GPU başlatma girişimini engeller, bu da kısa bir gecikmeye neden olabilir. |
| **Birden fazla sayfa (çok sayfalı TIFF)** | `ocrEngine.Image = ImageStream.FromFile("multi.tif", PageRange.All);` olarak ayarlayın | Tüm çerçeveleri yükler; Aspose her sayfayı işler ve çok sayfalı bir PDF oluşturur. |
| **İngilizce dışındaki OCR dili gerekiyor** | `ocrEngine.Language = Language.French;` (veya desteklenen herhangi bir dil) | İngilizce dışı belgelerde doğruluğu artırır. |
| **Gizli katman yerine görünür metin katmanı istiyorsunuz** | `pdfExportOptions.IncludeTextLayer = false;` ve manuel olarak `TextFragment` nesneleri ekleyin. | OCR metninin görüntünün üstünde seçilebilir metin olarak görünmesini istediğinizde faydalıdır. |
| **Ultra‑küçük PDF'ler** | Tanımadan önce `PdfCompression.High` ile `ImageResolution = 150` DPI'yi birleştirin. | Daha düşük DPI, görüntü verisini azaltır, PDF'i daha da küçültür ancak görsel kalite pahasına. |

> **Not:** Üretime ölçeklendirmeden önce kenar durumlarını her zaman küçük bir örnek üzerinde test edin. OCR doğruluğu görüntü kalitesi, gürültü ve dile göre değişebilir.

## Adım 6: Üretime Hazır Uygulamalar İçin İpuçları

1. **Error Logging** – `Console.WriteLine` yerine daha uygun bir günlükleme çerçevesi (Serilog, NLog) kullanarak tanılamayı kolaylaştırın.  
2. **Batch Processing** – Çekirdek mantığı, giriş/çıkış yollarını kabul eden bir metoda sarın, ardından bir TIFF dosyaları dizini üzerinde yineleyin.  
3. **Async I/O** – Aspose OCR kendisi eşzamanlı olsa da, dosya yükleme ve kaydetme işlemleri UI thread'lerini yanıt verir tutmak için async yapılabilir.  
4. **Security** – Bu işlevi bir web API üzerinden sunuyorsanız, dosya yollarını doğrulayın ve kötüye kullanımı önlemek için dosya boyutlarını sınırlayın.  
5. **Version Pinning** – Derlemeler arasında tutarlı davranışı garanti etmek için kesin sürüm numaralarını kullanın (`<PackageReference Include="Aspose.OCR" Version="23.12.0" />`).

## Sonuç

Tarayıcı görüntülerinden **searchable pdf** dosyaları **create searchable pdf** yapan, **convert tiff to pdf** ve **high compression pdf** ayarlarıyla **recognize image text** doğruluğu sağlayan **tam, uçtan uca bir çözüm** oluşturduk. Ortaya çıkan **searchable pdf from image** hafif, aranabilir ve indeksleme, arşivleme veya e‑keşif gibi sonraki iş akışları için hazır.

Bir fatura yığını mı var? Metodu bir döngüye yerleştirin, bir klasöre yönlendirin ve Aspose OCR'nin işi halletmesine izin verin. Farklı sıkıştırma seviyeleri veya dil paketleriyle deneme yapmak ister misiniz? Kod, bu seçenekleri saniyeler içinde değiştirecek kadar modülerdir.

---

*Hazır mısınız?* Bir filigran eklemeyi, meta veri gömmeyi veya birden fazla OCR‑işlenmiş PDF'yi birleştirmeyi deneyin. Aspose paketi birçok uzantı sunar—dökümanları keşfedin ve ilerlemeyi sürdürün. Kodlamanın tadını çıkarın!

![Create searchable PDF from image example screenshot](https://example.com/images/create-searchable-pdf.png "create searchable pdf example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}