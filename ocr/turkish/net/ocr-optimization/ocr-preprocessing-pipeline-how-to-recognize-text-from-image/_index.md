---
category: general
date: 2026-01-02
description: 'OCR ön işleme hattı oluşturmayı öğrenin: görüntüyü otomatik olarak eğriltme,
  OCR için görüntüyü ön işleme ve Aspose.OCR ile jpg dosyasından metin okuma – adım
  adım rehber.'
draft: false
keywords:
- ocr preprocessing pipeline
- recognize text from image
- auto deskew image
- preprocess image for ocr
- read text from jpg
language: tr
og_description: OCR ön işleme hattını keşfedin; görüntüleri otomatik olarak düzleştirir
  ve jpg gibi görüntü dosyalarından metin tanımanıza olanak tanır. Tam kod, açıklamalar
  ve ipuçları.
og_title: OCR ön işleme boru hattı – Tam C# Rehberi
tags:
- OCR
- C#
- Image Processing
title: OCR ön işleme boru hattı – C#'ta Görüntüden Metin Tanıma
url: /tr/net/ocr-optimization/ocr-preprocessing-pipeline-how-to-recognize-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ocr preprocessing pipeline – Tam C# Kılavuzu

Eğri, gürültülü veya sadece okunması zor **görüntüden metin tanıma** dosyalarıyla hiç zorlandınız mı? Yalnız değilsiniz. Gerçek dünyadaki birçok projede tarayıcı veya telefon kamerasından aldığınız ham fotoğraf, OCR motorunun işini yapabilmesi için biraz ilgiye (TLC) ihtiyaç duyar.

İşte **ocr preprocessing pipeline** burada devreye giriyor. Görüntüyü otomatik olarak düzleştirerek, arka plan lekelerini azaltarak ve genel olarak temizleyerek doğruluğu büyük ölçüde artırırsınız. Bu öğreticide, **OCR için görüntüyü ön işler**, resmi otomatik olarak düzleştirir ve sonunda Aspose.OCR kullanarak **jpg'den metin okur** tam çalışan bir örnek üzerinden ilerleyeceğiz.

> **Ne kazanacaksınız:** çarpık, gürültülü bir JPG'yi yükleyen, akıllı bir ön işleme hattı üzerinden çalışan ve çıkarılan metni konsola yazdıran, çalıştırmaya hazır bir C# konsol uygulaması.

## Önkoşullar

- .NET 6 SDK veya daha yenisi (kod .NET Core ile de derlenir)
- Visual Studio 2022 veya istediğiniz herhangi bir IDE
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)
- `skewed_noisy.jpg` gibi bir örnek görüntü, referans alabileceğiniz bir klasöre yerleştirilmiş

Başka hiçbir dış kütüphane gerekmez; diğer her şey Aspose.OCR içinde bulunur.

---

## 1. Adım – Projeyi Kurun ve Görüntünüzü Yükleyin

İlk olarak, yeni bir konsol projesi oluşturun ve Aspose.OCR referansını ekleyin. Ardından işlemek istediğiniz görüntüyü yükleyin.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);
```

> **Neden önemli:** `Bitmap` sınıfı, OCR motorunun ön işleme aşaması için ihtiyaç duyduğu doğrudan piksel erişimini sağlar. Yol yanlışsa `FileNotFoundException` alırsınız, bu yüzden konumu iki kez kontrol edin.

---

## 2. Adım – OCR Motoru Örneğini Oluşturun

Sonra, `OcrEngine` örneğini oluşturun. Bu nesne, tüm **ocr preprocessing pipeline**'ı yönetecek.

```csharp
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();
```

> **Pro ipucu:** Aynı `OcrEngine`'i birden fazla görüntüde yeniden kullanabilirsiniz; sadece her seferinde `RecognitionOptions`'ı sıfırlayın.

---

## 3. Adım – Ön İşleme Ayarlarını Yapılandırın (Hattın Çekirdeği)

Burada iki en güçlü özelliği etkinleştiriyoruz: **auto deskew image** ve **noise reduction**. Her ikisi de resmi doğru metin çıkarımı için hazırlayan hattın bir parçasıdır.

```csharp
        // Configure recognition options with the new preprocessing pipeline
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // Apply AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };
```

> **Nasıl çalışır:**  
> - `EnableSmartDeskew`, görüntünün temel açılarını inceler ve onu 0°'ye döndürür; bu, çarpık taramalar için çok önemlidir.  
> - `EnableNoiseReduction`, hafif bir AI filtresi çalıştırarak lekeleri siler, ancak soluk karakterleri silmez.  
> - `NoiseReductionLevel`, hızı kaliteye göre ayarlamanızı sağlar; `Medium` çoğu JPG için iyi bir dengedir.

---

## 4. Adım – OCR'ı Çalıştırın ve Sonucu Yakalayın

Şimdi görüntüyü ve seçenekleri motorun içine veriyoruz. Metod, çıkarılan dizeyi ve güven skorlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Perform OCR on the image using the configured options
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);
```

> **Köşe durum:** Görüntü tamamen boşsa, `ocrResult.Text` boş bir dize olur. Üretim kodunda ilerlemeden önce `ocrResult.HasText` kontrol etmek isteyebilirsiniz.

---

## 5. Adım – Tanınan Metni Çıktılayın

Son olarak, sonucu konsola yazdırın. Bu, sadece birkaç satır kodla **görüntüden metin tanıma** dosyalarını yapabildiğimizi gösterir.

```csharp
        // Output the recognized text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

**Beklenen çıktı (örnek):**

```
=== Extracted Text ===
Invoice #12345
Date: 01/01/2024
Total: $1,250.00
Thank you for your business!
```

Görüntü gürültülü ya da kötü döndürülmüşse, bozuk karakterler fark edeceksiniz. **ocr preprocessing pipeline** sayesinde bu sorunlar büyük ölçüde azalır.

---

## 6. Adım – Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlemeye hazır tam kaynak dosyası yer alıyor. `YOUR_DIRECTORY` ifadesini JPG'nizin gerçek yolu ile değiştirin.

```csharp
using Aspose.OCR;
using System.Drawing;

class PreprocessExample
{
    static void Main()
    {
        // 1️⃣ Load the image that needs OCR
        var imagePath = "YOUR_DIRECTORY/skewed_noisy.jpg";
        var image = new Bitmap(imagePath);

        // 2️⃣ Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // 3️⃣ Configure the preprocessing pipeline (auto deskew + noise reduction)
        var recognitionOptions = new RecognitionOptions
        {
            Preprocess = new PreprocessSettings
            {
                EnableSmartDeskew = true,          // Auto‑detect and correct rotation
                EnableNoiseReduction = true,      // AI‑based denoising
                NoiseReductionLevel = NoiseLevel.Medium
            },
            Language = Language.English
        };

        // 4️⃣ Run OCR with the configured pipeline
        var ocrResult = ocrEngine.Recognize(image, recognitionOptions);

        // 5️⃣ Print the extracted text
        System.Console.WriteLine("=== Extracted Text ===");
        System.Console.WriteLine(ocrResult.Text);
    }
}
```

Bunu `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve konsolun temizlenmiş metinle dolduğunu izleyin.

---

## 7. Adım – Daha İleri – Hattı İnce Ayarlama

**ocr preprocessing pipeline** esnektir. İşte keşfedebileceğiniz birkaç yaygın varyasyon:

| Varyasyon | Ne Zaman Kullanılır | Kod Parçası |
|-----------|---------------------|--------------|
| **Daha yüksek gürültü azaltma** (ör. `NoiseLevel.High`) | Düşük çözünürlüklü kameralardan çok grenli taramalar | `NoiseReductionLevel = NoiseLevel.High` |
| **Düzleştirmeyi devre dışı bırak** | Görüntüler zaten mükemmel hizalanmış | `EnableSmartDeskew = false` |
| **Çok‑dilli destek** | Belgeler hem İngilizce hem İspanyolca içeriyor | `Language = Language.English | Language.Spanish` |
| **Özel DPI ölçekleme** | Çok küçük fontlar yükseltme gerektiriyor | `recognitionOptions.Dpi = 300;` |

Bu ayarlarla deneme yapmak, **OCR için görüntüyü ön işleme** adımını veri kümenizin özelliklerine göre ince ayar yapmanızı sağlar.

---

## Sonuç

C#'ta **ocr preprocessing pipeline** oluşturduk; bu **görüntüyü otomatik düzleştirir**, gürültüyü azaltır ve sonunda JPG gibi **görüntüden metin tanıma** dosyalarını tanır. Aspose.OCR’nin `RecognitionOptions` içindeki `PreprocessSettings`'i yapılandırarak, titrek ve lekeli bir resmi sadece birkaç satır kodla temiz, aranabilir bir metne dönüştürdük.

> **Ana çıkarımlar:**  
> - Her zaman önce görüntüyü temizleyin – OCR motoru düz, düşük gürültülü girdilerde en iyi çalışır.  
> - Hattı tamamen yapılandırılabilir; düzleştirme ve gürültü azaltmayı ihtiyaçlarınıza göre ayarlayın.  
> - Aynı desen PDF'ler, TIFF'ler veya Aspose.OCR'ye beslediğiniz herhangi bir bitmap kaynağı için de çalışır.

Bir sonraki adıma hazır mısınız? Bir dosya topluluğunu hat üzerinden geçirmeyi deneyin veya kodu bir web API'ye entegre edin; böylece kullanıcılar resim yükleyip anında metin alabilir. Ayrıca Aspose’un belge dönüşüm özelliklerini keşfederek çıkarılan metni aranabilir PDF'lere dönüştürebilirsiniz.

Kodlamaktan keyif alın, ve OCR sonuçlarınız her zaman doğru olsun! 🚀

![ocr ön işleme hattının adımlarını gösteren diyagram: görüntüyü yükle → akıllı düzleştirme → gürültü azaltma → OCR → metni çıktıla](ocr-preprocessing-pipeline.png "ocr ön işleme hattı diyagramı")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}