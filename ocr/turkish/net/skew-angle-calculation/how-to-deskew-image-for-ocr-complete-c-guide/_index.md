---
category: general
date: 2026-01-06
description: Aspose OCR ile görüntüyü eğrilikten düzeltmeyi, gürültüyü kaldırmayı
  ve metni çıkarmayı öğrenin. Adım adım kılavuz, OCR için görüntünün nasıl yükleneceğini
  de gösterir.
draft: false
keywords:
- how to deskew image
- how to extract text
- how to remove noise
- recognize text from image
- load image for ocr
language: tr
og_description: Aspose OCR ile görüntüyü eğriltme, gürültüyü kaldırma ve metin çıkarma
  yöntemlerini öğrenin. Adım adım rehber ayrıca OCR için görüntünün nasıl yükleneceğini
  gösterir.
og_title: OCR için Görüntüyü Düzeltme – Tam C# Rehberi
tags:
- OCR
- C#
- Image Processing
title: OCR için Görüntüyü Düzeltme – Tam C# Kılavuzu
url: /tr/net/skew-angle-calculation/how-to-deskew-image-for-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için Görüntüyü Düzeltme – Tam C# Rehberi

Bir OCR motoruna göndermeden önce **görüntüyü nasıl düzeltir** (deskew) merak ettiniz mi? Yalnız değilsiniz—çoğu geliştirici, taranmış bir fotoğraf hafifçe eğik, gürültülü veya okunması zor olduğunda aynı sorunla karşılaşıyor. İyi haber? Aspose OCR ile birkaç C# satırıyla görüntüyü düzeltip temizleyebilir ve ardından metni çıkarabilirsiniz.

Bu öğreticide **metni nasıl çıkarır**, **gürültüyü nasıl kaldırır** ve tabii ki **görüntüyü nasıl düzeltir** (deskew) adımlarını inceleyeceğiz, böylece OCR sonuçları kusursuz olur. Sonunda **OCR için görüntüyü nasıl yüklersiniz** ve uygulamanız için temiz, aranabilir dizeler elde edersiniz.

---

## Gereksinimler

- **Aspose.OCR for .NET** (v23.12 veya daha yeni). NuGet paketi `Aspose.OCR`.
- .NET 6+ (herhangi bir güncel çalışma zamanı yeterlidir).
- Eğik veya lekeli bir örnek görüntü, ör. `skewed_photo.jpg`.
- Visual Studio, Rider veya tercih ettiğiniz editör.

Ek yerel kütüphanelere gerek yok—Aspose her şeyi süreç içinde halleder.

---

## Adım 1 – OCR Motorunu Kurun (Görüntüden Metin Tanıma)

**OCR için görüntüyü yüklemeden** önce bir motor örneğine ve okumak istediğimiz dile ihtiyacımız var.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

// Create the OCR engine and tell it we’re reading English text.
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.English
};
```

**Neden önemli:** `OcrEngine` işlemin kalbidir. `Language` ayarını erken yapmak, tanıma algoritmasının doğru karakter setini kullanmasını sağlar ve doğruluğu büyük ölçüde artırır.

---

## Adım 2 – Görüntünüzü Yükleyin (OCR için Görüntüyü Yükle)

Şimdi motoru diskteki dosyaya yönlendiriyoruz. Birçok öğreticinin durduğu nokta burada, ancak yaygın tuzakları da ele alacağız.

```csharp
// Load the image you want to process.
ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");
```

> **İpucu:** Test sırasında mutlak bir yol kullanın, ardından üretimde göreli yol ya da gömülü kaynakla değiştirin. Ayrıca görüntünün desteklenen bir formatta (JPEG, PNG, BMP, TIFF) olduğundan emin olun. “Unsupported format” hatası alırsanız, dosya uzantısını ve MIME tipini tekrar kontrol edin.

---

## Adım 3 – Ön İşlem: Düzeltme ve Lekeleri Kaldırma (Görüntüyü Nasıl Düzeltir & Gürültüyü Nasıl Kaldırır)

Eğik bir belge klasik bir OCR kabusudur. Aspose, yapılandırılabilir bir açıya kadar dönüşü otomatik olarak algılayan bir `DeskewFilter` sunar. Bunu `DespeckleFilter` ile birleştirerek tuz‑ve‑biber gürültüsünü temizleyebilirsiniz.

```csharp
// 1️⃣ Deskew – correct rotation up to 15° (adjust as needed)
ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });

// 2️⃣ Despeckle – reduce noise; Strength 1‑5 (3 is moderate)
ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });
```

### Deskew Filter Nasıl Çalışır
Filtre, görüntüyü baskın metin taban hatları için tarar, eğim açısını hesaplar ve bitmap'i buna göre döndürür. Görüntü zaten düz ise filtre hiçbir şey yapmaz—bu yüzden herhangi bir iş akışına güvenle ekleyebilirsiniz.

### Despeckle Filter Nasıl Yardımcı Olur
Gürültü genellikle izole karanlık ya da parlak pikseller olarak ortaya çıkar. Despeckle algoritması bir medyan filtresi uygular, kenarları (karakter çizgileri gibi) korurken lekeleri yumuşatır. Çok yüksek bir güç ince detayları bulanıklaştırabilir, bu yüzden `Strength = 3` ile başlayıp kaynağınıza göre ayarlayın.

> **Not:** Görüntüleriniz aşırı dönüşe sahipse (>15°), `MaxAngle` değerini artırın. Belgeler ters tarandıysa, deskew filtresinden önce özel bir döndürme adımına ihtiyaç duyabilirsiniz.

---

## Adım 4 – Tanıma Çalıştırın (Görüntüden Metin Tanıma)

Ön işleme tamamlandığında, motoru metni okumaya çağırıyoruz.

```csharp
if (ocrEngine.Recognize())
{
    // The recognized text is now stored in ocrEngine.Text
    Console.WriteLine("=== Extracted Text ===");
    Console.WriteLine(ocrEngine.Text);
}
else
{
    Console.WriteLine("Recognition failed – check the image quality.");
}
```

### İçeride Ne Oluyor?
1. **Binarizasyon:** Görüntüyü siyah‑beyaz’a çevirir, kontrastı keskinleştirir.
2. **Segmentasyon:** Bitmap’i satır, kelime ve karakterlere ayırır.
3. **Sınıflandırma:** Her karakteri eğitilmiş bir modele (İngiliz alfabesi, rakamlar, noktalama) karşılaştırır.
4. **Post‑processing:** Okunabilirliği artırmak için dil kuralları (ör. yazım denetimi) uygular.

Zaten **görüntüyü düzelttiğimiz** ve **gürültüyü kaldırdığımız** için bu aşamaların her biri daha temiz veri alır, bu da hatalı tanımanın azalması anlamına gelir.

---

## Adım 5 – Çıktıyı Doğrulayın ve Temizleyin (Metni Etkili Şekilde Nasıl Çıkarır)

Ham dize, gereksiz satır sonları veya fazladan boşluklar içerebilir. Hızlı bir temizlik, veriyi sonraki işleme hazır hâle getirir.

```csharp
string raw = ocrEngine.Text;

// Trim leading/trailing whitespace and collapse multiple newlines.
string cleaned = System.Text.RegularExpressions.Regex
    .Replace(raw, @"\s+", " ")
    .Trim();

Console.WriteLine("\n=== Cleaned Text ===");
Console.WriteLine(cleaned);
```

**Neden temizlenmeli?** Birçok OCR kütüphanesi orijinal düzeni korur; bu PDF’ler için harika ama düz metin akışları için gürültülüdür. Boşlukları normalleştirmek, sonucu bir veritabanına kaydetmenizi veya bir arama indeksine beslemenizi ekstra çaba olmadan sağlar.

---

## Tam Çalışan Örnek

Aşağıda her şeyi bir araya getiren, kopyala‑yapıştır‑hazır program yer alıyor. `Program.cs` olarak kaydedin, Aspose.OCR NuGet paketini ekleyin ve çalıştırın.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine
        OcrEngine ocrEngine = new OcrEngine
        {
            Language = OcrLanguage.English
        };

        // 2️⃣ Load the image you want to process
        //    (this demonstrates how to load image for OCR)
        ocrEngine.Image = ImageStream.FromFile(@"C:\Images\skewed_photo.jpg");

        // 3️⃣ Add preprocessing filters
        //    - Deskew up to 15° (how to deskew image)
        //    - Despeckle with moderate strength (how to remove noise)
        ocrEngine.Filters.Add(new DeskewFilter { MaxAngle = 15 });
        ocrEngine.Filters.Add(new DespeckleFilter { Strength = 3 });

        // 4️⃣ Perform recognition (recognize text from image)
        if (ocrEngine.Recognize())
        {
            // 5️⃣ Output raw and cleaned text (how to extract text)
            Console.WriteLine("=== Raw OCR Output ===");
            Console.WriteLine(ocrEngine.Text);

            string cleaned = System.Text.RegularExpressions.Regex
                .Replace(ocrEngine.Text, @"\s+", " ")
                .Trim();

            Console.WriteLine("\n=== Cleaned OCR Output ===");
            Console.WriteLine(cleaned);
        }
        else
        {
            Console.WriteLine("OCR failed – verify the image path and quality.");
        }
    }
}
```

**Beklenen çıktı** (örnek görüntü “Hello World” ifadesini içeriyorsa):

```
=== Raw OCR Output ===
Hello World

=== Cleaned OCR Output ===
Hello World
```

Görüntü çok eğik ise, `DeskewFilter` eklemeden önce ham çıktının bozuk karakterler içerdiğini göreceksiniz. Filtreyi ekledikten sonra metin okunabilir hâle gelir—tam da hedeflediğimiz şey.

---

## Sık Sorulan Sorular & Kenar Durumları

| Soru | Cevap |
|------|-------|
| *Görüntüm 15°’den fazla döndürülmüşse ne yapmalıyım?* | `DeskewFilter` içinde `MaxAngle` değerini artırın. 45°’e kadar değerler güvenlidir, ancak aşırı açılar için önce manuel bir döndürme (`Image.Rotate(angle)`) gerekebilir. |
| *Despeckle sonrası hâlâ harfler eksik.* | Daha yüksek bir `Strength` (4‑5) deneyin veya despeckle öncesinde bir `ContrastFilter` ekleyin. |
| *PDF’leri doğrudan işleyebilir miyim?* | Evet—her sayfayı bir görüntüye dönüştürmek için `PdfDocument` kullanın, ardından aynı iş akışını uygulayın. |
| *Motor çoklu iş parçacığı (thread) için güvenli mi?* | Her iş parçacığı için ayrı bir `OcrEngine` oluşturun; sınıf kendisi thread‑safe değildir. |
| *Çok dilli belgelerle nasıl başa çıkılır?* | `ocrEngine.Language = OcrLanguage.Multilingual` ayarlayın veya sayfa başına dili değiştirin. |

---

## Üretim‑Hazır OCR İçin İpuçları

1. **Batch İşleme:** Bir klasördeki tüm görüntüler üzerinde döngü kurun, aynı `OcrEngine` örneğini yeniden kullanarak yükü azaltın.
2. **Loglama:** `Recognize()` false döndüğünde `ocrEngine.LastError` değerini yakalayın; genellikle desteklenmeyen formatlar veya bozuk dosyalar hakkında bilgi verir.
3. **Performans:** Deskew adımı en CPU‑yoğun adımdır. Görüntüleriniz zaten düz ise filtreyi eklemeyi atlayabilirsiniz.
4. **Bellek Yönetimi:** `ImageStream` nesnelerini kullandıktan sonra (`ocrEngine.Image.Dispose()`) serbest bırakın; uzun çalışan servislerde bellek sızıntılarını önler.

---

## Sonuç

**Görüntüyü nasıl düzeltir**, **gürültüyü nasıl kaldırır**, **OCR için görüntüyü nasıl yüklersiniz** ve **metni nasıl çıkarırsınız** konularını Aspose OCR ve C# ile ele aldık. `DeskewFilter` ve `DespeckleFilter` ile ön işleme yaparak `Recognize()` metodunun temiz, aranabilir dizeler döndürme ihtimalini büyük ölçüde artırırsınız.

İlk kod satırından son temiz çıktıya kadar adımlar basit, ancak gerçek dünya senaryoları için yeterince güçlü—belge arşivleme hizmeti, fiş tarama mobil uygulaması veya toplu işleme arka ucu gibi projelerinizde rahatlıkla kullanabilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? **Dil algılama** adımı ekleyin ya da **özel OCR sözlükleri** ile sektöre özgü terminoloji için doğruluğu artırın. Gökyüzü sınır, ve artık sağlam bir temele sahipsiniz.

Kodlamanın tadını çıkarın, ve görüntüleriniz her zaman mükemmel düz olsun!

![Illustration of a corrected document after deskewing](deskewed_example.png "how to deskew image")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}