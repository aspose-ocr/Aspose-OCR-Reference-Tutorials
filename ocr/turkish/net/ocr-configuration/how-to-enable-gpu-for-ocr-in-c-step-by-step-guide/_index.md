---
category: general
date: 2026-04-04
description: Aspose OCR'de GPU'yu hızlıca nasıl etkinleştirirsiniz. Görüntüden metin
  çıkarmayı, OCR için görüntüyü yüklemeyi ve C# kullanarak metni tanımayı öğrenin.
draft: false
keywords:
- how to enable gpu
- extract text from image
- how to extract text
- how to recognize text
- load image for ocr
language: tr
og_description: Aspose OCR'de GPU'yu hızlıca nasıl etkinleştirirsiniz. Görüntüden
  metin çıkarmak, OCR için görüntüyü yüklemek ve C# ile metni tanımak için bu öğreticiyi
  izleyin.
og_title: C#'ta OCR için GPU'yu Nasıl Etkinleştirirsiniz – Tam Rehber
tags:
- Aspose OCR
- C#
- GPU acceleration
title: C#'ta OCR için GPU'yu nasıl etkinleştirirsiniz – Adım Adım Rehber
url: /tr/net/ocr-configuration/how-to-enable-gpu-for-ocr-in-c-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#’ta OCR için gpu’yu Nasıl Etkinleştirirsiniz – Tam Kılavuz

Aspose OCR kullanırken **gpu'yu nasıl etkinleştirileceğini** hiç merak ettiniz mi? Belki yüzlerce fişi işlerken bir performans duvarına çarptınız ve CPU yeterli gelmiyor. İyi haber şu ki, GPU hızlandırmasını açmak çok kolay ve bir kez açtığınızda OCR motorunun görüntüler üzerinde nasıl fırtına gibi çalıştığını göreceksiniz.

Bu öğreticide sadece GPU anahtarını çevirip kapatmayacağız, aynı zamanda **load image for OCR**, **recognize text**, ve nihayet **extract text from image** nasıl yapılacağını temiz bir C# örneğiyle göstereceğiz. Sonuna kadar, herhangi bir desteklenen resimden düz metni çıkaran, çalıştırmaya hazır bir programınız olacak—harici hizmetlere ihtiyaç duymadan.

## Gerekenler

- .NET 6+ (veya .NET Framework 4.7.2 ve sonrası).  
- Aspose.OCR for .NET, version 24.2.0 veya daha yeni (GPU bayrağı bu sürümde eklendi).  
- Uygun sürücülere sahip GPU‑destekli bir makine (NVIDIA CUDA 11+ harika çalışır).  
- İşlemek istediğiniz bir görüntü dosyası—taralı bir fiş, fotoğraflanmış bir fatura veya el yazısı bir not düşünün.

Eğer bunlara zaten sahipseniz, harika—hadi başlayalım.

## Adım 1: gpu’yu nasıl etkinleştirirsiniz – OCR Motorunu Yapılandırma

İlk yapmanız gereken, Aspose OCR'ye GPU'yu kullanmasını söylemektir. Bu, `OcrEngine` örneği üzerindeki `UseGpu` özelliğini ayarlayarak yapılır. Özellik varsayılan olarak `false` olduğundan, onu açıkça etkinleştiriyoruz.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;   // <-- GPU module namespace

// Create the OCR engine and enable GPU acceleration (available from version 24.2.0)
var ocrEngine = new OcrEngine
{
    // Enabling GPU can speed up recognition by 2‑5× on a modern card
    UseGpu = true
};
```

**Neden önemli:** `UseGpu` `true` olduğunda, kütüphane ağır matris hesaplamalarını grafik işlemciye devreder. Orta seviye bir RTX 3060'da, görüntü başına birkaç saniyeden bir saniyenin kesirine kadar gecikme azalmasını fark edeceksiniz.

> **Pro ipucu:** Eğer başsız bir CI ortamında çalışıyorsanız, GPU sürücüsünün kurulu olduğundan ve hizmet hesabının cihaza erişim iznine sahip olduğundan emin olun. Aksi takdirde motor sessizce CPU moduna geri dönecektir.

## Adım 2: OCR için Görüntü Yükleme – Motoru Dosyanıza Yönlendirin

Sırada **load image for OCR** yapmamız gerekiyor. Aspose OCR, System.Drawing tarafından desteklenen herhangi bir görüntü formatını (PNG, JPEG, BMP, TIFF, vb.) kabul eder. `ImageStream.FromFile` yardımcı yöntemi, dosyayı gerekli akış nesnesine sarar.

```csharp
// Replace the path with the location of your receipt or document
string imagePath = @"C:\MyImages\receipt.jpg";

ocrEngine.Image = ImageStream.FromFile(imagePath);
```

Eğer bir `byte[]`'den yüklemeyi tercih ederseniz (örneğin görüntü bir veritabanından geliyorsa), bunun yerine `ImageStream.FromBytes(byteArray)` kullanabilirsiniz—sonuç aynı, sadece kaynak farklı.

## Adım 3: metni nasıl tanırsınız – OCR İşlemini Çalıştırma

Motor yapılandırıldı ve görüntü yüklendiğine göre, **recognize text** zamanı geldi. `Recognize` metodu tüm ağır işleri yapar ve düz metin, güven skorları ve gerekirse daha sonra kullanabileceğiniz sınırlama kutularını içeren bir `OcrResult` nesnesi döndürür.

```csharp
// Run the recognition process (English is the default language)
OcrResult ocrResult = ocrEngine.Recognize();
```

`Recognize()` çağırmadan önce `ocrEngine.Language = OcrLanguage.French;` ayarlayarak dili de değiştirebilirsiniz. GPU hızlandırması, yüklediğiniz dil paketine bakılmaksızın çalışır.

## Adım 4: görüntüden metni nasıl çıkarırsınız – Sonucu Çıktılamak

Son olarak, sonuç nesnesinin `Text` özelliğini okuyarak **extract text from image** yaparız. Demo amaçlı sadece konsola yazdıracağız, ancak bir dosyaya, veritabanına yazabilir ya da başka bir servise besleyebilirsiniz.

```csharp
// Output the extracted plain‑text to the console
Console.WriteLine("=== OCR RESULT ===");
Console.WriteLine(ocrResult.Text);
```

**Beklenen çıktı** (gerçek metniniz görüntüye bağlı olarak farklı olacaktır):

```
=== OCR RESULT ===
Store: Coffee Corner
Date: 03/28/2026
Item          Qty   Price
Latte          2    $5.00
Muffin         1    $2.50
Total                 $12.50
```

Ham güven değerlerine ihtiyacınız varsa, `ocrResult.Regions` üzerinde döngü yapıp her bir `Region.Confidence` değerini inceleyebilirsiniz.

## Tam Çalışan Örnek – Tek Dosya, Çalıştırmaya Hazır

Aşağıda tam program yer alıyor. Yeni bir konsol projesine kopyalayıp yapıştırın, Aspose.OCR NuGet paketini geri yükleyin ve **F5** tuşuna basın.

```csharp
// ------------------------------------------------------------
// How to enable gpu for OCR in C# – Complete Example
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Gpu;   // GPU module namespace

class Program
{
    static void Main()
    {
        // -------- Step 1: Enable GPU ----------
        var ocrEngine = new OcrEngine
        {
            UseGpu = true   // <-- crucial for acceleration
        };

        // -------- Step 2: Load image ----------
        // Make sure the file exists; otherwise an exception is thrown.
        string imagePath = @"YOUR_DIRECTORY/receipt.jpg";
        ocrEngine.Image = ImageStream.FromFile(imagePath);

        // -------- Step 3: Recognize text -------
        OcrResult ocrResult = ocrEngine.Recognize();

        // -------- Step 4: Extract text ----------
        Console.WriteLine("=== OCR RESULT ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **Not:** `YOUR_DIRECTORY/receipt.jpg` ifadesini görüntünüzün gerçek yolu ile değiştirin. Program bir `FileNotFoundException` fırlatırsa, yolu ve dosya izinlerini tekrar kontrol edin.

## Yaygın Sorular & Kenar Durumları

### GPU algılanmazsa ne olur?

Aspose OCR otomatik olarak CPU moduna geri döner ve bir uyarı kaydeder. Hangi modun aktif olduğunu doğrulamak için, oluşturulduktan sonra `ocrEngine.IsGpuEnabled` özelliğine bakın—GPU sürücüsü başarıyla yüklendiğinde sadece `true` döner.

### Bir döngüde birden fazla görüntüyü işleyebilir miyim?

Kesinlikle. `ocrEngine.Image = …` satırını bir `foreach (var file in files)` döngüsü içine taşımanız yeterli. Aynı `OcrEngine` örneğini tutun; yeniden kullanmak, GPU kaynaklarını tekrar tekrar ayırma yükünden kaçınır.

```csharp
foreach (var file in Directory.GetFiles(@"C:\MyImages", "*.jpg"))
{
    ocrEngine.Image = ImageStream.FromFile(file);
    var result = ocrEngine.Recognize();
    Console.WriteLine($"{Path.GetFileName(file)} → {result.Text.Length} characters");
}
```

### İngilizce dışı dilleri nasıl ele alırım?

`Recognize()` çağırmadan önce dili ayarlayın:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;   // or any supported language enum
```

GPU hızlandırması aynı şekilde çalışır; sadece dil modeli değişir.

### Büyük, yüksek çözünürlüklü fotoğraflar ne olur?

Eğer bellek dışı hatalarla karşılaşırsanız, önce görüntüyü küçültün. Aspose OCR, `ImageHelper.Resize` sağlar – çok fazla detay kaybetmeden hızlıca küçültmenin bir yolu.

```csharp
ocrEngine.Image = ImageHelper.Resize(
    ImageStream.FromFile(imagePath), 
    maxWidth: 2000, 
    maxHeight: 2000);
```

## Sonuç

Aspose OCR için **gpu'yu nasıl etkinleştirirsiniz** konusunu ele aldık, size **load image for OCR** nasıl yapılacağını gösterdik, **recognize text** nasıl yapılacağını adım adım anlattık ve **extract text from image** nasıl yapılacağını özlü, üretim‑hazır bir C# programı ile gösterdik. `UseGpu` bayrağını değiştirerek, özellikle fiş, fatura veya yüksek hacimli belge akışlarını işlerken belirgin bir hız artışı elde edersiniz.

Bir sonraki adıma hazır mısınız? Bu OCR hattını bir veritabanı ile birleştirerek çıkarılan fişleri saklayabilir ya da düz metni bir doğal dil işleme modeline besleyerek harcama sınıflandırması yapabilirsiniz. Ayrıca `OcrResult.Regions` koleksiyonunu inceleyerek sınırlama kutusu koordinatlarını alabilir ve orijinal resimdeki her kelimeyi vurgulayan bir UI oluşturabilirsiniz.

Kodlamaktan keyif alın ve GPU hızlandırmasının OCR iş yüklerinize kattığı ekstra gücün tadını çıkarın!

---

![how to enable gpu illustration](gpu-ocr-diagram.png "how to enable gpu illustration")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}