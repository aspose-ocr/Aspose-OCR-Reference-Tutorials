---
category: general
date: 2026-03-17
description: C# ile PNG görüntülerini hızlı bir şekilde toplu OCR yapma. PNG dosyalarından
  metin çıkarmayı, PNG'yi metne dönüştürmeyi ve basit bir script ile dizinden görüntüleri
  okumayı öğrenin.
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: tr
og_description: C#'ta adım adım kodla PNG görüntülerini toplu OCR nasıl yapılır. PNG
  dosyalarından metin çıkarın, PNG'yi metne dönüştürün ve dizinden görüntüleri zahmetsizce
  okuyun.
og_title: C# ile PNG Görüntülerini Toplu OCR İşlemi – Tam Kılavuz
tags:
- OCR
- C#
- Image Processing
title: C# ile PNG Görüntüleri Toplu OCR – Tam Kılavuz
url: /tr/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta PNG Görüntüleri Toplu OCR İşlemi – Tam Kılavuz

Her zaman **toplu OCR** nasıl yapılır diye merak ettiniz mi, bir klasördeki ekran görüntülerini tek tek açmadan? Tek başınıza değilsiniz—geliştiriciler sürekli olarak büyük PNG koleksiyonlarını toplu OCR yapmanın yolunu soruyor, özellikle hedef, aşağı akış analizleri için metin PNG dosyalarını çıkarmak olduğunda.  

Bu öğreticide **metin PNG** dosyalarını **PNG'yi metne dönüştüren**, ve size **dizinden görüntüleri okuma** konusunda en iyi yolu gösteren hazır‑çalıştır C# örneği üzerinden ilerleyeceğiz. Sonunda her görüntünün yanına bir `.txt` dosyası bırakan tek bir betiğiniz olacak ve saatlerce manuel kopyala‑yapıştırma yapmaktan kurtulacaksınız.

## Başaracaklarınız

- OCR motorunu bir kez başlatıp tüm toplu işlem için yeniden kullanın.  
- Kendi döngünüzü yazmadan verilen klasördeki her `*.png` dosyasını tarayın.  
- Her OCR sonucunu ayrı bir metin dosyasına yazın, özgün dosya adını koruyarak.  
- Boş klasörler veya görüntü olmayan dosyalar gibi yaygın kenar durumlarını sorunsuz şekilde yönetin.

### Önkoşullar

- .NET 6.0 veya üzeri (kod .NET Core ve .NET Framework üzerinde de çalışır).  
- `OcrEngine`, `ImageStream` ve `OcrResult` tiplerini sunan bir OCR kütüphanesi (örneğin, örneklerde kullanılan kurgusal **FastOCR** SDK'sı).  
- Temel C# bilgisi—gelişmiş desenler gerekmez.

---

## PNG Görüntüleri Toplu OCR – Genel Bakış

Aşağıda **tam, çalıştırılabilir program** yer alıyor. Yeni bir konsol projesine kopyala‑yapıştırın, yer tutucu yolları değiştirin ve **F5** tuşuna basın.

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **Beklenen çıktı:** Her `image01.png` için tanınan karakterleri içeren bir `image01.txt` bulacaksınız. Konsol, her dosya yazıldıkça listeler.

![Toplu OCR diyagramı](how-to-batch-ocr-diagram.png "C# kullanarak PNG görüntüleri toplu OCR nasıl yapılır gösteren diyagram")

---

## Adım‑Adım Açıklama

### 1. OCR Motorunu Başlatma – İşlemin Kalbi  

`var ocrEngine = new OcrEngine();` satırı, tüm toplu işlem boyunca yeniden kullanılacak tek bir motor örneği oluşturur. Motoru yeniden kullanmak **kritik**tir çünkü çoğu OCR kütüphanesi oluşturulurken ağır kaynaklar (dil modelleri gibi) tahsis eder. Tek seferde başlatmak performansı büyük ölçüde artırır—özellikle onlarca ya da yüzlerce PNG'niz olduğunda.  

> **Pro ipucu:** İngilizce dışındaki bir dil gerekiyorsa, `ocrEngine.Config.Language = Language.Spanish;` (veya desteklenen herhangi bir enum) ayarlayın.  

### 2. Dizinden Görüntüleri Okuma – her PNG'yi bulma  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` ikinci anahtar kelime *dizinden görüntüleri okuma* sözünü tam olarak yerine getirir. Mutlak yol dizisi döndürür ve bunu daha sonra OCR motoruna besleriz.  

> **Neden `SearchOption.AllDirectories` kullanılmıyor?** Görüntüleriniz alt klasörlerdeyse, `GetFiles(path, "*.png", SearchOption.AllDirectories)` şeklinde değiştirebilirsiniz. Daha derin taramaların istenmeyen dosyaları da getirebileceğini unutmayın, bu yüzden filtrelemeyi ona göre ayarlayın.  

### 3. Dosya Yollarını ImageStream Nesnelerine Dönüştürme  

Çoğu OCR SDK'sı ham yol yerine bir akış bekler. LINQ ifadesi `Select(path => ImageStream.FromFile(path)).ToList()` **akış listesi** oluşturur ve toplu tanıyıcı tek bir çağrıda tüketebilir. Bu adım ayrıca dosya tanıtıcılarının yalnızca bir kez açılmasını sağlar, I/O yükünü azaltır.  

> **Kenar durumu:** Bir dosya bozuksa, `ImageStream.FromFile` bir istisna fırlatabilir. Dayanıklılık gerekiyorsa dönüşümü `try/catch` içinde sarmalayın.  

### 4. Tüm Toplu İçinde Metni Tanıma  

`ocrEngine.RecognizeBatch(imageStreams)` *toplu OCR nasıl yapılır* sorusunun tam yanıtıdır. Her görüntü üzerinde döngü kurup tek‑görüntü metodunu çağırmak yerine, tüm koleksiyonu motora veririz. İçeride kütüphane işi paralelleştirerek çok çekirdekli makinelerde hız artışı sağlar.  

> **İpucu:** OCR kütüphaneniz bir toplu metod sunmuyorsa, tek‑görüntü `Recognize` çağrısını `Parallel.ForEach` ile sararak benzer performans elde edebilirsiniz.  

### 5. Her OCR Sonucunu Yazma – PNG'yi metne dönüştürme  

Son `for` döngüsü `ocrResults[i].Text` değerini, orijinal PNG ile aynı adı taşıyan bir `.txt` dosyasına yazar. Bu, ikinci anahtar kelime *PNG'yi metne dönüştür* ifadesinin tam karşılığıdır. `Path.Combine` çağrısı çıktı klasörünün var olduğunu garanti eder ve yol‑geçiş hatalarını önler.  

> **Yaygın tuzak:** Çıktı klasörünü önceden oluşturmazsanız `DirectoryNotFoundException` alırsınız. `Directory.CreateDirectory(outputFolder);` satırı bunu önceden çözer.  

---

## Gerçek‑Dünya Varyasyonlarını Ele Alma

| Durum | Ne Değiştirilmeli | Neden |
|-----------|----------------|-----|
| **Boş giriş klasörü** | Erken `if (imagePaths.Length == 0)` korumasını tutun | Gereksiz bir OCR çağrısını önler ve dostça bir mesaj verir |
| **Karışık dosya türleri** | `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` kullanın | Sadece PNG'leri işlediğinizi garantiler, *extract text png* anahtar kelimesini hatasız karşılar |
| **Büyük görüntüler ( > 5 MB )** | OCR'ye beslemeden önce küçültün: `ImageStream.FromFile(path).Resize(1920, 1080)` (API destekliyorsa) | Bellek baskısını azaltır ve genellikle tanıma doğruluğunu artırır |
| **Farklı OCR dili** | `ocrEngine.Config.Language = Language.French;` ayarlayın | Motoru kaynak görüntülerin diline uyumlu hale getirir |

---

## Sıkça Sorulan Sorular (SSS)

**S: Bu JPEG veya TIFF dosyalarıyla da çalışır mı?**  
C: Temel mantık aynı kalır; arama desenini `"*.jpg"` ya da `"*.tif"` olarak değiştirin ve OCR kütüphanesinin bu formatları çözebildiğinden emin olun.

**S: Binlerce görüntüyü belleği tükenmeden nasıl işleyebilirim?**  
C: Toplu çağrıyı bir akış yaklaşımıyla değiştirin—örneğin 50 görüntülük bir parçayı işleyin, ardından bir sonraki parçayı yüklemeden önce akışları serbest bırakın.

**S: OCR güven skoruna ihtiyacım var. Nereden bulabilirim?**  
C: Çoğu `OcrResult` nesnesi bir `Confidence` özelliği sunar. Yazma adımını şu şekilde genişletebilirsiniz:

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## Özet

**Toplu OCR** PNG görüntülerini C#'ta baştan sona nasıl yapılır konusunu yeni kapattık. Tek bir motor başlatarak, dizinden görüntüleri okuyarak, akışlara dönüştürerek, tüm toplu işlemi tanıyarak ve sonunda her sonucu bir metin dosyasına yazarak, **extract text PNG**, **convert PNG to text** ve **read images from directory** görevleri için sağlam, üretim‑hazır bir desen elde ettiniz.  

Sırada ne var? OCR sağlayıcısını değiştirin, çok‑iş parçacıklı sonrası işleme (ör. yazım denetimi) ekleyin ya da `.txt` dosyalarını bir arama indeksine besleyin. Toplu iş akışını ustalaştığınızda sınır yoktur.  

Paylaşmak istediğiniz bir farklılık var mı? Yorum bırakın ve mutlu kodlamalar!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}