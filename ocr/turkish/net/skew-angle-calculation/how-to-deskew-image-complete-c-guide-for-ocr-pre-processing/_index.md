---
category: general
date: 2025-12-29
description: Aspose OCR ile görüntüyü eğrilikten düzeltmeyi, arka planı kaldırmayı
  ve metni çıkarmayı öğrenin. OCR için görüntüyü ön işleme ve görüntüden metni tanıma
  konusunda adım adım C# kodu.
draft: false
keywords:
- how to deskew image
- how to remove background
- how to extract text
- preprocess image for ocr
- recognize text from image
language: tr
og_description: Görüntüyü eğriltmeyi düzeltme ve OCR doğruluğunu artırma. Arka planı
  kaldırmak, OCR için görüntüyü ön işleme ve Aspose kullanarak görüntüden metin tanıma
  konusunda bu kılavuzu izleyin.
og_title: Görüntüyü Eğikliği Düzeltme – C# OCR Ön İşleme Öğreticisi
tags:
- Aspose OCR
- C#
- Image preprocessing
title: Görüntüyü Düzeltme – OCR Ön İşleme için Tam C# Rehberi
url: /tr/net/skew-angle-calculation/how-to-deskew-image-complete-c-guide-for-ocr-pre-processing/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü Çarpıtmayı Düzeltme – OCR Ön‑işleme için Tam C# Kılavuzu

Bir tarayıcıdan çıkan ve yamuk bir kartpostal gibi görünen **how to deskew image** dosyalarını hiç merak ettiniz mi? Yalnız değilsiniz. Birçok gerçek‑dünya projesinde kaynak resimler eğik, gürültülü veya benekli bir arka planla boğuşur ve bu da OCR'ın zorlanmasına neden olur.  

Bu öğreticide, sadece **how to deskew image** değil, aynı zamanda **how to remove background**, **how to extract text** ve sonunda Aspose OCR for .NET kullanarak **recognize text from image** yapan pratik bir çözümü adım adım inceleyeceğiz. Sonunda OCR için bir görüntüyü ön‑işleyen ve temiz, aranabilir metin döndüren çalıştırılabilir bir C# programına sahip olacaksınız.

## Gerekenler

- .NET 6 SDK veya daha yeni bir sürüm (kod .NET Core ve .NET Framework’te de çalışır)  
- Visual Studio 2022 (veya tercih ettiğiniz herhangi bir editör)  
- Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`)  
- Çarpık ve gürültülü bir örnek görüntü (ör. `skewed_noisy.jpg`)  

Hepsi bu—ekstra yerel kütüphane yok, karmaşık komut‑satırı araçları da yok. Hadi başlayalım.

## Adım 1 – Giriş Görüntüsünü Yükle (How to Deskew Image Burada Başlar)

İlk yapmanız gereken şey, görüntüyü belleğe almaktır. Aspose OCR’nin `Image.Load` yöntemi bir dosya yolunu kabul eder ve üzerinde işlem yapabileceğiniz bir `Image` nesnesi döndürür.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Program
{
    static void Main()
    {
        // Load the original photo that needs deskewing and cleaning
        Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");
```

> **Neden önemli:** Görüntüyü yüklemek, çarpıtmayı düzeltmeden arka plan kaldırmaya kadar sonraki tüm dönüşümleri uygulamak için bir tutamaç sağlar.

## Adım 2 – Görüntüyü Çarpıtmayı Düzelt (How to Deskew Image Pratikte)

Aspose OCR, eğim açısını yapılandırılabilir bir eşik değerine kadar otomatik algılayan kullanışlı bir `Deskew` filtresi ile birlikte gelir. Burada, çoğu taranmış belgenin bu değeri aşmadığı için **5°**'ye kadar izin veriyoruz.

```csharp
        // Auto‑detect and correct rotation up to 5 degrees
        Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);
```

> **Pro ipucu:** Belgeleriniz 5°'den fazla döndürülmüşse, `angleThreshold` değerini 10 veya 15'e yükseltin. Algoritma, daha büyük açılarda bile hızlı kalır.

## Adım 3 – Düzeltlenmiş Görüntüyü Gürültüden Arındır

Gürültü, OCR doğruluğunun sessiz katilidir. Basit bir gürültü azaltma işlemi, gerçek karakterleri bulanıklaştırmadan nokta lekelerini yumuşatır.

```csharp
        // Reduce random speckles and grain
        Image denoised = deskewed.Denoise();
```

> **Arka planda ne oluyor?** Filtre, kenarları (harfleri) korurken izole pikselleri bastıran bir medyan bulanıklığı uygular.

## Adım 4 – Arka Planı Kaldır (How to Remove Background Etkili Bir Şekilde)

Açık renkli veya desenli bir arka plan OCR motorunu şaşırtabilir. Aspose OCR’nin `RemoveBackground` yöntemi ön plan metnini izole eder.

```csharp
        // Strip away uneven lighting or paper texture
        Image processedImage = denoised.RemoveBackground();
```

> **Neden arka plan kaldırılıyor?** Metin ile arka plan arasındaki kontrastı artırarak, motor karakterleri daha güvenilir bir şekilde ayırt edebilir; bu da doğrudan **how to extract text** sonuçlarını iyileştirir.

## Adım 5 – OCR Motorunu Başlat

Görüntü artık düz, temiz ve yüksek kontrastlı olduğuna göre OCR motorunu örnekleyebiliriz. Temel Latin alfabesi için ekstra yapılandırma gerekmez, ancak gerekirse dilleri değiştirebilirsiniz.

```csharp
        // Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **Not:** Aspose OCR 100'den fazla dili destekler. Çok dilli desteğe ihtiyacınız varsa, tanıma işleminden önce `ocrEngine.Language = OcrLanguage.YourLanguage;` ayarlayın.

## Adım 6 – Görüntüden Metin Tanı (How to Extract Text)

Motor hazır olduğunda, ön‑işlenmiş görüntüyü ona verin. `Recognize` yöntemi, ham metin ve güven puanlarını içeren bir `OcrResult` nesnesi döndürür.

```csharp
        // Perform the actual OCR
        OcrResult ocrResult = ocrEngine.Recognize(processedImage);
```

> **Sonuç içgörüsü:** `ocrResult.Text` düz metni tutar, `ocrResult.Confidence` (sorgularsanız) motorun her satır hakkındaki güven düzeyini gösterir.

## Adım 7 – Tanınan Metni Çıktıla

Son olarak, çıkarılan metni konsola yazdırın—veya bir dosyaya, veritabanına, iş akışınıza uygun bir yere kaydedin.

```csharp
        // Show the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

Tam program artık çalıştırılabilir. Derleyip çalıştırın; kaynak resim çarpık ve gürültülü olsa bile temiz, okunabilir bir metin görmelisiniz.

![how to deskew image örneği](/images/deskew-demo.png "Aspose OCR kullanarak how to deskew image demo")

*Yukarıdaki ekran görüntüsü, çarpıtmayı düzeltilmiş görüntünün ön‑ve‑son halini göstererek ön‑işleme hattının etkisini ortaya koyar.*

## Kenar Durumları ve Sık Sorulan Sorular

### Görüntü 5°'den fazla döndürülmüşse ne olur?

`Deskew` çağrısındaki `angleThreshold` değerini artırın. Algoritma hâlâ doğru açıyı otomatik algılayacak, sadece daha geniş bir arama penceresinde.

### Belgem renkli metin içeriyor—`RemoveBackground` bunu bozar mı?

`RemoveBackground` parlaklık üzerine çalışır, bu yüzden renkli metin temizlenmeden önce gri tonlamaya dönüştürülür. Rengi sonraki işlemler için korumanız gerekiyorsa, bu adımı atlayıp sadece gürültü azaltmaya güvenin.

### Çok sayfalı PDF'leri nasıl ele alırım?

Her PDF sayfasını bir görüntüye dönüştürün (ör. Aspose.PDF kullanarak), ardından her görüntüyü aynı işlem hattından geçirin. Sayfalar üzerinde döngü yaparak `ocrResult.Text` dizelerini birleştirin.

### El yazısı notlar için doğruluğu artırabilir miyim?

`ocrEngine.Options.UseNeuralNetwork = true;` özelliğini etkinleştirmeyi (yeni Aspose sürümlerinde mevcut) ve işleme başlamadan önce görüntü çözünürlüğünü en az 300 dpi'ye yükseltmeyi düşünün.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, gerekli tüm `using` yönergeleri ve yorumları içeren tam kaynak dosya yer alıyor. Yeni bir konsol projesine yapıştırın ve **F5** tuşuna basın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main()
        {
            // 1️⃣ Load the original image (skewed, noisy, etc.)
            Image originalImage = Image.Load("YOUR_DIRECTORY/skewed_noisy.jpg");

            // 2️⃣ Deskew – auto‑detect tilt up to 5°
            Image deskewed = ImageFilters.Deskew(originalImage, angleThreshold: 5);

            // 3️⃣ Denoise – smooth out speckles
            Image denoised = deskewed.Denoise();

            // 4️⃣ Remove background – boost contrast
            Image processedImage = denoised.RemoveBackground();

            // 5️⃣ Initialise OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // 6️⃣ Recognize text from the cleaned image
            OcrResult ocrResult = ocrEngine.Recognize(processedImage);

            // 7️⃣ Output the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**Beklenen çıktı** (basit bir fatura örneği):

```
=== OCR Output ===
Invoice #12345
Date: 2025‑12‑01
Total: $1,250.00
Thank you for your business!
```

Çıktı bozuk görünüyorsa, kaynak görüntünün yeterince net olduğundan ve çarpıtma açısının ayarladığınız eşikten büyük olmadığından emin olun.

## Sonuç

**how to deskew image** adım adım ele alındı, **how to remove background** gösterildi, ön‑işleme ile **how to extract text** demonstrasyonu yapıldı ve sonunda Aspose OCR kullanılarak **recognize text from image** gerçekleştirildi. Tüm işlem hattı, toplu işleme, PDF dönüşümü veya daha büyük bir belge‑yönetim sistemine entegrasyon için genişletebileceğiniz kompakt bir C# programında yer alıyor.

Bir sonraki meydan okumaya hazır mısınız? Tarama PDF'lerinden oluşan bir klasörü bu işlem hattına beslemeyi deneyin ya da farklı gürültü azaltma ayarlarıyla denemeler yaparak güven puanlarını nasıl etkilediklerini görün. Parametrelerle ne kadar çok oynarsanız, hız ve doğruluk arasındaki dengeyi o kadar iyi anlayacaksınız.

Sorularınız veya hâlâ işbirliği yapmayan zor bir görüntünüz var mı? Aşağıya yorum bırakın, birlikte sorun giderelim. İyi kodlamalar, ve OCR sonuçlarınız her zaman kristal‑temiz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}