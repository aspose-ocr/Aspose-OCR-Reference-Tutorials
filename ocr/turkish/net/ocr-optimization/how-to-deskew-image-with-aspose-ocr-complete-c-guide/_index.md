---
category: general
date: 2026-04-03
description: Aspose OCR ile C#’ta görüntüyü eğriltme düzeltme (deskew) nasıl yapılır
  – OCR için görüntüyü ön işleme, görüntüden metin tanıma ve dakikalar içinde OCR
  doğruluğunu artırmayı öğrenin.
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- recognize text from image
- improve ocr accuracy
- load image for ocr
language: tr
og_description: C# ile Aspose OCR kullanarak görüntüyü eğrilikten düzeltme. Bu rehber,
  OCR için görüntüyü ön işleme, görüntüden metin tanıma ve doğruluğu artırma yöntemlerini
  gösterir.
og_title: Aspose OCR ile Görüntüyü Düzeltme – Tam C# Rehberi
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Aspose OCR ile Görüntüyü Düzleştirme – Tam C# Rehberi
url: /tr/net/ocr-optimization/how-to-deskew-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Görüntüyü Düzeltme – Tam C# Kılavuzu

Bir OCR motoruna vermeden önce **görüntüyü nasıl düzeltir** (deskew) merak ettiniz mi? Tek başınıza değilsiniz—eğik taramalar, açıyla çekilmiş fotoğraflar veya hafifçe yamuk PDF'ler bile herhangi bir metin‑tanıma kütüphanesini şaşırtabilir.  

Bu adım‑adım öğreticide tüm iş akışını inceleyeceğiz: resmi yüklemekten, **OCR için görüntüyü ön işleme** (düzeltme, gürültü azaltma, kontrast artırma, otomatik döndürme) aşamasına, **Aspose OCR ile görüntüden metin tanıma** aşamasına ve son olarak **OCR doğruluğunu artırma** ipuçlarına kadar. Sonunda, gürültülü, eğik bir PNG'yi profesyonelce işleyen çalıştırılabilir bir C# konsol uygulamanız olacak.

## Gereksinimler

- **.NET 6+** (veya .NET Framework 4.7.2 – API aynı şekilde çalışır)
- **Aspose.OCR for .NET** NuGet paketi (`Install-Package Aspose.OCR`)
- **Eğik** ve **gürültülü** bir örnek resim (ör. `skewed_noisy.png`)
- Visual Studio, Rider veya tercih ettiğiniz herhangi bir editör – özel bir araç gerekmez

> **Pro ipucu:** Eğik bir örnek yoksa, temiz bir ekran görüntüsünü Paint'te 10‑15° döndürün ve bir görüntü düzenleyiciyle biraz “tuz‑ve‑karabiber” gürültüsü ekleyin. Kod aynı şekilde çalışır.

Şimdi, derinlemesine inceleyelim.

## Görüntüyü Düzeltme ve OCR Doğruluğunu Artırma

İlk yapmanız gereken, Aspose’ın `OcrEngine`'ine gelen bitmap'i **düzelt** (deskew) demektir. Motor, aynı anda birden fazla kalite artırıcı özelliği açıp kapatmanızı sağlayan yerleşik bir `ImagePreprocessingOptions` sınıfı ile birlikte gelir.

```csharp
using Aspose.OCR;
using System.Drawing;

/// <summary>
/// Demonstrates how to deskew image, denoise, boost contrast, and run OCR.
/// </summary>
class PreprocessDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Configure preprocessing options
        ImagePreprocessingOptions opts = new ImagePreprocessingOptions
        {
            Deskew = true,          // <-- this is the key to how to deskew image
            Denoise = true,
            ContrastBoost = 30,    // increase contrast by 30 %
            AutoRotate = true
        };
        ocrEngine.PreprocessingOptions = opts;

        // 3️⃣ Load the image you want to process
        Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png");

        // 4️⃣ Run OCR on the pre‑processed bitmap
        string text = ocrEngine.Recognize(input);

        // 5️⃣ Show the result
        System.Console.WriteLine(text);
    }
}
```

### Neden Bu Çalışıyor

- **Deskew = true** motorun metin taban çizgisini algılayıp görüntüyü taban çizgisi yatay olana kadar döndürmesini sağlar. Bu olmadan, sadece 5° eğim bile doğruluğu %15‑20 azaltabilir.
- **Denoise** düşük çözünürlüklü belgeleri taradıktan sonra sıkça görülen rastgele lekeleri temizler.
- **ContrastBoost** ön plan (metin) ile arka plan (kağıt) arasındaki farkı artırır; bu **OCR doğruluğunu artırma** için çok önemlidir.
- **AutoRotate** dikey ve yatay yönleri otomatik olarak algılar, manuel kontrol ihtiyacını ortadan kaldırır.

Yukarıdaki kod **tam, çalıştırılabilir bir örnek** – sadece `YOUR_DIRECTORY` kısmını dosyanızın yolu ile değiştirin ve F5'e basın.

## OCR İçin Görüntüyü Ön İşleme – Gürültü Azaltma ve Kontrast Artırma

Hem gürültü azaltma hem de kontrast iyileştirme gerçekten gerekli mi diye merak edebilirsiniz. Kısa cevap: **evet, çoğu gerçek‑dünya senaryosunda**. İşte hızlı bir özet:

| Özellik | Ne işe yarar | Ne zaman önemlidir |
|---------|--------------|--------------------|
| **Deskew** | Eğik metin satırlarını düzeltir | Tarama formları, telefon‑kamerası çekimleri |
| **Denoise** | İzole pikselleri kaldırır | Düşük ışıkta taramalar, ucuz tarayıcılar |
| **ContrastBoost** | Koyu metni aydınlatır, arka planı karartır | Solmuş belgeler, solmuş mürekkep |
| **AutoRotate** | Dikey ve yatay yönü algılar | Karışık yönlendirmeli çok sayfalı PDF'ler |

Temiz, tamamen hizalanmış bir tarama işliyorsanız bayrakları kapatabilirsiniz, ancak **OCR için görüntüyü ön işleme** nadiren zarar veren güvenli bir varsayılandır.

## Görüntüden Metin Tanıma – Aspose OCR Kullanarak

Ön işleme hattı tamamlandığında motor, temizlenmiş bitmap'i dahili tanıyıcıya verir. `Recognize` metodu satır sonlarını koruyan düz bir `string` döndürür. Gerekirse sonucu daha da işleyebilirsiniz (ör. boşlukları kırpma, imla denetimi).

```csharp
string recognizedText = ocrEngine.Recognize(inputImage);
Console.WriteLine("--- OCR RESULT ---");
Console.WriteLine(recognizedText);
```

### Beklenen Çıktı

`skewed_noisy.png` içinde “Hello World!” ifadesi varsa, konsol şu şekilde bir çıktı verir:

```
--- OCR RESULT ---
Hello World!
```

Orta seviyede gürültü olsa bile, etkinleştirdiğimiz ön işleme adımları sayesinde **%95’in üzerinde doğruluk** elde etmelisiniz.

## OCR İçin Görüntü Yükleme – Dosya İşleme İpuçları

`Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png")` satırı **OCR için görüntü yüklemenin** en basit yoludur, ancak birkaç önemli ayrıntı vardır:

1. **Dosya kilitleri** – `FromFile` dosya tutamacını `Image` nesnesi dispose edilene kadar açık tutar. Dosyayı daha sonra silmeyi veya taşımayı planlıyorsanız bir `using` bloğu içinde kullanın.
2. **Desteklenen formatlar** – Aspose OCR BMP, JPEG, PNG, TIFF ve GIF formatlarını kabul eder. PDF'leriniz varsa, önce her sayfayı bir görüntüye dönüştürün (Aspose.PDF yardımcı olabilir).
3. **Bellek kullanımı** – Büyük görüntüler (5 MP üzeri) önemli miktarda RAM tüketebilir. `OutOfMemoryException` ile karşılaşırsanız, motorun önüne geçmeden önce `Bitmap` ile küçültmeyi düşünün.

```csharp
using (Image input = Image.FromFile(@"YOUR_DIRECTORY/skewed_noisy.png"))
{
    string result = ocrEngine.Recognize(input);
    Console.WriteLine(result);
}
```

## OCR Doğruluğunu Artırma – Gerçek Dünya İpuçları

Otomatik ön işleme rağmen bazı uç durumlar OCR motorlarını zorlayabilir. İş akışınıza ekleyebileceğiniz kanıtlanmış stratejiler şunlardır:

- **Görüntüyü ikilileştir** (`opts.Binarization = true`) arka plan düzensiz olduğunda.
- **Dili ayarla** (`ocrEngine.Language = Language.English`) karakter kümesini sınırlamak için.
- **DPI artır**: Tarama sürecini kontrol ediyorsanız en az 300 dpi hedefleyin.
- **Kenarları kırp**: Büyük beyaz kenarları kaldırın; bunlar satır algılamasını karıştırabilir.
- **Çıktıyı doğrula**: Tarih, sayı veya bilinen desenleri kontrol etmek için düzenli ifadeler kullanın, ardından düşük güvenilirlikli satırları manuel inceleme için işaretleyin.

> **Unutmayın:** Hedef sadece **görüntüden metin tanımak** değil, çeşitli belge kalitelerinde güvenilir bir şekilde yapabilmektir.

## Tam Çalışan Örnek – Tüm Adımlar Tek Dosyada

Aşağıda yeni bir konsol projesine kopyalayıp yapıştırabileceğiniz, bağımsız bir program yer alıyor.

```csharp
using Aspose.OCR;
using System;
using System.Drawing;

class DeskewOcrDemo
{
    static void Main()
    {
        // Create OCR engine
        OcrEngine engine = new OcrEngine();

        // Preprocess settings (deskew, denoise, contrast, auto‑rotate)
        engine.PreprocessingOptions = new ImagePreprocessingOptions
        {
            Deskew = true,
            Denoise = true,
            ContrastBoost = 30,
            AutoRotate = true
        };

        // Load image – make sure the path is correct
        const string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";

        // Using block prevents file‑handle leaks
        using (Image img = Image.FromFile(imagePath))
        {
            // Run OCR
            string text = engine.Recognize(img);

            // Output result
            Console.WriteLine("--- OCR RESULT ---");
            Console.WriteLine(text);
        }
    }
}
```

Programı çalıştırın, temizlenmiş ve düzeltilmiş metnin konsola yazdırıldığını göreceksiniz. `skewed_noisy.png` dosyasını temiz, düz bir tarama ile değiştirirseniz çıktı aynı olur—sadece motor düzeltme adımını atladığı için ufak bir performans artışı elde edersiniz.

## Sonuç

**Aspose OCR ile görüntüyü nasıl düzeltir** (deskew) konusunu ele aldık, **OCR için görüntüyü ön işleme** yöntemini gösterdik, **OCR için görüntü yükleme** yolunu doğru bir şekilde uyguladık ve sonunda **görüntüden metin tanıma** yaparken **OCR doğruluğunu artırma** üzerine odaklandık. Tam kod parçacığı herhangi bir .NET projesine eklenmeye hazır ve ek ipuçları daha zor girdilerle başa çıkmanız için bir yol haritası sunuyor.

Bir sonraki meydan okumaya hazır mısınız? Birden fazla görüntüyü zincirleyerek çok‑sayfalı bir OCR iş akışı oluşturmayı deneyin ya da İngilizce dışı belgeler için özel dil paketleriyle oynayın. Aynı ön işleme prensipleri geçerlidir—düzelt, gürültüyü azalt, kontrastı artır ve Aspose’un işi halletmesine izin ver.

Belirli bir dosya türü hakkında sorunuz mu var ya da `ContrastBoost` değerini ayarlamakta yardıma mı ihtiyacınız var? Aşağıya yorum bırakın ya da Aspose forumlarını ziyaret edin. İyi kodlamalar, OCR’unuz her zaman kusursuz olsun!  

![Orijinal eğik görüntünün solda ve düzeltilmiş, temizlenmiş sonucun sağda gösterildiği diyagram](deskew-diagram.png "Orijinal eğik görüntü ve düzeltilmiş sonuç diyagramı – görüntüyü düzeltme örneği")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}