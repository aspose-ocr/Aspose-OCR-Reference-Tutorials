---
category: general
date: 2026-04-06
description: C#'ta Aspose OCR kullanarak görüntü metnini tanıyın. Metni nasıl çıkaracağınızı,
  C#'ta görüntü dosyasını nasıl yükleyeceğinizi ve basit adım adım bir örnekle C#'ta
  JSON nasıl yazılacağını öğrenin.
draft: false
keywords:
- recognize image text
- how to extract text
- write json in c#
- load image file c#
language: tr
og_description: Aspose OCR ile C#'ta görüntü metnini tanıyın. Bu rehber, metni nasıl
  çıkaracağınızı, C#'ta görüntü dosyasını nasıl yükleyeceğinizi ve JSON'u hızlı bir
  şekilde C#'ta nasıl yazacağınızı gösterir.
og_title: C# ile resim metnini tanıma – Tam Adım Adım Kılavuz
tags:
- OCR
- C#
- Aspose
title: C#'da görüntü metnini tanıma – JSON Dışa Aktarımlı Tam Kılavuz
url: /tr/net/text-recognition/recognize-image-text-in-c-full-guide-with-json-export/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta görüntü metnini tanıma – Tam Adım‑Adım Kılavuz

Hiç taranmış bir makbuzdan **görüntü metnini tanıma** ihtiyacı duydunuz mu ama hangi kütüphaneyi seçeceğinizi bilemediniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada—gider takipçileri, fatura işleyicileri, hatta erişilebilirlik araçları—bir resimden kelimeleri çıkarmak ilk engeldir.  

Bu öğreticide, Aspose OCR kütüphanesini kullanarak **görüntü metnini tanıma**, **metni nasıl çıkarılır** gösteren, **c#'ta görüntü dosyasını yükleme** işlemini doğru şekilde yapan ve sonunda **c#'ta json yazma** ile sonuçları saklayıp aktarabileceğiniz bir çözümü adım adım inceleyeceğiz. Sonunda, herhangi bir PNG dosyasını düzenli bir JSON yüküne dönüştüren çalıştırılabilir bir konsol uygulamanız olacak.

---

## Gereksinimler

- **.NET 6+** (kod .NET Framework 4.8 ile de çalışır, ancak .NET 6 önerilir).
- **Aspose.OCR for .NET** NuGet paketi. `dotnet add package Aspose.OCR` komutuyla kurun.
- Uygulamanızın okuyabileceği bir konumda bulunan örnek bir resim (`input.png`).  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör—fancy IDE hilesi gerekmez.

> Pro ipucu: Resim dosyalarınızı proje içinde `Resources` adlı bir klasöre koyun; bu sayede yollar düzenli olur ve “dosya bulunamadı” hataları önlenir.

---

## 1. Adım: c#'ta görüntü dosyasını yükleme – Görüntüyü yükleyin

OCR motorunun sihrini çalıştırabilmesi için önce **c#'ta görüntü dosyasını yükleme** güvenli bir şekilde yapılmalıdır. `Image.FromFile` yöntemi, yol yanlışsa ya da dosya desteklenmeyen bir formatta ise istisna fırlatır; bu yüzden buna karşı önlem alacağız.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // Define input and output paths
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // Verify the image exists
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // Load the image – this is the “load image file c#” step
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // Continue to OCR...
        }
    }
}
```

*Neden önemli*: Görüntüyü bir `using` bloğu içinde yüklemek, yönetilmeyen GDI+ kaynaklarının hemen serbest bırakılmasını sağlar ve uzun çalışan servislerde bellek sızıntılarını önler.

---

## 2. Adım: Aspose OCR ile metni nasıl çıkarılır

Bitmap belleğe yüklendikten sonra **görüntü metnini tanıma** motoruna teslim ederiz. Aspose’un `OcrEngine`i oldukça basittir: bir örnek oluşturun, `Recognize` metodunu çağırın ve ham metin, güven skorları ve sınırlama kutuları gibi bilgileri içeren bir `OcrResult` nesnesi elde edin.

```csharp
// Inside the using block from Step 1
var ocrEngine = new OcrEngine();

// Perform OCR – this is the core “how to extract text” operation
OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

// Quick sanity check
if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
{
    Console.WriteLine("⚠️ No text detected. Try a clearer image.");
    return;
}
Console.WriteLine("✅ OCR succeeded. Extracted text:");
Console.WriteLine(ocrResult.Text);
```

*Açıklama*: `Recognize` metodu yerleşik sinir ağını çalıştırır. En iyi sonuçları yüksek kontrastlı, 300 DPI görüntülerde verir. Bulanık bir fotoğraf verirseniz güven skoru düşer—üretim kodu için ön‑işleme (düzeltme, ikilileştirme) düşünün.

---

## 3. Adım: c#'ta json yazma – OCR sonucunu dışa aktarma

Çoğu API JSON bekler, bu yüzden **c#'ta json yazma** işlemini Aspose’un `JsonExport`iyle yapacağız. Kütüphane, satır bilgileri ve güven değerlerini koruyarak tüm `OcrResult` nesnesini serileştirir.

```csharp
// Still inside the same using block
string jsonResult = JsonExport.ToJson(ocrResult);

// Persist the JSON to disk
File.WriteAllText(outputPath, jsonResult);
Console.WriteLine($"💾 JSON written to {outputPath}");
```

### Beklenen JSON çıktısı

```json
{
  "Text": "Total: $12.34\r\nDate: 2026-04-01\r\n...",
  "Words": [
    { "Text": "Total", "Confidence": 0.98, "Rectangle": { "X": 10, "Y": 15, "Width": 50, "Height": 12 } },
    { "Text": "$12.34", "Confidence": 0.96, "Rectangle": { "X": 70, "Y": 15, "Width": 45, "Height": 12 } }
    // … more words …
  ]
}
```

*Neden JSON?* Dilde bağımsızdır, ayrıştırması kolaydır ve aşağı akış doğrulaması için ihtiyaç duyabileceğiniz ayrıntılı OCR meta verilerini tutar.

---

## 4. Adım: Tam, çalıştırılabilir program

Parçaları bir araya getirdiğimizde, işte eksiksiz konsol uygulaması. Kopyala‑yapıştır, NuGet paketlerini geri yükle ve **F5** tuşuna bas.

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Export;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Configuration – adjust these paths as needed
        // -------------------------------------------------
        string inputPath  = Path.Combine("Resources", "input.png");
        string outputPath = Path.Combine("Resources", "output.json");

        // -------------------------------------------------
        // Validate input file
        // -------------------------------------------------
        if (!File.Exists(inputPath))
        {
            Console.WriteLine($"❌ Image not found at {inputPath}");
            return;
        }

        // -------------------------------------------------
        // Load image (load image file c#)
        // -------------------------------------------------
        using (Image receiptImage = Image.FromFile(inputPath))
        {
            // -------------------------------------------------
            // Initialize OCR engine and recognize text
            // -------------------------------------------------
            var ocrEngine = new OcrEngine();
            OcrResult ocrResult = ocrEngine.Recognize(receiptImage);

            if (ocrResult == null || string.IsNullOrWhiteSpace(ocrResult.Text))
            {
                Console.WriteLine("⚠️ No text detected. Try a clearer image.");
                return;
            }

            Console.WriteLine("✅ OCR succeeded. Sample output:");
            Console.WriteLine(ocrResult.Text.Substring(0, Math.Min(100, ocrResult.Text.Length)) + "...");

            // -------------------------------------------------
            // Convert result to JSON (write json in c#)
            // -------------------------------------------------
            string jsonResult = JsonExport.ToJson(ocrResult);
            File.WriteAllText(outputPath, jsonResult);
            Console.WriteLine($"💾 JSON written to {outputPath}");
        }
    }
}
```

Programı çalıştırın ve `Resources/output.json` dosyasını açın—motorun tanıdığı her şeyin güzel yapılandırılmış bir JSON temsili görünecek.

---

## Yaygın Kenar Durumlarını Ele Alma

| Durum | Yapılması Gereken | Neden |
|-----------|------------|-----|
| **Görüntü null veya bozuk** | `Image.FromFile`ı try/catch içinde sarmalayın ve istisnayı loglayın. | Uygulamanın çökmesini önler ve net bir hata mesajı verir. |
| **Düşük güven skorları** | `ocrResult.Words[i].Confidence` değerini kontrol edin. 0.75’in altındaysa ön‑işleme (DPI artırma, keskinleştirme) yapın. | Alt akış işlemleri (ör. tutar çıkarma) için güvenilirliği artırır. |
| **Büyük dosyalar (>10 MB)** | OCR öncesinde resmi küçültün (`receiptImage = new Bitmap(receiptImage, new Size(width/2, height/2))`). | Bellek yükünü azaltır ve tanıma süresini hızlandırır. |
| **Çok‑dilli belgeler** | `ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;` | Motorun her iki dilden karakterleri algılamasını sağlar. |

---

## Bonus: OCR sonucunu görselleştirme (isteğe bağlı)

Her kelimenin resim üzerindeki konumunu görmek isterseniz, sınırlama kutuları çizebilirsiniz:

```csharp
using (Graphics g = Graphics.FromImage(receiptImage))
{
    foreach (var word in ocrResult.Words)
    {
        var rect = new Rectangle(word.Rectangle.X, word.Rectangle.Y,
                                 word.Rectangle.Width, word.Rectangle.Height);
        g.DrawRectangle(Pens.Red, rect);
    }
    receiptImage.Save(Path.Combine("Resources", "annotated.png"));
}
```

Ortaya çıkan `annotated.png` dosyası, tanınan her kelimenin etrafında kırmızı dikdörtgenler gösterir—hata ayıklama için çok işe yarar.

---

## Sonuç

C#'ta **görüntü metnini tanıma** sürecini baştan sona tamamladık: görüntü dosyasını yükleme, Aspose OCR ile **metni nasıl çıkarılır** ve sonunda **c#'ta json yazma** ile veriyi her yere taşıma. Tam örnek kutudan çıkar çıkmaz çalışır ve ek ipuçları bulanık makbuzlar, devasa dosyalar veya çok‑dilli taramalarla başa çıkmanıza yardımcı olur.

Sırada ne var? Aspose yerine başka bir motor (Tesseract, Microsoft OCR) deneyin ve güven skorlarını karşılaştırın, ya da JSON’u bir veritabanına göndererek harcama raporlaması yapın. Konsol uygulamasını bir ASP .NET Core Web API'ye dönüştürüp görüntü yüklemelerini anında JSON olarak dönecek şekilde genişletebilirsiniz.

Ölçekleme, hata yönetimi veya Azure Functions entegrasyonu hakkında sorularınız mı var? Yorum bırakın ya da GitHub’da bana mesaj atın. İyi kodlamalar, OCR'ınız her zaman net olsun! 

---

![Screenshot of OCR JSON output – recognize image text example](https://example.com/ocr-example.png "recognize image text example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}