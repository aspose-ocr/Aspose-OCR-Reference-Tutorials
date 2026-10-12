---
category: general
date: 2026-02-17
description: C#'ta Aspose OCR kullanarak görüntüde OCR çalıştırın. JPG'den metin çıkarma,
  OCR için görüntüyü ön işleme ve adım adım kodla OCR için görüntü yükleme hakkında
  bilgi edinin.
draft: false
keywords:
- run OCR on image
- extract text from jpg
- preprocess image for OCR
- load image for OCR
language: tr
og_description: C#'ta Aspose OCR kullanarak görüntüde OCR çalıştırın. Bu rehber, jpg
  dosyasından metin nasıl çıkarılır, resim nasıl ön işleme tabi tutulur ve OCR için
  görüntü nasıl yüklenir, gösterir.
og_title: Aspose OCR ile Görüntüde OCR Çalıştırma – Tam C# Kılavuzu
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCR ile Görüntüde OCR Çalıştırma – Tam C# Rehberi
url: /tr/net/text-recognition/run-ocr-on-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Görüntü Üzerinde OCR Çalıştırma – Tam C# Rehberi

Görsel dosyalar üzerinde **OCR çalıştırma** ihtiyacınız oldu mu ama nereden başlayacağınızı bilemediniz mi? Gerçek dünyadaki birçok uygulamada – fatura tarayıcıları ya da makbuz izleyicileri gibi – ilk engel JPEG'ten güvenilir metin elde etmektir. İyi haber? Aspose OCR sayesinde **OCR çalıştırma** işlemini sadece birkaç satır C# kodu ile yapabilir ve **jpg'den metin çıkarma**, **OCR için görüntüyü ön işleme**, **OCR için görüntü yükleme** konularını da dağınık dokümanlar arasında kaybolmadan öğrenebilirsiniz.

Bu öğreticide, motoru nasıl kuracağınızı, faydalı ön işleme filtrelerini nasıl ekleyeceğinizi, bir resmi tanıyıcıya nasıl besleyeceğinizi ve sonucu konsola nasıl yazdıracağınızı gösteren tam, kopyala‑yapıştır‑hazır bir örnek üzerinden adım adım ilerleyeceğiz. Sonuna geldiğinizde, herhangi bir .NET projesine ekleyebileceğiniz ve görüntülerden anında metin çekebileceğiniz bağımsız bir programınız olacak.

## Gereksinimler

- .NET 6.0 veya üzeri (kod .NET Core üzerinde de çalışır)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- Referans alabileceğiniz bir klasörde bulunan örnek JPEG (`input.jpg`)  
- C# sözdizimi hakkında temel bir anlayış (özel bir şey gerekmez)

Bu parçalar zaten elinizdeyse harika – hemen başlayalım. Yoksa NuGet paketini ve bir test resmini edinin; rehberin geri kalanı bu adımları yaptığınızı varsayar.

## Adım 1: OCR Motorunu Oluşturma – Görüntü Üzerinde OCR Çalıştırmanın Çekirdeği

**OCR çalıştırma** için ilk yapmanız gereken `OcrEngine` nesnesini örneklemektir. Bu nesne tanıma için gereken tüm yapılandırma ve durumu tutar.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // Step 1 – create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Neden önemli:** `OcrEngine`, Aspose’un tanıma hattına giriş kapısıdır. Filters, dil paketleri veya `Recognize` metoduna erişemezsiniz.

## Adım 2: Ön‑İşleme Filtreleri Ekleme – JPG'den Metin Çıkarma Sırasında Doğruluğu Artırma

Kameradan gelen görüntüler nadiren mükemmeldir. Eğik açı ya da rastgele gren, en iyi OCR algoritmalarını bile zorlayabilir. **JPG'den metin çıkarma** işleminden önce birkaç filtre eklemek sonuçları büyük ölçüde iyileştirebilir.

```csharp
        // Step 2 – add preprocessing filters
        // Deskew corrects rotation; DenoiseGaussian reduces visual noise
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });
```

> **Profesyonel ipucu:** Kaynak görüntüleriniz zaten temizse `DenoiseGaussianFilter`'ı atlayabilirsiniz. Aşırı yumuşatma, soluk karakterleri silebilir.

## Adım 3: OCR İçin Görüntüyü Yükleme – JPEG'i Motora Besleme

Şimdi **OCR için görüntü yükleme** kısmına geliyoruz. Aspose, dosya yolunu motorun anlayacağı bir akıma dönüştüren kullanışlı bir `ImageStream.FromFile` yardımcı metodunu sunar.

```csharp
        // Step 3 – specify the path to the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        // Load the image and run OCR in one call
        var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));
```

> **Köşe durumu:** Dosya mevcut değilse, `FromFile` bir `FileNotFoundException` fırlatır. Çalışma zamanında eksik dosyalar bekliyorsanız çağrıyı try/catch içinde sarın.

## Adım 4: Tanınan Metni Alıp Görüntüleme

Son olarak, motor işi bitirdiğinde `Text` özelliği üzerinden düz metin sonucuna erişebilirsiniz. Konsola yazdırmak hızlı bir demo için yeterlidir, ancak bunu bir veritabanına ya da metin dosyasına da yazabilirsiniz.

```csharp
        // Step 4 – output the recognized text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı**

```
=== OCR Result ===
Invoice #12345
Date: 02/15/2026
Total: $1,234.56
```

İçerik, beslediğiniz resme bağlı olarak değişecektir, ancak anlamsız karakterler yerine düzgün biçimlendirilmiş bir metin bloğu görmelisiniz.

![OCR hattını gösteren diyagram – OCR çalıştırma, ön işleme, yükleme, tanıma](/images/ocr-pipeline.png "OCR çalıştırma hattı diyagramı")

### Her Adım Neden Önemli

| Adım | Amaç | Atlanırsa Ne Olur |
|------|------|-------------------|
| **Motoru oluştur** | İç yapıların başlatılması | Tanıyıcı yok – `NullReferenceException` alırsınız. |
| **Filtreleri ekle** | Döndürme ve gürültüyü düzelterek doğruluğu artırır | Eğik ya da gürültülü görüntüler bozuk çıktı üretir. |
| **Görüntüyü yükle** | Ham bitmap'i motora sağlar | Motorun işlenecek bir şeyi olmaz, `Text` alanı boş kalır. |
| **Sonucu oku** | Düz metin dizesini dışa aktarır | OCR çalıştırdınız ama sonucu görmezsiniz – pek faydalı değil! |

## Yaygın Varyasyonlar ve Süreci Nasıl Ayarlarsınız

### Dil Paketi Değiştirme

Aspose OCR, kutudan çıkar çıkmaz birden çok dili destekler. Eğer **OCR çalıştırma** sırasında Fransızca ya da Almanca gibi bir metinle karşılaşırsanız, `Recognize` çağrısından önce `Language` özelliğini ayarlayın.

```csharp
ocrEngine.Language = OcrLanguage.French;
```

### Çok Sayfalı PDF'lerle Çalışma

Kaynağınız tek bir JPEG yerine çok sayfalı bir PDF ise, önce her sayfayı bir görüntüye dönüştürüp (Aspose.PDF kullanarak) aynı hattaki her görüntüyü besleyebilirsiniz. Sayfalar üzerinde döngü oluşturmak basittir:

```csharp
foreach (var pageImage in pdfPagesAsImages)
{
    var result = ocrEngine.Recognize(ImageStream.FromMemory(pageImage));
    Console.WriteLine(result.Text);
}
```

### Büyük Dosyalarla Baş Etme

Yüksek çözünürlüklü fotoğrafları işlerken bellek tüketimi artabilir. **OCR için görüntü yükleme** işleminden önce görüntüyü küçültmeyi düşünün:

```csharp
using Aspose.Imaging;
using Aspose.Imaging.ImageOptions;

var loadOptions = new JpegLoadOptions { Width = 1024, Height = 768 };
using (var img = (Image)Image.Load(imagePath, loadOptions))
{
    var stream = new MemoryStream();
    img.Save(stream, new JpegOptions());
    var ocrResult = ocrEngine.Recognize(ImageStream.FromMemory(stream.ToArray()));
}
```

## Tam, Çalıştırmaya Hazır Örnek

Aşağıda, tartıştığımız her şeyi birleştiren tam program yer alıyor. Yeni bir console projesine kopyala‑yapıştır, `YOUR_DIRECTORY` kısmını `input.jpg` dosyasının bulunduğu klasörle değiştir ve **F5** tuşuna bas.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Add useful preprocessing filters
        ocrEngine.Filters.Add(new DeskewFilter());
        ocrEngine.Filters.Add(new DenoiseGaussianFilter { Sigma = 1.5 });

        // 3️⃣ Load the JPEG you want to process
        var imagePath = @"YOUR_DIRECTORY/input.jpg";

        try
        {
            // Recognize text – this is where we actually run OCR on image
            var ocrResult = ocrEngine.Recognize(ImageStream.FromFile(imagePath));

            // 4️⃣ Print the extracted text
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error processing image: {ex.Message}");
        }
    }
}
```

### Sonucu Doğrulama

1. Programı çalıştırın.  
2. Konsola bakın – `input.jpg` üzerindeki metni görmelisiniz.  
3. Çıktı karışık görünüyorsa, `DenoiseGaussianFilter` üzerindeki `Sigma` değerini ayarlamayı ya da `ContrastEnhancementFilter` gibi ek filtreler eklemeyi deneyin.

## Özet ve Sonraki Adımlar

Aspose OCR kullanarak **görüntü üzerinde OCR çalıştırma** sürecini, motor kurulumundan temiz, okunabilir metin elde etmeye kadar ele aldık. Temel çıkarımlar:

- Bir `OcrEngine` örneği oluşturun.  
- **OCR için görüntüyü ön işleme** için `DeskewFilter` ve `DenoiseGaussianFilter` gibi filtreler kullanın.  
- **OCR için görüntü yükleme** için `ImageStream.FromFile` kullanın.  
- `Recognize` metodunu çağırın ve `ocrResult.Text` ile **jpg'den metin çıkarma** işlemini tamamlayın.

Daha ileri gitmek ister misiniz? Şu fikirleri deneyin:

- **Toplu işleme** – bir klasördeki JPEG'leri okuyup her bir sonucu ayrı bir `.txt` dosyasına yazın.  
- **Azure Blob Storage entegrasyonu** – buluttan resimleri alıp OCR çalıştırın, ardından metni geri depolayın.  
- **NLP ile birleştirme** – çıkarılan metni bir dil‑anlama modeline besleyerek faturaları otomatik sınıflandırın.  

Farklı filtre kombinasyonları, dil paketleri ya da PNG ve TIFF gibi formatlarla denemeler yapmaktan çekinmeyin – aynı hat doğru bir şekilde **OCR için görüntü yükleme** yapıldığı sürece çalışır.

---

Herhangi bir sorunla karşılaşırsanız, aşağıya yorum bırakın ya da gelişmiş ayarlar için Aspose OCR dokümantasyonuna göz atın. İyi kodlamalar ve resimleri aranabilir metne dönüştürmenin tadını çıkarın!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}