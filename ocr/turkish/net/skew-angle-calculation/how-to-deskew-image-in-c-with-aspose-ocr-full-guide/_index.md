---
category: general
date: 2026-03-23
description: Aspose OCR kullanarak C#'de görüntünün eğimini nasıl düzelteceğinizi
  öğrenin. Gürültüyü nasıl kaldıracağınızı, görüntü dönüşünü nasıl düzelteceğinizi
  ve dakikalar içinde görüntüden metni nasıl tanıyacağınızı keşfedin.
draft: false
keywords:
- how to deskew image
- how to remove noise
- recognize text from image
- remove salt pepper noise
- correct image rotation
language: tr
og_description: Aspose OCR ile görüntünün eğriliğini hızlıca nasıl düzelteceğinizi
  öğrenin. Bu kılavuz ayrıca gürültüyü nasıl kaldıracağınızı, görüntü döndürmesini
  nasıl düzelteceğinizi ve görüntüden metni nasıl tanıyacağınızı gösterir.
og_title: C#'de Görüntüyü Eğrilikten Düzeltme – Tam Aspose OCR Öğreticisi
tags:
- OCR
- C#
- Image Preprocessing
title: Aspose OCR ile C#’ta Görüntüyü Düzleştirme – Tam Kılavuz
url: /tr/net/skew-angle-calculation/how-to-deskew-image-in-c-with-aspose-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta Görüntüyü Düzeltme – Tam Aspose OCR Öğreticisi

Hiç **görüntüyü nasıl düzeltir** dosyalar bir tarayıcıdan geliyor ve biraz eğik olduğunda merak ettiniz mi? Yalnız değilsiniz. Birçok gerçek dünya projesinde kaynak resim birkaç derece eğik, tuz‑ve‑biber gürültüsüyle kaplı ve hâlâ düz metin olarak okunması gerekiyor.  

İyi haber? Aspose OCR ile dönüşümü düzeltebilir, gürültüyü temizleyebilir ve ardından **görüntüden metni tanıma**—hepsi birkaç satırda. Bu öğreticide tüm süreci adım adım inceleyecek, her filtrenin neden önemli olduğunu açıklayacak ve size çalıştırmaya hazır bir C# programı sunacağız.

> *Pro tip:* Aspose OCR'ı daha önce hiç kullanmadıysanız, Aspose web sitesinden ücretsiz deneme sürümünü alın; API .NET 6+ ile kutudan çıkar çıkmaz çalışır.

---

## Gereksinimler

- **.NET 6 SDK** (veya herhangi bir yeni .NET sürümü) – kod Visual Studio, Rider veya `dotnet` CLI ile derlenir.  
- **Aspose.OCR NuGet package** – `dotnet add package Aspose.OCR` komutuyla kurun.  
- Hafifçe döndürülmüş ve gürültü içeren bir **örnek resim** (ör. `skewed.png`).  
- Temel C# bilgisi – uzman olmanız gerekmez, sadece `using` ifadeleri ve konsol ile rahat olmanız yeterlidir.

Hepsi bu. Başka OCR motoru, yerel DLL yok, sadece tek bir NuGet referansı.

---

## Görüntüyü Düzeltme – Adım Adım Genel Bakış

Aşağıda süreci mantıksal adımlara ayırıyoruz. Her adım net bir başlığa, bir kod parçacığına ve çağrının nedenini açıklayan kısa bir “neden” paragrafına sahiptir, böylece mantığını anlayabilirsiniz.

![görüntüyü nasıl düzeltir örnek](https://example.com/deskew-demo.png "görüntüyü nasıl düzeltir")

---

### Adım 1: OCR Motorunu Kurma

İlk olarak bir `OcrEngine` örneği oluşturuyoruz. `using` bloğu, işi bittiğinde yerel kaynakları serbest bırakarak doğru bir şekilde imha edilmesini sağlar.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Step 1 – instantiate the OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // The rest of the pipeline goes here...
        }
    }
}
```

*Neden önemli?* `OcrEngine`, Aspose OCR'ın kalbidir. Görüntüyü, filtre zincirini ve tanıma ayarlarını tutar. `using` içinde sarmak, özellikle toplu işte onlarca sayfa işlenirken bellek sızıntılarını önler.

---

### Adım 2: Tarama Görüntüsünü Yükleme

`ImageStream.FromFile` ile dosyayı yüklüyoruz. Yol, çalıştırılabilir dosyanın çalışma dizinine göre mutlak ya da göreli olabilir.

```csharp
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");
```

*Neden önemli?* Motor, bellek içi bir görüntü akışı üzerinde çalışır. Doğru yolu sağlamak, `FileNotFoundException` alabileceğiniz tek yerdir; bu yüzden çalıştırmadan önce klasör yapısını iki kez kontrol edin.

---

### Adım 3: Ön‑İşleme Filtrelerini Ekleme

Burada **gürültüyü nasıl kaldır** ve **görüntü dönüşümünü nasıl düzelt** sorularına yanıt veriyoruz. İki yerleşik filtre işi halleder:

```csharp
// DeskewFilter corrects small rotation (usually up to ±5°)
ocrEngine.Filters.Add(new DeskewFilter());

// DenoiseFilter removes salt‑and‑pepper noise
ocrEngine.Filters.Add(new DenoiseFilter());
```

*Bu filtreler neden?*
- **DeskewFilter** metin tabanlarını analiz eder, eğim açısını hesaplar ve bitmap'i yatay konuma döndürür. Olmasaydı OCR motoru karakterleri yanlış yorumlayabilir (ör. “l” vs. “i”).
- **DenoiseFilter** izole siyah/beyaz pikselleri yumuşatan medyan tabanlı bir algoritma uygular—görüntü işleme jargonunda “tuz ve biber gürültüsünü kaldır” anlamına gelir. Bu, güven skorlarını büyük ölçüde artırır.

Eğer çok bulanık bir taramanız varsa, `SharpenFilter` ekleyebilirsiniz, ancak bu isteğe bağlı bir ayardır.

---

### Adım 4: OCR Tanımasını Çalıştırma

Şimdi Aspose OCR'dan işini yapmasını istiyoruz. `Recognize` metodu, başarıyı gösteren bir boolean döndürür.

```csharp
if (ocrEngine.Recognize())
{
    // Step 5 – output the cleaned text
    Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
}
else
{
    Console.Error.WriteLine("OCR failed – check the image and filter configuration.");
}
```

*Sonucu neden kontrol ediyoruz:* Bazen motor herhangi bir metin bulamaz (ör. boş sayfa). `false` durumunu ele almak, daha sonra hata ayıklaması zor olabilecek sessiz bir hatayı önler.

---

### Adım 5: Çıktıyı Doğrulama

Programı çalıştırdığınızda aşağıdakine benzer bir şey görmelisiniz:

```
Cleaned text:
The quick brown fox jumps over the lazy dog.
```

Metin hâlâ bozuk görünüyorsa, şunları göz önünde bulundurun:

- **Deskew toleransını artırma** – `new DeskewFilter(0.1)` filtreye daha büyük açıları kabul ettirir.  
- **Denoising** öncesinde `BinarizeFilter` ekleyerek görüntüyü saf siyah‑beyaz'a dönüştürme.  
- **DPI'yi kontrol etme** – düşük çözünürlüklü taramalar (< 150 dpi) genellikle OCR'dan önce ölçeklendirilmelidir.

---

## Gürültüyü Kaldırma – İleri Seçenekler

Temel `DenoiseFilter`, tipik tarayıcı lekeleri için iyi çalışır, ancak bazen eski film taramalarında **tuz ve biber gürültüsünü kaldır** ile karşılaşırsınız. Bu durumlarda:

```csharp
// Apply a stronger median filter (kernel size 3x3)
ocrEngine.Filters.Add(new DenoiseFilter { KernelSize = 3 });
```

Veya denoising öncesinde bir **GaussianBlurFilter** zinciri ekleyin:

```csharp
ocrEngine.Filters.Add(new GaussianBlurFilter { Sigma = 0.8 });
ocrEngine.Filters.Add(new DenoiseFilter());
```

Bu ayarlamalar, biraz keskinliği temiz bir ikili görüntüye değiştirir ve genellikle OCR güven skorunu %5‑10 artırır.

---

## Görüntüden Metin Tanıma – Son İşlem İpuçları

`ocrEngine.Text` elde ettikten sonra şunları yapmak isteyebilirsiniz:

- **Boşlukları kırpma** – `ocrEngine.Text = ocrEngine.Text.Trim();`  
- **Satır sonlarını normalleştirme** – `ocrEngine.Text = ocrEngine.Text.Replace("\r\n", "\n");`  
- **Yazım denetimi çalıştırma** `System.Globalization` veya kaynak dil İngilizce değilse üçüncü taraf bir kütüphane kullanarak.

Bu adımlar, çıkarılan dizeyi arama indeksine ya da veri girişi formuna beslemek gibi sonraki işlemler için hazır hâle getirir.

---

## Kenar Durumları & Yaygın Tuzaklar

| Durum | Dikkat Edilmesi Gereken | Önerilen Çözüm |
|-----------|-------------------|---------------|
| Görüntü 10°'den fazla döndürülmüş | `DeskewFilter` varsayılan sınırda durur | Özel bir maksimum açı geçirin: `new DeskewFilter { MaxAngle = 15 }` |
| Çok koyu arka plan | Filtreler arka planı metin olarak yorumlayabilir | `InvertColorsFilter` ekleyin veya kontrastı artırın |
| Çok sayfalı PDF | `OcrEngine` bir seferde tek bir görüntü üzerinde çalışır | Her sayfayı döngüyle işleyin, her yinelemede yeni bir `OcrEngine` oluşturun |
| Latin dışı betik | Varsayılan dil İngilizcedir | `ocrEngine.Language = OcrLanguage.Thai;` olarak ayarlayın (veya desteklenen herhangi bir dil). |

---

## Tam Çalışan Örnek

Aşağıdaki kodu yeni bir konsol projesine (`dotnet new console -n OcrDemo`) kopyalayın. Aspose OCR paketini geri yükleyin, `YOUR_DIRECTORY/skewed.png` ifadesini test görüntünüzün yolu ile değiştirin ve çalıştırın.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;
using System;

class Preprocess
{
    static void Main()
    {
        // Initialize OCR engine
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // Load the image that may be slightly rotated
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/skewed.png");

            // Add preprocessing filters
            //   - DeskewFilter corrects small rotation
            //   - DenoiseFilter removes salt‑and‑pepper noise
            ocrEngine.Filters.Add(new DeskewFilter());
            ocrEngine.Filters.Add(new DenoiseFilter());

            // Perform OCR recognition
            if (ocrEngine.Recognize())
            {
                // Output the cleaned text
                Console.WriteLine("Cleaned text:\n" + ocrEngine.Text);
            }
            else
            {
                Console.Error.WriteLine("Recognition failed – verify the image and filters.");
            }
        }
    }
}
```

Bu programı çalıştırmak, temizlenmiş ve düzeltilmiş metni konsola yazdırır. Bu, **görüntüyü nasıl düzeltir** iş akışının 50 satırdan az kodla tamamlanmış halidir.

---

## Sonuç

Az önce Aspose OCR ile **görüntüyü nasıl düzeltir** konusunu ele aldık, **gürültüyü nasıl kaldırır** gösterdik, **doğru görüntü dönüşümünü** açıkladık ve **görüntüden metni tanıma** için güvenilir bir yöntem gösterdik. `DeskewFilter` ve `DenoiseFilter` zincirleyerek OCR motorunun yüksek güvenle okuyabileceği net, düz bir bitmap elde edersiniz.

Bundan sonra şunları keşfedebilirsiniz:

- Yüzlerce taramayı paralel olarak toplu işleme.  
- OCR sonucunu arşivleme için PDF/A'ya dışa aktarma.  
- Çok dilli belgeler için dil algılamayı entegre etme.

Bu fikirleri deneyin ve filtre parametrelerini özel taramalarınıza göre ayarlamaktan çekinmeyin. Kodlamanın tadını çıkarın, ve görüntüleriniz her zaman mükemmel düz olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}