---
category: general
date: 2026-04-26
description: Aspose OCR kullanarak C#’ta taranmış bir görüntüden aranabilir PDF oluşturun.
  Taranmış görüntüyü nasıl dönüştüreceğinizi, metni nasıl çıkaracağınızı ve hızlı
  bir şekilde aranabilir PDF oluşturacağınızı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned image
- extract text from image
- how to ocr document
- convert tiff to pdf
language: tr
og_description: Aspose OCR kullanarak taranmış bir görüntüden aranabilir PDF oluşturun.
  Dönüştürme, metin çıkarma ve aranabilir PDF üretmek için adım adım C# kodu.
og_title: Taranmış Görüntüden Aranabilir PDF Oluştur – C# Rehberi
tags:
- Aspose OCR
- C#
- PDF
- OCR
title: Tarama Görüntüsünden Aranabilir PDF Oluşturma – C# Rehberi
url: /tr/net/text-recognition/create-searchable-pdf-from-scanned-image-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Taralı Görüntüden Aranabilir PDF Oluşturma – C# Kılavuzu

Hiç **aranabilir PDF** dosyalarını kağıt sözleşmelerden, makbuzlardan veya eski arşivlerden oluşturmanız gerekti mi? Yalnız değilsiniz—çoğu geliştirici, bir müşterinin bir yığın TIFF taraması teslim etmesi ve son ürün olarak aranabilir bir PDF beklemesi durumunda bu engelle karşılaşır.  

Bu öğreticide, **bir belgeyi OCR ile nasıl işleyebileceğinizi** ve taranmış bir görüntüyü Aspose OCR for .NET ile **aranabilir PDF**'ye nasıl dönüştüreceğinizi tam olarak göstereceğiz. Sonunda **tarama görüntüsü** dosyalarını **görüntüden metin çıkarma** ve hatta çok sayfalı TIFF'leri sorunsuz bir şekilde işleyebileceksiniz.

## Gereksinimler

* .NET 6.0 veya daha yeni bir sürüm (API .NET Core, .NET Framework ve .NET 5+ ile çalışır).  
* Geçerli bir Aspose OCR lisansı veya değerlendirme filigranıyla çalışmaktan memnun olmanız.  
* `Aspose.OCR` NuGet paketinin yüklü olması (`dotnet add package Aspose.OCR`).  
* Aranabilir PDF'ye dönüştürmek istediğiniz örnek bir TIFF dosyası (ör. `contract_scan.tif`).

Hepsi bu—ekstra kütüphane yok, karmaşık yapılandırma yok. Hazır mısınız? Hadi başlayalım.

![Create searchable PDF example](create-searchable-pdf.png "create searchable pdf example")

## Adım 1 – OCR Motorunu Başlatma (Aranabilir PDF Oluşturma)

İlk olarak bir `OcrEngine` örneğine ihtiyacınız var. Bu nesne, bitmap'i okuyan, karakterleri tanımlayan ve size metni geri veren iş gücüdür.  

```csharp
using Aspose.OCR;
using Aspose.OCR.Output;

// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Tell the engine which language to look for – Latin works for most English documents
ocrEngine.Language = Language.Latin;
```

**Neden dili ayarlamalısınız?**  
Varsayılan bırakılırsa, Aspose tüm dil paketlerini deneyecek ve bu da işlemi yavaşlatır. `Language.Latin` belirtmek, motorun Latin alfabesine odaklanmasını sağlar, böylece İngilizce sözleşmeler için hız artışı ve daha doğru sonuçlar elde edersiniz.

## Adım 2 – Tarama Görüntünüzü Yükleyin (Tarama Görüntüsünü Dönüştürme)

Şimdi motoru işlemek istediğimiz görüntüyle besliyoruz. Aspose bir dosya yolu, bir akış veya hatta bir `byte[]` okuyabilir. Basitlik açısından `ImageStream.FromFile` kullanacağız.  

```csharp
// Load the TIFF (or any supported image format)
ocrEngine.Image = ImageStream.FromFile(@"C:\Docs\contract_scan.tif");
```

Daha sonra **TIFF'i PDF'ye dönüştürmeniz** gerekirse, çok sayfalı TIFF'lerin otomatik olarak işlendiğini unutmayın—her çerçeve ayrı bir PDF sayfası olur.

## Adım 3 – OCR'yi Çalıştırın ve Metni Alın (Görüntüden Metin Çıkarma)

OCR'yi çalıştırmak, `Recognize` metodunu çağırmak kadar kolaydır. Motor, düz metin, güven puanları ve düzen bilgilerini içeren bir `RecognitionResult` döndürür.  

```csharp
// Perform the OCR operation
RecognitionResult result = ocrEngine.Recognize();

// The raw text is available via the Text property
string extractedText = result.Text;

// Quick sanity check – print the first 200 characters
Console.WriteLine(extractedText.Substring(0, Math.Min(200, extractedText.Length)));
```

**Pro ipucu:** Sadece metne ihtiyacınız varsa (PDF yok), burada durup `extractedText`'i bir `.txt` dosyasına yazabilirsiniz. Ancak çoğu zaman amacımız aranabilir bir PDF olduğundan, devam edeceğiz.

## Adım 4 – Aranabilir PDF Olarak Kaydetme (Aranabilir PDF Oluşturma)

Aspose son adımı basitleştirir: sadece `Save` metodunu `SaveFormat.PdfSearchable` ile çağırın. Kütüphane, çıkarılan metni görünmez bir katman olarak gömerek orijinal görüntünün görünümünü korur.  

```csharp
// Save the result as a searchable PDF
ocrEngine.Save(@"C:\Docs\contract_searchable.pdf", SaveFormat.PdfSearchable);
```

`contract_searchable.pdf` dosyasını herhangi bir PDF görüntüleyicide açtığınızda, metni seçebilecek, kopyalayabilecek ve arayabileceksiniz—tam da bir müşterinin “aranabilir PDF”den beklediği şey.

## Çok Sayfalı TIFF'lerin İşlenmesi (TIFF'i PDF'ye Dönüştürme)

Kaynak dosyanız birden fazla sayfa içeriyorsa, Aspose her çerçeveyi otomatik olarak ayrı bir sayfa olarak ele alır. Ek döngülere gerek yok. Ancak, her sayfa için DPI veya görüntü kalitesini kontrol etmek isteyebilirsiniz:  

```csharp
// Optional: tweak image processing settings before OCR
ocrEngine.ImageProcessingOptions.Dpi = 300; // higher DPI improves accuracy
ocrEngine.ImageProcessingOptions.Compression = ImageCompression.Jpeg;
```

Bu seçenekleri ayarladıktan sonra, her çerçeve için **Adım 2**'yi tekrarlayın veya `ImageStream.FromFile`'ı çok sayfalı TIFF'e yönlendirip Aspose'un işi halletmesine izin verin.

## Yaygın Tuzaklar ve Çözüm Yolları

| Semptom | Muhtemel Neden | Çözüm |
|---------|----------------|-------|
| Metin bozuk veya eksik | Yanlış dil ayarı | `ocrEngine.Language`'ı doğru dil paketine ayarlayın (ör. `Language.German`). |
| PDF çok büyük (tek sayfalık tarama için 10 MB) | Varsayılan görüntü sıkıştırması düşük | `ocrEngine.ImageProcessingOptions.Compression`'ı `Jpeg` olarak ayarlayın ve makul bir `Quality` değeri (0‑100) belirleyin. |
| OCR çok yavaş çalışıyor | Varsayılan `Auto` dil algılamasını kullanmak | Beklediğiniz dili açıkça ayarlayın. |
| Aranabilir katman görünmüyor | `PdfSearchable` yerine `SaveFormat.Pdf` ile kaydedildi | `PdfSearchable` kullanın. |

## Tam Uçtan Uca Örnek

Her şeyi bir araya getirerek, Visual Studio'ya kopyalayıp yapıştırabileceğiniz çalıştırmaya hazır bir konsol uygulaması burada:  

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace SearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine
            {
                Language = Language.Latin,
                // Optional: improve accuracy for low‑resolution scans
                ImageProcessingOptions = { Dpi = 300, Compression = ImageCompression.Jpeg }
            };

            // 2️⃣ Load the scanned image (convert scanned image)
            string inputPath = @"C:\Docs\contract_scan.tif";
            ocrEngine.Image = ImageStream.FromFile(inputPath);

            // 3️⃣ Run OCR and extract text (extract text from image)
            RecognitionResult result = ocrEngine.Recognize();
            Console.WriteLine("First 200 characters of extracted text:");
            Console.WriteLine(result.Text.Substring(0, Math.Min(200, result.Text.Length)));

            // 4️⃣ Save as searchable PDF (create searchable pdf)
            string outputPath = @"C:\Docs\contract_searchable.pdf";
            ocrEngine.Save(outputPath, SaveFormat.PdfSearchable);
            Console.WriteLine($"Searchable PDF created at: {outputPath}");
        }
    }
}
```

**Gördükleriniz:**  
* OCR'lenmiş metnin bir kısmını yazdıran bir konsol penceresi.  
* Orijinal TIFF'inizin yanında bulunan bir `contract_searchable.pdf` dosyası. Açın, **Ctrl + F** tuşlarına basın ve orijinal taramada görülen herhangi bir kelimeyi arayın—voilà, çalışıyor.

## Sonraki Adımlar ve İlgili Konular

* **Belge toplu OCR** – yukarıdaki kodu bir `foreach` döngüsü içinde sararak tüm bir klasörü işleyin.  
* **TIFF dışındaki tarama görüntüsü** formatlarını (PNG, JPEG) dönüştürün – aynı API çalışır; sadece dosya uzantısını değiştirin.  
* **Görüntüden metin çıkarma** daha fazla analiz için – `result.Text`'i doğal dil işleme boru hattına besleyin.  
* **PDF boyutunu optimize etme** – `PdfSaveOptions`'ı keşfederek görüntüleri daha fazla sıkıştırın veya yalnızca gerektiğinde yazı tiplerini gömün.  

Bu fikirlerle deneyler yapın, ve “bu taramayı aranabilir PDF'ye dönüştür” taleplerinde hızlıca başvurulacak kişi olacaksınız.

---

### TL;DR

Artık Aspose OCR'i C# ile kullanarak taranmış görüntülerden **aranabilir PDF** dosyaları oluşturmayı biliyorsunuz. Süreç: motoru başlatın, görüntüyü yükleyin, OCR'yi çalıştırın ve `PdfSearchable` ile kaydedin. Dil ayarlarını, DPI'yi ve sıkıştırmayı kenar durumlarını yönetmek için ayarlayın ve **tarama görüntüsünü dönüştürmeye**, **görüntüden metin çıkarmaya** ve hatta **TIFF'i PDF'ye dönüştürmeye** ölçekli olarak hazırsınız. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}