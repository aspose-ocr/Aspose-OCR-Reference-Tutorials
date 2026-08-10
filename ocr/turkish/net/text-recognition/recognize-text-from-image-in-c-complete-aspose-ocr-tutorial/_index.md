---
category: general
date: 2026-05-06
description: Aspose OCR'i C#'ta kullanarak görüntüden metin tanımayı öğrenin. Makbuzdan
  metin çıkarın, OCR için görüntüyü yükleyin ve tam bir Aspose OCR örneğini görün.
draft: false
keywords:
- recognize text from image
- extract text from receipt
- load image for OCR
- Aspose OCR example
language: tr
og_description: Aspose OCR ile görüntüden metin tanımayı öğrenin, makbuzdan metin
  çıkarın ve OCR için görüntüyü yükleyin; kısa ve adım adım bir rehber.
og_title: C#'de görüntüden metin tanıma – Tam Aspose OCR Öğreticisi
tags:
- C#
- OCR
- Aspose
title: C#'de görüntüden metin tanıma – Tam Aspose OCR Öğreticisi
url: /tr/net/text-recognition/recognize-text-from-image-in-c-complete-aspose-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görselden Metin Tanıma C# – Tam Aspose OCR Öğreticisi

Herhangi bir zamanda **görselden metin tanıma** ihtiyacı duydunuz mu ama hangi kütüphaneyi seçeceğinizden emin değildiniz? Tek başınıza değilsiniz—birçok geliştirici, bir makbuzdan sayı çekmeye ya da bir form taramaya çalışırken aynı duvara çarpıyor. İyi haber, Aspose OCR tüm süreci çocuk oyuncağı haline getiriyor ve bu öğreticide size sadece birkaç C# satırıyla **makbuzdan metin çıkarma** işlemini gerçekleştiren **tam bir Aspose OCR örneği** göstereceğiz.

Önümüzdeki birkaç dakikada **OCR için görsel yükleme**, toplam tutarın bulunduğu tam bölgeyi tanımlama, motoru çalıştırma ve sonunda sonucu gösterme konularını öğreneceksiniz. Dış dökümantasyonlara belirsiz referanslar yok, eksik parçalar yok—kopyala‑yapıştır ve çalıştırmanız için gereken her şey burada. Biraz kurulum, birkaç adım ve görsel dosyalarından anında metin tanıma yapabileceksiniz.

> **Edineceğiniz Kazanımlar**  
> * Görsel dosyalarından metin tanıyan çalıştırılabilir bir C# konsol uygulaması.  
> * OCR'ı belirli bir dikdörtgene sınırlamanın (hız ve doğruluk) nedenlerini anlama.  
> * Bulanık makbuzlar veya döndürülmüş taramalar gibi yaygın kenar durumlarını ele almanın ipuçları.  

---

## Gereksinimler

| Gereksinim | Neden Önemli |
|-------------|----------------|
| .NET 6.0 SDK (or later) | Aspose OCR, .NET Standard 2.0 / .NET 5+ kütüphanesi olarak sunulur, bu yüzden herhangi bir yeni çalışma zamanı yeterlidir. |
| Visual Studio 2022 (or VS Code) | Rahat bir IDE hata ayıklamayı hızlandırır, ancak C# derleyebilen herhangi bir editör de iş görür. |
| **Aspose.OCR for .NET** NuGet paketi | Görselden metin tanıyan temel kütüphanedir. |
| A sample receipt image (`receipt.jpg`) | **Makbuzdan metin çıkarma** işlemini göstermek için bu dosyayı kullanacağız. |

NuGet paketini aşağıdaki komutla kurabilirsiniz:

```bash
dotnet add package Aspose.OCR
```

Bu işlem tamamlandığında OCR için görsel yüklemeye hazırsınız.

---

## Adım 1: Görseli OCR için yükleme

İlk yapmanız gereken, motoru analiz etmek istediğiniz dosyaya yönlendirmektir. İşte burada ikincil anahtar kelime **load image for OCR** doğal olarak devreye girer.

```csharp
using Aspose.OCR;
using System.Drawing;

// Create the OCR engine instance
var ocrEngine = new OcrEngine();

// Load the receipt image – replace the path with your own file location
ocrEngine.SetImage(@"C:\Images\receipt.jpg");
```

> **İpucu:** Görseliniz proje klasöründe bulunuyorsa, `ocrEngine.SetImage("receipt.jpg");` gibi bir göreli yol kullanabilirsiniz. Dosyanın çıktı dizinine kopyalandığından emin olun (`Copy to Output Directory = PreserveNewest`).

`SetImage` yöntemi, System.Drawing'ın çözebildiği (JPEG, PNG, BMP vb.) herhangi bir formatı kabul eder; bu yüzden tek bir dosya türüyle sınırlı değilsiniz.

---

## Adım 2: İlgi Alanı Bölgesini Tanımlama – **extract text from receipt**

Tüm resmi taramak CPU döngülerini boşa harcar ve gürültü oluşturabilir. Aspose OCR'a toplam tutarın tam nerede olduğunu söyleyerek hız ve doğruluğu artırırsınız. İşte **makbuzdan metin çıkarma** kısmı.

```csharp
// Define a rectangle that covers the total amount on the receipt
// (x, y, width, height) – adjust these numbers for your own layout
var roi = new Rectangle(150, 500, 300, 80);
ocrEngine.SetRegionOfInterest(roi);
```

> **Neden bir dikdörtgen?**  
> OCR motoru bir piksel ızgarası üzerinde çalışır. Bölgeyi sınırladığınızda diğer her şeyi görmez—mağaza logosu ya da başlık satırından gelen istenmeyen karakterler artık sorun olmaz.

Tam koordinatlardan emin değilseniz, piksel konumlarını gösteren bir görüntüleyici (ör. Paint.NET) ile sayıları gözlemleyebilirsiniz.

---

## Adım 3: Motoru Çalıştırma – **recognize text from image** (birincil anahtar kelime)

Şimdi sihir gerçekleşir. Az önce tanımladığınız dikdörtgen içindeki pikselleri okumaya Aspose'ı söylersiniz.

```csharp
// Perform the recognition
OcrResult result = ocrEngine.Recognize();
```

`OcrResult` ham metni, güven puanlarını ve her kelime için sınırlayıcı kutuları içerir. Hızlı bir demo için sadece düz metni yazdıracağız.

```csharp
Console.WriteLine("Total amount detected: " + result.Text);
```

Programı çalıştırdığınızda aşağıdakine benzer bir çıktı görmelisiniz:

```
Total amount detected: $23.45
```

Çıktı bozuk görünüyorsa, ROI koordinatlarını tekrar kontrol edin veya görüntü çözünürlüğünü artırmayı deneyin.

---

## Adım 4: Sonucu İşleme – **Aspose OCR example**'ı parlatma

Sağlam bir çözüm, sadece dizeyi konsola dökmekten daha fazlasını yapar. Aşağıda boşlukları temizleyen, gereksiz satır sonlarını kaldıran ve çıkarılan değerin para miktarı gibi göründüğünü doğrulayan küçük bir yardımcı bulunuyor.

```csharp
static string CleanAmount(string raw)
{
    // Remove any non‑numeric characters except dot and comma
    var cleaned = new string(raw
        .Where(c => char.IsDigit(c) || c == '.' || c == ',')
        .ToArray());

    // Normalize decimal separator to dot
    cleaned = cleaned.Replace(',', '.');

    // If we end up with an empty string, return a friendly message
    return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
}

// ...

string amount = CleanAmount(result.Text);
Console.WriteLine($"Parsed amount: ${amount}");
```

Bu yardımcı, herhangi bir daha büyük faturalama sistemine ekleyebileceğiniz gerçekçi bir **Aspose OCR örneği** sunar.

---

## Adım 5: Tam Çalıştırılabilir Program – nihai **extract text from receipt** demosu

Her şeyi bir araya getirdiğinizde tek bir, kopyala‑yapıştır dosyası elde edersiniz. `Program.cs` olarak kaydedin ve `dotnet run` komutunu çalıştırın.

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;
using System.Linq;

class Program
{
    static void Main()
    {
        // 1️⃣ Load the image for OCR
        var ocrEngine = new OcrEngine();
        ocrEngine.SetImage(@"C:\Images\receipt.jpg");   // <-- adjust path

        // 2️⃣ Define the region that holds the total amount
        var roi = new Rectangle(150, 500, 300, 80);
        ocrEngine.SetRegionOfInterest(roi);

        // 3️⃣ Run the engine – recognize text from image
        OcrResult result = ocrEngine.Recognize();

        // 4️⃣ Clean up the output
        string amount = CleanAmount(result.Text);
        Console.WriteLine($"Total amount detected: ${amount}");
    }

    // Helper that sanitises the OCR output
    static string CleanAmount(string raw)
    {
        var cleaned = new string(raw
            .Where(c => char.IsDigit(c) || c == '.' || c == ',')
            .ToArray());

        cleaned = cleaned.Replace(',', '.');
        return string.IsNullOrWhiteSpace(cleaned) ? "N/A" : cleaned;
    }
}
```

**Beklenen çıktı**

```
Total amount detected: $23.45
```

Makbuz görseli daha karanlık veya metin eğikse, `Total amount detected: 23,45` gibi bir şey görebilirsiniz. `CleanAmount` yöntemi bunu standart ondalık biçimine dönüştürür.

---

## Görselden metin tanıma yaparken yaygın tuzaklar

### 1. Yanlış ROI koordinatları
Dikdörtgen çok küçükse motor karakterleri kırpar; çok büyükse gürültüyü yeniden getirir. Sayıları ince ayarlamak için görsel bir araç kullanın ya da basit bir görüntü‑işleme kütüphanesi (ör. OpenCV) ile makbuz sınırlarını programatik olarak tespit edin.

### 2. Düşük çözünürlüklü taramalar
OCR doğruluğu 150 dpi altında dramatik şekilde düşer. Tarama sürecini kontrol edebiliyorsanız en az 300 dpi hedefleyin. Düşük çözünürlüklü bir dosyayla çalışıyorsanız, `ocrEngine.SetResolution(300);` komutunu `Recognize()` çağrısından önce ekleyin.

### 3. Eğik veya döndürülmüş makbuzlar
Aspose OCR otomatik döndürme yapabilir, ancak bunu etkinleştirmeniz gerekir:

```csharp
ocrEngine.SetAutoRotate(true);
```

### 4. Dil ayarları
Varsayılan dil İngilizcedir. Makbuzunuz başka alfabeler içeriyorsa dili açıkça ayarlayın:

```csharp
ocrEngine.Language = OcrLanguage.French; // or any supported language
```

---

## Kenar durumları & varyasyonlar – **Aspose OCR example**'ı genişletme

* **Birden fazla alan:** Tarih ve vergi tutarını da çekmek ister misiniz? Yeni bir dikdörtgenle ROI adımını tekrarlayın ve `Recognize()`'ı tekrar çağırın (veya ROI'yi sıfırladıktan sonra aynı motoru yeniden kullanın).  
* **Toplu işleme:** `foreach (var file in Directory.GetFiles(@"C:\Receipts"))` döngüsüyle mantığı sararak onlarca dosyayı otomatik olarak işleyin.  
* **Asenkron yürütme:** `Recognize` yöntemi senkroniktir, ancak bir UI uygulaması geliştiriyorsanız `Task.Run` ile arka plan iş parçacığına taşıyabilirsiniz.

---

## Görsel referans

![görselden metin tanıma örneği](/images/ocr-demo.png "Aspose OCR sonucunu gösteren ekran görüntüsü – görselden metin tanıma")

*Ekran görüntüsü, tam program çalıştırıldıktan sonra konsol çıktısını gösterir.*

---

## Sonuç

Aspose OCR kullanarak **görselden metin tanıma** işlemini gerçekleştirdik, **OCR için görsel yükleme** adımını inceledik ve **makbuzdan metin çıkarma** iş akışını oluşturduk. Tam **Aspose OCR örneği** sadece birkaç satır kod içeriyor, ancak en yaygın senaryoları kapsıyor: ROI seçimi, sonuç temizleme ve tipik tuzakların ele alınması.

Sonraki adımlar? Dikdörtgeni dinamik bir tespit rutinine değiştirin, farklı dillerle deney yapın veya çıktıyı otomatik gider takibi için bir veritabanına entegre edin. Ufkunuz geniş, ve şimdi sahip olduğunuz temel sayesinde genişletmesi çok kolay.

Sorularınız mı var ya da iş birliğine dirençli bir makbuz mu var?

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}