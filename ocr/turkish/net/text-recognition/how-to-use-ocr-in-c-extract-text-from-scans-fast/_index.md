---
category: general
date: 2026-03-13
description: C#'ta OCR nasıl kullanılır ve taramalardan metin çıkarılır. Aspose OCR,
  GPU hızlandırma ve adım adım kod ile TIFF'i metne dönüştürmeyi öğrenin.
draft: false
keywords:
- how to use OCR
- extract text from scans
- convert tiff to text
- c# ocr tutorial
language: tr
og_description: C#'ta OCR kullanarak taramalardan metin çıkarmak nasıl yapılır. Bu
  rehber, Aspose OCR ve GPU hızlandırmasıyla TIFF'i metne nasıl dönüştüreceğinizi
  gösterir.
og_title: C#'da OCR Nasıl Kullanılır – Taramalardan Metni Hızlıca Çıkar
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'ta OCR Nasıl Kullanılır – Taramalardan Metni Hızlıca Çıkar
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-scans-fast/
---

note the "Quick Checklist" bullet points.

Also "Common Pitfalls & Pro Tips (c# OCR tutorial)" table.

Also note the last row of table is cut off: "Use `Path.GetFullPath` to normalise, or prefix with `@"\\?\"` on Windows if paths exceed". The original ends abruptly. Keep as is.

Now produce final content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Taramalardan Metni Hızlıca Çıkarın

Hiç **OCR nasıl kullanılır** sorusunu aklınıza getirdiniz mi ve taranmış TIFF dosyalarının bir yığınından okunabilir metin çıkarmak istediniz mi? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—fatura dijitalleştirme, tarihi belgelerin arşivlenmesi ya da PDF'leri aranabilir hâle getirme gibi—geliştiricilerin **taramalardan metin çıkarmak** için güvenilir bir yola ihtiyacı var ve bu işi zahmetsizce yapmak istiyorlar.

İyi haber? Aspose OCR ve birkaç satır C# kodu ile TIFF'i metne dönüştürmek, mütevazı bir iş istasyonunda bile saniyeler içinde mümkün. Aşağıda tamamen çalıştırılabilir bir örnek ve her bir tercihin ardındaki mantığı bulacaksınız; böylece kendi iş akışınıza kolayca uyarlayabilirsiniz.

## Gereksinimler

İlerlemeye başlamadan önce aşağıdakilerin elinizde olduğundan emin olun:

| Gereklilik | Neden Önemli |
|------------|--------------|
| .NET 6+ (veya .NET Framework 4.7+) | Aspose OCR NuGet paketi modern .NET çalışma zamanlarını hedefler. |
| Visual Studio 2022 (veya tercih ettiğiniz herhangi bir IDE) | IntelliSense ve kolay hata ayıklama sağlar. |
| CUDA‑uyumlu bir GPU & sürücü (isteğe bağlı) | `ocrEngine.UseGpu = true` ifadesi, büyük toplularda belirgin bir hız artışı sağlar. |
| İşlemek istediğiniz TIFF görüntülerinin bulunduğu bir klasör | Bu öğreticide `*.tif` dosyaları kullanılıyor, ancak deseni ihtiyacınıza göre değiştirebilirsiniz. |
| Aspose.OCR NuGet paketi (`Install-Package Aspose.OCR`) | Ağır işi yapan temel kütüphane. |

Eğer bunlardan birini eksikse, şimdi temin edin—bağımlılık hatasıyla karşılaşmamak için ilerlemeden önce bu adımı atlamayın.

## Çözümün Genel Bakışı

Yüksek seviyede program üç şey yapar:

1. **Bir OCR motoru oluşturur** ve isteğe bağlı olarak GPU hızlandırmasını açar.  
2. **Bir klasördeki her TIFF dosyasını** dolaşır, tanıma işlemini çalıştırır ve elde edilen düz metni yakalar.  
3. **Metni**, orijinal görüntünün yanına bir `.txt` dosyası olarak yazar.

Hepsi bu. Kod kasıtlı olarak çok kısa tutulmuş, ancak açık dil seçimi, doğru kaynak temizliği ve yaygın kenar durumları için hata yönetimi gibi en iyi uygulamaları sergiliyor.

![C#'ta OCR nasıl kullanılır örneği](/images/how-to-use-ocr-csharp.png "C#'ta OCR kullanarak taramalardan metin çıkarma illüstrasyonu")

## Adım 1: OCR Motorunu Başlatın (OCR Nasıl Kullanılır)

İlk olarak bir `OcrEngine` örneğine ihtiyacınız var. Bu nesne, Aspose OCR işlevselliğinin kapısını açar. Varsayılan olarak CPU üzerinde çalışır, ancak `UseGpu = true` ayarı, kütüphaneye ağır matris hesaplamalarını grafik kartınıza devretmesini söyler—tabii ki CUDA‑uyumlu bir sürücü kuruluysa.

```csharp
using Aspose.OCR;
using System.IO;

// Initialise the engine ----------------------------------------------------
OcrEngine ocrEngine = new OcrEngine
{
    // Enable GPU acceleration if a compatible card is present.
    // If you don’t have a GPU, just leave this as false – the code will still run.
    UseGpu = true,

    // Choose English as the recognition language. Change this if you need
    // another language pack (e.g., Language.French, Language.Spanish, etc.).
    Language = Language.English
};
```

**Neden Önemli:**  
- **GPU hızlandırması**, yüksek çözünürlüklü taramalar için işleme süresini %70'e kadar azaltabilir.  
- **Açık dil seçimi**, motorun tahmin yapmasını engeller ve özellikle Latin dışı alfabelerde doğruluğu artırır.

## Adım 2: Motoru Taramalarınıza Yönlendirin (TIFF'i Metne Dönüştürün)

Sonra programa görüntülerin nerede olduğunu söyleriz. `Directory.GetFiles` ile `*.tif` filtresi kullanmak mantığı basit tutar ve `.jpg` ya da `.png` gibi alakasız dosyaların çekilmesini önler.

```csharp
// Define the folder that contains the scanned TIFF images -----------------
string inputFolder = @"C:\ScannedDocs"; // <-- replace with your actual path

// Verify the folder exists before we start looping
if (!Directory.Exists(inputFolder))
{
    Console.WriteLine($"❌ Folder not found: {inputFolder}");
    return;
}
```

**Kenar Durumu Notu:** Klasör boşsa, aşağıdaki döngü hiç çalışmaz; bu tamamen normaldir. Daha sonra dostça bir “Dosya bulunamadı” mesajı göreceksiniz.

## Adım 3: Her TIFF Dosyasını İşleyin (Taramalardan Metin Çıkarın)

Şimdi programın kalbi: her bir görüntüyü yüklemek, OCR çalıştırmak ve çıktıyı kaydetmek. `ImageStream.FromFile` yardımcı metodu dosyayı doğrudan belleğe akıtarak, önce bir `Bitmap` yüklemekten daha verimlidir.

```csharp
// Step 3: Iterate over every .tif file in the folder --------------------
string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

if (tiffFiles.Length == 0)
{
    Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
}
else
{
    foreach (var imagePath in tiffFiles)
    {
        try
        {
            // Load the current image into the engine
            ocrEngine.Image = ImageStream.FromFile(imagePath);

            // Perform OCR on the image
            ocrEngine.Recognize();

            // Build the output .txt file path (same name, different extension)
            string textPath = Path.ChangeExtension(imagePath, ".txt");

            // Save the extracted text
            File.WriteAllText(textPath, ocrEngine.Text);

            Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
        }
        catch (Exception ex)
        {
            // Log the error but continue with the next file
            Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

**Neden her yinelemeyi `try/catch` içinde sarıyoruz:**  
Bir belge topluluğunu taramak dağınıktır; bozuk bir TIFF ya da bellek yetersizliği tüm çalışmayı durdurmamalı. `catch` bloğu sorunu kaydeder ve devam eder, böylece işlem hattı dayanıklı kalır.

### Beklenen Çıktı

Her `example.tif` için yanına bir `example.txt` dosyası oluşturulur ve içinde şu tarz bir içerik bulunur:

```
Invoice #12345
Date: 2024‑01‑15
Total: $1,250.00
Thank you for your business!
```

OCR motoru bir satırı okuyamazsa, sadece boş bir satır bırakır ya da bozuk bir karakter gösterir—program çökmez.

## Adım 4: Temizlik ve Kaynak Serbest Bırakma (En İyi Uygulama)

`OcrEngine` `IDisposable` arayüzünü uygular, bu yüzden işiniz bittiğinde yerel kaynakları serbest bırakmak naziktir. Kısa bir konsol uygulamasında GC’ye güvenebilirsiniz, ancak açıkça `Dispose` çağırmak edinmesi gereken bir alışkanlıktır.

```csharp
// Dispose the engine when everything is finished -------------------------
ocrEngine.Dispose();
Console.WriteLine("🎉 All done! OCR engine released.");
```

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda yeni bir Console App projesine yapıştırabileceğiniz eksiksiz program yer alıyor. Aspose.OCR NuGet paketini eklediğiniz sürece olduğu gibi derlenir.

```csharp
using Aspose.OCR;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // --------------------------------------------------------------------
        // Step 1: Initialise the OCR engine (how to use OCR)
        // --------------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine
        {
            UseGpu = true,               // Enable GPU if available
            Language = Language.English  // Set language for recognition
        };

        // --------------------------------------------------------------------
        // Step 2: Define the folder containing TIFF scans (convert TIFF to text)
        // --------------------------------------------------------------------
        string inputFolder = @"C:\ScannedDocs"; // <-- adjust this path

        if (!Directory.Exists(inputFolder))
        {
            Console.WriteLine($"❌ Folder not found: {inputFolder}");
            return;
        }

        // --------------------------------------------------------------------
        // Step 3: Process each TIFF file (extract text from scans)
        // --------------------------------------------------------------------
        string[] tiffFiles = Directory.GetFiles(inputFolder, "*.tif");

        if (tiffFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No TIFF files found in the specified folder.");
        }
        else
        {
            foreach (var imagePath in tiffFiles)
            {
                try
                {
                    // Load image
                    ocrEngine.Image = ImageStream.FromFile(imagePath);

                    // Run OCR
                    ocrEngine.Recognize();

                    // Save result next to source image
                    string textPath = Path.ChangeExtension(imagePath, ".txt");
                    File.WriteAllText(textPath, ocrEngine.Text);

                    Console.WriteLine($"✅ Processed: {Path.GetFileName(imagePath)} → {Path.GetFileName(textPath)}");
                }
                catch (Exception ex)
                {
                    Console.WriteLine($"❌ Failed on {Path.GetFileName(imagePath)}: {ex.Message}");
                }
            }
        }

        // --------------------------------------------------------------------
        // Step 4: Clean‑up (c# OCR tutorial best practice)
        // --------------------------------------------------------------------
        ocrEngine.Dispose();
        Console.WriteLine("🎉 All done! OCR engine released.");
    }
}
```

### Hızlı Kontrol Listesi

- **GPU bayrağı** – CUDA sürücünüz yoksa `false` yapın ya da kaldırın.  
- **Dil** – `Language.English` yerine desteklenen başka bir dili seçin.  
- **Dosya deseni** – Taramalarınız başka bir formatta ise `"*.tif"` yerine `"*.png"` ya da `"*.*"` kullanın.  

## Yaygın Tuzaklar & Pro İpuçları (c# OCR öğreticisi)

| Tuzak | Nasıl Önlenir |
|-------|----------------|
| Büyük toplularda **bellek yetersizliği** | Dosyaları daha küçük parçalar halinde işleyin veya her 50 dosyada bir `GC.Collect()` çağırın (nadiren gerekir). |
| **GPU algılanmadı** ama `UseGpu = true` | Motor sessizce CPU’ya geri döner; oluşturulduktan sonra `ocrEngine.IsGpuAvailable` kontrol edebilirsiniz. |
| **Yanlış dil paketi** garip çıktıya neden olur | `ocrEngine.Language` değerini her zaman açıkça ayarlayın; varsayılan `Language.Unknown` olabilir. |
| **Dosya yolu Unicode karakterler içeriyor** | `Path.GetFullPath` ile normalleştirin, ya da Windows’da yollar 260 karakteri aşıyorsa `@"\\?\"` önekini ekleyin. |

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}