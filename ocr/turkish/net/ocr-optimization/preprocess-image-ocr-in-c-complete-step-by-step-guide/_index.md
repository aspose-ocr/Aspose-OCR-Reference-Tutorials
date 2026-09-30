---
category: general
date: 2026-02-20
description: C#'ta Aspose.OCR ile görüntü OCR ön işleme. Medyan filtre uygulamayı,
  görüntü gürültüsünü azaltmayı ve metin görüntüsünü verimli bir şekilde çıkarmayı
  öğrenin.
draft: false
keywords:
- preprocess image OCR
- apply median filter
- extract text image
- reduce image noise
- c# ocr example
language: tr
og_description: Aspose.OCR ile görüntü OCR ön işleme. Bu öğreticide medyan filtresi
  uygulama, görüntü gürültüsünü azaltma ve C# kullanarak metin görüntüsü çıkarma gösterilmektedir.
og_title: C#'ta Görüntü OCR Ön İşleme – Tam Kılavuz
tags:
- OCR
- C#
- Image Processing
title: C# ile Görüntü OCR Ön İşleme – Tam Adım Adım Rehber
url: /tr/net/ocr-optimization/preprocess-image-ocr-in-c-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntü OCR Ön İşleme – Tam Adım‑Adım Kılavuz

Hiç **görüntü OCR ön işleme** yapmanız gerekti ve taradığınız fotoğraflar bozuk metin döndürdü mü? Yalnız değilsiniz. Gerçek dünyadaki birçok projede—makbuzlar, kimlik kartları veya el yazısı notlar gibi—ham görüntü doğrudan tanıma için nadiren hazırdır. İyi haber? Birkaç basit ön işleme adımı doğruluğu büyük ölçüde artırabilir ve tümünü C# ile Aspose.OCR kullanarak yapabilirsiniz.

Bu öğreticide, **median filter uygulama**, **görüntü gürültüsünü azaltma** ve sonunda **metin görüntüsü çıkarma** işlemlerini temiz, okunabilir bir sonuçla nasıl gerçekleştireceğinizi adım adım göstereceğiz. Sonunda, herhangi bir .NET çözümüne ekleyebileceğiniz tamamen çalıştırılabilir bir C# konsol uygulamanız olacak. Belirsiz referanslar yok, sadece ihtiyacınız olan kod ve her satırın “neden”i.

---

## Gereksinimler

- **Aspose.OCR for .NET** (yazım anındaki en yeni sürüm, 23.12). NuGet üzerinden alabilirsiniz: `Install-Package Aspose.OCR`.
- .NET 6.0 veya üzeri (örnek bir konsol uygulaması kullanıyor, aynı mantık ASP.NET, WPF vb. içinde de çalışır).
- Temizlenmesi gereken bir örnek görüntü—ör. `skewed_photo.jpg`.  
- Biraz C# deneyimi; kavramlar junior geliştiriciler için bile anlaşılır.

> **Pro ipucu:** Kurumsal bir makinede çalışıyorsanız, NuGet beslemenizin dış paketlere izin verecek şekilde yapılandırıldığından emin olun, aksi takdirde kurulum başarısız olur.

---

## Adım 1 – OCR Motoru Örneğini Oluşturma  

İlk olarak bir `OcrEngine` başlatırsınız. Bu nesne tanıma ayarlarını tutar ve daha sonra ön‑işlenmiş bitmap'i işleyecektir.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;   // For Image handling
using System;

class PreprocessExample
{
    static void Main()
    {
        // Initialize the OCR engine – this is the core component that will read text.
        OcrEngine ocrEngine = new OcrEngine();

        // ... we’ll continue with loading and preprocessing the image below.
```

**Neden?**  
Motoru bir kez oluşturup birden çok görüntüde yeniden kullanmak yükü azaltır. Ayrıca, dili ya da tanıma modlarını daha sonra yeniden derlemeden ayarlamanıza olanak tanır.

---

## Adım 2 – Kaynak Görüntüyü Yükleme  

Ham dosyanıza işaret eden bir `System.Drawing.Image` nesnesine ihtiyacınız var. Gerçek bir projede bir akış (stream) alabilirsiniz, ancak açıklık olması açısından diskteki dosyayı okuyacağız.

```csharp
        // Load the image that requires preprocessing.
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");
```

> **Not:** `YOUR_DIRECTORY` ifadesini gerçek klasör yoluyla değiştirin. Dosya bulunamazsa bir `FileNotFoundException` fırlatılır—daha nazik bir hata yönetimi isterseniz yakalayabilirsiniz.

---

## Adım 3 – Görüntüyü Düzeltme ve Döndürme  

Çoğu taranmış belge hafifçe eğiktir. `DeskewAndRotate` filtresi otomatik olarak eğim açısını algılar ve resmi dik konuma döndürür.

```csharp
        // Correct orientation – crucial for accurate OCR.
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());
```

**Neden önemli?**  
OCR motorları metin satırlarının yatay olduğunu varsayar. 2 derecelik bir eğim bile tanıma doğruluğunu %15‑20 azaltabilir. Düzeltme, büyük bir kazanç elde etmenin en ucuz yoludur.

---

## Adım 4 – Görüntü Gürültüsünü Azaltmak İçin Median Filter Uygulama  

Düşük ışıklı fotoğraflarda gürültü, lekeler ya da rastgele pikseller olarak ortaya çıkar. Median filter, kenarları korurken bu gürültüyü temizler; OCR öncesi tam da ihtiyacımız olan şey budur.

```csharp
        // Reduce noise – radius of 2 is a good balance for most photos.
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));
```

**Neden median filter?**  
Ortalama (mean) filtreden farklı olarak, median filter her pikseli komşuluğunun medyan değeriyle değiştirir. Bu sayede izole gürültü silinirken metin çizgileri bulanıklaşmaz—**görüntü gürültüsünü azaltma** için klasik bir tekniktir.

---

## Adım 5 – Gerilme (Stretching) ile Kontrastı Artırma  

Gürültü temizlendikten sonra bir sonraki adım, metin ile arka plan arasındaki farkı artırmaktır. Kontrast gerilmesi, piksel yoğunluklarını tam 0‑255 aralığına yayar.

```csharp
        // Stretch contrast to make dark text pop against a light background.
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());
```

**Neden gerilim?**  
OCR motorları net bir ön‑arkaplan ayrımı gerektirir. Görüntü soluksa, motor metni arka plan olarak algılayabilir. Kontrast gerilmesi, manuel eşikleme yapmaya gerek kalmadan bu sorunu çözer.

---

## Adım 6 – Ön İşlenmiş Görüntüde OCR Gerçekleştirme  

Şimdi görüntü düz, temiz ve yüksek kontrastlı olduğuna göre OCR motoruna veriyoruz.

```csharp
        // Recognize the text from the cleaned image.
        string extractedText = ocrEngine.Recognize(processedImage);
```

**Ne elde edersiniz:**  
`extractedText` Aspose.OCR tarafından algılanan ham Unicode dizesini içerir. İsterseniz (trim, regex vb.) sonradan işleyebilirsiniz.

---

## Adım 7 – Tanınan Metni Çıktı Olarak Verme  

Son olarak sonucu konsola ya da bir dosyaya yazın—iş akışınıza uygun şekilde.

```csharp
        // Show the result in the console.
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

### Beklenen Çıktı

`skewed_photo.jpg` içinde “Hello World” ifadesi varsa, aşağıdakine benzer bir şey görürsünüz:

```
=== Extracted Text ===
Hello World
```

Görüntü hâlâ gürültülü ise bozuk karakterler görebilirsiniz—Adım 4’e geri dönüp median filter yarıçapını artırın ya da `GaussianBlur` gibi ek filtrelerle deney yapın.

---

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenmeye hazır tüm program yer alıyor. Eksik bir şey yok—sadece dosya yolunu değiştirin.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Filters;
using System.Drawing;
using System;

class PreprocessExample
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Load the source image that needs preprocessing
        Image sourceImage = Image.FromFile("YOUR_DIRECTORY/skewed_photo.jpg");

        // Step 3: Deskew and rotate the image to correct orientation
        Image processedImage = sourceImage.Apply(Preprocess.DeskewAndRotate());

        // Step 4: Reduce noise with a median filter (radius = 2)
        processedImage = processedImage.Apply(Preprocess.MedianFilter(radius: 2));

        // Step 5: Enhance contrast using contrast stretching
        processedImage = processedImage.Apply(Preprocess.ContrastStretch());

        // Step 6: Perform OCR on the preprocessed image
        string extractedText = ocrEngine.Recognize(processedImage);

        // Step 7: Output the recognized text
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(extractedText);
    }
}
```

> **Köşe durum ipucu:** Görüntünüz renkli bir arka plan üzerindeki renkli metni içeriyorsa, `ContrastStretch` uygulamadan önce gri tonlamaya dönüştürmeyi düşünün. Bunu pipeline içinde `Preprocess.Grayscale()` ile yapabilirsiniz.

---

## Yaygın Sorular & Varyasyonlar  

### Görüntü baş aşağıysa ne olur?  
`DeskewAndRotate` 180 derecelik döndürmeleri otomatik algılar, ancak deskew öncesinde `Preprocess.Rotate(angle: 180)` ile zorlayarak döndürme yapabilirsiniz.

### Median filter'ı atlayabilir miyim?  
Evet, ancak **görüntü gürültüsünü azaltma** faydaları büyük ölçüde azalır. Yüksek çözünürlüklü taramalarda filtre gereksiz olabilir; düşük ışıklı telefon fotoğraflarında ise genellikle zorunludur.

### Basit bir `Apply(Preprocess.Binarize())` ile nasıl farklıdır?  
Binarizasyon görüntüyü tamamen siyah‑beyaz yapar ve ince fontlarda sert olabilir. Bizim yaklaşımımız gri ton detayını korur, ardından kontrastı gerer—karışık boyutlu fontlar için genellikle daha iyi sonuç verir.

### **apply median filter** sadece bir ilgi alanına (region of interest) uygulanabilir mi?  
Aspose.OCR’nin `Apply` metodu tüm bitmap üzerinde çalışır, ancak önce görüntüyü kırpabilirsiniz (`sourceImage.Clone(new Rectangle(...), sourceImage.PixelFormat)`) ve ardından filtreyi bu alt‑görüntüye uygulayabilirsiniz.

---

## Sonraki Adımlar – Temel Ön İşlemenin Ötesine Geçmek  

- **Language Packs:** Fransızca veya Japonca karakterler çıkarmanız gerekiyorsa, uygun dil modelini `ocrEngine.Language = Language.French;` gibi bir satırla yükleyin.  
- **Custom Thresholding:** Son derece düşük kontrastlı taramalarda, median filter sonrası `Preprocess.AdaptiveThreshold()` ile deney yapın.  
- **Batch Processing:** Adımları bir `foreach (string file in Directory.GetFiles(...))` döngüsü içine alın ve her sonucu bir `.txt` dosyasına yazın.  
- **Performance Tuning:** Tek bir `OcrEngine` örneğini yeniden kullanın ve binlerce görüntü işlerken GC dalgalanmalarını önlemek için bir `Bitmap` tamponu önceden ayırın.

---

## Sonuç  

C# içinde **görüntü OCR ön işleme** sürecini baştan sona gösterdik: resmi yükleme, düzeltme, **median filter uygulama**, kontrast artırma ve sonunda Aspose.OCR ile **metin görüntüsü çıkarma**. Tam kod parçacığı herhangi bir projeye eklenmeye hazır ve açıklamalar her dönüşümün “nedenini” veriyor—kendi kenar durumlarınız için parametreleri ayarlayabilmeniz için.

Farklı fotoğraflarla deneyin, filter yarıçapını oynayın ve tanıma doğruluğunun nasıl yükseldiğini izleyin. Rahat hissettiğinizde yukarıda bahsedilen ileri düzey ayarları keşfedin; böylece ekibinizde temiz OCR boru hatları için başvurulacak kişi olursunuz.

İyi kodlamalar, OCR’nuz her zaman temiz okunsun! 

![preprocess image OCR example](/images/preprocess-image-ocr.png "preprocess image OCR – before and after processing")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}