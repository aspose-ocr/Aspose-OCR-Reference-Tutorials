---
category: general
date: 2025-12-29
description: Aspose OCR'yi kullanarak görüntü metnini dönüştürme ve Korece metni çıkarma.
  C#'ta metin görüntüsünü çıkarmak ve Korece metni tanımak için adım adım kılavuz.
draft: false
keywords:
- how to use aspose
- convert image text
- extract text image
- extract korean text
- recognize korean text
language: tr
og_description: Aspose OCR'yi kullanarak görüntü metnini dönüştürmeyi, Korece metni
  çıkarmayı ve resimlerden Korece metni tanımayı, eksiksiz bir C# örneğiyle öğrenin.
og_title: Aspose OCR Nasıl Kullanılır – C#'ta Korece Metin Tanıma
tags:
- Aspose
- OCR
- C#
- Image Processing
title: Aspose OCR'ı C#'da Nasıl Kullanılır – Görsellerden Korece Metin Tanıma
url: /tr/net/text-recognition/how-to-use-aspose-ocr-in-c-recognize-korean-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR'i C#'ta Nasıl Kullanılır – Görüntülerden Korece Metin Tanıma

Hiç **Aspose'u** bir fotoğraftan Korece karakterleri çıkarmak için nasıl kullanacağınızı merak ettiniz mi? Belki bir sokak işaretinin ekran görüntüsü, taranmış bir fiş ya da bir memeyi aranabilir metne dönüştürmeniz gerekiyor. İyi haber şu ki Aspose OCR bu işi çocuk oyuncağı haline getiriyor ve düşük seviyeli görüntü işleme püf noktalarıyla uğraşmanıza gerek kalmıyor.

Bu öğreticide, **tam, çalıştırılabilir bir örnek** üzerinden **görüntü metnini dönüştürme**, **metin görüntüsü çıkarma** ve özellikle **Korece metin çıkarma** işlemlerini Aspose OCR kütüphanesiyle nasıl yapacağınızı adım adım göstereceğiz. Sonunda tanınan Korece dizeyi konsola yazdıran bir uygulamanız olacak ve her satırın neden önemli olduğunu anlayacaksınız.

## Gereksinimler

- **.NET 6+** (herhangi bir yeni .NET SDK – Visual Studio, Rider veya `dotnet` CLI – çalışır)
- **Aspose.OCR for .NET** NuGet paketi  
  ```bash
  dotnet add package Aspose.OCR
  ```
- Korece karakterler içeren bir görüntü dosyası (ör. `korean_sign.jpg`).  
- Biraz C# bilgisi – daha önce “Hello World” yazdıysanız yeterli.

> **Pro ipucu:** Aspose OCR kutudan çıktığı haliyle 50'den fazla dili destekler. Biz, Hangul alfabesi genellikle genel OCR motorlarını zorladığı için Korece’ye odaklanacağız.

## Adım 1 – Aspose OCR'i Yükleyin ve Referans Verin

İlk olarak kütüphaneyi projenize ekleyin. Yukarıdaki NuGet komutu işi halleder, ancak UI üzerinden tercih ederseniz NuGet Package Manager’da *Aspose.OCR* araması yapabilirsiniz.

```csharp
// No code needed here – the package reference is enough.
// The using directives below will bring the types into scope.
using Aspose.OCR;
using Aspose.OCR.Models;
```

> **Neden önemli:** `using` ifadeleri `OcrEngine`, `Language` ve `Image` yardımcı sınıfına erişim sağlar. Bunlar olmadan derleyici bilinmeyen tipler hakkında şikayet eder.

## Adım 2 – İşlemek İstediğiniz Görüntüyü Yükleyin

Aspose OCR, JPEG, PNG, BMP ve birçok başka formatı okuyabilen kendi `Image` sarmalayıcısı ile çalışır. Korece metni içeren dosyayı ona gösterin.

```csharp
// Step 2: Load the image containing Korean characters
var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
var image = Image.Load(imagePath);
```

Dosya çalıştırılabilir dosyanızla aynı klasörde değilse yolu ona göre ayarlayın. `Image.Load` çağrısı **görüntü metnini** OCR motorunun anlayabileceği iç temsil biçimine **dönüştürür**.

![how to use aspose OCR example](/images/aspose-ocr-korean.png "how to use aspose OCR to recognize Korean text")

*Görsel alt metni: “Korece bir sokak işareti gösteren aspose OCR örneği.”*

## Adım 3 – OCR Motorunu Korece İçin Yapılandırın

Motorun hangi dili arayacağını bilmesi gerekir; aksi takdirde varsayılan olarak İngilizceyi kullanır ve Hangul karakterlerini kaçırır.

```csharp
// Step 3: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // Tell Aspose we want to recognize Korean (Hangul)
    Language = Language.Korean
};
```

> **Neden önemli:** `Language = Language.Korean` ayarı, motorun Korece dil paketini yüklemesini sağlar ve Hangul karakterleri için doğruluğu büyük ölçüde artırır. Bu adımı atlamak genellikle bozuk çıktıya yol açar.

## Adım 4 – Tanıma İşlemini Çalıştırın

Şimdi Aspose’dan görüntüyü okumasını isteyelim. `Recognize` metodu, çıkarılan dizeyi ve güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Step 4: Run OCR on the loaded image
OcrResult ocrResult = ocrEngine.Recognize(image);
```

Eğer daha büyük bir fotoğraftan **metin görüntüsü çıkarma** ihtiyacınız varsa (ör. birden fazla UI öğesi içeren bir ekran görüntüsü), `Recognize` çağrısından önce `image.Crop(...)` ile ilgi alanını kırpabilirsiniz. Bu, sadece resmin belirli bir kısmıyla ilgilendiğinizde işe yarayan pratik bir hiledir.

## Adım 5 – Tanınan Korece Metni Çıktılayın

Son olarak sonucu gösterin. Gerçek bir uygulamada bunu bir veritabanına kaydedebilir ya da bir çeviri API’sine gönderebilirsiniz, ancak bu öğreticide bir konsol çıktısı işleri basit tutar.

```csharp
// Step 5: Print the recognized Korean text
Console.WriteLine("Recognized Korean text:");
Console.WriteLine(ocrResult.Text);
```

### Beklenen Çıktı

```
Recognized Korean text:
서울특별시 강남구 테헤란로 123
```

Gerçek çıktınız elbette `korean_sign.jpg` içinde bulunan Korece karakterlere göre değişecektir.

## Tam Çalışan Örnek

Aşağıda **tam program** yer alıyor; yeni bir konsol projesine (`dotnet new console`) kopyalayıp yapıştırabilirsiniz. Görüntü dosyasının derlenmiş `.exe` ile aynı klasörde olduğundan emin olun ya da yolu ona göre ayarlayın.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;

class Program
{
    static void Main()
    {
        // 1️⃣ Install Aspose.OCR via NuGet before running this code.

        // 2️⃣ Load the image that contains Korean text.
        var imagePath = Path.Combine(Environment.CurrentDirectory, "korean_sign.jpg");
        var image = Image.Load(imagePath);

        // 3️⃣ Create the OCR engine and set it to recognize Korean.
        var ocrEngine = new OcrEngine
        {
            Language = Language.Korean   // 👈 This enables Hangul support.
        };

        // 4️⃣ Run the OCR process.
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // 5️⃣ Output the extracted Korean string.
        Console.WriteLine("Recognized Korean text:");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Programı `dotnet run` ile çalıştırın ve Korece karakterlerin konsolda belirdiğini izleyin.

## Yaygın Sorular & Kenar Durumları

### OCR bozuk karakterler döndürürse ne yapmalı?

- **Dil ayarını kontrol edin.** `Language.Korean` unutulması en sık yapılan hatadır.
- **Görüntü kalitesini artırın.** Daha net görüntüler, yüksek DPI ve doğru aydınlatma doğruluğu artırır.
- **Görüntüyü ön‑işleyin.** Aspose OCR, gürültülü taramaları temizleyebilen yerleşik filtreler (`image.Binarize()`, `image.Deskew()`) sunar.

### **görüntü metnini** toplu olarak **dönüştürmek** mümkün mü?

Kesinlikle. Yukarıdaki adımları bir klasördeki tüm görüntüler üzerinde dönen bir `foreach` döngüsü içine alabilirsiniz. İşte kısa bir örnek:

```csharp
foreach (var file in Directory.GetFiles(@"C:\KoreanImages", "*.jpg"))
{
    var img = Image.Load(file);
    var result = ocrEngine.Recognize(img);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), result.Text);
}
```

Bu betik **metin görüntüsü çıkarma** işlemini her dosya için yapar ve yanına bir `.txt` dosyası yazar.

### Aynı görüntüde birden fazla dili nasıl ele alırım?

Aspose OCR, `Language = Language.Auto` ayarlandığında dili otomatik algılayabilir. Ancak otomatik algılama daha yavaş olabilir ve tam dil belirtmeye göre biraz daha az doğru sonuç verir. Görüntünün hem Korece hem de İngilizce içerdiğini biliyorsanız, önce `Language.Korean`, ardından `Language.English` ile iki geçiş yapıp sonuçları birleştirebilirsiniz.

## Üretim‑Hazır OCR İçin İpuçları

- **OcrEngine’i önbellekle.** Her istek için yeni bir motor oluşturmak ek yük getirir. Çok sayıda görüntü işliyorsanız bir singleton tutun.
- **Görüntü boyutunu sınırlayın.** Büyük görüntüler bellek tüketir; motoru beslemeden önce genişliği ~1500 px olacak şekilde küçültün.
- **İstisnaları yakalayın.** `Recognize` çağrısını bir try/catch bloğuna sararak bozuk dosyalarla zarif bir şekilde başa çıkın.

## Sonuç

**Aspose’u** **görüntü metnini dönüştürmek**, **metin görüntüsü çıkarmak** ve özellikle **Korece metin çıkarmak** için birkaç satır C# kodu ile nasıl kullanacağınızı ele aldık. Adımlar şu şekilde:

1. Aspose OCR’i kurun.  
2. Görüntünüzü yükleyin.  
3. Motoru Korece için yapılandırın.  
4. `Recognize` metodunu çalıştırın.  
5. Sonucu çıktılayın.

Şimdi bu kod parçacığını toplu işleme, belge arşivleme ya da gerçek‑zaman çeviri uygulamaları gibi daha büyük iş akışlarına entegre edebilirsiniz. Daha ileri gitmek ister misiniz? Aspose’un `Image.Preprocess()` metodlarını deneyin, farklı dillerle oynayın ya da çıktıyı Azure Cognitive Services ile çeviri için birleştirin.

**Korece metin tanıma** ya da diğer Aspose özellikleri hakkında daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}