---
category: general
date: 2025-12-29
description: Tarama görüntülerinden Aspose OCR toplu işleme kullanarak aranabilir
  PDF oluşturun. Görüntüleri PDF'ye dönüştürmeyi, OCR için görüntüleri ön işlemeyi
  ve taranmış belgeleri eğriltmeyi (deskew) öğrenin.
draft: false
keywords:
- create searchable pdf
- batch ocr processing
- convert images to pdf
- preprocess images for ocr
- deskew scanned documents
language: tr
og_description: Aspose OCR toplu işleme kullanarak taranmış görüntülerden aranabilir
  PDF oluşturun. Görüntüleri PDF'ye dönüştürmeyi, OCR için görüntüleri ön işlemeyi
  ve taranmış belgeleri eğriltmeyi öğrenin.
og_title: Toplu OCR ile aranabilir PDF oluşturma – C# Rehberi
tags:
- OCR
- C#
- PDF/A
- Aspose
title: Toplu OCR ile aranabilir PDF oluşturma – C# Rehberi
url: /tr/net/ocr-optimization/create-searchable-pdf-with-batch-ocr-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Batch OCR ile aranabilir PDF oluşturma – C# Rehberi

Bir dağ gibi taranmış görüntüden **aranabilir pdf** dosyaları oluşturmanız gerektiğinde ama ilk adımda takıldıysanız? Yalnız değilsiniz—çoğu geliştirici, dağınık taramalar, düzensiz sayfalar veya sadece toplu dönüşümle uğraşırken aynı duvara çarpar.

İyi haber? Aspose OCR ile sadece **görüntüleri pdf'ye dönüştürmek** değil, aynı zamanda **OCR için görüntüleri ön işleme** ve hatta **taran belgeleri düzeltme** (deskew) otomatik olarak yapan bir **batch OCR işleme** hattı oluşturabilirsiniz. Bu öğreticide motoru kurmaktan çıktıyı cilalamaya kadar her adımı anlatacağız, böylece bir klasördeki dosyalar üzerinde çalıştırabilir ve aranabilir PDF/A‑2b mücevherleri elde edebilirsiniz.

> **Ne elde edeceksiniz:** bir dizindeki görüntüleri (veya PDF'leri) alan, her sayfayı temizleyen, OCR çalıştıran ve kaynağın yanına bir aranabilir PDF/A‑2b dosyası bırakan tek bir çalıştırılabilir C# konsol uygulaması. Parçalı kod parçacıkları yok, sadece tek bir tutarlı çözüm.

---

## Önkoşullar

- .NET 6 SDK veya daha yenisi (kod .NET Core ile de derlenir).  
- Bir Aspose OCR NuGet paketi (`Aspose.OCR`).  
- Aranabilir PDF'lere dönüştürmek istediğiniz taranmış görüntüler (TIFF, JPEG, PNG) veya PDF'lerden oluşan bir klasör.  
- (İsteğe bağlı) Gerçek bir lisans anahtarı—aksi takdirde deneme modu bir filigran ekler, ancak test için çalışır.

Eğer bunlara sahipseniz, başlayalım.

---

## Genel Bakış – Tüm işlem hattı nasıl aranabilir pdf oluşturur

1. **Deneme modunu etkinleştir** (veya lisansınızı yükleyin).  
2. **`OcrBatchProcessor`'ı yapılandır** – dosyaları nereden okuyacağını, PDF'leri nereye yazacağını, hangi formatı kullanacağını ve paralel olarak kaç iş parçacığı çalıştıracağını belirtin.  
3. **Her görüntüyü ön‑işle** – deskew, gürültü azaltma ve arka plan temizleme, böylece OCR motoru temiz bir sayfa görür.  
4. **Toplu işlemi çalıştır** – Aspose her dosyayı işler, OCR çalıştırır ve bir aranabilir PDF/A‑2b yazar.  
5. **Tamamlanmayı bildir** – basit bir konsol mesajı, ancak bir logger veya webhook ekleyebilirsiniz.

Bu yüksek seviyeli akış. Aşağıdaki kod, her adımı bol yorumla uygular, böylece bütünlüğü bozmadan herhangi bir kısmı ayarlayabilirsiniz.

---

## Adım 1 – Deneme modunu etkinleştir (veya lisansınızı yükleyin)

Herhangi bir Aspose sınıfını çağırmadan önce kütüphaneye lisanslı olduğunuzu bildirmeniz gerekir. Hızlı denemeler için deneme modu yeterlidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

// Activate trial mode – replace with OcrEngine.SetLicense("YourLicenseFile.lic") for production
OcrEngine.EnableTrialMode();
```

> **Pro ipucu:** lisans aktivasyonunu `Program.cs` dosyasının en üstünde tutun. Unutursanız, motor `Process()`'ı ilk çağırdığınızda bir istisna fırlatır.

---

## Adım 2 – Toplu OCR işleme motorunu yapılandır

İşte **batch OCR processing** nesnesini kurduğumuz yer. Bu örnekte `InputFolder` ve `OutputFolder` aynı, ancak isterseniz ayırabilirsiniz.

```csharp
// Define where your source images live and where the searchable PDFs should be saved
var ocrBatch = new OcrBatchProcessor
{
    // Folder that contains the images or PDFs to be processed
    InputFolder = @"C:\Scans\Incoming",

    // Folder where searchable PDF/A‑2b files will be saved
    OutputFolder = @"C:\Scans\Processed",

    // Choose the output format – searchable PDF/A‑2b (perfect for archiving)
    OutputFormat = SaveFormat.SearchablePdf,

    // Limit the number of concurrent OCR operations to avoid CPU spikes
    MaxDegreeOfParallelism = 3,

    // Pre‑process each image: deskew, denoise, and remove background
    Preprocess = img => ImageFilters
                            .Deskew(img)          // fixes rotated pages
                            .Denoise()            // reduces speckles
                            .RemoveBackground()   // clears colored backgrounds
};
```

### Bu ayarların önemi

- **`MaxDegreeOfParallelism`**: Çok fazla OCR iş parçacığı çalıştırmak CPU'yu aşırı yükleyebilir, özellikle düşük özellikli bir iş istasyonunda. Çoğu dört çekirdekli dizüstü bilgisayar için üç iş parçacığı ideal bir denge sağlar.  
- **`Preprocess`** pipeline: Üç filtre birlikte OCR doğruluğunu büyük ölçüde artırır. Deskew, yaygın “eğik tarama” sorununu düzeltir, denoise rastgele gürültüyü kaldırır ve arka plan temizleme, motorun sadece siyah‑beyaz metni görmesini sağlar.  
- **`SaveFormat.SearchablePdf`**: Bu, hem arşivlemeye uygun hem de aranabilir PDF/A‑2b dosyaları oluşturur—birçok uyumluluk standardının gereksinimi.

---

## Adım 3 – Toplu işlemi yürüt ve sihrin gerçekleşmesini izle

Toplu işlemi çalıştırmak `Process()`'ı çağırmak kadar basittir. Metot, tüm dosyalar tamamlanana kadar bloklanır, ardından döner. İlerleme raporlamasına ihtiyacınız varsa `ProgressChanged` olayını bağlayabilirsiniz (burada gösterilmemiştir).

```csharp
// Start processing – this will walk through every file in InputFolder
ocrBatch.Process();

// Let the user (or calling script) know we’re finished
Console.WriteLine("All files processed. Searchable PDFs are ready.");
```

Konsol son satırı yazdırdığında, `C:\Scans\Processed` içinde her giriş görüntüsü için bir aranabilir PDF bulacaksınız. Adobe Reader'da herhangi birini açın, **Ctrl+F** tuşuna basın ve taramadan yeni çıkarılan metni arayabilirsiniz.

---

## Adım 4 – Tam çalıştırılabilir program (kopyala‑yapıştır hazır)

Aşağıda yeni bir konsol projesine (`dotnet new console`) ekleyebileceğiniz **tam, bağımsız** program bulunuyor. Önce Aspose.OCR NuGet paketini eklediğinizden emin olun (`dotnet add package Aspose.OCR`).

```csharp
// Program.cs
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using Aspose.OCR.Batch;

namespace CreateSearchablePdfDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Activate trial mode (replace with real license for production)
            OcrEngine.EnableTrialMode();

            // 2️⃣ Configure batch OCR processing
            var ocrBatch = new OcrBatchProcessor
            {
                InputFolder = @"C:\Scans\Incoming",   // 👉 change to your source folder
                OutputFolder = @"C:\Scans\Processed", // 👉 change to your target folder
                OutputFormat = SaveFormat.SearchablePdf,
                MaxDegreeOfParallelism = 3,
                Preprocess = img => ImageFilters
                                        .Deskew(img)          // fixes rotated pages
                                        .Denoise()            // cleans up noise
                                        .RemoveBackground()   // strips colored backgrounds
            };

            // 3️⃣ Run the batch
            ocrBatch.Process();

            // 4️⃣ Notify completion
            Console.WriteLine("All files processed. Searchable PDFs are ready.");
        }
    }
}
```

### Beklenen çıktı

```
All files processed. Searchable PDFs are ready.
```

Çalıştırdıktan sonra `C:\Scans\Processed` klasörüne gittiğinizde bir dizi `.pdf` dosyası göreceksiniz—her biri aranabilir, her biri PDF/A‑2b uyumlu. Herhangi bir dosyayı açın, orijinal taramada bulunduğunu bildiğiniz bir kelimeyi yazın ve voilà, metin vurgulanacak.

---

## Yaygın sorular & uç‑durum yönetimi

### Kaynak klasörüm zaten PDF içeriyorsa ne olur?

Aspose OCR PDF'leri doğrudan alabilir; her sayfayı rasterleştirir, aynı **preprocess** filtrelerini uygular ve OCR katmanını gömer. Ek kod gerekmez.

### Çıktı formatını düz bir PDF'ye (aranamaz) nasıl değiştiririm?

`SaveFormat.SearchablePdf`'i `SaveFormat.Pdf` ile değiştirin. Aranabilir metin katmanını kaybedeceksiniz, ancak görsel doğruluk aynı kalır.

### Taramalarım renkli—arka plan temizleme bunu etkiler mi?

`RemoveBackground()` ana metni korurken beyaz olmayan arka planları hedef alır. Renkli grafikleri tutmanız gerekiyorsa bu filtreyi atlayabilirsiniz:

```csharp
.Preprocess = img => ImageFilters.Deskew(img).Denoise()
```

### Sınırlı RAM'e sahip bir sunucuda çalışıyorum—iş parçacığı sayısını azaltabilir miyim?

Kesinlikle. `MaxDegreeOfParallelism` değerini `1` veya `2` yapın. Toplu işlem daha uzun sürecek, ancak bellek kullanımı düşük kalacak.

---

## Görsel özet (isteğe bağlı)

Hızlı bir diyagram isterseniz, bu akışı hayal edin:

![Aranabilir pdf oluşturma iş akışı – giriş klasörü → ön‑işleme → OCR → aranabilir PDF çıktısı](/images/ocr-workflow.png)

*Image alt text:* **Aranabilir pdf iş akışı diyagramı** – toplu OCR işleme, dönüşüm ve deskew adımlarını gösterir.

---

## Sonuç

Artık herhangi bir taranmış görüntü topluluğundan **aranabilir pdf** dosyaları oluşturmak için **tam, üretime hazır** bir çözümünüz var. **Toplu OCR işleme**'yi kullanarak **görüntüleri pdf'ye dönüştürebilir**, **OCR için görüntüleri ön‑işleyebilir** ve taranmış belgeleri otomatik olarak **deskew** edebilirsiniz—hepsi sadece birkaç C# satırıyla.

Sonraki adımlar? Özel bir adlandırma şeması eklemeyi deneyin, OCR güven skorlarını yakalamak için bir günlükleme çerçevesi bağlayın veya soluk metinler için `Sharpen()` gibi diğer `ImageFilters` ile deney yapın. Aspose OCR API, ihtiyaçlarınıza göre büyüyebilecek kadar esnektir.

Kodlamaktan keyif alın, ve PDF'leriniz her zaman aranabilir olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}