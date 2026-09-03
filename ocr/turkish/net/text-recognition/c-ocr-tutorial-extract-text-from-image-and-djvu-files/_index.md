---
category: general
date: 2026-01-09
description: c# OCR öğreticisi, görüntü dosyalarından metin çıkarmayı ve Aspose.OCR
  kullanarak DJVU'yu metne dönüştürmeyi gösterir. Dakikalar içinde adım adım çıkarımı
  öğrenin.
draft: false
keywords:
- c# OCR tutorial
- extract text from image
- how to extract text
- convert djvu to text
- extract text from djvu
language: tr
og_description: c# OCR öğreticisi, görüntü dosyalarından metin çıkarma ve Aspose.OCR
  kullanarak DJVU'yu metne dönüştürme sürecini hızlıca gösterir. Çalışan bir çözüm
  için rehberi takip edin.
og_title: c# OCR öğreticisi – Görüntü ve DJVU'dan metin çıkarma
tags:
- OCR
- C#
- Aspose
title: 'c# OCR öğretici: Görüntü ve DJVU dosyalarından metin çıkarma'
url: /tr/net/text-recognition/c-ocr-tutorial-extract-text-from-image-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR öğreticisi – Görüntü ve DJVU dosyalarından metin çıkarma

Saçınızı yolmak zorunda kalmadan görüntü dosyalarından metin nasıl çıkarılır merak ettiniz mi? Bu **c# OCR öğreticisinde** normal bir resim *ve* bir DJVU belgesinden metin çıkaran tam, çalıştırmaya hazır bir örnek üzerinden ilerleyeceğiz.  

Eğer **DJVU'yu metne dönüştürmek** için hızlı bir yol arıyorsanız, doğru yerdesiniz—ekstra dönüştürücüler yok, sadece saf C# kodu.

## Öğrenecekleriniz

- Aspose.OCR kütüphanesini bir .NET projesinde nasıl kuracağınız.  
- Görüntü dosyalarından **metin çıkarmak** için gereken tam kod.  
- **DJVU** dosyalarından metin çıkarmak için öz bir yöntem (evet, aynı motor bunu yapar).  
- Yaygın tuzaklar (büyük dosyalar, eksik yazı tipleri, lisanslama) ve bunlardan nasıl kaçınılacağı.  

Tek ihtiyacınız, güncel bir .NET SDK ve NuGet paketini indirmek için bir internet bağlantısı. Önceden OCR deneyimi gerekmez.

## Önkoşullar

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 veya daha yeni | Aspose.OCR, .NET Standard 2.0 hedefler, bu yüzden .NET 6+ en iyi performansı sağlar. |
| Visual Studio 2022 (veya VS Code) | IDE'ler paket yönetimini sorunsuz hâle getirir, ancak herhangi bir editör de çalışır. |
| NuGet paketi **Aspose.OCR** | Bu, asıl işi yapan motor. |
| Örnek bir görüntü (`sample.png`) ve bir DJVU dosyası (`sample.djvu`) | Her iki çıkarma senaryosunu göstermek için bunları kullanacağız. |

Paketi aşağıdaki komutla kurabilirsiniz:

```bash
dotnet add package Aspose.OCR
```

> **Pro ipucu:** Bir CI sunucusunda iseniz, derleme adımına `--no-restore` ekleyin ve başta bir kez restore yaparak süreci hızlandırın.

## Adım 1: OCR motorunu başlatma – c# OCR öğreticisinin kalbi

İlk yaptığımız şey `OcrEngine` bir örnek oluşturmaktır. Bunu, yazılımınızdaki tarayıcıyı açmak gibi düşünün.

```csharp
using Aspose.OCR;

var ocrEngine = new OcrEngine();
```

Neden her seferinde yeni bir motor oluşturuyoruz? Çünkü motor, yapılandırmayı (dil, algılama modu vb.) tutar. Yeni başlamak, eski ayarların çalıştırmalar arasında sızmasını önler.

## Adım 2: Bir görüntüyü yükleyip tanıma – görüntüden metin nasıl çıkarılır

Şimdi motoru normal bir bitmap (PNG, JPEG, BMP…) ile besleyeceğiz. `RecognizeImage` metodu tespit edilen dizeyi döndürür.

```csharp
// Path to your image file
string imagePath = @"C:\OCR\sample.png";

// Perform OCR
string imageText = ocrEngine.RecognizeImage(imagePath);

// Show the result
Console.WriteLine("=== Text extracted from image ===");
Console.WriteLine(imageText);
```

Dikkat edilmesi gereken birkaç nokta:

* **Dosya varlığı** – Yol yanlışsa metod `FileNotFoundException` fırlatır. Kullanıcı tarafından sağlanan yollar bekliyorsanız `try/catch` ile sarın.
* **Görüntü kalitesi** – OCR, 300 dpi veya daha yüksek çözünürlükte en iyi çalışır. Düşük çözünürlüklü taramalar bozuk çıktı üretebilir.
* **Dil desteği** – Varsayılan olarak Aspose.OCR İngilizce varsayar. Değiştirmek için `RecognizeImage`'den önce `ocrEngine.Language = Language.Spanish;` ayarlayın.

## Adım 3: DJVU belgesinden metin tanıma – DJVU'yu metne dönüştürme

DJVU, birden çok sayfa tutabilen bir konteyner formatıdır. Aspose.OCR bunu doğrudan işleyebilir; sadece dosyayı gösterirsiniz.

```csharp
// Path to your DJVU file
string djvuPath = @"C:\OCR\sample.djvu";

// Perform OCR on the DJVU file
string djvuText = ocrEngine.RecognizeImage(djvuPath);

// Output the result
Console.WriteLine("\n=== Text extracted from DJVU ===");
Console.WriteLine(djvuText);
```

Motor, her sayfayı bir görüntü olarak çıkarır ve aynı tanıma hattını çalıştırır. Bu yüzden ayrı bir “DJVU'yu metne dönüştür” adımına ihtiyacınız yok—OCR motoru sizin için yapar.

### Çok sayfalı DJVU dosyalarını işleme

DJVU'nuz birden fazla sayfa içeriyorsa, `RecognizeImage` onları sırayla birleştirir. Her sayfayı ayrı ayrı ihtiyacınız varsa, `List<string>` döndüren aşırı yüklemeyi kullanabilirsiniz:

```csharp
var pagesText = ocrEngine.RecognizeImage(djvuPath, true); // true = return per‑page list
for (int i = 0; i < pagesText.Count; i++)
{
    Console.WriteLine($"\n--- Page {i + 1} ---");
    Console.WriteLine(pagesText[i]);
}
```

## Adım 4: Daha iyi doğruluk için motoru ince ayar yapma – bunun önemi

Kutudan çıkar çıkmaz sonuçlar makul, ancak birkaç ayarı değiştirerek artırabilirsiniz:

```csharp
ocrEngine.Language = Language.English;      // set detection language
ocrEngine.Dpi = 300;                        // enforce 300 DPI processing
ocrEngine.IsDetectOrientation = true;      // auto‑rotate tilted pages
ocrEngine.IsDetectSkew = true;              // correct slanted text
```

Bu bayraklar, önce DJVU olarak kaydedilen taranmış PDF'lerden **metin nasıl çıkarılır** konusunda özellikle faydalıdır. Yön algılamayı açmak, görüntüleri manuel olarak döndürmek zorunda kalmanızı önler.

## Adım 5: Lisanslama ve çalışma zamanı hatalarıyla başa çıkma

Aspose.OCR, birkaç sayfadan sonra çıktıya “Demo” damgası ekleyen ücretsiz bir deneme sürümüyle gelir. Filigranı kaldırmak için lisans dosyanızı ekleyin:

```csharp
// Assuming you have a license.xml in the project root
var license = new Aspose.OCR.License();
license.SetLicense("license.xml");
```

Bu adımı unutursanız, motor hâlâ çalışır ancak sonuç “Demo” kelimesini içerir. Ayrıca, büyük DJVU dosyalarını işlerken `OutOfMemoryException`'a dikkat edin—daha önce gösterildiği gibi sayfa sayfa işlemeyi düşünün.

## Tam, çalıştırılabilir örnek

Aşağıda her şeyi bir araya getiren bağımsız bir konsol programı var. Kopyala‑yapıştır, dosya yollarını ayarla ve **Run** tuşuna bas.

```csharp
// Complete c# OCR tutorial – extract text from image and DJVU
using System;
using Aspose.OCR;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Set up licensing (optional, removes demo watermark)
            // var license = new License();
            // license.SetLicense("license.xml");

            // 2️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine
            {
                Language = Language.English,
                Dpi = 300,
                IsDetectOrientation = true,
                IsDetectSkew = true
            };

            // 👉 Extract text from a regular image
            string imagePath = @"C:\OCR\sample.png";
            try
            {
                string imageText = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("=== Text extracted from image ===");
                Console.WriteLine(imageText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"Image OCR failed: {ex.Message}");
            }

            // 👉 Extract text from a DJVU file (convert DJVU to text)
            string djvuPath = @"C:\OCR\sample.djvu";
            try
            {
                // Single string for all pages
                string djvuText = ocrEngine.RecognizeImage(djvuPath);
                Console.WriteLine("\n=== Text extracted from DJVU ===");
                Console.WriteLine(djvuText);
            }
            catch (Exception ex)
            {
                Console.WriteLine($"DJVU OCR failed: {ex.Message}");
            }

            // Keep console open
            Console.WriteLine("\nPress any key to exit...");
            Console.ReadKey();
        }
    }
}
```

**Beklenen çıktı** (dosyalar “Hello World” ifadesini içeriyorsa):

```
=== Text extracted from image ===
Hello World

=== Text extracted from DJVU ===
Hello World
```

Eğer kaynak birden çok satır içeriyorsa, bunlar orijinal belgede olduğu gibi görünecek.

## Yaygın sorular ve uç‑durum yönetimi

* **Görüntü siyah‑beyaz olursa ne olur?**  
  OCR sorunsuz çalışır, ancak kontrastı `ocrEngine.ImagePreprocessOptions = ImagePreprocessOptions.Contrast;` ile artırabilirsiniz.

* **Sadece sayıları çıkarabilir miyim?**  
  Evet—`RecognizeImage`'i çağırmadan önce `ocrEngine.CharWhitelist = "0123456789";` ayarlayın.

* **Dosya boyutu için bir limit var mı?**  
  Motor, tüm dosyayı belleğe okur. ~100 MB'den büyük dosyalar için sayfa‑sayfa işleyin (Adım 3'teki liste aşırı yüklemeye bakın).

* **Bu, Tesseract'tan nasıl farklıdır?**  
  Aspose.OCR, yerleşik DJVU desteği ve yerel bağımlılıkları olmayan ticari bir kütüphanedir; Tesseract ise yerel ikili dosyalar ve ayrı DJVU dönüşüm araçları gerektirir.

## Sonuç

Az önce **c# OCR öğreticisini** tamamladınız; bu, Aspose.OCR kullanarak **görüntü dosyalarından metin çıkarma** ve sorunsuz **DJVU'yu metne dönüştürme** yollarını gösteriyor. Örnek, paket kurulumundan lisanslamaya, tek sayfalı görüntü çıkarımından çok sayfalı DJVU işleme kadar her şeyi kapsar ve doğruluğu artırma ipuçları bile içerir.

Sonraki adımda **PDF'lerden metin çıkarma**, OCR adımını bir web API'ye entegre etme veya çok dilli belgeler için dil paketleriyle deneme yapma gibi konuları keşfedebilirsiniz. Sınır yok—sadece temel çıkarımları hatırlayın: motoru ayarlayın, bir dosya verin ve dizeyi geri okuyun.

Başka sorularınız mı var? Bir yorum bırakın, kodu kendi belgelerinizde deneyin ve iyi kodlamalar!

![c# OCR tutorial screenshot showing console output](/images/csharp-ocr-tutorial.png "c# OCR tutorial – console output example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}