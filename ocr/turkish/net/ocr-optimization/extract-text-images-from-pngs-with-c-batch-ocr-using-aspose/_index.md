---
category: general
date: 2026-02-09
description: C# ile toplu OCR için maksimum paralellik ayarlayarak metin görüntülerini
  hızlıca çıkarın – taranmış sayfaları dönüştürmeyi öğrenin, birden fazla görüntü
  OCR'ını yönetin ve PNG metnini verimli bir şekilde okuyun.
draft: false
keywords:
- extract text images
- set max parallelism
- convert scanned pages
- multiple image ocr
- read png text
language: tr
og_description: Maksimum paralellik ayarlayarak C#'ta metin görüntülerini çıkarın.
  Bu öğreticide taranmış sayfaları nasıl dönüştüreceğiniz, birden fazla görüntü OCR'si
  çalıştıracağınız ve Aspose OCR ile PNG metnini okuyacağınız gösterilmektedir.
og_title: C# ile PNG'lerden metin görüntülerini çıkarma – Tam Batch OCR Kılavuzu
tags:
- OCR
- C#
- Aspose
- Batch Processing
title: C# ile PNG'lerden metin görüntülerini çıkarın – Aspose OCR kullanarak toplu
  OCR
url: /tr/net/ocr-optimization/extract-text-images-from-pngs-with-c-batch-ocr-using-aspose/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'lerden Metin Görüntülerini C# ile Çıkarma – Aspose OCR Kullanarak Toplu OCR

Hiç bir klasördeki taranmış PNG'lerden **metin görüntülerini** çıkarmanız gerekti, ancak “Bunu nasıl hızlı yaparım?” sorusunda takıldıysanız? Yalnız değilsiniz. Gerçek dünyadaki birçok projede, geliştiricilerin **maksimum paralellik ayarlaması** yapması gerekir, böylece onlarca sayfa saniyeler içinde, dakikalar yerine işlenir.

Bu rehberde, **taranmış sayfaları dönüştüren**, **çoklu görüntü OCR** çalıştıran ve sonunda **png metnini okuyan** eksiksiz, çalıştırılabilir bir örnek üzerinden adım adım ilerleyeceğiz. Belirsiz “belgelere bakın” bağlantıları yok—sadece kopyala‑yapıştırabileceğiniz kod, her satırın neden önemli olduğuna dair açıklamalar ve yaygın tuzaklardan kaçınmanız için ipuçları.

> **Pro ipucu:** Eğer başka bir yerde zaten Aspose OCR kullanıyorsanız, aynı `OcrEngine` sınıfının burada da göründüğünü fark edeceksiniz, ancak gerçek paralel işleme için yapılandırmasını biraz değiştireceğiz.

## Gerekenler

- **.NET 6+** (or .NET Framework 4.6+). API aynı şekilde çalışır, ancak daha yeni çalışma zamanları daha iyi iş parçacığı yönetimi sağlar.  
- **Aspose.OCR for .NET** – NuGet üzerinden kurun: `Install-Package Aspose.OCR`.  
- Birkaç PNG taraması içeren bir klasör (`page1.png`, `page2.png`, …).  
- Kendinizi rahat hissettiğiniz bir IDE veya editör (Visual Studio, Rider, VS Code…).

Hepsi bu. Ek hizmetler, bulut anahtarları yok, sadece saf yerel işleme.

## metin görüntülerini çıkar – Toplu OCR için Maksimum Paralellik Ayarlama

Birden fazla dosyada OCR başlattığınızda, motor varsayılan olarak tek bir iş parçacığı kullanır. Bu güvenli ama acı verici derecede yavaştır. `MaxDegreeOfParallelism` yapılandırarak motorun aynı anda kaç iş parçacığı oluşturabileceğini belirlersiniz.

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // 1️⃣ Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };
```

**Neden 4?**  
Dört, çoğu modern dizüstü bilgisayarda ideal bir noktadır—CPU'yu meşgul edecek kadar çekirdek, ancak diğer süreçleri aç bırakmayacak kadar az. Eğer bunu 16 çekirdekli bir sunucuda çalıştırıyorsanız, belirgin bir hız artışı için sayıyı 12 ya da 14'e çıkarın.

## Taranmış Sayfaları Dönüştür – Image Stream Koleksiyonunu Oluşturma

Aspose her görüntüyü bir `ImageStream` olarak bekler. `FromFile` yardımcı yöntemi dosyayı okur, bellekte tutar ve OCR motoruna verir. Görüntüleriniz bir veritabanından veya HTTP yanıtından geliyorsa `MemoryStream` de besleyebilirsiniz.

```csharp
        // 2️⃣ Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };
```

**Köşe durumu:** Eğer herhangi bir dosya eksik ya da bozuksa, `FromFile` bir `FileNotFoundException` fırlatır. Güvenilir olmayan giriş bekliyorsanız, oluşturmayı bir `try/catch` bloğuna sarın.

## çoklu görüntü ocr – Toplu OCR Gerçekleştirme

Şimdi asıl iş burada gerçekleşir. `RecognizeBatch`, daha önce ayarladığınız iş parçacığı sayısına kadar yeni iş parçacıkları oluşturur, her görüntüyü işler ve bir `OcrResult` nesnesi listesi döndürür.

```csharp
        // 3️⃣ Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);
```

Arka planda, her iş parçacığı kendi görüntüsünü yükler, sinir ağını çalıştırır ve düz metni çıkarır. Sonuçların sırası, giriş listesinin sırası ile eşleşir, böylece sayfa 1 → sonuç 0 gibi güvenle eşleştirme yapabilirsiniz.

## png metnini oku – Çıkarılan İçeriği Görüntüleme

Son olarak sonuçlar üzerinde döngü kurar ve düz metni konsola yazdırırız. Burada çıktıyı bir dosyaya, veritabanına ya da hatta bir sonraki NLP servisine yönlendirebilirsiniz.

```csharp
        // 4️⃣ Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

### Beklenen Konsol Çıktısı

```
--- Page 1 ---
This is the first scanned line of text.
Another line appears here.

--- Page 2 ---
Second page starts with a header.
More content follows…

--- Page 3 ---
Final page ends with a signature.
```

Eğer boş bölümler görürseniz, PNG'lerin tamamen beyaz görüntü olmadığından emin olun—OCR bir miktar kontrast gerektirir.

## Pratik İpuçları & Yaygın Tuzaklar

| Durum | Ne Yapmalı |
|-----------|------------|
| Büyük toplularda **bellek baskısı** | Görüntüleri 10‑20 dosya grupları halinde işleyin, ardından artış fark ederseniz `GC.Collect()` çağırın. |
| **Yanlış dil algılama** | `RecognizeBatch` çağırmadan önce `ocrEngine.Configuration.Language = OcrLanguage.English;` (veya hedef dilinizi) ayarlayın. |
| **Paralellik olmasına rağmen yavaş performans** | SSD'nizin I/O'yu kısıtlamadığından emin olun; tüm dosyaları önce belleğe okuyun (biz `ImageStream.FromFile` ile yaptığımız gibi). |
| **Eksik karakterler** | Daha yüksek çözünürlük için `ocrEngine.Configuration.DPI = 300;` değerini artırın. |

## Örneği Genişletmek – PNG'den PDF veya DOCX'e

Eğer sonunda **taranmış sayfaları** aranabilir PDF'lere dönüştürmeniz gerekirse, aynı `ocrResults[i].PlainText` değerini bir PDF kütüphanesine (ör. Aspose.PDF) besleyin ve metni görünmez bir katman olarak üstüne yerleştirin. Aynı paralellik yöntemi orada da çalışır.

## Tam Kaynak Kodu (Kopyala‑Yapıştır Hazır)

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
using Aspose.OCR.Models;

class BatchExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine and allow up to 4 parallel threads
        var ocrEngine = new OcrEngine
        {
            Configuration = { MaxDegreeOfParallelism = 4 }
        };

        // Step 2: Build a collection of image streams to be processed
        List<ImageStream> imageStreams = new List<ImageStream>
        {
            ImageStream.FromFile(@"YOUR_DIRECTORY/page1.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page2.png"),
            ImageStream.FromFile(@"YOUR_DIRECTORY/page3.png")
        };

        // Step 3: Perform batch OCR on the prepared images
        IList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // Step 4: Display the extracted text for each page
        for (int i = 0; i < ocrResults.Count; i++)
        {
            Console.WriteLine($"--- Page {i + 1} ---");
            Console.WriteLine(ocrResults[i].PlainText);
        }
    }
}
```

Bunu `BatchExample.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolunuzun, o PNG taramalarının içinde gizli olan metinle dolduğunu izleyin.

## Görsel Özet

![metin görüntülerini çıkar örneği](images/ocr-batch.png){alt="metin görüntülerini çıkar örneği"}

Diagram akışı gösterir: **PNG dosyaları → ImageStream koleksiyonu → OcrEngine (maksimum paralellik) → OCR sonuçları → Konsol / sonraki depolama**.

## Sonuç

Artık C#'ta **metin görüntülerini çıkarmak**, **maksimum paralellik ayarlamak**, **taranmış sayfaları dönüştürmek**, **çoklu görüntü OCR** işlemek ve **png metnini** verimli bir şekilde okumak için sağlam, uçtan uca bir tarifiniz var. Kod kendi içinde bağımsız, açıklamalar “nasıl” ve “neden”i kapsıyor ve ipuçları sizi yaygın baş ağrılarından koruyor.

Sırada ne var? PNG listesini dinamik bir `Directory.GetFiles` döngüsüyle değiştirin, farklı iş parçacığı sayılarıyla deney yapın veya çıktıyı aranabilir bir PDF'ye besleyin. Aynı desen, fazladan neredeyse bir satır kod eklemeden yüzlerce sayfaya ölçeklenebilir.

Sorularınız veya zor bir köşe durumu mı var? Aşağıya bir yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}