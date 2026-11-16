---
category: general
date: 2026-03-05
description: Aspose OCR kullanarak bir JPEG'i aranabilir PDF'ye dönüştürürken PDF'ye
  fontları gömün. JPEG'ten metni tanımayı ve PDF/A‑2b uyumluluğu için fontları gömmeyi
  öğrenin.
draft: false
keywords:
- embed fonts in pdf
- recognize text from jpeg
- how to create searchable pdf
- convert image to searchable pdf
- perform ocr on image
language: tr
og_description: JPEG'i aranabilir bir PDF'ye dönüştürürken PDF'ye yazı tiplerini gömün.
  Bu adım adım kılavuz, JPEG'den metni nasıl tanıyacağınızı ve PDF/A‑2b uyumlu dosyalar
  oluşturacağınızı gösterir.
og_title: PDF'ye Yazı Tipi Göm – JPEG'den Aranabilir PDF'ler Oluştur
tags:
- Aspose OCR
- PDF generation
- C#
- .NET
title: PDF'ye Yazı Tipi Göm – JPEG'den Aranabilir PDF'ler Oluştur
url: /tr/net/ocr-configuration/embed-fonts-in-pdf-make-searchable-pdfs-from-jpeg/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PDF'ye Yazı Tipi Göm – JPEG'den Aranabilir PDF'ler Oluştur

Tarayıcıdan oluşturulan PDF dosyalarına **yazı tiplerini gömmen** gerektiğinde hiç zorlandınız mı? Tek başınıza değilsiniz. Çoğu geliştirici, PDF'nin kendi makinesinde düzgün göründüğünü, ancak başka bir yerde açıldığında eksik metinler gösterdiğini fark eder; çünkü yazı tipleri gömülmemiştir.  

İyi haber? Aspose OCR ile **JPEG'den metin tanıyabilir**, gerekli yazı tiplerini gömebilir ve sadece birkaç satır C# koduyla tam arama yapılabilir bir PDF/A‑2b belgesi oluşturabilirsiniz. Bu öğreticide her adımı—her ayarın neden önemli olduğu, yaygın tuzaklardan nasıl kaçınılacağı ve son PDF'nin nasıl görünmesi gerektiği—adım adım inceleyeceğiz.

Bu rehberin sonunda **görüntüyü aranabilir PDF'ye dönüştürebilecek**, yazı tiplerini doğru şekilde gömebilecek ve **görüntü dosyalarında OCR** işlemini programatik olarak nasıl yapacağınızı anlayacaksınız.

---

## Gerekenler

- **Aspose.OCR for .NET** (en son sürüm, ör. 23.10) – ağır işi yapan kütüphane.
- Geçerli bir **Aspose OCR lisans dosyası** (`Aspose.OCR.lic`). Ücretsiz deneme çalışır, ancak lisanslı sürüm değerlendirme filigranlarını kaldırır.
- Yazılı veya basılı metin içeren bir JPEG resmi (`input.jpg`).
- .NET geliştirme ortamı (Visual Studio, Rider veya C# uzantılı VS Code).

Ek NuGet paketlerine ihtiyaç yok; OCR motoru PDF oluşturma yardımcılarını zaten içinde barındırıyor.

---

## Adım 1: OCR Motorunu Kurun ve Lisansı Uygulayın *(PDF'ye Yazı Tipi Göm)*

Herhangi bir tanıma çalıştırmadan önce bir `OcrEngine` örneği oluşturmalı ve hangi lisansı kullanacağını belirtmelisiniz. Lisans adımını atlamak, motorun değerlendirme modunda çalışmasına neden olur; bu da her sayfaya “Powered by Aspose” üst bilgisini ekler.

```csharp
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Apply your license – replace the path with the actual location of your .lic file
ocrEngine.SetLicense("Aspose.OCR.lic");
```

**Neden önemli:** Lisans sadece filigranları kaldırmakla kalmaz, aynı zamanda daha sonra yazı tiplerini gömmek için ihtiyaç duyacağımız PDF/A uyumluluk seçeneklerini de açar.

---

## Adım 2: İşlemek İstediğiniz JPEG Resmini Yükleyin *(JPEG'den Metin Tanıma)*

OCR motoru, bir `Image` özelliği aracılığıyla `ImageStream` kabul eder. Dönüştürmek istediğiniz JPEG'i bu özelliğe yönlendirin.

```csharp
// Load the source JPEG image
ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");
```

**İpucu:** Resminiz bir akışta (ör. bir API üzerinden yüklenmiş) bulunuyorsa, `FromFile` yerine `ImageStream.FromStream(yourStream)` kullanabilirsiniz.

---

## Adım 3: Aranabilir PDF İçin PDF Kaydetme Seçeneklerini Yapılandırın

Bu, “PDF'ye yazı tipi göm” ihtiyacının kalbidir. `PdfSaveOptions` ile:

1. **PDF/A‑2b** hedefleyin (yaygın kabul gören arşiv standardı).
2. **Kullanılan tüm yazı tiplerini göm** ki PDF her yerde aynı şekilde görüntülensin.
3. **Kayıpsız Flate sıkıştırması** uygulayarak dosya boyutunu makul tutun.
4. Orijinal JPEG'i arka plan katmanı olarak tutun; böylece görsel sadakati korunur.

```csharp
// Set up PDF export options
var pdfSaveOptions = new PdfSaveOptions
{
    // Produce a PDF/A‑2b compliant document
    PdfAStandard = PdfAStandard.PdfA2b,

    // Ensure every font used by the OCR text is embedded
    EmbedFonts = true,

    // Use lossless compression for the text and graphics streams
    Compression = PdfCompression.Flate,

    // Keep the original image behind the OCR layer (makes the PDF searchable)
    RenderOriginalImage = true
};
```

**Bu ayarlar neden?**  
- **PdfAStandard.PdfA2b** uzun vadeli koruma garantiler ve yazı tiplerinin gömülmesini zorunlu kılar.  
- **EmbedFonts = true** anahtar kelime hedefini karşılayan açık bayraktır.  
- **Compression.Flate** kaliteyi kaybetmeden boyutu azaltır.  
- **RenderOriginalImage** taranmış sayfanın görsel görünümünü korurken gizli OCR katmanı aranabilir metin sağlar.

---

## Adım 4: Görüntü Üzerinde OCR Tanımasını Çalıştırın *(Görüntüde OCR Yap)*

Her şey hazır olduğunda tanıma işlemini başlatın. Motor JPEG'i analiz eder, karakterleri çıkarır ve dahili olarak bir metin katmanı oluşturur.

```csharp
// Execute OCR – this populates the internal text layer
ocrEngine.Recognize();
```

**Sık sorulan soru:** *Dil veya sözlük belirtmem gerekiyor mu?*  
Belgeniz İngilizce değilse, `ocrEngine.Language = OcrLanguage.French;` (veya desteklenen başka bir dil) satırını `Recognize()` çağrısından önce ekleyin. Varsayılan dil İngilizcedir.

---

## Adım 5: Sonucu Yazı Tipi Gömülü Aranabilir PDF Olarak Kaydedin

Son olarak sonucu diske yazın. `Save` yöntemi hedef yolu ve daha önce tanımladığımız `PdfSaveOptions` nesnesini alır.

```csharp
// Save the searchable PDF with embedded fonts
ocrEngine.Save(@"C:\MyImages\output.pdf", pdfSaveOptions);
```

`output.pdf` dosyasını Adobe Acrobat ya da herhangi bir PDF görüntüleyicide açtığınızda şunları yapabilmelisiniz:

- **Arama** kutusuna, orijinal JPEG'de bulunan herhangi bir kelimeyi yazabilmek.  
- **Yazı tipi eksik uyarısı** almamak (`EmbedFonts = true` sayesinde).  
- Dosyanın **PDF/A‑2b** standardına uygun olduğunu doğrulamak (Dosya → Özellikler → PDF/A).

---

## Tam Çalışan Örnek

Aşağıda, doğrudan çalıştırabileceğiniz tam program yer alıyor. Yeni bir Console App projesine kopyalayıp yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;
using Aspose.OCR.Saving;

namespace ImageToSearchablePdf
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine and apply license
            var ocrEngine = new OcrEngine();
            ocrEngine.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

            // 2️⃣ Load JPEG image
            ocrEngine.Image = ImageStream.FromFile(@"C:\MyImages\input.jpg");

            // 3️⃣ Configure PDF save options (embed fonts, PDF/A‑2b, etc.)
            var pdfSaveOptions = new PdfSaveOptions
            {
                PdfAStandard = PdfAStandard.PdfA2b,
                EmbedFonts = true,
                Compression = PdfCompression.Flate,
                RenderOriginalImage = true
            };

            // 4️⃣ Run OCR recognition
            ocrEngine.Recognize();

            // 5️⃣ Save searchable PDF with embedded fonts
            string outputPath = @"C:\MyImages\output.pdf";
            ocrEngine.Save(outputPath, pdfSaveOptions);

            Console.WriteLine($"✅ PDF created at: {outputPath}");
            Console.WriteLine("Open it in any PDF viewer and try searching for words from the original JPEG.");
        }
    }
}
```

**Beklenen çıktı:**  
Konsol bir başarı mesajı verir ve `output.pdf` hedef klasörde oluşur. PDF'yi açıp görüntüleyicinin arama kutusunu kullandığınızda `input.jpg` içinde bulunan herhangi bir kelime bulunabilmelidir.

---

## Sık Sorulan Sorular & Kenar Durumlar

### 1. “JPEG'im çok sayfalı bir TIFF ise ne olur?”
Aspose OCR her sayfayı ayrı ayrı işler. TIFF'i bir dizi JPEG'e dönüştürün (veya her sayfa için `ImageStream.FromFile` kullanın) ve OCR sürecini döngü içinde çalıştırarak aynı PDF'ye ekleyin; aynı `OcrEngine` örneğini yeniden kullanın.

### 2. “DPI veya görüntü ön işleme kontrol edebilir miyim?”
Evet. `Recognize()` çağrısından önce görüntü çözünürlüğünü ayarlayabilirsiniz:

```csharp
ocrEngine.Image.DpiX = 300;
ocrEngine.Image.DpiY = 300;
ocrEngine.Image.AutoRotate = true; // auto‑rotate for landscape scans
```

Daha yüksek DPI, özellikle küçük yazı tiplerinde tanıma doğruluğunu artırır.

### 3. “PDF'im Adobe Reader’da hâlâ eksik yazı tipleri gösteriyor—neyin hatası?”
**PDF/A‑2b** hedeflediğinizden ve `EmbedFonts` değerinin `true` olduğundan emin olun. `PdfAStandard` değerini **None** olarak değiştirirseniz PDF/A doğrulama adımı atlanır ve bazı yazı tipleri gömülmemiş kalabilir.

### 4. “OCR katmanı mobil cihazlarda aranabilir mi?”
Kesinlikle. Gizli metin katmanı PDF spesifikasyonunun bir parçasıdır; iOS Files, Android PDF Viewer gibi metin çıkarımını destekleyen tüm PDF görüntüleyiciler arama yapabilir.

### 5. “Sağ‑dan‑soluya diller (ör. Arapça) nasıl ele alınır?”
Tanımadan önce dili ayarlayın:

```csharp
ocrEngine.Language = OcrLanguage.Arabic;
ocrEngine.Recognize();
```

Aspose OCR, `EmbedFonts` true olduğunda metin yönünü otomatik değiştirir ve uygun yazı tiplerini gömer.

---

## Pro İpuçları & Yaygın Tuzaklar

- **Pro ipucu:** Kaynak görüntüleriniz renkli fotoğraf ise, önce gri tonlamaya dönüştürmeyi düşünün (`ocrEngine.Image.ConvertToGrayscale();`). Bu, dosya boyutunu azaltırken OCR doğruluğunu etkilemez.  
- **Dikkat:** Ücretsiz deneme lisansı büyük bir görüntüyle kullanıldığında OCR metni kesilebilir. Üretim ortamları için tam lisansa geçin.  
- **Performans ipucu:** Birden fazla görüntüde aynı `OcrEngine` örneğini yeniden kullanmak, OCR DLL'lerinin tekrar yüklenmesinden kaynaklanan yükü azaltır.  
- **Güvenlik notu:** PDF/A‑2b dosyaları tasarım gereği **salt okunur** olduğundan, istem dışı betik enjeksiyonunu önler; bu da uyumluluk gerektiren ortamlar için ekstra bir avantajdır.

---

## Sonuç

**PDF'ye yazı tipi gömme**, **JPEG'den metin tanıma** ve **aranabilir PDF/A‑2b** standardına uygun bir PDF üretme sürecinin tamamını ele aldık. Özetle:

1. `OcrEngine`'i başlatın ve lisansınızı uygulayın.  
2. JPEG görüntüyü yükleyin.  
3. `PdfSaveOptions`'ı yapılandırın (yazı tiplerini göm, PDF/A‑2b, sıkıştırma).  
4. `Recognize()`'ı çalıştırın.  
5. Ayarladığınız seçeneklerle kaydedin.

Artık bu akışı web servislerine, masaüstü yardımcı programlarına veya toplu işlere entegre ederek **görüntüyü anında aranabilir PDF'ye dönüştürebilirsiniz**. Bir sonraki adımda, çok sayfalı PDF'lerden veya zaten PDF olarak üretilen dosyalardan **aranabilir PDF** oluşturmayı keşfedebilirsiniz.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}