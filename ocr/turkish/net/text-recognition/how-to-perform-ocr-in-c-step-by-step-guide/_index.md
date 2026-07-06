---
category: general
date: 2026-02-14
description: C#'ta Aspose.OCR kullanarak OCR nasıl yapılır – görüntüden metin çıkarmayı,
  dosyadan görüntü yüklemeyi ve görüntü üzerinde OCR'ı hızlıca çalıştırmayı öğrenin.
draft: false
keywords:
- how to perform OCR
- extract text from image
- load image from file
- recognize text from jpg
- run OCR on image
language: tr
og_description: C#'ta Aspose.OCR ile OCR nasıl yapılır. Bu kılavuz, görüntüden metin
  nasıl çıkarılır, görüntü dosyadan nasıl yüklenir ve görüntü üzerinde OCR nasıl verimli
  bir şekilde çalıştırılır, gösterir.
og_title: C#'de OCR Nasıl Yapılır – Tam Programlama Öğreticisi
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'ta OCR Nasıl Yapılır – Adım Adım Rehber
url: /tr/net/text-recognition/how-to-perform-ocr-in-c-step-by-step-guide/
---

answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Yapılır – Tam Programlama Öğreticisi

Telefonunuzla yeni çektiğiniz bir fotoğraftan **OCR nasıl yapılır** diye hiç merak ettiniz mi? Belki bir navigasyon uygulaması için JPEG'den sokak işareti metnini çekmeniz gerekiyor, ya da taranmış sözleşmelerden oluşan bir yığın var ve bunları aranabilir metne dönüştürmek istiyorsunuz. Kısacası, *görüntüden metin çıkarma* işlemini buluta göndermeden yapmak istiyorsunuz.

İyi haber şu ki, tüm bunları yerel olarak Aspose.OCR for .NET ile yapabilirsiniz. Bu öğreticide bir dosyadan görüntü yüklemeyi, JPG'den metin tanımayı ve sonunda **görüntüde OCR çalıştırma** işlemini tamamen çevrim dışı olarak nasıl yapacağınızı adım adım göstereceğiz. Sonunda, tanınan Arapça metni konsola yazdıran hazır bir kod parçacığına sahip olacaksınız.

> **Elde edeceğiniz şey:** bağımsız, çalıştırılabilir bir C# programı, her satırın neden önemli olduğuna dair açıklamalar ve eksik kaynaklar ya da desteklenmeyen diller gibi yaygın kenar durumlarını ele almanız için ipuçları.

## Ön Koşullar

İlerlemeye başlamadan önce şunların olduğundan emin olun:

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6.0 veya üzeri (veya .NET Framework 4.7+) | Aspose.OCR, .NET Standard 2.0 hedefler; bu yüzden herhangi bir modern çalışma zamanı yeterlidir. |
| Visual Studio 2022 (veya C# uzantılı VS Code) | Bir IDE, NuGet paketlerini yönetmeyi ve konsol uygulamasını çalıştırmayı kolaylaştırır. |
| Aspose.OCR NuGet paketi (`Aspose.OCR`) | OCR işini gerçekten yapan kütüphane budur. |
| Çevrim dışı OCR kaynaklarını içeren bir klasör (Aspose'tan indirin) | Çevrim dışı kaynaklar, tanıma sırasında herhangi bir HTTP çağrısı yapılmasını engeller. |
| Bir görüntü dosyası (ör. `arabic_sign.jpg`) | Arapça metin içeren bir JPEG kullanacağız, ancak herhangi bir dil çalışır. |

Eğer bunlardan birini kaçırdıysanız, şimdi temin edin—yarı yolda eksik bir bağımlılıkla karşılaşmadan öğreticiye başlamak istemezsiniz.

## Adım 1: Aspose.OCR'ı Yükleyin ve Kaynakları Hazırlayın

İlk olarak, Aspose.OCR paketini projenize ekleyin:

```bash
dotnet add package Aspose.OCR
```

Paket yüklendikten sonra Aspose web sitesinden **çevrim dışı OCR kaynak paketi**ni indirin. Makinenizde bir klasöre çıkartın, örneğin:

```
C:\OCRResources\
```

> **Neden önemli:** Kaynakları başlangıçta bir kez yüklemek, ağ gecikmesini ortadan kaldırır ve hiçbir şeyin makineden çıkmaması sayesinde çözümünüz GDPR‑dostu olur.

## Adım 2: OCR Motorunu Oluşturun ve Kaynak Klasörünü Belirtin

Şimdi `Engine` sınıfını örnekleyip kaynakların nerede olduğunu söyleyeceğiz. Bu, **C#'ta OCR nasıl yapılır** sorusunun yerel yanıtının kalbidir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Step 2: Initialize the OCR engine with the offline resource folder
Engine ocrEngine = new Engine
{
    // Replace with the path you used in the previous step
    ResourceFolder = @"C:\OCRResources"
};

// Load the resources into memory – this prevents any hidden HTTP calls
ocrEngine.LoadResources();
```

> **Pro ipucu:** `LoadResources` çağrısını bir try‑catch bloğuna sarın; klasör yolu yanlış olursa istisna tam olarak hangi dosyanın eksik olduğunu size söyleyecektir.

## Adım 3: Görüntüyü Dosyadan Yükleyin

Şimdi **dosyadan görüntü yükleme** işlemini yapmamız gerekiyor ki motor analiz edebilsin. Aspose.OCR, kendi `ImageStream` sarmalayıcısını kullanır.

```csharp
// Step 3: Load the JPEG you want to recognize
ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");
```

Görüntünüz başka bir yerdeyse sadece yolu değiştirin. `ImageStream` sınıfı, alttaki bitmap işleme detaylarını soyutlar; böylece GDI+ uyumluluğu hakkında endişelenmenize gerek kalmaz.

## Adım 4: JPG'den Dil Ayarlarıyla Metin Tanıma

Şimdi **C#'ta OCR nasıl yapılır** sorusunun özü devreye giriyor—karakterleri gerçekten tanımak. Arapça tanıma isteyeceğiz, ancak `Language.Arabic`ı başka desteklenen bir dil ile değiştirebilirsiniz.

```csharp
// Step 4: Run OCR specifying the desired language (Arabic in this example)
OcrResult ocrResult = ocrEngine.Recognize(
    image,
    new OcrOptions { Language = Language.Arabic }
);
```

> **Neden bir dil belirtilir?** OCR motoru, dile özgü sözlükler ve karakter modelleri kullanır. Doğru dili sağlamak, özellikle Arapça gibi karmaşık şekillere sahip yazı sistemlerinde doğruluğu büyük ölçüde artırır.

## Adım 5: Çıkarılan Metni Görüntüleyin

Son olarak **görüntüden metin çıkarma** işlemini yapıp ekrana yazdıralım. Bu, OCR'un başarılı olduğunu doğrulamanın en basit yoludur.

```csharp
// Step 5: Output the recognized text to the console
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(ocrResult.Text);
```

Programı çalıştırdığınızda, işaret üzerindeki Arapça ifadenin konsolda yazdırıldığını görmelisiniz. Çıktı bozuk görünüyorsa, doğru dilin seçildiğini ve kaynak klasörünün Arapça veri dosyalarını içerdiğini bir kez daha kontrol edin.

## Tam Çalışan Örnek

Aşağıda, tüm adımları bir araya getiren, derlenmeye hazır tam program yer alıyor. Yeni bir konsol projesine (`dotnet new console`) kopyalayıp **F5** tuşuna basın.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // Step 1: Configure the OCR engine with offline resources
            // -------------------------------------------------
            Engine ocrEngine = new Engine
            {
                ResourceFolder = @"C:\OCRResources" // <-- change to your folder
            };
            ocrEngine.LoadResources(); // Loads language packs, fonts, etc.

            // -------------------------------------------------
            // Step 2: Load the image you want to process
            // -------------------------------------------------
            ImageStream image = ImageStream.FromFile(@"C:\OCRResources\arabic_sign.jpg");

            // -------------------------------------------------
            // Step 3: Recognize text – specify language to improve accuracy
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(
                image,
                new OcrOptions { Language = Language.Arabic } // Change as needed
            );

            // -------------------------------------------------
            // Step 4: Output the result
            // -------------------------------------------------
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Beklenen çıktı (örnek):**

```
=== OCR Result ===
مطار القاهره الدولي
```

Görüntüyü bir İngiliz işaretiyle değiştirip `Language.English` ayarlarsanız, aynı kod İngilizce metni çıktılar. Bu, **görüntüde OCR çalıştırma**ın ne kadar esnek olduğunu gösterir.

## Görüntüden Metin Çıkarma – Yaygın Senaryoların Ele Alınması

### 1. Çok Sayfalı veya Çok Çerçeveli Görüntüler

Bazı görüntü formatları (ör. TIFF) birden fazla sayfa içerebilir. Böyle durumlarda **görüntüden metin çıkarma** için her çerçeveyi döngüye alın:

```csharp
for (int i = 0; i < image.FramesCount; i++)
{
    image.CurrentFrame = i;
    OcrResult pageResult = ocrEngine.Recognize(image, new OcrOptions { Language = Language.English });
    Console.WriteLine($"Page {i + 1}: {pageResult.Text}");
}
```

### 2. Düşük Çözünürlüklü Görüntüler

OCR doğruluğu 70 dpi'nin altına düştüğünde dramatik olarak azalır. Bulanık sonuçlarla karşılaşırsanız, önce görüntüyü büyütmeyi düşünün:

```csharp
using System.Drawing;
using System.Drawing.Drawing2D;

// Load as Bitmap, resize, then wrap back into ImageStream
Bitmap bmp = new Bitmap(@"C:\OCRResources\lowres.jpg");
Bitmap highRes = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
ImageStream highResStream = ImageStream.FromBitmap(highRes);
```

### 3. Eksik Dil Paketi

*“Language data not found”* gibi bir istisna alırsanız, ilgili `.dat` dosyalarının `ResourceFolder` içinde bulunduğunu bir kez daha kontrol edin. Aspose, her dil için ayrı bir zip dosyası sunar.

## Görüntüde OCR Çalıştırma – Performans İpuçları

- **Motoru Önbellekle:** Her görüntü için yeni bir `Engine` oluşturmak ek yük getirir. Toplu işleme için tek bir örnek tutun.
- **Güvenli Paralelleştirme:** `Engine`, `LoadResources` sonrası yalnızca okuma‑only işlemler için thread‑safe'dir. Farklı görüntülerde `Recognize` çağıran birden fazla görev başlatabilirsiniz.
- **İş Bittiğinde Serbest Bırak:** `Engine` `IDisposable` implement eder, .NET GC sonunda temizler. `using` bloğu içinde `ocrEngine.Dispose()` çağırmak iyi bir alışkanlıktır.

```csharp
using (Engine ocrEngine = new Engine { ResourceFolder = @"C:\OCRResources" })
{
    ocrEngine.LoadResources();
    // run recognitions here
}
```

## JPG'den Metin Tanıma – Dikkat Edilmesi Gereken Kenar Durumları

| Durum | Kontrol Edilecek | Çözüm |
|-----------|---------------|-----|
| **Bozuk JPEG** | `ImageStream.FromFile` `FileNotFoundException` veya `ArgumentException` fırlatır. | Dosya bütünlüğünü doğrulayın, gerekirse bir grafik editörüyle yeniden kaydedin. |
| **Desteklenmeyen dil** | `Language` enum'ı hedef dilinizi içermiyor. | Aspose.OCR'ı en son sürüme güncelleyin; yeni diller düzenli olarak eklenir. |
| **Karışık betik görüntüleri** (ör. İngilizce + Arapça) | Tek dil seçeneği ikincil betiği kaçırabilir. | Farklı dil seçenekleriyle OCR'ı iki kez çalıştırıp sonuçları birleştirin. |

## Özet – Artık C#'ta OCR Nasıl Yapılır Biliyorsunuz

Bu rehberde Aspose.OCR kullanarak **C#'ta OCR nasıl yapılır** konusunu, NuGet paketini kurmaktan tanınan metni ekrana yazdırmaya kadar ele aldık. **Dosyadan görüntü yükleme**, **görüntüden metin çıkarma**, **JPG'den metin tanıma** ve üretim ortamına uygun **görüntüde OCR çalıştırma** konularını güvenle uygulayabileceksiniz.

### Sıradaki Adımlar

- **PNG veya BMP** gibi diğer dosya formatlarıyla deney yapın—sadece dosya uzantısını değiştirin.
- **Veritabanı entegrasyonu** ile OCR sonuçlarını aranabilir arşivlerde saklayın.
- **Bilgisayarla görme** (ör. OCR öncesi metin bölgelerini tespit etme) ile hız kazanın.

Dil ayarlarını istediğiniz gibi değiştirin, klasörleri toplu işleyin veya çıktıyı bir web API'ye bağlayın. OCR bir yapı taşıdır; gerçek güç, onu daha büyük iş akışlarına dokunduğunuzda ortaya çıkar.

Kodlamaktan keyif alın, ve görüntüleriniz her zaman kristal‑net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}