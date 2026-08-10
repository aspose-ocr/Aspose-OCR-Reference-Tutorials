---
category: general
date: 2026-02-13
description: C#'ta OCR kullanarak görüntüden metin çıkarma, fotoğraf veya JPG'den
  metin tanıma ve internet olmadan görüntüde OCR çalıştırma.
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from photo
- recognize text from jpg
- run OCR on image
language: tr
og_description: C#'ta OCR kullanarak görüntüden metin çıkarma, fotoğraftan metin tanıma
  ve tam, çalıştırılabilir bir örnekle görüntüde OCR çalıştırma.
og_title: C#'ta OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma
tags:
- OCR
- C#
- Image Processing
title: C#'ta OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma ve Fotoğraftan Metin
  Tanıma
url: /tr/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image-and-recognize-te/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta OCR Nasıl Kullanılır – Görüntüden Metin Çıkarma ve Fotoğraftan Metin Tanıma

Hiç **OCR nasıl kullanılır** diye merak ettiniz mi, bir ekran görüntüsünden, taranmış bir makbuzdan ya da telefonunuzla çektiğiniz rastgele bir fotoğraftan kelimeleri çıkarmak için? Tek başınıza değilsiniz. Gerçek dünyadaki birçok uygulamada resimleri aranabilir metne dönüştürmemiz gerekiyor ve bunu yerel olarak—kararsız bir internet bağlantısı olmadan—yapmak bir bulmaca gibi hissettirebilir.

Bu yüzden bu rehber, bir C# OCR motoru kullanarak **görüntüden metin çıkarma** dosyalarını adım adım nasıl yapacağınızı gösteriyor ve ayrıca **fotoğraftan metin tanıma**, **JPG'den metin tanıma** ve **görüntüde OCR çalıştırma** dosyalarını doğrudan diskinizdeki dosyalarda nasıl yapacağınızı kapsıyor. Sonunda kutudan çıkar çıkmaz çalışan, kopyala‑yapıştır hazır bir programınız olacak.

## Öğrenecekleriniz

- Basitleştirilmiş Çince (veya bağladığınız herhangi bir dil) için bir OCR motorunu nasıl yapılandıracağınızı.  
- Yerel bir klasörden **kaynakları yüklemek** için gereken tam kod—ağ çağrısı gerektirmez.  
- JPEG, PNG veya BMP gibi **fotoğraftan metin tanıma** dosyalarını nasıl yapacağınızı.  
- Eksik model dosyaları veya desteklenmeyen görüntü formatları gibi yaygın kenar durumlarını ele almak için ipuçları.  
- Visual Studio'ya bırakıp anında sonuç görebileceğiniz tam, çalıştırılabilir bir örnek.

### Önkoşullar

- .NET 6.0 veya üzeri (burada kullanılan API .NET Standard 2.0 hedefli, bu yüzden daha eski sürümler de çalışır).  
- C# ve Visual Studio (veya tercih ettiğiniz herhangi bir IDE) hakkında temel bilgi.  
- Kullandığınız OCR kütüphanesi (parça, dil modelleriyle birlikte gelen kurgusal bir `OcrEngine` sınıfı varsayar).  
- Gerekli dil model dosyalarını içeren bir klasör—bunu motorun Çince karakterleri okumasını sağlayan “beyin” olarak düşünün.

> **Pro ipucu:** Henüz Çince model dosyalarına sahip değilseniz, satıcı sitesinden bir kez indirin ve `C:\OcrResources` gibi bir klasöre yerleştirin. Motor bir daha internete bağlanmak zorunda kalmayacak.

---

![Diagram showing OCR process on a photo](path/to/ocr-diagram.png "Diagram showing OCR process on a photo")

## OCR Nasıl Kullanılır: Motoru Kurma

İlk olarak ihtiyacınız olan şey, ilgilendiğiniz dil için yapılandırılmış bir OCR motoru örneğidir. Bu öğreticide **Basitleştirilmiş Çince** hedefliyoruz, ancak `OcrLanguage.ChineseSimplified` yerine `OcrLanguage.English` (veya başka bir enum değeri) koymak sadece tek satırlık bir değişikliktir.

```csharp
using System;
using YourOcrLibrary;   // Replace with the actual namespace of your OCR SDK

// Step 1: Create and configure the OCR engine for Simplified Chinese
var ocrEngine = new OcrEngine
{
    // Primary keyword appears here naturally
    Language = OcrLanguage.ChineseSimplified,

    // Point to a folder that already contains the Chinese model files
    ResourceFolder = @"C:\OcrResources"
};
```

**Neden önemli:**  
`Language` özelliğini ayarlamak, motorun hangi karakter setini bekleyeceğini söyler. `ResourceFolder`, motorun sinir ağı ağırlıklarını ve dil sözlüklerini aradığı yerdir—beynin hafıza bankası gibi düşünün. Yanlış klasöre işaret ederseniz motor bir `FileNotFoundException` fırlatır ve takılı kalırsınız.

## Görüntüden Metin Çıkarma – Kaynakları Yükleme

Motor gerçekten bir şey okuyabilmeden önce, bu model dosyalarını belleğe yüklemeniz gerekir. Bu adım **kritiktir** çünkü her görüntüyü işlediğinizde bir ağ çağrısı yapmaktan kaçınır.

```csharp
// Step 2: Load the language resources from the specified folder (no internet required)
try
{
    ocrEngine.LoadResources();
    Console.WriteLine("Resources loaded successfully.");
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Failed to load OCR resources: {ex.Message}");
    // In a real app you might fallback to a default language or abort gracefully
}
```

**Ne yanlış gidebilir?**  
Klasör yolu yanlışsa veya dosyalar bozuksa, `LoadResources()` bir istisna yükseltir. Yukarıdaki `try/catch` bloğu, üretimde sıkça ihtiyaç duyacağınız zarif hata yönetimini gösterir.

## Fotoğraftan Metin Tanıma – OCR Çalıştırma

Şimdi eğlenceli kısım: bir görüntü dosyasını motora beslemek ve tanınan metni geri almak. Bu, **görüntüde OCR çalıştırma** senaryolarının çekirdeğidir, ister JPEG, PNG ister BMP olsun.

```csharp
// Step 3: Recognize text from an image file
string imagePath = @"C:\OcrResources\photo.jpg";

try
{
    var recognitionResult = ocrEngine.RecognizeImage(imagePath);
    Console.WriteLine("=== OCR Output ===");
    Console.WriteLine(recognitionResult.Text);
}
catch (Exception ex)
{
    Console.Error.WriteLine($"Error during OCR processing: {ex.Message}");
}
```

`RecognizeImage` yöntemi, tipik olarak şunları içeren bir `RecognitionResult` (veya SDK'nızın adlandırdığı şey) döndürür:

- `Text` – düz metin transkripsiyonu.  
- `Confidence` – motorun her satır hakkında ne kadar emin olduğunu gösteren sayısal bir puan.  
- `BoundingBoxes` – isteğe bağlı olarak her kelimenin resimde nerede bulunduğunun koordinatları.

**Neden güven puanına önem vermelisiniz:**  
Bir veri girişi otomasyon aracı geliştiriyorsanız, bir eşik (ör. 0.85) belirleyebilir ve düşük güven puanlı satırları kullanıcıdan onaylatabilirsiniz. Bu, genel doğruluğu büyük ölçüde artırır.

## JPG'den Metin Tanıma – Farklı Formatları Ele Alma

Birçok geliştirici OCR'un sadece PNG'lerde çalıştığını varsayar, ancak modern motorlar **JPG** dosyalarını da sorunsuz işler. Tek sorun, JPEG sıkıştırmasının modeli şaşırtabilecek artefaktlar oluşturabilmesidir.

```csharp
// Bonus: Recognize text from a JPG with optional preprocessing
string jpgPath = @"C:\OcrResources\scanned_doc.jpg";

// Optional: use a simple image‑preprocess step to improve accuracy
var preprocessed = ImageHelper.DenoiseAndDeskew(jpgPath); // pseudo‑method
var result = ocrEngine.RecognizeImage(preprocessed);
Console.WriteLine($"Detected text ({result.Confidence:P0} confidence):");
Console.WriteLine(result.Text);
```

`DenoiseAndDeskew` yardımcı fonksiyonuna sahip değilseniz, birçok kütüphane (ör. OpenCvSharp) bu işlevleri sağlar. Ana çıkarım: **görüntüde OCR çalıştırma** dosyaları, bir tarayıcıdan ya da telefon kamerasından geldiyse biraz temizlikten sonra yapılmalıdır.

## Görüntüde OCR Çalıştırma – İpuçları, Kenar Durumları ve En İyi Uygulamalar

### 1. Bellek Yönetimi
Büyük dil modellerini yüklemek yüzlerce megabayt tüketebilir. İşiniz bittiğinde motoru serbest bırakın:

```csharp
ocrEngine.Dispose(); // or using statement if the SDK implements IDisposable
```

### 2. Toplu İşleme
Onlarca fotoğrafı işlemek zorundaysanız, kaynakları bir kez yükleyin, ardından döngü içinde kullanın:

```csharp
string[] files = Directory.GetFiles(@"C:\BatchPhotos", "*.jpg");
foreach (var file in files)
{
    var res = ocrEngine.RecognizeImage(file);
    File.WriteAllText(Path.ChangeExtension(file, ".txt"), res.Text);
}
```

### 3. Çok‑Dilli Senaryolar
`ocrEngine.Language` değerini yeniden atayarak ve `LoadResources()` tekrar çağırarak dilleri anlık olarak değiştirebilirsiniz. Ancak ekstra yükleme süresine dikkat edin.

### 4. Boş Sonuçları Ele Alma
Bazen motor boş bir string döndürür. Bu genellikle görüntünün çok bulanık olduğu ya da metin renginin arka planla karıştığı anlamına gelir. Hızlı bir kontrol:

```csharp
if (string.IsNullOrWhiteSpace(recognitionResult.Text))
{
    Console.WriteLine("No text detected – consider increasing image contrast.");
}
```

### 5. Güvenlik Hususları
Kullanıcı tarafından yüklenen dosyaları doğrudan OCR motoruna doğrulama yapmadan vermeyin. En azından dosya uzantısını ve boyutunu kontrol edin, ayrıca kötü amaçlı yazılım taraması yapmayı düşünün.

## Tam Çalışan Örnek

Aşağıda, yeni bir Console App projesine kopyalayabileceğiniz tek bir, bağımsız program bulunuyor. **OCR nasıl kullanılır**, **görüntüden metin çıkarma**, **fotoğraftan metin tanıma**, **JPG'den metin tanıma** ve **görüntüde OCR çalıştırma** konularını bir arada gösterir.

```csharp
// File: Program.cs
using System;
using System.IO;
using YourOcrLibrary; // Replace with actual namespace

namespace OcrDemo
{
    class Program
    {
        static void Main()
        {
            // ------------------------------
            // 1️⃣ Configure the OCR engine
            // ------------------------------
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.ChineseSimplified,
                ResourceFolder = @"C:\OcrResources"
            };

            // Load language resources (no internet needed)
            try
            {
                ocrEngine.LoadResources();
                Console.WriteLine("Resources loaded.");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"Failed to load resources: {ex.Message}");
                return;
            }

            // -------------------------------------------------
            // 2️⃣ Recognize text from a photo (JPG in this case)
            // -------------------------------------------------
            string imagePath = @"C:\OcrResources\photo.jpg";

            if (!File.Exists(imagePath))
            {
                Console.Error.WriteLine($"Image not found: {imagePath}");
                return;
            }

            try
            {
                var result = ocrEngine.RecognizeImage(imagePath);
                Console.WriteLine("\n=== OCR Output ===");
                Console.WriteLine(result.Text);
                Console.WriteLine($"\nConfidence: {result.Confidence:P2}");
            }
            catch (Exception ex)
            {
                Console.Error.WriteLine($"OCR error: {ex.Message}");
            }

            // Clean up
            ocrEngine.Dispose();
        }
    }
}
```

**Beklenen çıktı (örnek):**

```
Resources loaded.

=== OCR Output ===
中华人民共和国
北京
2026年02月13日

Confidence: 92.45%
```

Gerçek metniniz, görüntü içeriğine bağlı olarak farklılık gösterecek, ancak konsolda bir Unicode karakter bloğu ve bir güven puanı yüzde olarak yazdırılmış olarak görmelisiniz.

## Sonuç

C#'ta **OCR nasıl kullanılır** konusunu baştan sona yürüttük—motoru yapılandırma, dil kaynaklarını yükleme ve sonunda **fotoğraftan metin tanıma** ya da **JPG** dosyalarından metin tanıma, internete hiç dokunmadan. Yukarıdaki adımları izleyerek **görüntüden metin çıkarma** dosyalarını, **görüntüde OCR çalıştırma** varlıklarını ve yeni başlayanları sık sık tuzağa düşüren en yaygın sorunları halledebilirsiniz.

Bir sonraki meydan okumaya hazır mısınız? Motoru bir PDF sayfasını görüntüye dönüştürerek beslemeyi deneyin ya da farklı bir dil paketini deneyerek güven puanlarının nasıl değiştiğini görün. You might

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}