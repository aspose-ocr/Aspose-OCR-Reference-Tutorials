---
category: general
date: 2026-04-26
description: C# ile PNG dosyalarından hızlıca metin çıkarın. Görüntüleri metne dönüştürmeyi,
  PNG dosyalarını okumayı, görüntüler arasında döngü yapmayı ve dakikalar içinde toplu
  OCR işlemi yapmayı öğrenin.
draft: false
keywords:
- extract text from png
- convert images to text
- read png files
- loop through images
- batch ocr images
language: tr
og_description: C# ile PNG dosyalarından metni hızlıca çıkarın. Bu kılavuz, görüntüleri
  metne dönüştürmeyi, PNG dosyalarını okumayı, görüntüler arasında döngü yapmayı ve
  toplu OCR işlemi gerçekleştirmeyi gösterir.
og_title: PNG'den Metin Çıkarma – Tam C# Toplu OCR Eğitimi
tags:
- C#
- OCR
- Aspose
title: PNG'den Metin Çıkarma – Tam C# Toplu OCR Öğreticisi
url: /tr/net/text-recognition/extract-text-from-png-complete-c-batch-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# PNG'den Metin Çıkarma – Tam C# Toplu OCR Öğreticisi

Hiç **PNG'den metin çıkarma** ihtiyacı duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici, ekran görüntüsü klasöründe OCR yapmaya ilk kez çalıştığında bu duvara çarpar. İyi haber şu ki, birkaç satır C# ve Aspose OCR ile görüntüleri metne dönüştürebilir, PNG dosyalarını okuyabilir, görüntüler üzerinde döngü kurabilir ve her şeyi tek seferde toplu‑işlem yapabilirsiniz.  

Bu öğreticide, tam olarak bunu yapan hazır bir konsol uygulamasını adım adım inceleyeceğiz. Sonunda, bir dizindeki her PNG dosyasından metni çıkaran ve her görüntünün yanına eşleşen bir `.txt` dosyası oluşturan bağımsız bir çözüme sahip olacaksınız. Ek script yok, manuel kopyala‑yapıştır yok—sadece saf kod.

## Gereksinimler

- **.NET 6 SDK** (veya daha yeni bir .NET sürümü). Ücretsiz, hızlı ve her yerde çalışır.
- **Aspose.OCR for .NET** (NuGet paketi). Kütüphane, uyumlu bir GPU varsa GPU hızlandırması sağlar, aksi takdirde otomatik olarak CPU'ya geçer.
- İşlemek istediğiniz bir kaç **PNG görüntüsü** içeren bir klasör.  
- Bir metin editörü veya IDE—Visual Studio, VS Code, Rider—ne tercih ederseniz.

Hepsi bu. Eğer bunlar zaten elinizdeyse, hazırsınız demektir.

![png'den metin çıkarma örneği](image.png "png'den metin çıkarma demo ekran görüntüsü")

*Resim alt metni: “C# toplu OCR kullanarak png'den metin çıkarma”*

## Adım 1 – Projeyi Oluşturun ve Aspose.OCR'ı Yükleyin

İlk olarak yeni bir konsol projesi oluşturun ve Aspose OCR paketini ekleyin.

```bash
dotnet new console -n PngOcrBatch
cd PngOcrBatch
dotnet add package Aspose.OCR
```

Neden bir konsol uygulaması kullanıyoruz? Toplu işler için en basit barındırıcıdır ve komut satırından çalıştırılabilir ya da bir görev zamanlayıcıyla planlanabilir. Daha sonra bir UI'ye ihtiyaç duyarsanız, çekirdek mantığı bir sınıf kitaplığına taşıyabilirsiniz.

## Adım 2 – GPU Hızlandırmalı OCR Motorunu (veya CPU geri dönüşünü) Başlatın

Aspose, desteklenen bir GPU'yu otomatik olarak algılayan bir `GpuOcrEngine` sunar. Hiçbiri bulunmazsa, normal CPU motoruna geri döner—ekstra kod gerekmez.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // Create the OCR engine – GPU if available, otherwise CPU
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;   // Latin covers most Western alphabets

        // The rest of the code lives in a separate method for clarity
        ProcessFolder(ocrEngine, @"C:\MyPngFolder");
    }

    // …
}
```

**İpucu:** GPU'suz bir başsız sunucuda çalışıyorsanız, `GpuOcrEngine` yerine `OcrEngine` kullanabilirsiniz; kod aynı şekilde davranır.

## Adım 3 – Hedef Dizin İçindeki Görüntüler Üzerinde Döngü Kurun

**Görüntüler üzerinde döngü** kurmamız ve sadece PNG dosyalarını seçmemiz gerekiyor. `Directory.GetFiles` metodu işi halleder ve boş bir klasör durumuna karşı koruma sağlar.

```csharp
static void ProcessFolder(OcrEngine engine, string folderPath)
{
    if (!Directory.Exists(folderPath))
    {
        Console.WriteLine($"❌ Folder not found: {folderPath}");
        return;
    }

    // Grab every *.png file – this is the “read png files” part
    string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

    if (pngFiles.Length == 0)
    {
        Console.WriteLine("⚠️ No PNG files found. Make sure the folder contains .png images.");
        return;
    }

    foreach (var pngPath in pngFiles)
    {
        Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
        ExtractAndSave(engine, pngPath);
    }
}
```

`SearchOption.TopDirectoryOnly` kullanımına dikkat edin. Daha sonra alt‑klasörlere de bakmanız gerekirse, sadece `AllDirectories` olarak değiştirin. Bu küçük değişiklik, **görüntüleri metne dönüştür** işlemini tek bir satırla tüm ağaçta yapmanızı sağlar.

## Adım 4 – OCR'ı Gerçekleştir ve Sonucu Kaydet

Şimdi **toplu OCR görüntüleri** iş akışının çekirdeği devreye giriyor. Her PNG'yi yüklüyoruz, `Recognize()` çalıştırıyoruz ve çıkarılan dizeyi aynı temel ada sahip bir `.txt` dosyasına yazıyoruz.

```csharp
static void ExtractAndSave(OcrEngine engine, string imagePath)
{
    try
    {
        // Load the PNG into the engine
        engine.Image = ImageStream.FromFile(imagePath);

        // Run recognition – this returns a RecognitionResult object
        RecognitionResult result = engine.Recognize();

        // Build the output path (same name, .txt extension)
        string txtPath = Path.ChangeExtension(imagePath, ".txt");

        // Write the OCR text to disk
        File.WriteAllText(txtPath, result.Text);

        Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
    }
    catch (Exception ex)
    {
        // Edge case: corrupted PNG or unsupported format
        Console.WriteLine($"❗ Error processing {Path.GetFileName(imagePath)}: {ex.Message}");
    }
}
```

**Neden try/catch içinde sarmalıyoruz?** Gerçek dünya görüntü toplulukları genellikle bozuk bir dosya ya da nadir bir renk profili kullanan bir PNG içerir. İstisna yakalanırsa tüm çalışmanın çökmesi önlenir ve kalan dosyalar işlenmeye devam eder.

## Adım 5 – Uygulamayı Çalıştırın ve Çıktıyı Doğrulayın

Uygulamayı derleyip başlatın:

```bash
dotnet run
```

Aşağıdaki gibi bir konsol kaydı görmelisiniz:

```
🔎 Processing: invoice1.png
✅ Saved: invoice1.txt
🔎 Processing: screenshot_2024.png
✅ Saved: screenshot_2024.txt
...
```

Oluşturulan herhangi bir `.txt` dosyasını açın—çıkarılan metin orada. Dosya boşsa, görüntü kalitesini tekrar kontrol edin; OCR, net ve yüksek kontrastlı metinlerde en iyi sonucu verir.

### Hızlı Doğrulama Scripti (isteğe bağlı)

Her PNG'nin eşleşen bir metin dosyası aldığından emin olmak istiyorsanız, bu küçük PowerShell tek satırını çalıştırın:

```powershell
Get-ChildItem -Path "C:\MyPngFolder" -Filter *.png |
  ForEach-Object { 
    $txt = $_.BaseName + ".txt"
    if (-Not (Test-Path $txt)) { Write-Host "Missing: $txt" }
  }
```

## Yaygın Varyasyonlar ve Kenar Durumları

| Durum | Değiştirilecek Şey |
|-----------|----------------|
| **Latin dışı diller** (ör. Kiril) | `ocrEngine.Language = Language.Cyrillic;` |
| **Büyük görüntü seti (>10 000 dosya)** | İşlem hızını artırmak için `Parallel.ForEach` kullanın, ancak GPU bellek kullanımına dikkat edin. |
| **Orijinal görüntü sırasını korumak** | `foreach` öncesinde `pngFiles` dizisini sıralayın (`Array.Sort(pngFiles);`). |
| **GPU'suz bir CI sunucusunda çalıştırma** | GPU başlatma hatalarını önlemek için `GpuOcrEngine` yerine `OcrEngine` kullanın. |
| **Belirli bir anahtar kelime içeren dosyaları işlemek** | `result.Text` alındıktan sonra, dosyayı yazmadan önce `result.Text.Contains("Invoice")` kontrol edin. |

Bu ayarlamalar, **görüntüleri metne dönüştür** boru hattını neredeyse her senaryoya uyarlamanızı sağlar.

## Tam Kaynak Kodu (Kopyala‑Yapıştır Hazır)

```csharp
// ------------------------------------------------------------
// Extract Text from PNG – Batch OCR using Aspose.OCR (C#)
// ------------------------------------------------------------
using Aspose.OCR;
using Aspose.OCR.Gpu;
using System;
using System.IO;

class Program
{
    static void Main()
    {
        // 1️⃣ Create OCR engine (GPU if possible)
        OcrEngine ocrEngine = new GpuOcrEngine();
        ocrEngine.Language = Language.Latin;

        // 2️⃣ Define the folder that holds your PNG files
        string targetFolder = @"C:\MyPngFolder";   // <-- change to your path

        // 3️⃣ Process every PNG in the folder
        ProcessFolder(ocrEngine, targetFolder);
    }

    static void ProcessFolder(OcrEngine engine, string folderPath)
    {
        if (!Directory.Exists(folderPath))
        {
            Console.WriteLine($"❌ Folder not found: {folderPath}");
            return;
        }

        string[] pngFiles = Directory.GetFiles(folderPath, "*.png", SearchOption.TopDirectoryOnly);

        if (pngFiles.Length == 0)
        {
            Console.WriteLine("⚠️ No PNG files found.");
            return;
        }

        foreach (var pngPath in pngFiles)
        {
            Console.WriteLine($"🔎 Processing: {Path.GetFileName(pngPath)}");
            ExtractAndSave(engine, pngPath);
        }
    }

    static void ExtractAndSave(OcrEngine engine, string imagePath)
    {
        try
        {
            engine.Image = ImageStream.FromFile(imagePath);
            RecognitionResult result = engine.Recognize();

            string txtPath = Path.ChangeExtension(imagePath, ".txt");
            File.WriteAllText(txtPath, result.Text);

            Console.WriteLine($"✅ Saved: {Path.GetFileName(txtPath)}");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"❗ Error on {Path.GetFileName(imagePath)}: {ex.Message}");
        }
    }
}
```

Bunu `Program.cs` olarak kaydedin, `dotnet run` komutunu çalıştırın ve sihrin gerçekleşmesini izleyin.

## Sonuç

Artık C# kullanarak **PNG dosyalarından metin çıkarma** için **tam, üretim‑hazır** bir yönteme sahipsiniz. Öğreticide, projeyi kurmaktan GPU‑hızlandırmalı bir OCR motoru başlatmaya, **görüntüler üzerinde döngü** kurmaya ve **toplu OCR görüntüleri** işleyip sonuçları düz metin olarak kaydetmeye kadar her şeyi ele aldık.  

Bir sonraki adımları merak ediyorsanız, şunları deneyin:

- Diğer formatlar (JPG, BMP) için **görüntüleri metne dönüştür**  
- ...

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}