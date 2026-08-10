---
category: general
date: 2026-02-27
description: Aspose OCR kullanarak taranmış bir PDF'den saniyeler içinde aranabilir
  PDF oluşturun. Taranmış PDF'yi nasıl dönüştüreceğinizi, OCR ile PDF'yi nasıl dönüştüreceğinizi
  ve PDF'den metni nasıl zahmetsizce çıkaracağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- ocr convert pdf
- extract text from pdf
- convert image pdf
language: tr
og_description: Aranabilir PDF'yi anında oluşturun. Bu öğreticide, taranmış PDF'yi
  nasıl dönüştüreceğinizi, OCR ile PDF dönüştürmeyi ve Aspose OCR ile PDF'den metin
  çıkarmayı gösteriyor.
og_title: Aranabilir PDF Oluşturma – Hızlı Aspose OCR Rehberi
tags:
- Aspose OCR
- C#
- PDF processing
title: Aspose OCR ile Tarama Görüntülerinden Aranabilir PDF Oluştur
url: /tr/net/text-recognition/create-searchable-pdf-from-scanned-images-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Tarayıcı Görüntülerinden Aspose OCR ile Aranabilir PDF Oluşturma

Hiç kağıt‑only bir faturadan **aranabilir PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilmiyor muydunuz? Aspose OCR ile sadece birkaç C# satırıyla **aranabilir PDF** oluşturabilirsiniz—harici hizmetlere gerek yok, manuel kopyala‑yapıştırmaya gerek yok.  

Bu rehberde, **tarayıcı pdf** dosyalarını tamamen aranabilir PDF'lere **dönüştürmek** için ihtiyacınız olan her şeyi adım adım inceleyecek, her adımın neden önemli olduğunu açıklayacak ve PDF çıktısı yerine ham string'leri tercih ederseniz **pdf'den metin çıkarma** nasıl yapılır gösterileceğiz. Sonunda, yaygın “sadece görüntü PDF” sorununu ele alan yeniden kullanılabilir bir kod parçacığı ve kenar durumları için birkaç ipucu elde edeceksiniz.

![Aspose OCR kullanarak aranabilir PDF oluşturma](image-placeholder.png "Aspose OCR kullanarak aranabilir PDF oluşturma")

## Gereksinimler

- .NET 6.0 veya üzeri (API .NET Core, .NET Framework ve .NET 5+ üzerinde çalışır)
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir editör)
- Bir Aspose OCR NuGet paketi (`Aspose.OCR`) – bunu ilk adımda kuracağız
- Aranabilir **PDF**'ye dönüştürmek istediğiniz taranmış bir PDF dosyası (sadece görüntü)

Hepsi bu—ek OCR motorları yok, deneme sürümü için lisans derdi yok. Şimdi, başlayalım.

## Adım 1: Aspose OCR Kütüphanesini Kurun (ve Hızlı Bir İpucu)

Herhangi bir kod çalıştırılmadan önce kütüphane referans alınmalıdır. Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Visual Studio’nun Paket Yöneticisini kullanıyorsanız, “Aspose.OCR” için arama yapın ve **Install** (Yükle) düğmesine tıklayın. Ücretsiz deneme sürümü 20 sayfaya kadar çalışır, bu test için mükemmeldir.

Paketi kurmak, `OcrEngine`, `OcrLanguage` ve `OcrOutputFormat` sınıflarına erişim sağlar—**ocr convert pdf** için kullanacağımız üç sınıf.

## Adım 2: OCR Motorunu Yapılandırın (Aranabilir PDF Oluşturma – Temel Ayarlar)

Motorun hangi dili tanıyacağını ve hangi çıktı formatını istediğinizi bilmesi gerekir. Bizim durumumuzda, aranabilir bir İngilizce dilinde PDF istiyoruz.

```csharp
using Aspose.OCR;
using System;

// Step 2: Set up the OCR engine
var ocrEngine = new OcrEngine
{
    // Choose the language of the source document
    Language = OcrLanguage.English,

    // Tell Aspose we want a searchable PDF as the result
    OutputFormat = OcrOutputFormat.SearchablePdf
};
```

`Language` değerini açıkça ayarlamak neden önemli? Motor dili tahmin ettiğinde OCR doğruluğu büyük ölçüde düşer, özellikle sayılar veya karışık betikler içeren belgelerde. İngilizceye sabitleyerek daha temiz metin katmanları elde ederiz, bu da daha sonra **pdf'den metin çıkarma** adımını iyileştirir.

## Adım 3: Taranmış PDF'yi Aranabilir PDF'ye Dönüştürün

Motor hazır olduğuna göre, kaynak dosyayı gösterin ve sonucu nereye yazacağını belirtin. Bu tek çağrı işi halleder: her sayfayı rasterleştirir, OCR çalıştırır ve görünmez bir metin katmanı içeren yeni bir PDF yazar.

```csharp
// Step 3: Perform the conversion
ocrEngine.RecognizePdf(
    @"C:\Docs\invoice_scanned.pdf",   // input – image‑only PDF
    @"C:\Docs\invoice_searchable.pdf" // output – searchable PDF
);
```

Kaynak PDF birden fazla sayfa içeriyorsa, Aspose OCR bunları sırasıyla işler ve orijinal düzeni korur. Çıktı dosyası herhangi bir PDF görüntüleyicide açılabilir; artık daha önce sadece resim olan kelimeleri seçip arayabileceğinizi fark edeceksiniz.

### Sonucu Doğrulama (PDF'den Metin Çıkarma)

Conversion'ın başarılı olduğundan kesin olarak emin olmak için, programlı olarak metni çekmek isteyebilirsiniz:

```csharp
using Aspose.Pdf;           // Add Aspose.PDF if you also need text extraction
using System.Text;

// Load the newly created searchable PDF
var doc = new Document(@"C:\Docs\invoice_searchable.pdf");
var sb = new StringBuilder();

foreach (Page page in doc.Pages)
{
    // Extract the hidden text layer
    sb.Append(page.Text);
}

Console.WriteLine("Extracted text:\n" + sb.ToString());
```

Bu kod parçacığı, OCR adımından sonra **pdf'den metin çıkarma** nasıl yapılacağını gösterir; indeksleme veya içeriği bir arama motoruna beslemek için kullanışlıdır. Bu bölüm için ayrı `Aspose.PDF` paketine ihtiyacınız olduğunu unutmayın; bu hafif bir eklentidir.

## Adım 4: **Görüntü PDF'yi Dönüştürürken** Ortak Kenar Durumlarını Ele Alın

Temel akış çoğu PDF için çalışsa da, gerçek dünyadaki dosyalar zorluklar çıkarabilir:

| Durum | Neden Oluşur | Nasıl Ele Alınır |
|-----------|----------------|------------------|
| **Döndürülmüş sayfalar** | Tarayıcılar bazen sayfaları otomatik olarak 90° döndürür. | `RecognizePdf` çağrılmadan önce `ocrEngine.RotatePages = true` ayarlayın. |
| **Karışık diller** | Faturalar Fransızca veya Almanca terimler içerebilir. | `OcrLanguage.Multilingual` kullanın veya birden fazla dili `|` ile birleştirin (örneğin, `OcrLanguage.English | OcrLanguage.French`). |
| **Büyük dosyalar (> 100 sayfa)** | Ücretsiz deneme sınırları dosyanın ortasında işleme durabilir. | Bir lisans satın alın veya OCR'dan önce `Aspose.Pdf` kullanarak PDF'i parçalara bölün. |
| **Düşük çözünürlüklü taramalar** | Metin bulanıklaşır, OCR doğruluğu düşer. | `ocrEngine.ImageResolution = 300` (varsayılan 200) ile DPI'yi artırın. |

Bu senaryoları ele almak, **ocr convert pdf** işlem hattınızın üretimde sağlam kalmasını sağlar.

## Adım 5: Tüm Süreci Otomatikleştirin (Bir Metot İçinde Paketleyin)

Bir fatura‑işleme servisi geliştiriyorsanız, muhtemelen yeniden kullanılabilir bir metot istersiniz. İşte giriş ve çıkış yollarını kabul eden, döndürmeyi ele alan ve çıkarılan metni döndüren kompakt bir sürüm.

```csharp
using Aspose.OCR;
using Aspose.Pdf;
using System;
using System.Text;

public static class PdfSearchableHelper
{
    /// <summary>
    /// Converts an image‑only PDF to a searchable PDF and returns the hidden text.
    /// </summary>
    /// <param name="inputPath">Path to the scanned PDF.</param>
    /// <param name="outputPath">Path where the searchable PDF will be saved.</param>
    /// <returns>All extracted text as a single string.</returns>
    public static string ConvertAndExtract(string inputPath, string outputPath)
    {
        // 1️⃣ Initialize OCR engine
        var ocr = new OcrEngine
        {
            Language = OcrLanguage.English,
            OutputFormat = OcrOutputFormat.SearchablePdf,
            RotatePages = true,            // fixes rotated scans automatically
            ImageResolution = 300          // improve accuracy on low‑res scans
        };

        // 2️⃣ Perform conversion
        ocr.RecognizePdf(inputPath, outputPath);

        // 3️⃣ Load result and pull out hidden text
        var doc = new Document(outputPath);
        var sb = new StringBuilder();

        foreach (Page page in doc.Pages)
            sb.Append(page.Text);

        return sb.ToString();
    }
}
```

Şimdi şu şekilde çağırabilirsiniz:

```csharp
string extracted = PdfSearchableHelper.ConvertAndExtract(
    @"C:\Docs\contract_scanned.pdf",
    @"C:\Docs\contract_searchable.pdf");

Console.WriteLine("OCR completed. Extracted text length: " + extracted.Length);
```

Bu, **convert image pdf** → **searchable PDF** tam bir iş akışı, tek bir metot içinde paketlenmiş ve herhangi bir ASP.NET Core servisine ya da konsol uygulamasına ekleyebileceğiniz bir haldedir.

## Sıkça Sorulan Sorular (SSS)

**S: Bu macOS/Linux'ta çalışır mı?**  
C: Kesinlikle. .NET 6 çalışma zamanı ve Aspose OCR platformlar arasıdır, bu yüzden aynı kod Windows, macOS ve Linux konteynerlerinde çalışır.

**S: Sadece metne ihtiyacım var ve aranabilir PDF'ye ihtiyacım yoksa ne olur?**  
C: `OutputFormat` adımını atlayın ve `OutputFormat = OcrOutputFormat.Text` ayarlayın. Motor doğrudan düz metin döndürür.

**S: Orijinal PDF'nin meta verilerini koruyabilir miyim?**  
C: Evet. Dönüştürmeden sonra, kaynak `Document` nesnesinden yeni nesneye `doc.Info.Title`, `doc.Info.Author` vb. kullanarak meta verileri kopyalayabilirsiniz.

**S: Sayfa sayısı için bir limit var mı?**  
C: Ücretsiz deneme sürümü belge başına 20 sayfa ile sınırlıdır. Tam lisans bu sınırlamayı kaldırır.

## Sonuç

Artık **aranabilir PDF** nasıl oluşturulacağını biliyorsunuz

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}