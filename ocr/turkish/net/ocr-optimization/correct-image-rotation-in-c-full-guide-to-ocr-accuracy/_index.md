---
category: general
date: 2026-03-04
description: Aspose OCR kullanarak doğru görüntü döndürme ve görüntü gürültüsünü kaldırarak
  metin görüntüsü çıkarın. OCR doğruluğunu artırmayı ve C#'ta görüntü OCR'sini yüklemeyi
  öğrenin.
draft: false
keywords:
- correct image rotation
- remove image noise
- extract text image
- improve ocr accuracy
- load image ocr
language: tr
og_description: Görüntü döndürmeyi hızlıca düzeltin; görüntü gürültüsünü kaldırın,
  metin görüntüsünü çıkarın ve Aspose OCR ile C#'ta OCR doğruluğunu artırın.
og_title: Doğru Görüntü Döndürme – C#'ta OCR Doğruluğunu Artırın
tags:
- OCR
- C#
- Image Processing
title: C#'ta Doğru Görüntü Döndürme – OCR Doğruluğu İçin Tam Kılavuz
url: /tr/net/ocr-optimization/correct-image-rotation-in-c-full-guide-to-ocr-accuracy/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Doğru Görüntü Döndürme – C#'ta OCR Doğruluğunu Artırın

Tarama belgesinden metin almadan önce **görüntü döndürmeyi düzeltme** gerektiğinde hiç oldu mu? Tek başınıza değilsiniz. Çoğu geliştirici, fotoğraf birkaç derece yanlı olduğunda ya da lekelerle dolu olduğunda bir duvara çarpar ve OCR motoru anlamsız bir şeyler üretir.  

İyi haber? Birkaç C# satırı ve Aspose OCR ile görüntüyü düzleştirebilir, gürültüyü azaltabilir ve sonunda *metin görüntüsü çıkarma* işlemini güvenilir bir şekilde yapabilirsiniz. Bu öğreticide tüm süreci adım adım inceleyeceğiz—*load image OCR*, **görüntü gürültüsünü kaldırma** filtrelerini uygulayacağız ve **OCR doğruluğunu artırma** konusunda temiz, okunabilir bir metin elde edeceğiz.

## Öğrenecekleriniz

- Aspose OCR kütüphanesini nasıl kurup referans göstereceğinizi.  
- Özel bir filtre ardışık düzeninin **görüntü döndürmeyi düzeltme** için neden önemli olduğunu.  
- Tam olarak **load image OCR** yapacak kodu, bir *DeskewFilter* ve *DenoiseFilter* uygulamayı ve `Recognize` çağırmayı.  
- Aşırı eğim veya yoğun gren gibi kenar‑durumları ele almak için ipuçları.  
- Sonucu nasıl doğrulayacağınızı ve ayarları daha iyi **OCR doğruluğunu artırma** için nasıl ayarlayacağınızı.

## Önkoşullar

| Gereksinim | Sebep |
|-------------|--------|
| .NET 6.0 SDK (or later) | Modern dil özellikleri ve daha iyi performans |
| Visual Studio 2022 (or VS Code) | Kolay hata ayıklama ve IntelliSense |
| Aspose.OCR NuGet package | Kullanacağımız OCR motoru |
| A sample image (e.g., `skewed_noisy.png`) | **görüntü döndürmeyi düzeltme** ve **görüntü gürültüsünü kaldırma** göstermek için |

Eğer bunlara zaten sahipseniz, harika—devam edelim.

## Adım 1: Aspose  OCR'yi Kurun

Proje klasörünüzde bir terminal açın ve şu komutu çalıştırın:

```bash
dotnet add package Aspose.OCR
```

Bu, en son kararlı sürümü (Mart 2026 itibarıyla, sürüm 23.12) indirir. Paket, ihtiyacımız olan tüm filtre sınıflarını içerir, bu yüzden ekstra bağımlılık yok.

## Adım 2: OCR Motorunu Başlatın

Bir motor örneği oluşturmak basittir, ancak bunu erken yapmamızın nedenini anlamak faydalıdır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Create an OCR engine instance
            OcrEngine ocrEngine = new OcrEngine();
```

`OcrEngine` merkezi bir hubdır—yükleme, ön‑işleme ve tanıma işlemlerini koordine eden “beyin” gibi düşünün. Bunu bir kez örnekleyip birden çok görüntüde yeniden kullanmak, her çağrıda birkaç milisaniye tasarruf sağlayabilir.

## Adım 3: Özel Bir Filtre Ardışık Düzeni Oluşturun  

İşte sihrin gerçekleştiği yer. Filtreleri zincirleyerek **görüntü döndürmeyi düzeltme**, **görüntü gürültüsünü kaldırma** ve metin kenarlarını keskinleştirmek için resmi *ikiliye dönüştürme* yapabiliriz.

```csharp
            // Step 3: Build a custom filter pipeline to improve recognition
            ocrEngine.Filters = new FilterBuilder()
                .Add(new DeskewFilter { MaxAngle = 5 })                         // correct up‑to‑5° rotation
                .Add(new DenoiseFilter { Strength = DenoiseStrength.Medium }) // remove image noise
                .Add(new BinarizeFilter { Threshold = 127 })                  // convert to black‑and‑white
                .Build();
```

- **DeskewFilter**: Metnin temel çizgisini algılar ve görüntüyü geri döndürür. 5° ile sınırlıyoruz çünkü bu değerin üzerindeki açılarda algoritma metin yönünü yanlış yorumlayabilir.  
- **DenoiseFilter**: Karakterleri bulanıklaştırmadan lekeleri yumuşatan bir medyan filtresi uygular—*OCR doğruluğunu artırma* için kritik.  
- **BinarizeFilter**: Görüntüyü saf siyah‑beyaz hâle getirir; birçok OCR motoru daha hızlı desen eşleştirme için bunu tercih eder.

> **Pro ipucu:** Belgeleriniz 5°'den fazla döndürülebiliyorsa, `MaxAngle` değerini 10 veya 15'e yükseltin, ancak performansı izlemeyi unutmayın.

## Adım 4: OCR İçin Görüntüyü Yükleyin  

Şimdi gerçekten **görüntü OCR yükleme** yapıyoruz. `ImageInfo.Load` yöntemi dosyayı motorun anlayacağı bir formata okur.

```csharp
            // Step 4: Load the image that needs OCR processing
            string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
            var imageInfo = ImageInfo.Load(imagePath);
```

Yolun gerçek bir dosyaya işaret ettiğinden emin olun; aksi takdirde `FileNotFoundException` alırsınız. Bir web API'si oluşturuyorsanız, bir `IFormFile` alabilir ve akışını doğrudan `ImageInfo.Load`'a besleyebilirsiniz.

## Adım 5: Tanıma ve Metin Çıkarma

Filtreler yerinde ve görüntü yüklendiğinde, motoru karakterleri okumaya sonunda istekte bulunuruz.

```csharp
            // Step 5: Perform OCR on the prepared image
            var ocrResult = ocrEngine.Recognize(imageInfo);

            // Step 6: Output the recognized text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

`Recognize` çağrısı, ham metin, güven puanları ve gerekirse daha sonra kullanabileceğiniz sınırlayıcı kutuları içeren bir `OcrResult` nesnesi döndürür. Çoğu kullanım senaryosu için `ocrResult.Text` tek ihtiyacınız olan şeydir.

### Beklenen Çıktı

`skewed_noisy.png` dosyası “Hello, World!” cümlesini içeriyorsa, aşağıdakine benzer bir şey görmelisiniz:

```
=== OCR Output ===
Hello, World!
```

Çıktı bozuk görünüyorsa, `DenoiseStrength` değerini `High` yapmayı veya `BinarizeFilter` içindeki `Threshold` ayarını değiştirmeyi deneyin. Küçük ayarlamalar genellikle belirgin bir **OCR doğruluğunu artırma** artışı sağlar.

## Adım 6: Kenar Durumları ve Olası Senaryolar  

### Aşırı Eğilim (> 5°)

Varsayılan `MaxAngle = 5` çoğu taranmış fiş için çalışır. 12° döndürülmüş taranmış yasal belgeler için şu şekilde ayarlayın:

```csharp
.Add(new DeskewFilter { MaxAngle = 12 })
```

Ancak unutmayın: daha büyük açılar işleme süresini artırır ve metin temel çizgisi düzensizse artefaktlar oluşturabilir.

### Çok Gürültülü Arka Planlar

Görüntü, kötü aydınlatmada çekilmiş bir fotoğraf ise, ikiliye dönüştürmeden sonra ikinci bir `DenoiseFilter` ekleyin:

```csharp
.Add(new DenoiseFilter { Strength = DenoiseStrength.High })
```

### Çok Dilli Belgeler

Aspose OCR dili otomatik algılar, ancak zorlayabilirsiniz:

```csharp
ocrEngine.Language = OcrLanguage.Spanish;
```

Bu, varsayılan algılama zorlandığında **OCR doğruluğunu artırma** daha da sağlayabilir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

Aşağıda, derlenip çalıştırılmaya hazır tam program yer alıyor. `YOUR_DIRECTORY` ifadesini görüntünüzün bulunduğu gerçek klasörle değiştirin.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Filters;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Initialize OCR engine
            OcrEngine ocrEngine = new OcrEngine();

            // Build filter pipeline: correct image rotation, remove image noise, binarize
            ocrEngine.Filters = new FilterBuilder()
                .Add(new DeskewFilter { MaxAngle = 5 })
                .Add(new DenoiseFilter { Strength = DenoiseStrength.Medium })
                .Add(new BinarizeFilter { Threshold = 127 })
                .Build();

            // Load the image you want to OCR
            string imagePath = @"YOUR_DIRECTORY/skewed_noisy.png";
            var imageInfo = ImageInfo.Load(imagePath);

            // Perform OCR
            var ocrResult = ocrEngine.Recognize(imageInfo);

            // Show the extracted text
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

`dotnet run` ile çalıştırın. Konsolda temizlenmiş metnin yazdırıldığını görmelisiniz.

## Sıkça Sorulan Sorular

**S: Bu PDF'lerle çalışır mı?**  
C: Evet. Her PDF sayfasını bir görüntüye dönüştürün (örneğin `Aspose.PDF` kullanarak) ve bitmap'i `ImageInfo.Load`'a besleyin.

**S: Görüntüm zaten tamamen düzse ne olur?**  
C: `DeskewFilter` neredeyse sıfır açı tespit eder ve görüntüyü dokunmadan bırakır—performans kaybı yok.

**S: Bir grup görüntüyü işleyebilir miyim?**  
C: Kesinlikle. Tanıma kodunu bir `foreach` döngüsü içinde sarın; hız için aynı `OcrEngine` örneğini yeniden kullanın.

## Sonuç

Artık **görüntü döndürmeyi düzeltme** ve **görüntü gürültüsünü kaldırma** için sağlam, uçtan uca bir tarifiniz var, bu sayede *metin görüntüsü çıkarma* işlemini güvenle yapabilirsiniz. Özel bir filtre zinciri yapılandırarak sürekli **OCR doğruluğunu artırma** sağlayacak ve tüm *load image OCR* iş akışını sorunsuz hale getireceksiniz.

Sonraki adımlar? Daha yüksek `DenoiseStrength` ile denemeler yapın, farklı ikiliye dönüştürme eşiklerini oynayın veya kodu yüklemeleri kabul eden bir ASP.NET Core uç noktasına entegre edin. Bu ilkeler, faturalar, pasaportlar veya el yazısı notlar işlenirken de aynı şekilde geçerlidir.

Kodlamaktan keyif alın ve OCR sonuçlarınız her zaman kristal gibi net olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}