---
category: general
date: 2026-02-17
description: C# ile Aspose OCR kullanarak çok sayfalı bir TIFF'ten aranabilir PDF
  oluşturun. TIFF'i PDF'ye nasıl dönüştüreceğinizi ve PDF'yi dakikalar içinde dosyaya
  nasıl yazacağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert tiff to pdf
- write pdf to file
- ocr engine c#
- convert multi page tiff
language: tr
og_description: Aspose OCR kullanarak C#'ta çok sayfalı TIFF'ten aranabilir PDF oluşturun.
  Bu kılavuz, TIFF'i PDF'e dönüştürmeyi ve PDF'i dosyaya yazmayı gösterir.
og_title: C#'ta Aranabilir PDF Oluştur – TIFF'i PDF'ye Dönüştür
tags:
- Aspose OCR
- C#
- PDF generation
title: C#'ta Aranabilir PDF Oluştur – TIFF'i PDF'ye Dönüştür
url: /tr/net/text-recognition/create-searchable-pdf-in-c-convert-tiff-to-pdf/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Aranabilir PDF Oluşturma – TIFF'i PDF'e Dönüştürme

Tarayıcıdan taranmış bir belgeden **aranabilir PDF oluşturma** ihtiyacı hiç duydunuz mu ama nereden başlayacağınızı bilmiyor muydunuz? Yalnız değilsiniz. Birçok ofis‑otomasyon projesinde gereksinim, çok sayfalı bir TIFF'i arama, kopyalama ve indeksleme yapabileceğiniz bir PDF'e dönüştürmektir.  

Bu öğreticide, Aspose OCR ile **aranabilir PDF oluşturma**, **tiff'i pdf'e dönüştürme** ve diske **pdf'i dosyaya yazma** konularını gösteren tam, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Sonunda tüm süreci, her parçanın neden önemli olduğunu ve **ocr engine c#** ile **convert multi page tiff** senaryosunda dikkat etmeniz gerekenleri anlayacaksınız.

## Ne Oluşturacaksınız

- Diskten çok sayfalı bir TIFF görüntüsü yükleyin.  
- Aspose OCR’nin `OcrEngine`i ile her sayfada OCR çalıştırın.  
- Oluşan aranabilir PDF’i belleğe akıtın.  
- Tek bir `WriteAllBytes` çağrısıyla PDF’i dosyaya kaydedin.  

Harici hizmetler, karmaşık komut satırı araçları yok—herhangi bir .NET konsol uygulamasına ekleyebileceğiniz saf C# kodu.

> **Pro ipucu:** Aspose OCR ticari bir kütüphanedir, ancak ücretsiz deneme sürümü öğrenme amaçlı mükemmel çalışır. Üretimde kullanacaksanız geçerli bir lisans ayarladığınızdan emin olun.

## Önkoşullar

- .NET 6.0 SDK (veya daha yeni bir .NET sürümü).  
- Visual Studio 2022 veya VS Code—sevdiğiniz IDE yeterli.  
- Aspose.OCR NuGet paketi (`dotnet add package Aspose.OCR`).  
- Bilinen bir klasöre yerleştirilmiş çok sayfalı bir TIFF dosyası (`multi_page.tif`).  

Hepsi bu. Ek bir yapılandırma gerekmez.

![Aranabilir PDF örneği](https://example.com/create-searchable-pdf.png){: .align-center alt="Aranabilir PDF örneği"}

## Adım 1 – OCR Motorunu Başlatma (ocr engine c#)

Herhangi bir görüntüyü işleyebilmemiz için bir `OcrEngine` örneğine ihtiyacımız var. Bu nesne tüm OCR ayarlarını tutar ve sahne arkasında ağır işi yapar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

Her çalıştırmada yeni bir motor oluşturuyoruz çünkü motor iç kaynakları önbelleğe alır; kullanımdan sonra serbest bırakılması, büyük çok sayfalı TIFF'lerle çalışırken kritik olan yerel belleği temizler.

## Adım 2 – Çok Sayfalı TIFF'i Yükleme (convert multi page tiff)

Aspose OCR bir TIFF akışını doğrudan okuyabilir, bu yüzden dosyaya işaret ediyoruz.

```csharp
        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");
```

TIFF'iniz bir akışta (ör. veritabanından) bulunuyorsa `FromFile` yerine `FromStream` kullanın. Motor sayfa sayısını otomatik olarak algılar, bu yüzden **convert multi page tiff** için ekstra döngüye gerek kalmaz.

## Adım 3 – PDF için MemoryStream Hazırlama (write pdf to file)

Doğrudan diske yazmıyoruz çünkü akış, PDF boyutunu inceleme, şifreleme ya da HTTP üzerinden gönderme gibi işlemlere izin verir.

```csharp
        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
```

`using` bloğu, akışın serbest bırakılmasını garanti eder ve dosya tutamağı sızıntılarını önler—uzun süre çalışan servislerde bu çok önemlidir.

## Adım 4 – OCR Çalıştır ve Aranabilir PDF Olarak Kaydet (create searchable pdf)

Şimdi çekirdek işlem: TIFF'i `SaveAsSearchablePdf`e besleyin. Metod, sayfa sayfa OCR yapar ve içinde görünmez bir metin katmanı bulunan bir PDF yazar.

```csharp
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);
```

Aspose, her TIFF karesi için bir PDF sayfası oluşturur, OCR motorunu çalıştırır ve tanınan metni üstüne bindirir. Bu, taranmış bir belgeyi **create searchable pdf** çıktısına dönüştüren tam mekanizmadır.

## Adım 5 – PDF'i Diske Yaz (write pdf to file)

Son olarak, bellek tamponunu fiziksel bir dosyaya döküyoruz.

```csharp
            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }
```

`WriteAllBytes` çoğu platformda atomiktir, yani işlem yazma sırasında çökse bile yarım kalmış bir dosya elde etmezsiniz. Mevcut bir PDF'e ekleme yapmanız gerekiyorsa Aspose.PDF kullanmayı düşünün.

## Adım 6 – Onay Mesajı

Konsola kısa bir mesaj, her şeyin başarılı olduğunu bildirir.

```csharp
        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

Programı çalıştırın, gerçek bir TIFF dosyasına yönlendirin ve `result.pdf` dosyasının kaynak dosyanızın yanında oluştuğunu göreceksiniz. Herhangi bir PDF görüntüleyicide açıp metni seçmeyi deneyin—OCR katmanının çalıştığını göreceksiniz.

## Kenar Durumları ve Yaygın Tuzaklar

| Durum | Ne Yapmalı |
|-----------|------------|
| **Çok büyük TIFF (yüzlerce MB)** | İşlem belleği limitini artırın veya sayfaları partiler halinde işleyin: bir çerçeveyi tek seferde yükleyin, `SaveAsSearchablePdf`i mevcut bir akısa ekleyen bir `PdfSaveOptions` ile çağırın. |
| **OCR dili İngilizce değil** | `ocrEngine.Language = Language.Spanish;` (veya desteklenen başka bir dil) kodunu `SaveAsSearchablePdf` çağrısından önce ayarlayın. |
| **Lisans eksik** | Deneme sürümü bir filigran ekler. Lisansı şu şekilde kaydedin: `License license = new License(); license.SetLicense("Aspose.OCR.lic");`. |
| **Bozuk TIFF dosyası** | `ImageStream.FromFile`ı try/catch bloğuna alın ve `Aspose.OCR.Exception` detaylarını kaydedin. |
| **Görselleri olmadan aranabilir PDF gerekiyor** | `PdfSaveOptions` → `RemoveImages = true` ayarını kullanarak çıktı boyutunu küçültün. |

Bu ipuçları, çözümünüzü üretim ortamları için yeterince dayanıklı hâle getirir.

## Tam Çalışan Örnek (Tüm Adımlar Birleştirilmiş)

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;
using System;
using System.IO;

class SearchablePdfDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Optional: set language if needed
        // ocrEngine.Language = Language.English;

        // Step 2: Load the multi‑page TIFF image to be processed
        ImageStream tiffImage = ImageStream.FromFile("YOUR_DIRECTORY/multi_page.tif");

        // Step 3: Prepare a memory stream that will hold the generated PDF
        using (MemoryStream pdfMemoryStream = new MemoryStream())
        {
            // Step 4: Run OCR on the image and write the searchable PDF into the memory stream
            ocrEngine.SaveAsSearchablePdf(tiffImage, pdfMemoryStream);

            // Step 5: Save the PDF from the memory stream to a file on disk
            File.WriteAllBytes("YOUR_DIRECTORY/result.pdf", pdfMemoryStream.ToArray());
        }

        // Step 6: Inform the user that the PDF has been created
        Console.WriteLine("Searchable PDF created.");
    }
}
```

**Beklenen sonuç:** `result.pdf` `YOUR_DIRECTORY` içinde ortaya çıkar. Açtığınızda her orijinal TIFF sayfası yanında gizli, seçilebilir bir metin katmanı gösterir—tarama görüntülerinden **create searchable pdf** elde etmek için tam olarak ihtiyacınız olan şey.

## Özet

**convert tiff to pdf** iş akışından **create searchable PDF** oluşturma, **write pdf to file** işlemi, **ocr engine c#** rolü ve **convert multi page tiff** kaynağı için özel hususları kapsayan her şeyi ele aldık. Kod kendi içinde bağımsız, .NET 6+ üzerinde çalışır ve minimum değişiklikle web API'lerine ya da arka plan servislerine uyarlanabilir.

### Sıradaki Adımlar

- PDF hassas veriler içeriyorsa `PdfSaveOptions` ile **parola koruması ekleyin**.  
- `PdfSaveOptions.CompressionLevel` ayarını değiştirerek **çıktıyı sıkıştırın**.  
- PDF'i doğrudan tarayıcılara sunmak için **ASP.NET Core ile bütünleştirin**.  
- Sunucusuz OCR boru hatları için **Azure Functions'ı keşfedin**.

Denemeler yapmaktan çekinmeyin—giriş formatını değiştirin, farklı OCR dilleri deneyin ya da PDF'i bir belge yönetim sistemine yönlendirin. **convert tiff to pdf** ve **write pdf to file** konularında programatik olarak ne kadar çok şey yapabileceğinizi gördükçe sınırlarınız genişleyecek.

Kodlamanın tadını çıkarın, PDF'leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}