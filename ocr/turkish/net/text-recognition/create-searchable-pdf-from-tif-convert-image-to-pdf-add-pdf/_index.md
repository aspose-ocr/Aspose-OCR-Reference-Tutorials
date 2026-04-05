---
category: general
date: 2026-04-04
description: C#'ta TIF görüntüsünden aranabilir PDF oluşturun – görüntüyü PDF'ye nasıl
  dönüştüreceğinizi, PDF meta verilerini nasıl ekleyeceğinizi öğrenin ve Aspose.OCR
  kullanarak aranabilir bir belge oluşturun.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- add metadata to pdf
- add pdf metadata
- create pdf from tif
language: tr
og_description: C# ile bir TIF dosyasından aranabilir PDF oluşturun. Görüntüyü PDF’ye
  dönüştürün, PDF meta verilerini ekleyin ve Aspose.OCR kullanarak aranabilir bir
  belge üretin.
og_title: TIF'ten Aranabilir PDF Oluştur – Adım Adım Kılavuz
tags:
- Aspose.OCR
- C#
- PDF generation
title: TIF'ten Aranabilir PDF Oluştur – Görüntüyü PDF'ye Dönüştür, PDF Meta Verilerini
  Ekle
url: /tr/net/text-recognition/create-searchable-pdf-from-tif-convert-image-to-pdf-add-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# TIF'ten Aranabilir PDF Oluşturma – Tam C# Kılavuzu

Tarayıcıdan alınmış bir faturadan **aranabilir PDF** oluşturmanız gerektiğinde, metnin aranabilir kalmasını ve dosya meta verilerinin düzenli olmasını nasıl sağlayacağınızı hiç merak ettiniz mi? Yalnız değilsiniz. Birçok otomasyon projesinde PDF'in hem makine‑okunabilir hem de başlık, yazar ve güven eşiği gibi bilgilerle düzgün bir şekilde etiketlenmiş olması gerekir.  

Bu rehberde **görüntüyü PDF'e dönüştüren**, **PDF meta verilerini ekleyen** ve düşük‑güvenilirlikli OCR sonuçlarını filtreleyen eksiksiz bir çözümü adım adım inceleyeceğiz; tüm bunlar Aspose.OCR kütüphanesi ile yapılacak. Sonunda, .NET projenize kolayca ekleyebileceğiniz bir kod parçacığı ve kenar durumlarıyla başa çıkmak için birkaç ipucu elde edeceksiniz.

## Önkoşullar

- .NET 6.0 veya daha yeni bir sürüm (kod .NET Framework 4.6+ üzerinde de çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- Aranabilir PDF'e dönüştürmek istediğiniz bir TIF görüntüsü (ör. `input.tif`)  
- C# ve Visual Studio (veya tercih ettiğiniz IDE) konusunda temel bilgi

Başka bir dış hizmete ihtiyaç yok – tüm süreç yerel olarak çalışır.

## Adım 1 – OCR Motorunu Kurun (Aranabilir PDF Çekirdeği)

İlk olarak, hangi dili tanıyacağını bilen bir `OcrEngine` örneğine ihtiyacımız var. Çoğu iş senaryosunda İngilizce yeterli olur, ancak `Language.English` yerine desteklenen başka bir dili de kullanabilirsiniz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Pdf;   // PDF‑related extensions

// Initialize OCR engine with English language
OcrEngine ocrEngine = new OcrEngine
{
    Language = Language.English
};
```

**Neden önemli:** OCR motoru, raster pikselleri Unicode metne dönüştürme işini yapar. Dili doğru ayarlamak doğruluğu artırır ve daha sonra filtrelenecek düşük‑güvenilir kelime sayısını azaltır.

> **Pro ipucu:** Çok dilli belgeler işliyorsanız, birden fazla motor örneği oluşturun veya `Language.Multilingual` kullanarak Aspose'un dil algılamasını otomatik yapmasına izin verin.

## Adım 2 – TIF Görüntüsünü Yükleyin (TIF'ten PDF Oluşturma)

Şimdi motoru kaynak dosyaya yönlendiriyoruz. `ImageStream.FromFile` yardımcı yöntemi, OCR motorunun tüketebileceği bir akıma görüntüyü okur.

```csharp
// Load the TIF image you want to make searchable
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.tif");
```

Şunu düşünebilirsiniz: *“JPEG ya da PNG besleyebilir miyim?”* Kesinlikle—Aspose.OCR çoğu raster formatı destekler. Sadece dosya uzantısını değiştirin, sorun yok.

## Adım 3 – PDF Seçeneklerini Yapılandırın (PDF'e Meta Veri Ekleme)

Dönüştürmeden önce bir `PdfOptions` nesnesi tanımlıyoruz. Burada **PDF meta verilerini** (başlık, yazar vb.) ekliyor ve motorun belirli bir eşik altında kalan kelimeleri atmasını sağlıyoruz.

```csharp
PdfOptions searchablePdfOptions = new PdfOptions
{
    Title = "Invoice #12345",
    Author = "MyCompany",
    // Hide words with confidence lower than 0.8 (80%)
    MinConfidence = 0.8f
};
```

**Burada ne oluyor?**  
- `Title` ve `Author`, PDF'in belge bilgi sözlüğünün bir parçası haline gelir; bu da dosyanın belge yönetim sistemlerinde daha kolay indekslenmesini sağlar.  
- `MinConfidence` bir koruma katmanıdır: OCR, soluk karakterleri sık sık yanlış okur; bunları filtrelemek aranabilir katmanı temiz tutar ve sonraki metin çıkarımını iyileştirir.

Özel meta veriye (ör. `Subject`, `Keywords`) ihtiyacınız varsa, `PdfOptions.CustomProperties` üzerinden ayarlayabilirsiniz.

## Adım 4 – Görüntüyü Aranabilir PDF'e Dönüştürün (Görüntüyü PDF'e Çevirme)

Motor hazır ve seçenekler ayarlandıktan sonra son çağrı dönüşümü gerçekleştirir. Orijinal görüntünün altına OCR metin katmanını gömerek bir aranabilir PDF dosyası yazar.

```csharp
ocrEngine.ConvertToSearchablePdf(
    outputPath: @"YOUR_DIRECTORY/output.pdf",
    pdfOptions: searchablePdfOptions);
```

Bu satır çalıştıktan sonra `output.pdf` şunları içerir:
- Görsel arka plan olarak orijinal TIF görüntüsü  
- Arama motorları ve kopyala‑yapıştır işlemlerinin okuyabileceği görünmez bir metin katmanı  
- Daha önce tanımladığımız meta veriler (başlık, yazar vb.)

### Beklenen Sonuç

Oluşturulan PDF'i Adobe Reader ya da herhangi bir PDF görüntüleyicide açın ve metni seçmeyi deneyin. Orijinal taramaya karşılık gelen cümleleri kopyalayabilmelisiniz. Belgenin **Properties** (Özellikler) penceresinde başlık “Invoice #12345” ve yazar “MyCompany” olarak görünecek.

## Adım 5 – Güven Filtrelemesini Doğrulayın (MinConfidence Neden Yardımcı Olur)

Düşük‑güvenilir kelimelerin gerçekten kaldırıldığını kontrol etmek faydalıdır. `pdftotext` gibi bir araçla PDF'in gizli metnini inceleyebilirsiniz:

```bash
pdftotext output.pdf - | grep -i "unlikelyword"
```

Kelime hiç görünmüyorsa, `MinConfidence` filtresi amaçlandığı gibi çalışmış demektir. Daha agresif ya da daha toleranslı bir filtre istiyorsanız eşik değerini (ör. `0.7f`) ayarlayın.

## Adım 6 – Çoklu Sayfaları İşleme (Çok Sayfalı TIF'ten Aranabilir PDF Oluşturma)

Birçok fatura çok sayfalı TIFF dosyaları olarak gelir. Aspose.OCR, her çerçeveyi otomatik olarak ayrı bir sayfa olarak işler. Motoru çok sayfalı dosyaya yöneltmeniz yeterli; aynı `ConvertToSearchablePdf` çağrısı çok sayfalı bir aranabilir PDF üretir.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/multi_page.tif");
ocrEngine.ConvertToSearchablePdf(@"YOUR_DIRECTORY/multi_output.pdf", searchablePdfOptions);
```

**Kenar durumu:** Bir sayfa boşsa, OCR hâlâ boş bir metin katmanı oluşturabilir; bu zararsızdır. Ancak, dönüşümden önce `ocrEngine.HasText` kontrolü yaparak boş sayfaları atlayabilirsiniz.

## Adım 7 – Tam Örneği Paketleme (Tüm Adımlar Bir Arada)

Aşağıda, her şeyi bir araya getiren tek bir, çalıştırılabilir program yer alıyor. `YOUR_DIRECTORY` kısmını makinenizdeki gerçek klasör yolu ile değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Pdf;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = Language.English
        };

        // 2️⃣ Load the TIF image (create pdf from tif)
        string inputPath = @"YOUR_DIRECTORY/input.tif";
        ocrEngine.Image = ImageStream.FromFile(inputPath);

        // 3️⃣ Set PDF metadata and confidence filter
        PdfOptions pdfOptions = new PdfOptions
        {
            Title = "Invoice #12345",
            Author = "MyCompany",
            MinConfidence = 0.8f
        };

        // 4️⃣ Convert to searchable PDF (convert image to pdf)
        string outputPath = @"YOUR_DIRECTORY/output.pdf";
        ocrEngine.ConvertToSearchablePdf(outputPath, pdfOptions);

        Console.WriteLine($"✅ Searchable PDF created at: {outputPath}");
    }
}
```

Programı çalıştırın (`dotnet run` ya da Visual Studio’da **F5** tuşuna basın) ve onay mesajını göreceksiniz. Oluşturulan PDF, kaynak görüntünüzün yanında yer alacak ve indeksleme ya da arşivleme için hazır olacaktır.

## Sık Sorulan Sorular & Dikkat Edilmesi Gerekenler

| Soru | Cevap |
|------|-------|
| **Aranabilir katmana özel bir font ekleyebilir miyim?** | OCR katmanı Unicode kullanır; görsel görünüm altındaki görüntü tarafından sağlanır, ek bir font gömmeye gerek yoktur. |
| **TIF'im renkli ise ne olur?** | Aspose.OCR, renkli görüntüleri OCR için otomatik olarak gri tonlamaya çevirir, ancak `PdfOptions.PreserveColor = true` ayarıyla PDF'de orijinal renkleri koruyabilirsiniz. |
| **Kütüphane çoklu iş parçacığı (thread‑safe) mi?** | Her `OcrEngine` örneği tek bir iş parçacığı tarafından kullanılmalıdır. Paralel işleme için her iş parçacığına ayrı bir motor oluşturun. |
| **PDF'i nasıl şifreleyebilirim?** | OCR dönüşümünden sonra `PdfOptions.Security` kullanarak bir şifre ve izinler belirleyebilirsiniz. |

## Sonraki Adımlar (PDF Araç Setinizi Genişletin)

- **Toplu işleme:** Bir klasördeki tüm TIFF dosyalarını döngüye alıp her biri için aranabilir PDF oluşturun.  
- **Son işlem:** Oluşturulan PDF'leri tek bir ana belgeye birleştirmek için Aspose.PDF kullanın.  
- **İleri düzey meta veri:** SharePoint ya da ECM sistemleriyle daha iyi entegrasyon için özel XMP alanları doldurun.  

Tüm bu uzantılar, az önce ele aldığımız temel kalıp üzerine inşa edilir: **aranabilir PDF oluşturma**, **görüntüyü PDF'e çevirme** ve **PDF meta verisi ekleme**.

---

*Kodlamanız keyifli olsun! Herhangi bir sorunla karşılaşırsanız aşağıya yorum bırakın ya da en yeni API güncellemeleri için Aspose.OCR belgelerine göz atın.*

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}