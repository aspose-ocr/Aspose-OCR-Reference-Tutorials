---
category: general
date: 2026-01-10
description: OCR'yi hızlı bir şekilde nasıl çalıştırır ve bir görüntüden Arapça metni
  nasıl çıkarırsınız. Görüntüyü metne dönüştürmeyi, PNG'den metin okumayı öğrenin
  ve Aspose OCR ile metin çıkarmanın nasıl yapıldığını görün.
draft: false
keywords:
- how to run OCR
- extract arabic text
- convert image to text
- read text from png
- how to extract text
language: tr
og_description: C#'ta OCR nasıl çalıştırılır ve bir PNG görüntüsünden Arapça metin
  nasıl çıkarılır. Bu rehber, görüntüyü metne dönüştürmeyi ve PNG'den metni adım adım
  okumayı gösterir.
og_title: C#'ta OCR Nasıl Çalıştırılır – PNG'den Arapça Metin Çıkarma
tags:
- OCR
- C#
- Aspose
title: C#'ta OCR Nasıl Çalıştırılır – PNG'den Arapça Metin Çıkarma
url: /tr/net/text-recognition/how-to-run-ocr-in-c-extract-arabic-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'de OCR Nasıl Çalıştırılır – PNG'den Arapça Metin Çıkarma

Arapça karakterler içeren bir resimde **OCR nasıl çalıştırılır** diye hiç merak ettiniz mi? Tek başınıza değilsiniz. Birçok geliştirici, bir PNG'den **Arapça metin çıkarmak** gerektiğinde, sağ‑dan‑sol scriptleri sorunsuz şekilde işleyebilecek kütüphaneyi bilmedikleri için bir duvara çarpar.  

Bu öğreticide, **görüntüyü metne dönüştürmek**, **PNG'den metin okumak** ve sonunda Aspose.OCR kullanarak **metni nasıl çıkaracağınızı** temiz bir C# konsol uygulamasında öğreneceksiniz. Sonunda, Arapça dizeyi doğrudan terminalinize yazdıran çalıştırmaya hazır bir programınız olacak.

## Öğrenecekleriniz

- Aspose.OCR NuGet paketini kurun ve referans verin.  
- OCR motorunu Arapça dil desteği için yapılandırın.  
- Bir PNG görüntüsü yükleyin ve tanıma sürecini çalıştırın.  
- Çıkarılan metni alın ve görüntüleyin.  
- Daha iyi doğruluk için ayarları ince ayar yapın ve yaygın tuzakları yönetin.

OCR konusunda önceden deneyim gerekmez, sadece C#'a ve bir .NET geliştirme ortamına (Visual Studio, Rider veya `dotnet` CLI yeterlidir) temel bir anlayışınız olmalı.

---

## OCR Nasıl Çalıştırılır – Aspose OCR Kurulumu

### Adım 1: Aspose.OCR NuGet Paketini Ekleyin

İlk ihtiyacımız olan şey OCR kütüphanesidir. Aspose.OCR ticari bir üründür, ancak öğrenme amaçları için mükemmel çalışan ücretsiz bir deneme sürümü sunar.

```bash
# Using the .NET CLI
dotnet add package Aspose.OCR
```

Alternatif olarak, Visual Studio'da **NuGet Package Manager**'ı açın, **Aspose.OCR**'ı arayın ve **Install** (Yükle) düğmesine tıklayın.

> **Pro ipucu:** Kütüphaneyi bir CI boru hattında kullanmayı planlıyorsanız, sürümü kilitlemek için `-v` bayrağını ekleyin, örn., `dotnet add package Aspose.OCR -v 23.10`.

### Adım 2: Yeni Bir Konsol Projesi Oluşturun (eğer yoksa)

```bash
dotnet new console -n ArabicOcrDemo
cd ArabicOcrDemo
```

Artık kodumuz için hazır, yeni bir `Program.cs` dosyanız var.

---

## Arapça Metin Çıkarma – OCR Kodunu Yazma

Aşağıda eksiksiz, çalıştırmaya hazır program yer alıyor. `Program.cs` olarak kaydedin (veya otomatik oluşturulan dosyanın yerine koyun).

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Config;

namespace ArabicOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Create an OCR engine instance
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();

            // -------------------------------------------------
            // Step 2: Choose the language for recognition.
            // Here we use Arabic. You can swap this for
            // OcrLanguage.Korean, OcrLanguage.SerbianCyrillic, etc.
            // -------------------------------------------------
            ocrEngine.Language = OcrLanguage.Arabic;

            // -------------------------------------------------
            // Step 3: Load the image containing the text.
            // Replace the path with the location of your PNG.
            // -------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/arabic_sample.png";
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // -------------------------------------------------
            // Step 4: Run the OCR process.
            // -------------------------------------------------
            ocrEngine.Recognize();

            // -------------------------------------------------
            // Step 5: Display the extracted text.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Arabic Text ===");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

#### Her Satırın Önemi

- **`OcrEngine`**: Görüntü yüklemeyi, dil seçimini ve tanıma işlemini koordine eden merkezi sınıftır.  
- **`Language = OcrLanguage.Arabic`**: Arapça sağ‑dan‑sol bir betik ve benzersiz glifler kullanır; dili ayarlamak motorun doğru karakter modellerini uygulamasını sağlar.  
- **`ImageStream.FromFile`**: PNG, JPEG, BMP ve birçok diğer formatı işler. Eğer bir `MemoryStream`'den (örneğin, yüklenen bir dosya) okumanız gerekirse, bu çağrıyı ona göre değiştirin.  
- **`Recognize()`**: Ağır işi yapar—piksel analizi, segmentasyon ve karakter sınıflandırması.  
- **`ocrEngine.Text`**: Son Unicode dizesi, daha fazla işleme, depolamaya veya görüntülemeye hazır.

### Beklenen Çıktı

`arabic_sample.png` dosyası “مرحبا بالعالم” (Hello World) ifadesini içeriyorsa, konsol şu çıktıyı verir:

```
=== Extracted Arabic Text ===
مرحبا بالعالم
```

Eğer çıktı bozuk görünüyorsa, görüntünün net olduğundan, dilin Arapça olarak ayarlandığından ve OCR motoru sürümünün belgelerle eşleştiğinden emin olun.

---

## Görüntüyü Metne Dönüştürme – Doğruluğu Ayarlama

Varsayılan ayarlar çoğu temiz tarama için işe yarasa da, gerçek dünya görüntüleri genellikle biraz ekstra ilgi gerektirir.

| Ayar | Ne İşe Yarar | Ne Zaman Kullanılır |
|------|--------------|---------------------|
| `ocrEngine.Config.Preprocess = true` | Otomatik ikilileştirme ve gürültü kaldırmayı etkinleştirir. | Gölge içeren taranmış belgeler. |
| `ocrEngine.Config.Deskew = true` | Görüntüyü hafif eğimi düzeltmek için döndürür. | Eğimli çekilmiş fotoğraflar. |
| `ocrEngine.Config.PageSegMode = PageSegMode.SingleBlock` | Tüm görüntüyü tek bir metin bloğu olarak ele alır. | Basit başlıklar veya tek satırlı etiketler. |
| `ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزس شصضطظعغفقكلمنهوية"` | Tanıma sadece Arapça karakterlerle sınırlanır. | Karışık dil sayfalarında yanlış pozitifleri azaltır. |

Bu satırları motoru oluşturduktan hemen sonra ekleyebilirsiniz:

```csharp
ocrEngine.Config.Preprocess = true;
ocrEngine.Config.Deskew = true;
ocrEngine.Config.CharWhitelist = "ءاأإآبتثجحخدذرزسشصضطظعغفقكلمنهوية";
```

---

## PNG'den Metin Okuma – Farklı Görüntü Kaynaklarını Yönetme

Bazen PNG bir veritabanında bulunur veya bir web isteğinden gelir. İşte `byte[]`'den okuyan hızlı bir varyant:

```csharp
byte[] pngBytes = File.ReadAllBytes("YOUR_DIRECTORY/arabic_sample.png");
using var ms = new MemoryStream(pngBytes);
ocrEngine.Image = ImageStream.FromStream(ms);
ocrEngine.Recognize();
Console.WriteLine(ocrEngine.Text);
```

Akışın geri kalanı aynı kalır, bu da **metni nasıl çıkaracağınız**ın kaynağa bakılmaksızın tutarlı olduğu anlamına gelir.

---

## Metni Nasıl Çıkarırsınız – İleri Seçenekler ve Kenar Durumları

### 1. Çok Sayfalı PDF'ler veya TIFF'ler

Çok sayfalı bir belgeyi OCR'lamak istiyorsanız, her sayfa üzerinde döngü oluşturun:

```csharp
var pdfDoc = new Aspose.Pdf.Document("multi_page.pdf");
foreach (var page in pdfDoc.Pages)
{
    using var img = page.ConvertToImage();
    ocrEngine.Image = ImageStream.FromBitmap(img);
    ocrEngine.Recognize();
    Console.WriteLine($"Page {page.Number}: {ocrEngine.Text}");
}
```

> **Not:** Bu kod parçacığı için `Aspose.PDF` paketine ihtiyacınız olacak.

### 2. Dili Otomatik Algılama

Aspose.OCR ayrıca otomatik algılama sunar, ancak daha yavaştır. Görüntünün Arapça mı yoksa başka bir betik mi içerdiğinden emin değilseniz, bunu etkinleştirin:

```csharp
ocrEngine.Language = OcrLanguage.AutoDetect;
```

Motor her dil modelini deneyecek ve en iyi eşleşmeyi seçecek.

### 3. Performans İpuçları

- **`OcrEngine`** nesnesini birden çok görüntü için yeniden kullanın; her seferinde yeni bir örnek oluşturmak ek yük getirir.  
- **Paralel çalıştırın** yalnızca her iş parçacığı için ayrı motor örnekleriniz varsa—tek bir örneği paylaşmak yarış koşullarına neden olur.

## Sonuç

C#'de **OCR nasıl çalıştırılır** konusunu baştan sona ele aldık, **Arapça metin çıkarma**, **görüntüyü metne dönüştürme**, **PNG'den metin okuma** ve çeşitli senaryolarda **metni nasıl çıkaracağınız** sorusuna yanıt vermeyi gösterdik. Örnek kod eksiksiz, bağımsız ve herhangi bir .NET konsol projesine yapıştırmaya hazır.

Sonraki adımlar? `OcrLanguage.Arabic`'i Korece ya da Sırp Kiril alfabesiyle değiştirerek kütüphanenin çok dilli gücünü görün. Gürültülü taramalarda doğruluğu artırmak için ön işleme bayraklarıyla deneyler yapın ya da OCR rutinini bir web API'ye entegre edin, böylece kullanıcılar görüntü yükleyip anında metin sonuçları alabilir.

Kodlamaktan keyif alın ve OCR sonuçlarınız her zaman kristal gibi net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}