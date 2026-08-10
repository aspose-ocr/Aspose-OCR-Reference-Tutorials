---
category: general
date: 2026-03-18
description: Aspose OCR kullanarak C#'ta aranabilir PDF oluşturun. Görüntüyü PDF'ye
  dönüştürün, OCR metin katmanını ekleyin ve birkaç kolay adımda PDF baytlarını dosyaya
  yazın.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- recognize text from image
- add ocr text layer
- write pdf bytes to file
language: tr
og_description: Aspose OCR ile C#'ta hızlıca aranabilir PDF oluşturun. Görüntüyü PDF'ye
  dönüştürmeyi, OCR metin katmanı eklemeyi ve PDF baytlarını dosyaya yazmayı öğrenin.
og_title: Görüntüden Aranabilir PDF Oluştur – Hızlı C# OCR Rehberi
tags:
- OCR
- PDF
- C#
- Aspose
title: OCR ile Görüntüden Aranabilir PDF Oluşturma – C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-image-with-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden OCR ile Aranabilir PDF Oluşturma – C# Kılavuzu

Tarama görüntüsünden **aranabilir PDF** oluşturmanız gerektiğinde? Aspose OCR ile bunu birkaç satırda yapabilirsiniz, ağır kütüphanelere gerek yok. Bu öğreticide **görüntüyü PDF'ye dönüştüreceğiz**, üzerine bir **OCR metin katmanı** ekleyeceğiz ve sonunda **PDF baytlarını dosyaya yazacağız**, böylece kullanıcılarınızın gerçekten arama yapabileceği standartlara uygun bir PDF/A‑2b belgesi elde edeceksiniz.

Neden düz bir yalnızca görüntü dosyası yerine aranabilir PDF ile uğraşacağınızı merak ediyorsanız, kullanıcı deneyimini düşünün: aranabilir PDF, insanların metni kopyalamasına, seçmesine ve indekslemesine olanak tanır—arşivler, yasal belgeler veya daha sonra metin çıkarımı gerektiren herhangi bir iş akışı için harika. Hadi başlayalım.

## Gereksinimler

- .NET 6 veya daha yenisi (kod .NET Framework 4.7+ üzerinde de çalışır)
- Bir Aspose.OCR NuGet paketi (`Aspose.OCR` sürüm 23.10 veya daha yenisi)
- Aranabilir PDF'ye dönüştürmek istediğiniz bir raster görüntü (`.png`, `.jpg`, vb.)
- Biraz C# bilgisi—fantezi bir şey değil, sadece temeller

Hepsi bu. Harici araç yok, ekstra dönüştürücü yok. Tüm ağır işleri Aspose OCR motoru halleder.

## Aranabilir PDF Oluşturma – Genel Bakış

Koda dalmadan önce süreci özetleyelim:

1. **Instantiate** OCR motorunu – bu nesne resimlerden metin okuma yeteneğine sahiptir.  
2. **Load** kaynak görüntüyü – motorun içine bir `ImageStream` besleyeceğiz.  
3. **Configure** PDF/A‑2b kaydetme seçeneklerini – bu, Aspose'a tanınan metni gizli bir katman olarak gömmesini söyler.  
4. **Run** OCR'ı ve **capture** ortaya çıkan PDF baytlarını.  
5. **Write** bu baytları diske, nihai aranabilir PDF dosyasını üretmek.

Bu adımların her biri doğrudan bir ya da iki C# satırına karşılık gelir, bu da tüm iş akışını büyük bir proje yerine küçük bir betik gibi hissettirir.

## Adım 1: Görüntüyü PDF'ye Dönüştür – Görüntüyü Yükle

İlk iş olarak OCR motoruna okuyacak bir şey vermeliyiz. `ImageStream.FromFile` yardımcı işlevi dosyayı Aspose'un işleyebileceği bir akıma yükler.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

// 1️⃣ Load the source image you want to turn into a searchable PDF
ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");
```

> **Pro tip:** Görüntü çözünürlüğünüzü 300 dpi veya daha yüksek tutun; düşük çözünürlüklü taramalarda OCR doğruluğu büyük ölçüde düşer.

## Adım 2: Görüntüden Metni Tanı ve OCR Metin Katmanı Ekle

Şimdi OCR motorunu oluşturup metni tanımasını söylüyoruz. Tanıma sonucunu `IncludeTextLayer = true` ayarı olan `PdfSaveOptions` ile eşleştirdiğimizde sihir gerçekleşir. Bu bayrak, Aspose'a çıkarılan karakterleri görünmez bir metin katmanı olarak gömmesini zorlar; bu da PDF'nin aranabilir olmasını sağlar.

```csharp
// 2️⃣ Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// 3️⃣ Set up PDF/A‑2b save options – includes the hidden text layer
PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
{
    PdfCompliance = PdfCompliance.PdfA2b, // ensures PDF/A‑2b compliance
    IncludeTextLayer = true               // this is the key for searchable PDFs
};
```

Neden PDF/A‑2b? Bu, uzun vadeli korunmayı garanti eden bir ISO standardı arşiv formatıdır ve bizim için önemli olan, PDF'nin aranabilir bir metin katmanı içermesini zorlamasıdır. Arşiv uyumluluğuna ihtiyacınız yoksa `PdfCompliance` ayarını tamamen kaldırabilirsiniz, ancak bunu tutmanın bir maliyeti yoktur.

## Adım 3: PDF Baytlarını Dosyaya Yaz – Sonucu Kaydet

Motor hazır ve seçenekler ayarlandığında, tanıma işlemini çalıştırıp Aspose'dan PDF'yi `byte[]` olarak vermesini hemen isteriz. Ardından bu baytları `File.WriteAllBytes` kullanarak diske yazarız. Basit ama güçlü.

```csharp
// 4️⃣ Perform OCR on the image and get the PDF bytes
byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

// 5️⃣ Write the PDF/A‑2b file to the output location
System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
Console.WriteLine("PDF/A‑2b file created – you now have a searchable PDF!");
```

Bu `Console.WriteLine` satırı isteğe bağlıdır, ancak programı bir terminalden çalıştırdığınızda anlık geri bildirim sağlar.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, işte tam, çalıştırmaya hazır program. Yeni bir konsol projesine kopyala‑yapıştır, `YOUR_DIRECTORY` ifadesini gerçek bir yol ile değiştir ve **F5** tuşuna bas.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;
using Aspose.OCR.Output;
using System;

class PdfA2bDemo
{
    static void Main()
    {
        // Step 1: Load the source image
        ImageStream image = ImageStream.FromFile("YOUR_DIRECTORY/input.png");

        // Step 2: Create OCR engine and configure PDF/A‑2b options
        OcrEngine ocrEngine = new OcrEngine();
        PdfSaveOptions pdfSaveOptions = new PdfSaveOptions
        {
            PdfCompliance = PdfCompliance.PdfA2b,
            IncludeTextLayer = true
        };

        // Step 3: Recognize and save as PDF bytes
        byte[] pdfBytes = ocrEngine.Recognize(image).Save(pdfSaveOptions);

        // Step 4: Write the bytes to a searchable PDF file
        System.IO.File.WriteAllBytes("YOUR_DIRECTORY/output.pdf", pdfBytes);
        Console.WriteLine("PDF/A‑2b file created.");
    }
}
```

### Beklenen Çıktı

- Belirttiğiniz klasörde `output.pdf` adlı bir dosya oluşur.  
- Adobe Acrobat Reader veya herhangi bir PDF görüntüleyicide açın ve metni seçmeyi deneyin—kelimeleri kopyalayabiliyorsanız **aranabilir PDF** başarıyla oluşturulmuş demektir.  
- Doğru uyumluluk bayrağını kullandığımız için belge PDF/A‑2b doğrulama araçlarından da geçecektir.

## Yaygın Sorular & Özel Durumlar

**Görüntüm birden fazla sayfa içeriyorsa ne olur?**  
Her sayfayı kendi `ImageStream`'i içinde paketleyip `OcrEngine`'e sırasıyla besleyin. Aspose sayfaları otomatik olarak tek bir PDF'de birleştirir.

**OCR dilini değiştirebilir miyim?**  
Tabii ki. `Recognize` çağrısından önce `ocrEngine.Language = Language.English;` (veya desteklenen herhangi bir dil) olarak ayarlayın.

**Büyük dosyalar için bellek kullanımı nasıl?**  
Gigabayt ölçeğinde taramalar işliyorsanız, tüm `byte[]`'ı bellekte tutmak yerine sonucu doğrudan bir `FileStream`'e akıtmayı düşünün:

```csharp
using (var file = new FileStream("output.pdf", FileMode.Create))
{
    ocrEngine.Recognize(image).Save(pdfSaveOptions, file);
}
```

**Bir lisansa ihtiyacım var mı?**  
Aspose, filigran‑sız bir değerlendirme ile ücretsiz deneme sunar. Üretim kullanımında, değerlendirme bannerını kaldırmak ve tam özellikleri açmak için bir lisans satın alın.

## Daha İyi OCR Doğruluğu İçin İpuçları

- **Görüntüyü ön‑işlemden geçir**: eğikliği düzelt, lekeleri temizle ve kontrastı artır.  
- **Kayıpsız formatlar** kullan: PNG gibi; JPEG sıkıştırma artefaktları motoru yanıltabilir.  
- **Renkli arka planlardan kaçın**; düz beyaz arka plan en iyi sonuçları verir.

## Sonraki Adımlar

Artık **aranabilir PDF** oluşturabildiğinize göre, şunları yapmak isteyebilirsiniz:

- `Directory.GetFiles` kullanarak bir klasördeki görüntüleri **toplu işleyin**.  
- Daha sonra indeksleme için `PdfDocument` API'leriyle **gizli metni çıkarın**.  
- OCR'ı dijital imzalarla **birleştirerek** müdahale tespitli arşivler oluşturun.  

Bunların tümü, ele aldığımız aynı temel desen üzerine kuruludur: yükle, tanı, yapılandır, kaydet.

---

*Tarama arşivlerinizi aranabilir PDF'lere dönüştürmeye hazır mısınız? Kodu alın, görüntülerinize yönlendirin ve Aspose'un ağır işleri halletmesine izin verin. Kodlamanın tadını çıkarın!*

![Aranabilir PDF örneği oluşturma](/images/create-searchable-pdf.png "Bir görüntüden oluşturulan aranabilir PDF'nin illüstrasyonu")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}