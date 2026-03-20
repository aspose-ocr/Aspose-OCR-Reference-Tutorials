---
category: general
date: 2026-03-20
description: 'Aranabilir PDF''yi hızlıca oluşturun: görüntüyü PDF''ye dönüştürün,
  görüntüden metni çıkarın ve tam aranabilirlik için gizli bir metin katmanı ekleyin.'
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- extract text from image
- pdf with hidden text
- scan image to pdf
language: tr
og_description: C#'ta bir görüntüyü PDF'ye dönüştürerek, metni çıkararak ve anında
  arama için gizli bir katman ekleyerek aranabilir PDF oluşturun.
og_title: Görüntüden Aranabilir PDF Oluşturma – Tam C# Öğreticisi
tags:
- Aspose
- C#
- OCR
- PDF generation
title: C#'ta Görüntüden Aranabilir PDF Oluşturma – Adım Adım Rehber
url: /tr/net/text-recognition/create-searchable-pdf-from-image-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Aranabilir PDF Oluşturma C# – Tam Kılavuz

Hiç taranmış bir faturadan **aranabilir PDF** oluşturmanız gerekti ama her şeyi el ile yazmak istemediniz mi? Tek başınıza değilsiniz. Birçok ofis iş akışında, bir bitmap taramayı gerçekten arama yapabileceğiniz bir PDF’ye dönüştürmek günlük bir sıkıntıdır. İyi haber? Birkaç satır C# ve Aspose’un OCR & PDF kütüphaneleriyle tüm süreci otomatikleştirebilirsiniz—manuel kopyala‑yapıştırmaya gerek kalmaz.

Bu öğreticide **görüntüyü PDF’ye dönüştürme**, o görüntüden metni çıkarma ve ardından metni görünmez bir katman olarak ekleyerek son dosyanın yerel bir PDF gibi davranmasını sağlayacağız. Sonunda, bir **gizli metinli PDF** oluşturmak için hazır bir yönteme sahip olacaksınız; bu yöntem, fatura, sözleşme ya da makbuz gibi herhangi bir taranmış belge için çalışır.

## Gereksinimler

- .NET 6.0 veya üzeri (kod `using var` ifadelerini kullandığı için yeni bir SDK hayatı kolaylaştırır)
- Aspose.OCR ve Aspose.Pdf NuGet paketleri (`Install-Package Aspose.OCR` ve `Install-Package Aspose.Pdf`)
- Metni indekslemek istediğiniz örnek bir görüntü dosyası (PNG, JPG veya TIFF)
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir IDE

> **Pro tip:** Çok sayfalı taramalarla çalışıyorsanız, sadece her görüntü üzerinde döngü yapın ve adımları tekrarlayın – aynı mantık geçerlidir.

---

## 1. Adım – OCR Motorunu Başlatma (Görüntüden Metin Çıkarma)

Aranabilir metni gömmeden önce, karakterleri resimden okumamız gerekir. Aspose’un `OcrEngine`i bu işi yapar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine and tell it which language to look for.
// English works for most invoices, but you can set Language.French, etc.
using var ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Neden önemli:** Motoru doğru dil ile başlatmak doğruluğu büyük ölçüde artırır. Bunu atlayarsanız OCR sayıları yanlış tanıyabilir—finansal belgelerde kesinlikle kaçınmak istediğiniz bir durumdur.

---

## 2. Adım – Taradığınız Görüntüyü Yükleme (Görüntüyü PDF’ye Dönüştürme)

Şimdi bitmap’i belleğe alıyoruz. Aspose doğrudan `System.Drawing.Image` ile çalışır, bu yüzden .NET’in desteklediği herhangi bir format yeterlidir.

```csharp
using System.Drawing;

// Replace the path with the location of your scanned file.
var inputImage = Image.FromFile(@"C:\Docs\invoice.png");
```

Eğer zaten çok sayfalı bir TIFF üreten bir **görüntüyü PDF’ye tarama** iş akışınız varsa, sadece dosya uzantısını değiştirin ve her sayfa için yükleme adımını tekrarlayın.

---

## 3. Adım – OCR’u Çalıştırma ve Tanınan Metni Yakalama

Görüntü hazır olduğunda OCR motorundan sihrini yapmasını istiyoruz.

```csharp
// Perform OCR – the result contains the raw text and confidence scores.
var ocrResult = ocrEngine.Recognize(inputImage);

// For debugging, you might want to see what was read.
Console.WriteLine("OCR Output:");
Console.WriteLine(ocrResult.Text);
```

**Köşe durumu:** Görüntü düşük çözünürlüklü (< 300 dpi) ise güven puanı düşer. Motoru beslemeden önce ölçeklendirmeyi artırmayı ya da daha yüksek DPI’da yeniden taramayı düşünün.

---

## 4. Adım – PDF Oluşturma ve Orijinal Görüntüyü Arka Plan Olarak Yerleştirme

Bir **gizli metinli PDF** hâlâ taramanın görsel temsilini gerektirir. Görüntüyü sayfa arka planı olarak ekleyeceğiz.

```csharp
using Aspose.Pdf;

// Start a fresh PDF document.
var pdfDocument = new Document();

// Add a new page.
var pdfPage = pdfDocument.Pages.Add();

// Insert the image; it will fill the page by default.
pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
{
    ImageInfo = new ImageInfo(@"C:\Docs\invoice.png")
});
```

**Neden görüntüyü arka plan olarak kullanıyoruz:** Kullanıcılar hâlâ orijinal taramayı, imzaları ve damgaları koruyarak görebilir; gizli metin katmanı ise arama yeteneği sağlar.

---

## 5. Adım – OCR Metnini Görünmez Bir Katman Olarak Üst Üste Bindirme (PDF with Hidden Text)

İşte kritik kısım: Görüntünün üstüne `TextFragment` ekliyoruz ancak bunu görünmez olarak ayarlıyoruz. Aspose.Pdf bunu kolaylaştırır.

```csharp
using Aspose.Pdf.Text;

// Create a text fragment from the OCR result.
var searchableText = new TextFragment(ocrResult.Text)
{
    // Position (0,0) aligns with the bottom‑left of the page.
    Position = new Position(0, 0),

    // Make the text invisible – it still participates in search.
    TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
};

// Add the invisible text to the same page.
pdfPage.Paragraphs.Add(searchableText);
```

**Açıklama:** Küçük bir font boyutu ayarlayıp parçayı gizli işaretlemek, görsel çıktıyı temiz tutarken PDF’nin metin katmanının OCR çıktısını içermesini sağlar. Arama motorları ve PDF okuyucular bunu indeksler.

---

## 6. Adım – Aranabilir PDF’yi Kaydetme

Son olarak belgeyi diske yazıyoruz.

```csharp
// Choose a destination path.
string outputPath = @"C:\Docs\invoice_searchable.pdf";

// Save the PDF. The file now contains both the image and searchable text.
pdfDocument.Save(outputPath);

Console.WriteLine($"Searchable PDF created at: {outputPath}");
```

Oluşan dosyayı Adobe Reader’da açın, **Ctrl + F** tuşlarına basın, faturada gördüğünüz bir kelimeyi yazın ve vurgulanan sonucu görün – metin hiç görünür olmamıştı bile.

---

## Tam Çalışan Örnek (Tüm Adımlar Birlikte)

Aşağıda bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz tam program yer alıyor. NuGet paketleri yüklü ve dosya yolları doğru olduğu sürece olduğu gibi derlenip çalışır.

```csharp
// ------------------------------------------------------------
// Create Searchable PDF from Image – Complete C# Example
// ------------------------------------------------------------
using System;
using System.Drawing;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.Pdf;
using Aspose.Pdf.Text;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        using var ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load scanned image
        var inputImagePath = @"C:\Docs\invoice.png";
        var inputImage = Image.FromFile(inputImagePath);

        // 3️⃣ Perform OCR
        var ocrResult = ocrEngine.Recognize(inputImage);
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);

        // 4️⃣ Create PDF and add image as background
        var pdfDocument = new Document();
        var pdfPage = pdfDocument.Pages.Add();
        pdfPage.Paragraphs.Add(new Aspose.Pdf.Image
        {
            ImageInfo = new ImageInfo(inputImagePath)
        });

        // 5️⃣ Add invisible searchable text layer
        var searchableText = new TextFragment(ocrResult.Text)
        {
            Position = new Position(0, 0),
            TextState = { Font = FontRepository.FindFont("Arial"), FontSize = 0.1f, IsHidden = true }
        };
        pdfPage.Paragraphs.Add(searchableText);

        // 6️⃣ Save the searchable PDF
        var outputPath = @"C:\Docs\invoice_searchable.pdf";
        pdfDocument.Save(outputPath);
        Console.WriteLine($"✅ Searchable PDF saved to: {outputPath}");
    }
}
```

**Beklenen sonuç:**  
- `invoice_searchable.pdf` `invoice.png` ile tamamen aynı görünüme sahiptir.  
- Metin araması, orijinal taramada yer alan herhangi bir kelime için çalışır.  
- Dosya boyutu sadece hafifçe artar (gizli metin birkaç kilobayt ekler).

---

## Sık Sorulan Sorular & Köşe Durumları

### Tek bir PDF içinde birden fazla sayfa işleyebilir miyim?
Kesinlikle. OCR‑ve‑PDF mantığını `foreach (string imagePath in imageFiles)` döngüsü içinde sarın, her yineleme için yeni bir `Page` oluşturun. Gizli metin katmanı her sayfaya eklenir, böylece arama tüm belge boyunca çalışır.

### Belgem birden fazla dil içeriyorsa ne yapmalıyım?
`ocrEngine.Language` değerini `Language.Multilingual` olarak ayarlayın ya da her dil segmenti için ayrı motorlar oluşturun. Aspose karışık‑dil sonuçları döndürür; bu çıktıyı aynı PDF sayfasına besleyebilirsiniz.

### DPI’yı ya da görüntü ölçeklendirmesini nasıl kontrol ederim?
Görüntüyü PDF’ye eklemeden önce `System.Drawing` ile yeniden boyutlandırabilirsiniz:

```csharp
var resized = new Bitmap(inputImage, new Size(1240, 1754)); // A4 at 150 dpi
```

Ardından yeniden boyutlandırılmış `resized` nesnesini PDF görüntü yapıcısına geçirin.

### Gizli metin tüm görüntüleyicilerde gerçekten görünmez mi?
Çoğu modern görüntüleyici `IsHidden` bayrağını saygı gösterir. Eğer bir görüntüleyici hâlâ küçük metni gösteriyorsa, font boyutunu daha da küçültün (ör. `0.01f`) ya da `TextState.FillColor = Color.Transparent` ile tamamen şeffaf yapın.

### Güvenlik hakkında ne söyleyebilirsiniz—PDF’i şifre korumalı yapabilir miyim?
Evet. İçeriği eklemeyi bitirdikten sonra şu kodu çağırın:

```csharp
pdfDocument.Encrypt("ownerPwd", "userPwd", EncryptionAlgorithms.AES256);
```

Artık aranabilir PDF, organizasyonunuzun gizlilik politikalarına da uyar.

---

## Üretim‑Hazır Uygulamalar İçin İpuçları

- **Toplu işleme:** Büyük görüntü setleri için `Parallel.ForEach` kullanın, ancak `OcrEngine` örneklerinin thread‑unsafe olduğuna dikkat edin—her iş parçacığı için bir tane oluşturun.  
- **Hata yönetimi:** OCR çağrılarını try/catch ile sarın; `ocrResult.IsRecognized` değerini kontrol ederek başarısız sayfaları atlayın.  
- **Günlükleme:** `ocrResult.Confidence` değerlerini kaydedin; düşük güven puanı görüntü ön‑işleme (düzeltme, lekesizleştirme) ihtiyacını gösterebilir.  
- **Performans:** Tüm sayfalar için aynı `Document` nesnesini yeniden kullanın, böylece dosyaları tekrar tekrar açıp kapatmazsınız.  
- **Test:** Aranabilir PDF’nin çıkarılan metnini (`pdfDocument.Pages[1].ExtractText()`) OCR çıktısıyla karşılaştırın; kesinti olmadığından emin olun.

---

## Sonuç

C# kullanarak düz görüntülerden **aranabilir PDF** dosyaları oluşturmayı size gösterdik. Metni Aspose.OCR ile çıkarıp PDF sayfasına görünmez bir katman olarak ekleyip sonucu kaydederek, orijinal taramanın tam aynı görünümüne sahip ama yerel bir PDF gibi davranan bir belge elde edersiniz. Bu teknik klasik **görüntüyü PDF’ye dönüştürme** iş akışını kapsar, bir **gizli metinli PDF** ekler ve **görüntüyü PDF’ye tarama** ihtiyacını gerçek bir arama yeteneğiyle çözer.

Bir sonraki adıma hazır mısınız? Kodu bir klasördeki makbuzları toplu işlemek için genişletin ya da anlık olarak aranabilir PDF döndüren bir web API’sine entegre edin. Farklı fontlarla denemeler yapabilir, meta veri ekleyebilir ya da denetim izleri için OCR güven puanlarını PDF açıklamaları olarak gömebilirsiniz.

Bu kılavuzu faydalı bulduysanız bir yıldız bırakın, ekip arkadaşlarınızla paylaşın ya da kendi ayarlamalarınızı yorum olarak ekleyin. Mutlu kodlamalar ve PDF’leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}