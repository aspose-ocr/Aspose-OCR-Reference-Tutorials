---
category: general
date: 2026-03-18
description: Aspose OCR'de GPU cihazını ayarlayarak görüntüden metni hızlıca çıkarın.
  OCR için görüntünün nasıl yükleneceğini, fiş görüntüsünün nasıl tanınacağını öğrenin
  ve doğru sonuçlar elde edin.
draft: false
keywords:
- set GPU device
- extract text from image
- how to extract text
- load image for OCR
- recognize receipt image
language: tr
og_description: Aspose OCR'de GPU cihazını ayarlayarak görüntüden metni hızlıca çıkarın.
  OCR için görüntüyü yüklemek ve fiş görüntüsünü tanımak için bu adım adım kılavuzu
  izleyin.
og_title: C#'ta OCR için GPU Aygıtını Ayarlama – Tam Programlama Rehberi
tags:
- OCR
- C#
- GPU
- Aspose
title: C#'ta OCR için GPU Aygıtını Ayarlama – Tam Programlama Rehberi
url: /tr/net/ocr-configuration/set-gpu-device-for-ocr-in-c-complete-programming-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR için GPU Aygıtını C#'da Ayarlama – Tam Programlama Rehberi

Daha hızlı OCR işleme için **GPU aygıtını ayarlamanız** mı gerekiyor? Bu rehberde Aspose OCR kullanarak GPU aygıtını nasıl ayarlayacağınızı adım adım gösterecek ve ardından bir fiş görüntüsünden sadece birkaç satır kodla metin çıkaracağız.  

Eğer **OCR için görüntü yükleme** konusunda zorlandıysanız ya da yüksek çözünürlüklü taramalardan *metin nasıl çıkarılır* diye merak ettiyseniz, doğru yerdesiniz. Sonunda bir fiş görüntüsünü tanıyan, düz metni yazdıran ve GPU mevcut değilse sorunsuz bir şekilde geri dönüş yapan çalıştırılabilir bir programınız olacak.

## Bu Öğreticide Neler Kapsanıyor

* Aspose OCR NuGet paketini kurma (tek dış bağımlılık).  
* GPU aygıtını ayarlama (`set GPU device`) ve isteğe bağlı olarak farklı bir GPU indeksi seçme.  
* OCR için bir görüntü dosyasını yükleme – evet, bu birçok yeni başlayanı zorlayan korkunç “OCR için görüntü yükleme” adımını da içerir.  
* Tanıma motorunu çalıştırarak **fiş görüntüsünü tanıma** içeriği.  
* Ortaya çıkan dizeyi çıkararak **görüntüden metin çıkarma** yapabilir ve uygulamanızda kullanabilirsiniz.  

Sihir yok, gizli doküman bağlantıları yok – sadece Visual Studio'ya kopyalayıp yapıştırabileceğiniz ve bugün çalıştırabileceğiniz eksiksiz, bağımsız bir çözüm.

## Önkoşullar

* .NET 6.0 veya daha yeni bir sürüm (kod .NET Core ve .NET Framework'te de çalışır).  
* Uygun sürücüler yüklü bir GPU‑destekli makine – aksi takdirde kütüphane otomatik olarak CPU moduna geçer.  
* Tam yoluyla referans verebileceğiniz bir örnek fiş görüntüsü (ör. `receipt_highres.png`).  

Hepsi bu. NuGet paketiniz eksikse, proje klasörünüzde `dotnet add package Aspose.OCR` komutunu çalıştırın.

---

## Adım 1 – Aspose OCR'de GPU Aygıtını Ayarlama

İlk yapmanız gereken OCR motorunda **GPU aygıtını ayarlamaktır**. Bu, Aspose'a ağır işi CPU yerine grafik kartına devretmesini söyler.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // Create the OCR engine instance
        var ocrEngine = new OcrEngine();

        // Enable GPU processing – this is where we set the GPU device
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu;

        // (Optional) Choose a specific GPU if you have more than one.
        // The default is device 0, but you can set it to 1, 2, etc.
        ocrEngine.Settings.GpuDeviceId = 0;
```

**Neden önemli:**  
`ProcessingMode.Gpu` ile çalıştığında, altındaki CUDA çekirdekleri karakter segmentasyonunu ve sinir‑ağları çıkarımını büyük ölçüde hızlandırabilir. Modern bir RTX 3080'de yüksek çözünürlüklü fişler için OCR sürelerinin saniyelerden alt saniyelere düştüğünü göreceksiniz.

> **Pro ipucu:** Hangi GPU indeksini kullanacağınızdan emin değilseniz, `OcrEngine.GetAvailableGpuDevices()` (yeni sürümlerde mevcut) metodunu çağırın ve en fazla boş belleğe sahip olanı seçin.

## Adım 2 – OCR için Görüntü Yükleme

Motor yapılandırıldıktan sonra **OCR için görüntü yüklememiz** gerekiyor. Aspose, dosya I/O'yu soyutlayan ve bellek, ağ ya da diskten gelen akışları destekleyen kullanışlı bir `ImageStream` sarmalayıcısı sunar.

```csharp
        // Load the receipt image you want to recognize
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        var imageStream = ImageStream.FromFile(imagePath);
```

**Ne yanlış gidebilir?**  
Dosya yolu yanlışsa ya da görüntü bozuksa, `FromFile` bir `FileNotFoundException` fırlatır. Akışı oluşturmadan önce hızlı bir `File.Exists(imagePath)` kontrolü, sizi kötü bir çöküşten kurtarır.

## Adım 3 – Fiş Görüntüsünü Tanıma

Görüntü elinizde olduğunda `Recognize` metodunu çağırırız. Bu adım, daha önce kurduğumuz GPU‑hızlandırmalı boru hattını kullanarak **fiş görüntüsünü tanıma** içeriğini gerçekten gerçekleştirir.

```csharp
        // Perform OCR – this returns an OcrResult object
        var ocrResult = ocrEngine.Recognize(imageStream);
```

**Perde Arkası:**  
Motor önce görüntüyü normalize edilmiş bir gri tonlamalı bitmap'e dönüştürür, ardından karakter olasılıklarını tahmin eden bir derin‑öğrenme modeli çalıştırır. GPU'da olduğumuz için model tüm bitmap'i paralel olarak işler, bu da büyük fişlerin hızlı bitmesini sağlar.

## Adım 4 – Görüntüden Metin Çıkarma ve Çıktıyı Doğrulama

Son olarak, `OcrResult` içindeki düz‑metin sonucunu alır ve konsola yazarız. Bu, **görüntüden metin çıkarma** yaptığınız ve çıktıyı sonraki mantığa (ör. satır öğelerini ayrıştırma) besleyebileceğiniz anıdır.

```csharp
        // Output the recognized plain text
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

**Beklenen çıktı:**  

```
=== OCR Result ===
Store Name
Date: 03/15/2026
Item A   $12.99
Item B   $5.49
Total    $18.48
==================
```

Metin bozuk görünüyorsa, görüntünün yüksek çözünürlüklü olduğundan ve GPU sürücüsünün güncel olduğundan emin olun. Ayrıca düşük ışıklı fişlerde kontrastı artırmak için `ocrEngine.Settings.PreprocessMode` ayarını değiştirebilirsiniz.

## Adım 5 – CPU'ya Geri Dönüş (Köşe Durumları Yönetimi)

Hedef makinede uyumlu bir GPU yoksa ne olur? Çökmek yerine durumu tespit edip CPU işleme geçebilirsiniz.

```csharp
        // Detect GPU availability – fallback if needed
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, falling back to CPU mode.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }
```

**Bunu neden ekledik?**  
CI boru hatlarında veya bulut konteynerlerinde genellikle GPU'suz başsız sunucularda çalışırsınız. Zarif bir gerileme, aynı kodun her yerde çalışmasını sağlar.

## Yaygın Tuzaklar ve Pratik İpuçları

| Tuzak | Nasıl Önlenir |
|---------|--------------|
| `ProcessingMode`'u görüntüyü yüklemeden önce ayarlamayı unutmak. | Her zaman motoru önce yapılandırın (Adım 1). |
| Yanlış GPU indeksini (`GpuDeviceId`) kullanmak. | Mevcut aygıtları sorgulayın veya varsayılan `0`'ı kullanın. |
| Düşük çözünürlüklü görüntü yüklemek, bu da OCR doğruluğunu azaltır. | Fişler için en az 300 DPI hedefleyin. |
| `ImageStream`'i serbest bırakmamak – dosya kilitlenmelerine yol açar. | Akışı bir `using` bloğuna alın veya manuel olarak `Dispose()` çağırın. |
| CUDA'sız makinelerde `IsGpuAvailable` bayrağını görmezden gelmek. | Adım 5'teki geri dönüş mantığını ekleyin. |

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda derlemeye hazır tüm program yer alıyor. `Program.cs` olarak kaydedin, Aspose OCR NuGet paketini ekleyin ve çalıştırın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class GpuDemo
{
    static void Main()
    {
        // ---------- Step 1: Set GPU device ----------
        var ocrEngine = new OcrEngine();
        ocrEngine.Settings.ProcessingMode = ProcessingMode.Gpu; // set GPU device
        ocrEngine.Settings.GpuDeviceId = 0; // use the first GPU (change if needed)

        // Optional: fallback if GPU isn't present
        if (!ocrEngine.IsGpuAvailable)
        {
            Console.WriteLine("GPU not detected, switching to CPU.");
            ocrEngine.Settings.ProcessingMode = ProcessingMode.Cpu;
        }

        // ---------- Step 2: Load image for OCR ----------
        var imagePath = @"C:\OCR\Samples\receipt_highres.png";
        if (!System.IO.File.Exists(imagePath))
        {
            Console.WriteLine($"File not found: {imagePath}");
            return;
        }
        var imageStream = ImageStream.FromFile(imagePath);

        // ---------- Step 3: Recognize receipt image ----------
        var ocrResult = ocrEngine.Recognize(imageStream);

        // ---------- Step 4: Extract text from image ----------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(ocrResult.Text);
        Console.WriteLine("==================");
    }
}
```

Programı çalıştırmak, çıkarılan fiş metnini konsola yazdırır, tam da daha önce gösterildiği gibi. Artık bu dizeyi bir ayrıştırıcıya, veritabanına ya da ihtiyacınız olan herhangi bir iş mantığına yönlendirebilirsiniz.

## Sonuç

Aspose OCR'de **GPU aygıtını ayarlamayı**, **OCR için görüntü yüklemeyi** ve **fiş görüntüsünü tanımayı** gösterdik; böylece **görüntüden metin çıkarma** işlemini ışık hızında yapabilirsiniz. Eksiksiz, çalıştırılabilir örnek hem “nasıl” hem de “neden” olduğunu göstererek GPU hızlandırması gerektiren herhangi bir C# OCR projesi için sağlam bir temel sunar.

Bir sonraki adıma hazır mısınız? Şunları deneyin:

* `Parallel.ForEach` kullanarak birden fazla görüntüyü paralel işleme.  
* Düşük kontrastlı taramalarda sonuçları iyileştirmek için `ocrEngine.Settings.PreprocessMode` ayarını ince ayar yapma.  
* OCR çıktısını JSON'a aktararak sonraki analizler için kullanma.  

Herhangi bir sorunla karşılaşırsanız yorum bırakmaktan çekinmeyin, iyi kodlamalar!

![Diagram showing how to set GPU device for OCR processing](set-gpu-device.png "set GPU device")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}