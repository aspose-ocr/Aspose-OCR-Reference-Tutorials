---
category: general
date: 2026-03-21
description: Aspose OCR ile görüntü dosyalarını nasıl eğriltme düzeltip metin görüntüsünü
  tanıyacağınızı öğrenin. JPG'yi metne dönüştürün ve birkaç satır C# kodu ile görüntü
  dönüşünü düzeltin.
draft: false
keywords:
- how to deskew image
- recognize text image
- convert jpg to text
- correct image rotation
- recognize text jpg
language: tr
og_description: Aspose OCR kullanarak görüntüyü eğriltmeyi düzeltme ve JPEG'lerden
  metin çıkarma. JPG'yi metne dönüştürmek ve görüntü döndürmesini düzeltmek için bu
  adım adım rehberi izleyin.
og_title: C# ile Görüntüyü Eğri Düzeltme – Hızlı Aspose OCR Öğreticisi
tags:
- OCR
- C#
- Aspose
title: C#'ta Görüntüyü Eğrilik Düzeltme (Deskew) Nasıl Yapılır – Aspose OCR Kullanarak
  Tam Rehber
url: /tr/net/skew-angle-calculation/how-to-deskew-image-in-c-complete-guide-using-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Görüntüyü Düzleştirme – Aspose OCR Kullanarak Tam Kılavuz

Bir tarayıcıdan gelen ve garip bir açıyla taranmış **görüntüyü nasıl düzleştireceğinizi** hiç merak ettiniz mi? Yalnız değilsiniz—çok sayıda geliştirici, makbuz, fatura ya da el yazısı notlardan metin çıkarmaya çalışırken bu sorunu yaşıyor. İyi haber şu ki, Aspose OCR sayesinde görüntü döndürmesini düzeltebilir ve sadece birkaç satır kodla temiz, aranabilir metin elde edebilirsiniz.

Bu öğreticide, kütüphaneyi kurmaktan otomatik düzleştirmeyi etkinleştirmeye, metin görüntüsünü tanımaya ve son olarak bir JPG'yi metne dönüştürmeye kadar tüm süreci adım adım göstereceğiz. Sonunda, **metin jpg dosyalarını tanıyan** ve önce manuel olarak döndürmeye gerek kalmadan çalışan bir konsol uygulamanız olacak.

## Gereksinimler

- **.NET 6.0** veya üzeri (kod .NET Core ve .NET Framework’te aynı şekilde çalışır)  
- **Aspose.OCR for .NET** NuGet paketi – 23.12 veya daha yeni bir sürüm önerilir  
- Uygulamanızın okuyabileceği bir yerde bulunan örnek **eğik JPEG** (ör. `skewed_receipt.jpg`)  
- Visual Studio, VS Code veya tercih ettiğiniz herhangi bir C# editörü  

Başka bir üçüncü‑taraf araca ihtiyaç yok. Kütüphane, düzleştirme, OCR ve hatta dil algılamayı dahili olarak yönetir.

![how to deskew image example](/images/deskew-example.png "how to deskew image using Aspose OCR")

## Adım 1: Projeyi Oluşturun ve Aspose.OCR'ı Yükleyin

Düzeni korumak için yeni bir konsol projesi başlatın:

```bash
dotnet new console -n DeskewDemo
cd DeskewDemo
dotnet add package Aspose.OCR --version 23.12.0
```

`dotnet add package` satırı **Aspose.OCR** ikili dosyalarını ve tüm yerel bağımlılıkları getirir. Windows kullanıyorsanız yerel DLL'ler otomatik olarak eklenir; Linux/macOS'ta `libgdiplus` paketini kurmanız gerekebilir, ancak bu tek seferlik bir kurulumdur.

## Adım 2: Otomatik Düzleştirmeyi Etkinleştirin (Görüntü Döndürmesini Düzeltin)

Şimdi `Program.cs` dosyasını açın ve içeriğini aşağıdaki kodla değiştirin. Buradaki kilit satır `ocrEngine.Settings.Deskew = true;` – bu, motorun **görüntüyü nasıl düzleştireceğini** otomatik olarak belirleyen bayraktır.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // -----------------------------------------------------------------
            // 1️⃣ Create an OCR engine (CPU mode is fine for most desktop apps)
            // -----------------------------------------------------------------
            var ocrEngine = new OcrEngine();

            // ---------------------------------------------------------------
            // 2️⃣ Turn on deskewing – this corrects image rotation for us
            // ---------------------------------------------------------------
            ocrEngine.Settings.Deskew = true;   // <-- how to deskew image is handled here

            // ---------------------------------------------------------------
            // 3️⃣ Point the engine at the JPEG you want to process
            // ---------------------------------------------------------------
            string imagePath = "YOUR_DIRECTORY/skewed_receipt.jpg";

            // ---------------------------------------------------------------
            // 4️⃣ Run OCR – the result already contains the corrected text
            // ---------------------------------------------------------------
            OcrResult ocrResult = ocrEngine.Recognize(imagePath);

            // ---------------------------------------------------------------
            // 5️⃣ Output the text – this is your “convert jpg to text” step
            // ---------------------------------------------------------------
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### Neden Düzleştirme Etkinleştirilmeli?

Bir tarayıcı sayfayı açıyla beslediğinde, metin tabanı eğimli olur. Geleneksel OCR motorları her karakteri eğik bir versiyon olarak okur ve doğruluk büyük ölçüde düşer. `Deskew = true` ayarını yaparak Aspose OCR, arka planda hızlı bir Hough‑transformu çalıştırır, bitmap'i yatay konuma döndürür ve ardından tanıma işlemini gerçekleştirir. Sonuç, Photoshop'ta resmi manuel olarak döndürmüş gibi olur—daha hızlı ve tamamen otomatik.

## Adım 3: Metin Görüntüsünü Tanıyın ve JPG'yi Metne Dönüştürün

`Recognize` çağrısı aynı anda iki işi yapar:

1. **Görüntüyü düzleştirir** (çünkü bayrak açıktı).  
2. **Metin içeriğini çıkarır**, bir `OcrResult` nesnesi olarak döner.

`ocrResult.Text` değerini düz bir string gibi kullanabilir, bir dosyaya yazabilir veya sonraki işleme boru hatlarına aktarabilirsiniz. Kelime bazında ham güven skorlarına ihtiyacınız varsa, `ocrResult.Words` koleksiyonu `Confidence` değerlerini içerir.

### Örnek Çıktı

`skewed_receipt.jpg` basit bir makbuz içeriyorsa, aşağıdaki gibi bir çıktı görebilirsiniz:

```
=== Recognized Text ===
Store: Coffee Corner
Date: 2026-03-20
Item   Qty   Price
Latte   2    5.00
Bagel   1    2.50
Total          12.50
```

Orijinal görüntü yaklaşık 7° döndürülmüş olmasına rağmen sayıların düzgün hizalandığını fark edeceksiniz. Bu, kütüphanenin içinde bulunan **görüntü döndürmesini düzeltme** sihiridir.

## Adım 4: Örneği Çalıştırın ve Sonuçları Doğrulayın

Derleyip çalıştırın:

```bash
dotnet run
```

Her şey doğru bağlandıysa, çıkarılan metin konsola yazdırılacaktır. `FileNotFoundException` gibi bir istisna alırsanız, JPEG dosyasının yolunu kontrol edin ve dosyanın okunabilir olduğundan emin olun.

### Yaygın Tuzaklar ve Profesyonel İpuçları

- **Büyük Görüntüler** – OCR bellek kullanımı görüntü boyutlarıyla artar. Motorun içine vermeden önce çok büyük dosyaları (ör. > 3000 px genişlik) yeniden boyutlandırın.  
- **Latin Olmayan Yazı Sistemleri** – Varsayılan olarak motor İngilizce kabul eder. Başka bir alfabe için **görüntüdeki metni tanımak** istiyorsanız `ocrEngine.Settings.Language = OcrLanguage.French;` (veya desteklenen başka bir dil) ayarlayın.  
- **Toplu İşlem** – Çok sayıda dosya için aynı `OcrEngine` örneğini yeniden kullanın; dosya başına yeni bir motor oluşturmak gereksiz yük getirir.  
- **Kalite Kontrolü** – Düzleştirmeden sonra `ocrEngine.Settings.DeskewedImage.Save("corrected.jpg");` ile düzeltilmiş bitmap'i dışa aktarabilir, döndürme düzeltmesini görsel olarak doğrulayabilirsiniz.

## Tam Çalışan Örnek (Hepsi Bir Arada)

Aşağıda `Program.cs` içine kopyalayıp yapıştırabileceğiniz, yorumlar, hata yönetimi ve isteğe bağlı olarak düzleştirilmiş görüntüyü kaydetme adımını içeren eksiksiz bir program yer alıyor.

```csharp
using System;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace DeskewDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Path to the input JPEG – change this to your actual file location
            string inputPath = @"YOUR_DIRECTORY\skewed_receipt.jpg";

            if (!File.Exists(inputPath))
            {
                Console.WriteLine($"Error: File not found – {inputPath}");
                return;
            }

            try
            {
                // 1️⃣ Create OCR engine (CPU mode is sufficient for most scenarios)
                var ocrEngine = new OcrEngine();

                // 2️⃣ Enable automatic deskewing – this is the core of how to deskew image
                ocrEngine.Settings.Deskew = true;

                // Optional: Save the corrected image to verify the rotation fix
                // ocrEngine.Settings.DeskewedImagePath = "corrected.jpg";

                // 3️⃣ Perform OCR – this simultaneously deskews and extracts text
                OcrResult result = ocrEngine.Recognize(inputPath);

                // 4️⃣ Output the recognized text – effectively convert jpg to text
                Console.WriteLine("=== Recognized Text ===");
                Console.WriteLine(result.Text);
            }
            catch (Exception ex)
            {
                Console.WriteLine("An unexpected error occurred:");
                Console.WriteLine(ex.Message);
            }
        }
    }
}
```

Programı çalıştırdığınızda **metin jpg dosyalarını tanıyacak**, otomatik olarak eğikliği düzeltecek ve temiz, aranabilir metni konsola yazdıracaktır.

## Sonuç

Artık Aspose OCR kullanarak **görüntüyü nasıl düzleştireceğinizi** ve içeriğini nasıl çıkaracağınızı gösteren sağlam, üretime hazır bir kod parçacığınız var. Bu yaklaşım makbuzlar, faturalar, taranmış sözleşmeler veya metni tam olarak yatay olmayan herhangi bir JPEG için işe yarar.

İleride keşfedebileceğiniz adımlar:

- Bir klasördeki JPEG'leri toplu işleyip her bir sonucun `.txt` dosyasına yazılması ( *convert jpg to text* konusuna geri dönüyor).  
- OCR adımını bir ASP.NET Core API'sine entegre ederek istemcilerin görüntü yükleyip JSON formatında metin almasını sağlamak.  
- `ocrEngine.Settings.Language` veya `ocrEngine.Settings.RecognitionMode` gibi farklı OCR ayarlarıyla denemeler yaparak İngilizce dışı belgelerde doğruluğu artırmak.  

Deneyin, ayarları ince ayarlayın ve motorun ağır işi halletmesine izin verin. Her zaman olduğu gibi bir sorunla karşılaşırsanız ya da akıllı bir iyileştirme paylaşmak isterseniz, aşağıya yorum bırakın. İyi kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}