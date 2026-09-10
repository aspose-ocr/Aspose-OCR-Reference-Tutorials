---
category: general
date: 2026-01-04
description: Tarayıcıdan gelen PDF'den hızlıca aranabilir PDF oluşturun. Tarayıcı
  PDF'sini nasıl dönüştüreceğinizi, PDF'ye OCR eklemeyi ve Aspose OCR ile C#’ta görüntü
  kalitesini nasıl ayarlayacağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- add ocr to pdf
- adjust image quality
- how to use ocr
language: tr
og_description: Create searchable PDF from a scanned PDF quickly. Follow this step‑by‑step
  guide to convert scanned PDF, add OCR to PDF, and adjust image quality.
og_title: Aspose OCR ile Tarama Dosyalarından Aranabilir PDF Oluştur
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCR Kullanarak Tarama Dosyalarından Aranabilir PDF Oluşturma
url: /tr/net/ocr-optimization/create-searchable-pdf-from-scanned-files-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR Kullanarak Tarama Dosyalarından Aranabilir PDF Oluşturma

Hiç **aranabilir PDF** oluşturmanız gereken bir yığın taranmış belgeyle karşılaştınız mı ve nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici belge‑yönetim hatları oluştururken bu engelle karşılaşıyor. İyi haber? Aspose OCR ile **taranmış PDF**'yi **dönüştürebilir**, OCR ekleyebilir ve sadece birkaç C# satırıyla görüntü kalitesini ince ayar yapabilirsiniz.

Bu öğreticide, taranmış bir PDF'yi yüklemekten tamamen aranabilir bir sürüm olarak kaydetmeye kadar tüm süreci adım adım inceleyeceğiz. Sonunda **OCR'ı Aspose ile nasıl kullanacağınızı**, her ayarın neden önemli olduğunu ve işler planlandığı gibi gitmediğinde neyi ayarlamanız gerektiğini tam olarak öğreneceksiniz. Belirsiz referanslar yok—bugün projenize ekleyebileceğiniz tam, çalıştırılabilir bir örnek.

## Ön Koşullar

İlerlemeye başlamadan önce şunların yüklü olduğundan emin olun:

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework ile de çalışır)
- Geçerli bir Aspose OCR lisansı (ücretsiz deneme sürümü test için yeterlidir)
- `input.pdf` adlı bir giriş PDF'i, kontrol ettiğiniz bir klasöre yerleştirilmiş
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir C# editörü

Hepsi bu kadar. Bu maddelerden biri size yabancı geliyorsa, eksik parçayı kurun—başka bir şeye ihtiyacınız yok.

## Adım 1: OCR Motorunu Başlatın ve Taranmış PDF'yi Yükleyin  
**(Bu, PDF'ye **ilk kez OCR eklediğimiz** yerdir.)**

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Load the scanned PDF from disk
ocrEngine.LoadPdf(@"C:\Docs\input.pdf");
```

*Bu adım neden?*  
`OcrEngine`, Aspose OCR'ın kalbidir. PDF'i yüklemek, motorun daha sonra analiz edeceği raster görüntülerini nereden bulacağını belirtir. Bunu atlamanız, dönüştürülecek bir şey olmamasına ve sonraki adımların bir istisna fırlatmasına yol açar.

> **İpucu:** PDF'iniz şifre korumalıysa, çalışma zamanı hatasını önlemek için `ocrEngine.LoadPdf(path, password)` kullanın.

## Adım 2: Birincil ve Ek Dilleri Ayarlayın  
**(PDF'i İngilizce, Fransızca ve Almanca **dönüştüreceğiz**.)**

```csharp
// Primary language – the most common language in the document
ocrEngine.Config.Language = Language.English;

// Add extra languages if the document contains multilingual text
ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };
```

*Dil neden önemli?*  
OCR doğruluğu, beklediği karakter setine bağlıdır. İngilizceyi birincil dil olarak belirleyip Fransızca/Almanca ekleyerek, motor aksanlı karakterleri ve özel glifleri doğru yorumlayabilir. Bunu atlamak genellikle bozuk metinlere yol açar.

## Adım 3: Görüntü Kalitesini Ayarlayın – PDF Çıktısını İnce Ayar Yapın  
**(Burada **görüntü kalitesini** dosya boyutu ve okunabilirlik arasında dengelemek için ayarlıyoruz.)**

```csharp
PdfSaveOptions pdfOptions = new PdfSaveOptions
{
    ImageQuality = 90,          // JPEG quality for embedded images (0‑100)
    Compress = true,            // Enable PDF compression to shrink file size
    PreserveOriginalLayout = true // Keep the scanned layout intact
};
```

*`ImageQuality` neden ayarlanmalı?*  
Daha yüksek bir değer (90‑100) keskinliği korur, bu da OCR doğruluğu için kritiktir, ancak dosya boyutunu da şişirir. Milyonlarca sayfayı arşivliyorsanız, okunabilirliği çok fazla kaybetmeden daha ince bir PDF elde etmek için 70‑80 aralığına düşürün.

## Adım 4: Sonucu Aranabilir PDF Olarak Kaydedin  
**(Şimdi nihayet **aranabilir PDF** oluşturuyoruz ve indeksleyebileceksiniz.)**

```csharp
// Export the OCR result as a searchable PDF
ocrEngine.SaveAsSearchablePdf(@"C:\Docs\output.pdf", pdfOptions);

// Let the user know we’re done
Console.WriteLine("Searchable PDF created at C:\\Docs\\output.pdf");
```

*Aslında ne oluyor?*  
Aspose OCR, her sayfadan bir metin katmanı çıkarır ve bunu orijinal görüntünün arkasına gömer. PDF görsel olarak aynı kalır, ancak artık metni seçebilir, kopyalayabilir ve arayabilirsiniz—sonraki iş akışları için büyük bir avantaj.

## Adım 5: Çıktıyı Doğrulayın (Opsiyonel ama Tavsiye Edilir)  
Her şeyin sorunsuz çalıştığını varsaymak kolaydır, ancak hızlı bir kontrol ileride baş ağrısını önler.

```csharp
using System.Diagnostics;

// Open the generated PDF automatically (Windows only)
Process.Start(new ProcessStartInfo
{
    FileName = @"C:\Docs\output.pdf",
    UseShellExecute = true
});
```

Dosyayı açın, bir kelimeyi seçmeyi deneyin veya `Ctrl+F` tuşlarına basıp orijinal taramada mevcut bir ifadeyi yazın. Metin seçilebiliyorsa, **aranabilir PDF** oluşturmayı başarıyla tamamlamışsınız demektir.

## Yaygın Kenar Durumları ve Çözüm Yolları  

| Durum | Neden Oluşur | Hızlı Çözüm |
|-----------|----------------|-----------|
| **Karışık çözünürlüklü sayfalar** (bazıları 150 dpi, diğerleri 300 dpi) | OCR kalitesi sayfa bazında değişir, bu da tutarsız arama sonuçlarına yol açar. | `ocrEngine.Config.Dpi = 300;` kodunu yüklemeden önce ayarlayarak yukarı örnekleme yapın veya `ImageProcessor` ile DPI'yi normalleştirin. |
| **Şifreli PDF** | Aspose OCR şifre olmadan okuyamaz. | Daha önce gösterildiği gibi şifreyi `LoadPdf` metoduna iletin. |
| **Büyük PDF'ler (>500 MB)** | Bellek tüketimi artar, `OutOfMemoryException` oluşur. | Belgeyi bölümlere ayırarak işleyin: `ocrEngine.SplitPdfIntoPages();` ardından her sayfayı ayrı ayrı OCR'layıp sonuçları birleştirin. |
| **Latin dışı karakterler** (ör. Kiril) | Dil eklenmediği için karakterler “?” olur. | `AdditionalLanguages` koleksiyonuna `Language.Russian` (veya gerekli dili) ekleyin. |
| **Çok düşük görüntü kalitesi** | Metin bulanıklaşır, OCR başarısız olur. | `ImageQuality` değerini artırın veya `pdfOptions.Dpi = 300;` kullanarak daha yüksek çözünürlüklü görüntüler gömün. |

## Tam, Hazır‑Kod Örneği  

Aşağıda yeni bir konsol uygulamasına kopyalayıp yapıştırabileceğiniz eksiksiz program yer alıyor. Tüm adımları, hata yönetimini ve açıklamaları içeriyor.

```csharp
using System;
using System.Diagnostics;
using Aspose.OCR;
using Aspose.OCR.Models;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Paths – adjust to your environment
            string inputPath = @"C:\Docs\input.pdf";
            string outputPath = @"C:\Docs\output.pdf";

            try
            {
                // 1️⃣ Initialize OCR engine and load scanned PDF
                OcrEngine ocrEngine = new OcrEngine();
                ocrEngine.LoadPdf(inputPath);

                // 2️⃣ Configure languages (primary + additional)
                ocrEngine.Config.Language = Language.English;
                ocrEngine.Config.AdditionalLanguages = new[] { Language.French, Language.German };

                // 3️⃣ Set PDF save options – adjust image quality as needed
                PdfSaveOptions pdfOptions = new PdfSaveOptions
                {
                    ImageQuality = 90,
                    Compress = true,
                    PreserveOriginalLayout = true
                };

                // 4️⃣ Save as searchable PDF
                ocrEngine.SaveAsSearchablePdf(outputPath, pdfOptions);
                Console.WriteLine($"✅ Searchable PDF created at {outputPath}");

                // 5️⃣ Optional: open the file to verify
                Process.Start(new ProcessStartInfo
                {
                    FileName = outputPath,
                    UseShellExecute = true
                });
            }
            catch (Exception ex)
            {
                // Friendly error message – helps during debugging
                Console.WriteLine($"❌ Oops! Something went wrong: {ex.Message}");
                // For real‑world apps, consider logging the stack trace
            }
        }
    }
}
```

**Beklenen çıktı:**  
```
✅ Searchable PDF created at C:\Docs\output.pdf
```

`output.pdf` dosyasını açtığınızda, orijinal taramada bulunan herhangi bir metni seçebilmeli ve arayabilmelisiniz.

---

## Sıkça Sorulan Sorular (SSS)

**S: Hem taranmış görüntüler hem de yerel metin içeren PDF'lerle çalışır mı?**  
C: Kesinlikle. Aspose OCR yalnızca gerektiği yerde gizli bir metin katmanı ekler, mevcut metni olduğu gibi bırakır.

**S: PDF klasörünü toplu iş olarak işleyebilir miyim?**  
C: Evet. Yukarıdaki kodu `foreach (var file in Directory.GetFiles(folder, "*.pdf"))` döngüsüyle sarın ve çıktı yolunu buna göre ayarlayın.

**S: Son PDF boyutunu daha da küçültmenin bir yolu var mı?**  
C: `ImageQuality` değerini 70‑80 aralığına düşürün, `Compress` özelliğini etkinleştirin veya `pdfOptions.Dpi = 150` ile gömülen görüntüleri aşağı örnekleyin.

**S: PDF oluşturmadan OCR metnini çıkarmak mümkün mü?**  
C: PDF'yi yükledikten sonra `ocrEngine.ExtractText();` metodunu çağırın. Bu, saklayabileceğiniz veya indeksleyebileceğiniz düz metin dizesi döndürür.

---

## Özet  

Aspose ile **OCR'ı nasıl kullanacağınızı**, **taranmış PDF'yi nasıl oluşturacağınızı**, **PDF'ye OCR eklemeyi** ve **optimum sonuçlar için görüntü kalitesini nasıl ayarlayacağınızı** ele aldık. Tam kod örneği çalıştırılmaya hazır ve sorun giderme tablosu beklenmedik durumlarda size yol gösterecek.

Sıradaki adım? Şunları deneyin:

- Çok dilli arşivler için farklı dil paketleri
- `ImageProcessor` ile özel görüntü ön‑işleme (eğikliği düzeltme, lekeleri temizleme)
- Aranabilir PDF'yi SharePoint veya ElasticSearch hattına entegre etme

Herhangi bir sorunla karşılaşırsanız veya akıllı bir ayar keşfettiyseniz yorum bırakın. İyi kodlamalar ve anında aranabilir PDF'lerin tadını çıkarın!

![Create searchable PDF flowchart showing OCR engine → language config → PDF save options → searchable PDF output](create-searchable-pdf-flow.png)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}