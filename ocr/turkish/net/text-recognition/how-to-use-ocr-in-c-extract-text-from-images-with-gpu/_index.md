---
category: general
date: 2026-02-13
description: C#'ta OCR kullanarak görüntü dosyalarından metin çıkarmayı, GPU işlemeyi
  etkinleştirmeyi ve taramaları hızlı bir şekilde metne dönüştürmeyi öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from image
- how to extract text
- convert scan to text
- enable gpu processing
language: tr
og_description: C#'ta OCR nasıl kullanılır? Bu kılavuz, görüntü dosyalarından metin
  çıkarmayı, GPU işlemeyi etkinleştirmeyi ve taramaları metne dönüştürmeyi gösterir.
og_title: C#'da OCR Nasıl Kullanılır – GPU ile Görsellerden Metin Çıkarma
tags:
- OCR
- C#
- Aspose
- GPU
- Image Processing
title: C#'ta OCR Nasıl Kullanılır – GPU ile Görüntülerden Metin Çıkarma
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-with-gpu/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – GPU ile Görüntülerden Metin Çıkarma

Hiç **OCR nasıl kullanılır** sorusunu aklınızda canlandırıp taranmış bir belgeden metin çıkarmayı düşündünüz mü? Tek başınıza değilsiniz—geliştiriciler sürekli olarak “Görüntü dosyalarından metni verimli bir şekilde nasıl çıkarabilirim?” sorusunu soruyor. İyi haber şu ki Aspose.OCR ile tam da bunu yapabilirsiniz ve desteklenen donanımlarda **GPU işleme** özelliğini etkinleştirerek belirgin bir hız artışı elde edebilirsiniz.

Bu öğreticide, **OCR nasıl kullanılır**, **görüntüden metin nasıl çıkarılır**, **tarama nasıl metne dönüştürülür** ve GPU mevcut değilse ne yapılacağı gibi konuları gösteren eksiksiz, uçtan uca bir örnek üzerinden ilerleyeceğiz. Sonunda, tanınan metni ekrana yazdıran ve GPU'nun gerçekten kullanılıp kullanılmadığını belirten çalıştırılabilir bir C# konsol uygulamanız olacak.

## Gereksinimler

- .NET 6 SDK veya daha yeni bir sürüm (kod .NET Core ile de çalışır)  
- Visual Studio 2022 veya tercih ettiğiniz herhangi bir editör  
- Aspose.OCR for .NET paketi (NuGet üzerinden temin edilebilir)  
- Test amaçlı yüksek çözünürlüklü bir görüntü dosyası (ör. `highres_scan.tif`)  

Karmaşık bir kurulum gerekmez—sadece birkaç NuGet komutu ve hazırsınız.

## Adım 1: Aspose.OCR'ı Yükleyin ve Projeyi Hazırlayın

İlk iş olarak OCR kütüphanesini projenize eklemeniz gerekiyor. Çözüm klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Bu komut, **OcrDemo** adında yeni bir konsol projesi oluşturur ve `Aspose.OCR` NuGet paketini ekler. Kütüphane, kullanacağımız `OcrEngine` sınıfını içerir.

> **Pro tip:** Eğer ayrı bir GPU'ya sahip bir makinede çalışıyorsanız, en yeni grafik sürücüsünün yüklü olduğundan emin olun; aksi takdirde kütüphane otomatik olarak CPU moduna geçer.

## Adım 2: Tam OCR Kodunu Yazın

Şimdi `Program.cs` dosyasını açın ve içeriğini aşağıdaki kodla değiştirin. Her satır yorumlanmış, böylece *neden* bu işlemleri yaptığımızı görebilirsiniz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Enums;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -------------------------------------------------
            // 1️⃣  Create an OCR engine and request GPU processing.
            //    If the GPU isn’t present, Aspose.OCR will silently
            //    switch to CPU mode – no crash, no extra code needed.
            // -------------------------------------------------
            var ocrEngine = new OcrEngine
            {
                ProcessingMode = OcrProcessingMode.Gpu
            };

            // -------------------------------------------------
            // 2️⃣  Define the path to the image you want to process.
            //    Replace the placeholder with the actual file location.
            // -------------------------------------------------
            string imagePath = @"YOUR_DIRECTORY/highres_scan.tif";

            // -------------------------------------------------
            // 3️⃣  Perform the recognition. The method returns an
            //    OcrResult object that contains the extracted text,
            //    confidence scores, and more.
            // -------------------------------------------------
            OcrResult ocrResult = ocrEngine.RecognizeImage(imagePath);

            // -------------------------------------------------
            // 4️⃣  Report whether the GPU was really used.
            //    This is handy for debugging performance issues.
            // -------------------------------------------------
            Console.WriteLine($"GPU used: {ocrEngine.IsGpuEnabled}");

            // -------------------------------------------------
            // 5️⃣  Output the recognized text to the console.
            //    In a real app you might write this to a file,
            //    a database, or feed it into another workflow.
            // -------------------------------------------------
            Console.WriteLine("=== Extracted Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Neden Bu Şekilde Çalışır

- **ProcessingMode = Gpu** motorun önce GPU'yu denemesini sağlar. Kütüphane düşük seviyeli CUDA/OpenCL çağrılarını soyutladığı için cihaz bağlamlarını kendiniz yönetmek zorunda değilsiniz.  
- **IsGpuEnabled** GPU yolunun başarılı olup olmadığını onaylayan bir bool değişkendir. `false` görürseniz, motor otomatik olarak CPU'ya geçmiştir—panik yapmanıza gerek yok.  
- **RecognizeImage** tüm ağır işi yapar: görüntüyü yükler, OCR modelini çalıştırır ve düz metin sonucunu döndürür. Özel gereksinimleriniz (ör. eğikliği düzeltme) olmadıkça bitmap'i manuel olarak ön işleme almanıza gerek yoktur.

## Adım 3: Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Derleyip çalıştırın:

```bash
dotnet run
```

Her şey doğru kurulduysa, aşağıdakine benzer bir çıktı göreceksiniz:

```
GPU used: True
=== Extracted Text ===
This is the first line of the scanned document.
Here is the second line, and so on…
```

GPU mevcut değilse, ilk satır `GPU used: False` olarak görünecek, ancak çıkarılan metin yine de görünecek—bu, sorunsuz geri dönüş sayesinde mümkün oluyor.

> **Sık sorulan soru:** *Görselim TIFF yerine JPEG olsaydı ne olur?*  
> `RecognizeImage` metodu, .NET'in `System.Drawing` tarafından desteklenen (JPEG, PNG, BMP vb.) herhangi bir formatı kabul eder. Sadece `imagePath` içindeki dosya uzantısını değiştirmeniz yeterlidir.

## Adım 4: Opsiyonel – Daha İyi Doğruluk İçin Ayarları İnce Ayarlayın

Aspose.OCR birkaç ayar sunar:

| Ayar | Ne İşe Yarar | Ne Zaman Kullanılır |
|------|--------------|---------------------|
| `ocrEngine.Language` | Belirli bir dili zorlar (ör. `OcrLanguage.English`) | Belgenin dili biliniyorsa |
| `ocrEngine.PageSegMode` | Motorun sayfaları bloklara nasıl böleceğini kontrol eder | Çok sütunlu düzenlerde |
| `ocrEngine.DetectOrientation` | Dikey olmayan metni otomatik döndürür | Baş aşağı taranmış görüntülerde |

Bu özellikleri `RecognizeImage` metodunu çağırmadan önce ayarlayabilirsiniz. Örneğin:

```csharp
ocrEngine.Language = OcrLanguage.English;
ocrEngine.DetectOrientation = true;
```

## Adım 5: Akışı Görselleştirin (Alt Metinli Görsel)

Aşağıda, **OCR nasıl kullanılır** sorusunu isteğe bağlı GPU hızlandırmasıyla gösteren basit bir diyagram yer alıyor. Kodun çalışması için gerekli olmasa da büyük resmi kavramanıza yardımcı olur.

![GPU işleme ile OCR nasıl kullanılır diagramı](/images/ocr-gpu-flow.png)

*Alt metin:* *GPU işleme ile OCR nasıl kullanılır diagramı, gerektiğinde CPU'ya geri dönüşü vurgular.*

## Kenar Durumları & Sorun Giderme

1. **GPU’da Bellek Yetersizliği** – Çok büyük görüntüler GPU belleğini aşabilir. Bu durumda kütüphane otomatik olarak CPU'ya geçer. Bellek kullanımını düşük tutmak için görüntüyü önceden ölçeklendirebilirsiniz.  
2. **Desteklenmeyen Görüntü Formatı** – `RecognizeImage` *NotSupportedException* hatası verirse, dosya uzantısını kontrol edin ve görüntünün bozuk olmadığından emin olun. PNG'ye dönüştürmek genellikle sorunu çözer.  
3. **Düşük Güven Skoru** – OCR sonucunda çok sayıda okunamayan karakter varsa, ön işleme (ikilileştirme, gürültü giderme) yapmayı veya daha yüksek çözünürlüklü bir tarama kullanmayı düşünün.  

## Özet: Neler Başardık

**OCR nasıl kullanılır** sorusunu bir C# konsol uygulamasında ele aldık, **görüntü dosyalarından metin nasıl çıkarılır** gösterdik ve **GPU işleme** özelliğini nasıl etkinleştirip daha hızlı sonuç alabileceğinizi gösterdik. Artık **tarama nasıl metne dönüştürülür**, GPU'nun gerçekten kullanılıp kullanılmadığını nasıl kontrol edersiniz ve kenar durumları için birkaç ayarı nasıl ayarlarsınız biliyorsunuz.

### Sonraki Adımlar

- Çıktıyı bir **arama indeksi** (ör. Elasticsearch) içine besleyerek taranmış PDF'lerinizi aranabilir hâle getirin.  
- **Toplu işleme** deneyin—bir klasördeki tüm görüntüler üzerinde döngü kurup her sonucu bir `.txt` dosyasına yazın.  
- OCR'ı **çeviri API'leri** ile birleştirerek taranmış yabancı dil belgelerini otomatik olarak çevirin.  

Daha fazla sorunuz mu var? Yorum bırakın, iyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}