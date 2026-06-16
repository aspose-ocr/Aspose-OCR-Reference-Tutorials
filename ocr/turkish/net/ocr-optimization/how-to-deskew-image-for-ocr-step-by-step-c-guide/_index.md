---
category: general
date: 2026-03-04
description: Görüntüyü eğriltme düzeltmeyi ve kontrast ayarlarıyla OCR doğruluğunu
  artırarak, OCR için görüntüyü iyileştirip metni tanımayı öğrenin.
draft: false
keywords:
- how to deskew image
- recognize text from image
- how to apply contrast
- improve OCR accuracy
- enhance image for OCR
language: tr
og_description: Görüntüyü düzeltme ve OCR sonuçlarını artırma. Kontrastı nasıl uygulayacağınızı
  öğrenin, OCR doğruluğunu geliştirin ve yeniden kullanılabilir akışlarla görüntüden
  metin tanıyın.
og_title: Görüntüyü Nasıl Düzeltiriz – Tam C# OCR Öğreticisi
tags:
- OCR
- C#
- image‑processing
title: OCR için Görüntüyü Düzeltme – Adım Adım C# Rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-for-ocr-step-by-step-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Düzleştirme – Tam C# OCR Öğreticisi

Hiç **görüntüyü nasıl düzleştireceğinizi** merak ettiniz mi, böylece OCR motorunuz gerçekten metni okuyabilsin? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—taratılmış makbuzlar, fotoğraflanmış sözleşmeler veya telefon kamerasından çekilmiş bulanık makbuzlar—resim tam olarak dik değildir. Eğik bir sayfa karakter tanıyıcıyı yanıltır ve sonuç anlamsız bir karışıma dönüşür.

İyi haber? Görüntüyü düzleştirerek **ve** kontrastı ayarlayarak **OCR doğruluğunu büyük ölçüde artırabilirsiniz**. Bu öğreticide, bir görüntüye düzleştirme filtresi ve kontrast artırımı uyguladıktan sonra **görüntüden metin tanıma** işlemini nasıl yapacağınızı gösteren eksiksiz bir C# örneği üzerinden adım adım ilerleyeceğiz. Ayrıca **kontrastı nasıl uygulayacağınızı** doğru şekilde açıklayacak, kenar durumlarını tartışacak ve herhangi bir projeye ekleyebileceğiniz yeniden kullanılabilir bir pipeline sunacağız.

## Bu Kılavuzdan Ne Öğreneceksiniz

- Düzleştirmenin ve kontrastın OCR için neden önemli olduğuna dair net bir açıklama.
- Bir filtre pipeline’ı oluşturup bir OCR motoruna bağlayan ve birden fazla resmi okuyan çalıştırılabilir bir C# kod örneği.
- Aynı pipeline’ı birçok dosya için yeniden kullanma, hata durumlarını yönetme ve doğruluk artışını ölçme ipuçları.
- Görüntü ikilileştirme, gürültü giderme ve çok‑dilli OCR gibi ilgili konulara yönlendiren bağlantılar (sayfadan ayrılmadan).

**Önkoşullar** – .NET 6+ ortamına, bir filtre pipeline’ını destekleyen bir OCR kütüphanesine (ör. Tesseract‑.NET, IronOCR veya herhangi bir ticari SDK) ve birkaç örnek PNG dosyasına ihtiyacınız var. Harici hizmetler gerekli değil.

---

## Adım 1 – Neden Düzleştirme İlk Yapılması Gereken Şey

Taralı bir sayfa birkaç derece bile döndürülmüşse, OCR motoru her satırın taban çizgisini bir açıyla görür. Çoğu tanıyıcı yatay metin varsayar; herhangi bir sapma güven puanlarını düşürür ve ikame hatalarına yol açar.

> **Pro ipucu:** Mümkünse, resmi düz bir yüzeyde ve iyi aydınlatmayla çekin; yazılım düzeltmeleri iyi veriyi tamamen yerine koyamaz.

Kod açısından, “görüntüyü nasıl düzleştireceğiniz” genellikle baskın metin satırı yönelimini tespit edip bitmap’i 0°'ye geri döndürmek anlamına gelir. Çoğu OCR SDK'sı bunu otomatik yapan bir `DeskewFilter` sunar.

```csharp
// Create a deskew filter – it analyses the image and rotates it back.
var deskew = new DeskewFilter();
```

Filtre, sayfanın arka plandan çok daha fazla metin içerdiği varsayımına dayanır; bu, çoğu belge için doğrudur. Çok fazla boşluk içeren bir fotoğrafınız varsa, bir yedek algoritma gerekebilir—ancak çoğu taranmış PDF için varsayılan yeterlidir.

---

## Adım 2 – Karakterleri Öne Çıkaracak Şekilde Kontrastı Artırma

Kontrast, en karanlık ve en açık pikseller arasındaki farktır. Düşük‑kontrast taramalar soluk görünür ve OCR motoru bir karakterin nerede başladığını ya da bittiğini ayırt edemez. Kontrastı artırarak görsel ayrımı “keskinleştirir”, bu da **OCR doğruluğunu artırır**.

```csharp
// Set the contrast level – 1.0 is neutral, >1.0 brightens the darks and whites.
var contrast = new ContrastFilter { Level = 1.2 };
```

Neden 1.2? Pratikte mütevazı bir artış (%10‑30) yeterlidir. Çok fazla artırırsanız ince fontlardaki ince detayları kaybedersiniz. Denemekten çekinmeyin; daha sonra bütün uygulamayı yeniden derlemeden seviyeyi ayarlamanızı sağlayan bir pipeline oluşturacağız.

---

## Adım 3 – Yeniden Kullanılabilir Bir Filtre Pipeline’ı Oluşturma

Şimdi iki filtreyi tek bir pipeline’da birleştiriyoruz. Böylece **görüntüden metin tanıma** her seferinde aynı ön‑işleme adımlarını izler ve tutarlı sonuçlar elde edilir.

```csharp
using YourOcrLibrary;          // Replace with the actual namespace of your OCR SDK
using YourOcrLibrary.Filters; // Namespace where DeskewFilter & ContrastFilter live

// Step 3: Build a filter pipeline that deskews the image and enhances contrast
var filterPipeline = new FilterBuilder()
    .Add(new DeskewFilter())                 // First: straighten the page
    .Add(new ContrastFilter { Level = 1.2 }) // Then: make the text pop
    .Build();
```

**Neden bir pipeline?**  
- **Modülerlik:** OCR çağrısına dokunmadan filtre ekleyip çıkarabilirsiniz.  
- **Performans:** Kütüphane işlemleri toplu hâle getirebilir, bellek tüketimini azaltır.  
- **Yeniden Kullanılabilirlik:** Aynı pipeline’ı birden çok `engine.Recognize` çağrısına bağlayabilirsiniz.

---

## Adım 4 – Pipeline’ı OCR Motoruna Bağlama

Çoğu OCR motoru bir `Filters` özelliği ya da `SetFilters` metodu sunar. Pipeline’ı burada atadığınızda, sonraki her görüntü karakter analizine başlamadan önce düzleştirme + kontrast adımlarından geçer.

```csharp
// Step 4: Attach the pipeline to the OCR engine so it processes images using these filters
var engine = new OcrEngine(); // Instantiate your OCR engine (configure language, etc.)
engine.Filters = filterPipeline;
```

Dil modelini (ör. English → Spanish) değiştirmeniz gerekiyorsa, filtreleri **bağlamadan önce** yapabilirsiniz; ön‑işleme aşaması için sıra önemli değildir.

---

## Adım 5 – İlk Görüntüden Metin Tanıma

Pipeline’ı çalıştıralım. Bir PNG yükleyecek, OCR’u çalıştıracak ve sonucu yazdıracağız. Aynı `engine` örneğini kullandığımıza dikkat edin—filtreleri yeniden oluşturmanıza gerek yok.

```csharp
// Step 5: Recognize text from the first image using the configured engine
var firstImagePath = @"C:\Images\doc1.png";
var firstResult = engine.Recognize(ImageInfo.Load(firstImagePath));

Console.WriteLine("=== First Document ===");
Console.WriteLine(firstResult.Text);
```

**Görmeniz gereken:** Ham bir taramaya göre çok daha az bozuk karakter içeren, düzgün yönlendirilmiş temiz metin. Hâlâ hatalar görüyorsanız, kontrast adımından sonra bir `BinarizeFilter` (siyah‑beyaz dönüşüm) eklemeyi düşünün.

---

## Adım 6 – Aynı Pipeline’ı Ek Dosyalar İçin Yeniden Kullanma

Filtre pipeline’ının en büyük avantajlarından biri, ekstra yük olmadan onlarca dosya arasında yeniden kullanılabilmesidir.

```csharp
// Step 6: Recognize text from a second image to demonstrate reuse of the same pipeline
var secondImagePath = @"C:\Images\doc2.png";
var secondResult = engine.Recognize(ImageInfo.Load(secondImagePath));

Console.WriteLine("\n=== Second Document ===");
Console.WriteLine(secondResult.Text);
```

Taralı PDF’lerle dolu bir klasörünüz varsa, sadece `Directory.GetFiles(...)` üzerinden döngü kurup her seferinde `engine.Recognize` çağırın. Düzleştirme ve kontrast adımları tutarlı kalır; bu da toplu işlerde **OCR için görüntüyü iyileştirme** anahtarıdır.

---

## Tam Çalışan Örnek – Hepsini Bir Araya Getirin

Aşağıda eksiksiz, bağımsız bir program yer alıyor. Yeni bir console projesine kopyalayıp yapıştırın, OCR SDK’nız için uygun NuGet paketini ekleyin ve çalıştırın. İki örnek görüntü için tanınan metni çıktılar.

```csharp
// ------------------------------------------------------------
// Complete C# OCR Example – Deskew + Contrast Pipeline
// ------------------------------------------------------------
using System;
using System.IO;
using YourOcrLibrary;          // e.g., IronOcr, Tesseract.NET, etc.
using YourOcrLibrary.Filters; // Filters live here

class Program
{
    static void Main()
    {
        // 1️⃣ Build the filter pipeline (deskew + contrast)
        var filterPipeline = new FilterBuilder()
            .Add(new DeskewFilter())                 // Straighten the page
            .Add(new ContrastFilter { Level = 1.2 }) // Boost contrast a bit
            .Build();

        // 2️⃣ Create and configure the OCR engine
        var engine = new OcrEngine
        {
            // Example: set language to English (adjust as needed)
            Language = OcrLanguage.English,
            Filters = filterPipeline
        };

        // 3️⃣ Define image paths (replace with your own)
        string[] imagePaths = {
            @"C:\Images\doc1.png",
            @"C:\Images\doc2.png"
        };

        // 4️⃣ Process each image
        foreach (var path in imagePaths)
        {
            if (!File.Exists(path))
            {
                Console.WriteLine($"⚠️ File not found: {path}");
                continue;
            }

            var result = engine.Recognize(ImageInfo.Load(path));

            Console.WriteLine($"\n=== {Path.GetFileName(path)} ===");
            Console.WriteLine(result.Text);
        }

        Console.WriteLine("\n✅ All done – you have successfully deskewed and enhanced contrast for OCR!");
    }
}
```

### Beklenen Çıktı

```
=== doc1.png ===
Invoice #12345
Date: 2024‑02‑15
Total: $1,250.00
...

=== doc2.png ===
Meeting Minutes
1. Project kickoff...
2. Budget approval...
...
```

Bu çıktıyı **filtre pipeline’ı olmadan** bir çalıştırma ile karşılaştırırsanız, eksik karakterler, yanlış yerleştirilmiş sayılar veya tamamen karışık satırlar göreceksiniz. Bu, **görüntüyü nasıl düzleştireceğinizi** ve **kontrastı nasıl doğru uygulayacağınızı** öğrenmenin ölçülebilir etkisidir.

---

## Yaygın Sorular & Kenar Durumları

| Soru | Cevap |
|----------|--------|
| *Görüntü zaten dik ise ne olur?* | `DeskewFilter` 0° rotasyon tespit eder ve orijinal bitmap’i döndürür, dolayısıyla neredeyse hiç ek yük oluşturmaz. |
| *Bunu PDF’lerle kullanabilir miyim?* | Evet. Çoğu OCR SDK’sı bir PDF sayfasını `ImageInfo` olarak yüklemenize izin verir. Aynı pipeline, bitmap aynı şekilde işlendiği için çalışır. |
| *Belgelerimde renkli metin var—kontrast renkleri bozar mı?* | Kontrast filtresi parlaklık üzerinde çalışır, renkler korunur ancak daha ayırt edilebilir hâle gelir. Saf siyah‑beyaz isterseniz, kontrast adımından sonra bir `BinarizeFilter` ekleyin. |
| *Doğruluk artışını nasıl ölçebilirim?* | Pipeline öncesi ve sonrası aynı test seti üzerinde OCR çalıştırın, ardından karakter hata oranını (CER) ya da kelime hata oranını (WER) hesaplayın. Genellikle %10‑30 hata düşüşü görürsünüz. |
| *Performans maliyeti nedir?* | Düzleştirme küçük bir CPU maliyeti ekler (genellikle sayfa başına < 100 ms). Kontrast ise basit bir piksel‑bazlı işlemdir; genel etki OCR adımına kıyasla çok düşüktür. |

---

## Sonraki Adımlar – OCR’unuzu Bir Üst Seviyeye Taşıyın

Artık **görüntüyü nasıl düzleştireceğinizi**, **kontrastı nasıl uygulayacağınızı** ve yeniden kullanılabilir bir pipeline ile **görüntüden metin tanıma** yapabildiğinize göre, aşağıdaki ilgili konuları keşfetmeyi düşünün:

- **Gürültü azaltma** – düzleştirmeden önce bir `MedianFilter` ekleyerek lekeleri temizleyin.  
- **İkilileştirme** – karmaşık yazı sistemleri için saf siyah‑beyaz dönüşüm.  
- **Çok‑sayfa işleme** – PDF sayfaları üzerinden döngü kurup sonuçları aranabilir bir indeksde saklayın.  
- **Dil modelleri** – `OcrLanguage.English` ve `OcrLanguage.French` arasında anlık geçiş yapın.  
- **Son‑işleme** – yaygın OCR hatalarını (ör. “0” vs “O”) düzeltmek için yazım denetimi veya regex kullanın.

Bu adımlar aynı `FilterBuilder` zincirine eklenebilir, böylece **OCR için görüntüyü iyileştirme** ihtiyacını karşılayan modüler, sürdürülebilir bir çözüm elde edersiniz.

---

## Sonuç

**Görüntüyü nasıl düzleştireceğinizi**, kontrast ayarlamanın **OCR doğruluğunu artırmadaki** etkisini ve temiz, yeniden kullanılabilir bir pipeline ile **görüntüden metin tanıma** işlemini nasıl yapacağınızı kapsamlı bir şekilde ele aldık.

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}