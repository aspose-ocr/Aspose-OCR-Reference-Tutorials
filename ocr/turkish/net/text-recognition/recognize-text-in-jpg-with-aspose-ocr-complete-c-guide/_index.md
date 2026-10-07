---
category: general
date: 2026-01-09
description: Aspose OCR'i C#'ta kullanarak jpg'deki metni hızlıca tanıyın. Tek bir
  öğreticide görüntüden metin çıkarma, görüntüyü JSON ve EPUB'a dönüştürmeyi öğrenin.
draft: false
keywords:
- recognize text in jpg
- extract text from image
- convert image to json
- convert image to epub
- create epub from image
language: tr
og_description: Aspose OCR ile jpg'deki metni tanıyın. Bu kılavuz, görüntüden metin
  çıkarmayı, görüntüyü JSON ve EPUB'a dönüştürmeyi ve bir görüntüden ePub oluşturmayı
  gösterir.
og_title: JPG'de metni tanıma – Tam C# Öğreticisi
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCR ile jpg'de metin tanıma – Tam C# Rehberi
url: /tr/net/text-recognition/recognize-text-in-jpg-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JPG'de Metin Tanıma – Tam C# Rehberi

JPG dosyalarında **JPG'de metin tanıma** ihtiyacı hiç duydunuz mu ama hangi kütüphaneyi seçeceğinizden emin değildiniz? Yalnız değilsiniz. Birçok geliştirici, bir fotoğraf ya da taranmış belgeden kelimeleri çıkarmaya ilk kez çalıştıklarında aynı duvara çarpar.  

İyi haber? Aspose OCR ile birkaç satır C# koduyla **görüntüden metin çıkarabilir**, ardından anında **görüntüyü JSON'a dönüştürebilir** ya da hatta **görüntüyü EPUB'a dönüştürebilir**—hepsi IDE'nizden çıkmadan.

Bu öğreticide, doğru NuGet paketlerini kurmaktan JPG'de metin tanımaya, sonucu yapılandırılmış JSON ve ePub belgesi olarak kaydetmeye kadar tüm iş akışını adım adım inceleyeceğiz. Sonuna geldiğinizde programlı olarak **görüntüden epub oluşturma** yeteneğine sahip olacaksınız; bu, e‑öğrenme platformları, dijital kütüphaneler veya aranabilir e‑kitaplara ihtiyaç duyan herhangi bir uygulama için kullanışlı bir hiledir.

---

## Gerekenler

- **.NET 6+** (veya .NET Framework 4.6+). Kod, herhangi bir yeni çalışma zamanında çalışır.
- **Aspose.OCR** NuGet paketi – temel OCR motoru.
- **Aspose.Publishing** NuGet paketi – ePub çıktı formatı için gereklidir.
- Diskinizde bir yerde bulunan `input.jpg` adlı bir görüntü dosyası (yolu kendi dosyanıza göre değiştirin).
- Bir metin editörü veya IDE (Visual Studio, VS Code, Rider—seçim size).

Hepsi bu. Ek hizmetler, harici API'ler yok, sadece birkaç kütüphane ve bir JPG dosyası.

---

## Adım 1: Projenizi **JPG'de metin tanıma** için ayarlayın

İlk olarak, yeni bir konsol uygulaması oluşturun (veya mevcut bir projeye ekleyin). Ardından NuGet Paket Yöneticisi aracılığıyla iki Aspose paketini ekleyin:

```bash
dotnet add package Aspose.OCR
dotnet add package Aspose.Publishing
```

> **Pro ipucu:** Visual Studio kullanıyorsanız, projeye sağ‑tıklayın → *Manage NuGet Packages* → *Aspose.OCR* ve *Aspose.Publishing* paketlerini arayın, ardından **Install** (Yükle) düğmesine tıklayın.

Bu paketler, **görüntüden metin çıkarma** ve daha sonra bir ePub dosyası oluşturma ihtiyacınız olan her şeyi sağlar.

---

## Adım 2: Aspose OCR Kullanarak **görüntüden metin çıkarma**

Şimdi JPG'yi okuyup karakterleri çıkaran kodu yazacağız.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToTextDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create an OCR engine instance
            var ocrEngine = new OcrEngine();

            // 2️⃣ Recognize text from the JPG file
            // Replace the path with the location of your own image
            string inputPath = @"YOUR_DIRECTORY\input.jpg";
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // 3️⃣ Show the recognized text in the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Neden bu çalışıyor:** `OcrEngine`, düşük seviyeli görüntü ön işleme, dil algılama ve karakter segmentasyonunu soyutlar. Sadece bir dosyaya işaret edersiniz ve `OcrResult` nesnesi içinde düz metin dizesi (`ocrResult.Text`) ve zengin bir meta veri seti döndürür.

---

## Adım 3: **Görüntüyü JSON'a dönüştürme** – OCR Sonucunu Dışa Aktarma

OCR çıktısını yapılandırılmış bir formatta (API'ler, veritabanları veya sonraki işlemler için) saklamanız gerekiyorsa, Aspose sonucu JSON'a serileştirmeyi çok basit hale getirir.

```csharp
// 4️⃣ Convert the OCR result to JSON
string jsonContent = ocrResult.ToJson();

// 5️⃣ Save the JSON to disk
string jsonPath = @"YOUR_DIRECTORY\output.json";
File.WriteAllText(jsonPath, jsonContent);

Console.WriteLine($"JSON saved to: {jsonPath}");
```

Oluşturulan JSON yaklaşık olarak şu şekilde görünür (kısaltılmıştır):

```json
{
  "Text": "Hello world!",
  "Confidence": 0.98,
  "PageCount": 1,
  "Words": [
    { "Value": "Hello", "Confidence": 0.99 },
    { "Value": "world!", "Confidence": 0.97 }
  ]
}
```

**Ne zaman kullanılır:** OCR verilerini bir web servisine besliyorsanız, NoSQL bir depoda saklıyorsanız veya herhangi bir dil tarafından ayrıştırılabilen taşınabilir bir temsil gerektiriyorsa JSON mükemmeldir.

---

## Adım 4: **Görüntüyü EPUB'a dönüştürme** – eKitap Olarak Kaydetme

Aspose Publishing, EPUB dahil olmak üzere çeşitli e‑kitap formatlarını destekler. `OcrResult` üzerinde `Save` metodunu çağırarak tanınan metni ve isteğe bağlı olarak orijinal görüntüyü içeren tam uyumlu bir ePub dosyası oluşturabilirsiniz.

```csharp
// 6️⃣ Save the OCR result as an ePub document
string epubPath = @"YOUR_DIRECTORY\output.epub";
ocrResult.Save(epubPath, OcrOutputFormat.Epub);

Console.WriteLine($"EPUB created at: {epubPath}");
```

**Ne elde edersiniz:** Herhangi bir okuyucuda (Calibre, Apple Books, Adobe Digital Editions) açabileceğiniz bir ePub. Dosya, aranabilir içerik olarak çıkarılan metni ve arka plan katmanı olarak kaynak görüntüyü içerir—**görüntüden epub oluşturma** iş akışları için idealdir.

---

## Adım 5: Tam Çalışan Örnek – JPG'den JSON ve EPUB'a

Her şeyi bir araya getirerek, işte tam ve çalıştırmaya hazır program. Bunu `Program.cs` dosyasına kopyalayıp yapıştırın, dosya yollarını ayarlayın ve **F5** tuşuna basın.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Output;

namespace ImageToEpubDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            var ocrEngine = new OcrEngine();

            // Path to the input JPG
            string inputPath = @"YOUR_DIRECTORY\input.jpg";

            // Recognize text
            var ocrResult = ocrEngine.RecognizeImage(inputPath);

            // Output recognized text to console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
            Console.WriteLine();

            // Export to JSON
            string jsonPath = @"YOUR_DIRECTORY\output.json";
            File.WriteAllText(jsonPath, ocrResult.ToJson());
            Console.WriteLine($"JSON saved to: {jsonPath}");

            // Export to EPUB
            string epubPath = @"YOUR_DIRECTORY\output.epub";
            ocrResult.Save(epubPath, OcrOutputFormat.Epub);
            Console.WriteLine($"EPUB created at: {epubPath}");
        }
    }
}
```

Programı çalıştırın ve üç şey görmelisiniz:

1. Konsolda tanınan metin yazdırılır.
2. `output.json` dosyası, yapılandırılmış OCR verilerini içerir.
3. `output.epub` dosyası, herhangi bir e‑kitap okuyucusunda açılabilir.

---

## Yaygın Sorular ve Kenar Durumları

- **Görüntü PNG veya BMP ise ne olur?**  
  Aspose OCR, çoğu raster formatını (PNG, BMP, TIFF, GIF) destekler. `inputPath` içindeki dosya uzantısını değiştirmeniz yeterlidir; aynı kod çalışır.

- **İngilizce dışındaki bir dili belirtebilir miyim?**  
  Evet. `RecognizeImage` metodunu çağırmadan önce `ocrEngine.Language = OcrLanguage.French;` (veya desteklenen herhangi bir dil) olarak ayarlayın.

- **Çok sayfalı PDF'ler ne olur?**  
  PDF'ler için önce her sayfayı bir görüntüye dönüştürürsünüz (Aspose.PDF bunu yapabilir) ve ardından her görüntüyü `RecognizeImage` metoduna beslersiniz. Ortaya çıkan `OcrResult` nesneleri, JSON veya EPUB'a dışa aktarmadan önce birleştirilebilir.

- **Düşük güven puanları alıyorum. Doğruluğu nasıl artırabilirim?**  
  Görüntüyü ön işleme tabi tutun: kontrastı artırın, eğikliği düzeltin veya gri tonlamaya çevirin. Aspose OCR ayrıca ayarlayabileceğiniz `PreprocessOptions` sunar.

---

## Sonuç

Artık Aspose OCR kullanarak **JPG dosyalarında metin tanıma**, ardından veri akışları için **görüntüyü JSON'a dönüştürme** ve aranabilir e‑kitaplar oluşturmak için **görüntüyü EPUB'a dönüştürme** konularında sağlam, uçtan uca bir tarifiniz var. Yaklaşım hafiftir, sadece iki NuGet paketi gerektirir ve tüm modern .NET çalışma zamanlarında çalışır.

Buradan şunları yapabilirsiniz:

- JSON çıktısını bir arama indeksine entegre edin (Azure Cognitive Search, Elastic).
- Görüntü klasörünü toplu işleyerek bir ePub kitap kütüphanesi oluşturun.
- İş akışını çeviri API'leriyle genişleterek çok dilli e‑kitapları otomatik oluşturun.

Deneyin, farklı görüntü kaliteleriyle oynayın ve OCR motorunun zor işini yapmasına izin verin. Kodlamanın tadını çıkarın!

---

![recognize text in jpg output screenshot](placeholder-image.png "recognize text in jpg example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}