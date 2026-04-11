---
category: general
date: 2026-04-11
description: Aspose OCR kullanarak JPG'den metin tanıma, görüntüleri düzleştirme ve
  gürültüyü kaldırma yoluyla C#'ta OCR'ı nasıl geliştireceğinizi öğrenin.
draft: false
keywords:
- how to improve OCR
- recognize text from jpg
- extract text from image
- how to deskew image
- how to remove noise
language: tr
og_description: JPG'den metin tanıma, görüntüleri düzleştirme ve gürültüyü kaldırma
  ile OCR'yi nasıl geliştireceğinizi keşfedin—tam C# rehberi.
og_title: C#'de Aspose OCR ile OCR Doğruluğunu Nasıl Artırabilirsiniz
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C#'ta Aspose OCR ile OCR Doğruluğunu Nasıl Artırabilirsiniz
url: /tr/net/ocr-optimization/how-to-improve-ocr-accuracy-in-c-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# ile Aspose OCR'da OCR Doğruluğunu Nasıl Artırabilirsiniz

Hiç **OCR'ı nasıl geliştirebileceğinizi** merak ettiniz mi, taramalarınız okunabilir metinden çok soyut bir sanat eserine benziyorsa? Tek başınıza değilsiniz. Gerçek dünyadaki birçok projede—faturalar, makbuzlar veya el yazısı notlar gibi—kaynak görüntüler genellikle eğik, grenli ya da gürültülü olur. İyi haber? Aspose OCR, bu karmaşayı temiz, makine‑okunur karakterlere dönüştürebilecek bir dizi ön‑işleme ayarı sunar. Bu öğreticide, **OCR'ı nasıl geliştirebileceğinizi** **JPG'den metin tanıma**, görüntüyü düzeltme ve istenmeyen gürültüyü temizleme yoluyla gösteren eksiksiz, çalıştırılabilir bir örnek üzerinden ilerleyeceğiz.

> *İpucu:* Ön‑işlemeyi atlayırsanız, muhtemelen şifreli bir bulmaca gibi karışık bir çıktı alırsınız. Bunu önleyelim.

![How to improve OCR with Aspose OCR preprocessing](https://example.com/ocr-preprocess.png "how to improve OCR with Aspose OCR")

## Öğrenecekleriniz

1. Aspose OCR motorunu en yüksek doğruluk için nasıl yapılandıracağınızı.  
2. **JPG'den metin tanıma** için gereken tam kodu.  
3. *AutoDeskew* ve *RemoveNoise*'ı etkinleştirmenin neden önemli olduğunu ve nasıl ayarlayacağınızı.  
4. **Görüntüden metin çıkarma** işlemini özel bir filtre yazmadan nasıl yapacağınızı.  
5. Yaygın tuzaklar (eksik dosya, desteklenmeyen format) ve hızlı çözümler.

Sonunda, herhangi bir JPG'yi alıp temizleyebilen ve çıkarılan dizeyi çıktıya veren tek bir C# konsol uygulamanız olacak—sonraki işlem veya depolama için hazır.

## Önkoşullar

- .NET 6.0 SDK veya daha yenisi (örnek, kısalık için üst‑seviye ifadeler kullanıyor).  
- Aspose.OCR NuGet paketi (`dotnet add package Aspose.OCR`).  
- `input.jpg` adlı örnek bir JPG görüntüsü, çalıştırılabilir dosyayla aynı klasöre yerleştirilmiş.  
- C#'a temel aşinalık—ileri kavramlar gerekmez.

Eğer zaten bir projeniz varsa, sadece kodu yapıştırın; aksi takdirde yeni bir konsol uygulaması oluşturun:

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

Şimdi koda dalalım.

## OCR'ı Nasıl Geliştirirsiniz: Ön‑İşleme Ayarları Genel Bakışı

**OCR'ı nasıl geliştireceğiniz**'in kalbi `PreprocessSettings` nesnesinde yatar. Bunu, gerçek karakter tanıma motoru çalışmadan önce çalışan mini bir görüntü düzenleyici olarak düşünün. Aşağıda en etkili bayrakların hızlı bir özeti yer alıyor:

| Setting                | Ne işe yarar                                            | Tipik kullanım durumu |
|------------------------|---------------------------------------------------------|-----------------------|
| `AutoDeskew`           | Derin öğrenme tabanlı bir eğikliği düzeltme algoritması uygular. | Hafif eğik taranmış sayfalar. |
| `AdaptiveThreshold`    | Düşük ışıklı veya soluk görüntülerde kontrastı artırır. | Solmuş mürekkebi olan eski makbuzlar. |
| `RemoveNoise`          | Çizikleri bastırmak için Gaussian bulanıklaştırma filtresi uygular. | Akıllı telefon flaşıyla çekilmiş fotoğraflar. |
| `NoiseRemovalStrength`| Saldırganlığı kontrol eder (1 = düşük, 3 = yüksek).   | Kaynağın ne kadar grenli olduğuna göre ince ayar. |

Bu seçenekleri etkinleştirmek, kusurlu girdilerde **OCR'ı nasıl geliştireceğiniz** için temelde “gizli sos”tur.

## Aspose OCR ile JPG'den Metin Tanıma

Aşağıda tam, çalıştırılabilir program yer alıyor. Her satır açıklamalı, böylece sadece *ne* yaptığını değil, *neden* olduğunu da görebilirsiniz.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class PreprocessDemo
{
    static void Main()
    {
        // ------------------------------------------------------------
        // Step 1: Create an OCR engine instance.
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();

        // ------------------------------------------------------------
        // Step 2: Fine‑tune preprocessing to improve accuracy.
        // ------------------------------------------------------------
        ocrEngine.Settings.Preprocess = new PreprocessSettings
        {
            AutoDeskew = true,               // How to deskew image automatically.
            AdaptiveThreshold = true,        // Improves contrast for better recognition.
            RemoveNoise = true,              // How to remove noise before OCR.
            NoiseRemovalStrength = 2         // Medium strength; adjust 1‑3 as needed.
        };

        // ------------------------------------------------------------
        // Step 3: Load the JPG image you want to process.
        // ------------------------------------------------------------
        // If the file is missing, Aspose will throw a FileNotFoundException.
        // Wrap it in a try/catch if you need graceful fallback.
        ImageStream image;
        try
        {
            image = ImageStream.FromFile("input.jpg");
        }
        catch (Exception ex)
        {
            Console.WriteLine($"Error loading image: {ex.Message}");
            return;
        }

        // ------------------------------------------------------------
        // Step 4: Run the OCR engine on the preprocessed image.
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // ------------------------------------------------------------
        // Step 5: Display the extracted text.
        // ------------------------------------------------------------
        Console.WriteLine("=== Extracted Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

### Beklenen Çıktı

Eğer `input.jpg` içinde “Invoice #12345 – Total: $256.78” ifadesi varsa, konsol şu çıktıyı verir:

```
=== Extracted Text ===
Invoice #12345 – Total: $256.78
```

Gördüğünüz gibi çıktı temiz, tire ve dolar işareti korunmuş—**görüntüden metin çıkarma** dosyalarında tam da beklediğiniz gibi.

## Ön‑İşleme Ayarlarıyla Görüntüyü Düzeltme (Deskew) Nasıl Yapılır

Deskew (düzeltme) neden önemlidir? 2 derece bile karakter segmentasyon aşamasını şaşırtarak harflerin yanlış tanımlanmasına yol açabilir. `AutoDeskew` bayrağı, altında çalışan bir konvolüsyonel sinir ağı ile baskın açıyı tespit eder ve görüntüyü temel konumuna döndürür.

Daha fazla kontrol gerekiyorsa, açıyı manuel olarak ayarlayabilirsiniz:

```csharp
ocrEngine.Settings.Preprocess = new PreprocessSettings
{
    AutoDeskew = false,          // Turn off automatic detection.
    // Manually specify a rotation angle (in degrees):
    DeskewAngle = -1.8           // Positive = clockwise, negative = counter‑clockwise.
};
```

> **Manuel düzeltme ne zaman kullanılmalı:** Kamera görüntüleri sabit bir miktarda (örneğin, monte bir tarayıcı) eğiyorsa, açıyı kod içinde sabitlemek işlem süresinden ufak bir tasarruf sağlar.

## Daha Temiz Çıkarma İçin Gürültüyü Nasıl Kaldırırsınız

Gürültü, özellikle düşük ışıklı fotoğraflarda rastgele lekeler veya gren olarak ortaya çıkar. `RemoveNoise` bayrağı, kenarları (gerçek karakterleri) korurken arka planı yumuşatan çift yönlü bir filtre uygular. `NoiseRemovalStrength` özelliği, agresifliği ayarlamanıza izin verir:

| Güç | Etki |
|----------|--------|
| 1        | Hafif yumuşatma—hafif grenli fotoğraflar için iyidir. |
| 2        | Dengeli—çoğu akıllı telefon çekimi için uygundur. |
| 3        | Ağır yumuşatma—görüntü çok gürültülü olduğunda kullanın, ancak ince çizgilerin bulanıklaşmasına dikkat edin. |

Eğer ağır yumuşatmadan sonra küçük fontların okunamaz hale geldiği bir durumla karşılaşırsanız, sadece gücü azaltın ya da filtreyi tamamen devre dışı bırakın.

## Görüntüden Metin Çıkarma: JPG'nin Ötesinde

Demo'muz JPG'ye odaklansa da, Aspose OCR PNG, BMP, TIFF ve hatta PDF sayfalarını destekler. JPG dışındaki **görüntüden metin çıkarma** formatları için sadece `ImageStream.FromFile` içindeki dosya uzantısını değiştirin. Çok sayfalı TIFF'lerde her sayfayı döngüyle işleyebilirsiniz:

```csharp
for (int i = 0; i < tiffPageCount; i++)
{
    ImageStream page = ImageStream.FromFile($"input_{i}.tiff");
    OcrResult result = ocrEngine.Recognize(page);
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(result.Text);
}
```

Bu kod parçacığı, aynı **OCR'ı nasıl geliştireceğiniz** iş akışını bir yığın taranmış belgeyi toplu işlemek için nasıl ölçeklendirebileceğinizi gösterir.

## Yaygın Tuzaklar ve Çözüm Yolları

| Belirti | Muhtemel Neden | Hızlı Çözüm |
|---------|----------------|-------------|
| Boş çıktı | Ön‑işlemeden sonra görüntü tamamen beyaz (aşırı agresif eşik) | `NoiseRemovalStrength` değerini azaltın veya `AdaptiveThreshold = false` yapın. |
| Bozuk karakterler | Yanlış dil modeli (varsayılan İngilizce) | `ocrEngine.Settings.Language = Language.English;` ayarlayın veya özel bir dil paketi yükleyin. |
| Büyük dosyalarda çökme | Yüksek çözünürlüklü görüntü nedeniyle bellek yetersizliği | Tanıma öncesinde `ocrEngine.Settings.ImageResizeFactor = 0.5;` ile ölçek küçültün. |
| Döndürülmüş taramalarda çıktı yok | `AutoDeskew` yanlışlıkla devre dışı bırakıldı | `AutoDeskew = true` yapın veya doğru `DeskewAngle` sağlayın. |

Bunları akılda tutmak, üretim hatlarında **OCR'ı nasıl geliştireceğinizi** denediğinizde saatlerce sürecek hata ayıklamayı önleyecektir.

## Bonus: Hız ve Doğruluk İçin Ayarlama

Günde binlerce makbuz işliyorsanız, hızı önceliklendirebilirsiniz. `AdaptiveThreshold`'ı kapatın ve `NoiseRemovalStrength = 1` ayarlayın. Öte yandan, tek bir karakterin eksik olması maliyetli olabilecek yasal belgeler için tüm bayrakları açık tutun ve `NoiseRemovalStrength` değerini 3'e çıkarmayı düşünün.

## Özet

C# ile Aspose OCR kullanarak **OCR'ı nasıl geliştireceğiniz** konusundaki tüm süreci ele aldık: motoru oluşturma, ön‑işlemeyi yapılandırma (*görüntüyü düzeltme* ve *gürültüyü kaldırma*'ın temeli), JPG yükleme, metin tanıma ve kenar durumlarını ele alma. Kod bağımsız, kutudan çıkar çıkmaz çalışır ve **JPG'den metin tanıma** ve **görüntüden metin çıkarma** dosyaları için gerekli adımları gösterir.

### Sıradaki Adımlar

- Diğer görüntü formatları (PNG, TIFF) ile deney yaparak aynı ayarların nasıl davrandığını görün.  
- OCR çıktısını bir veritabanına entegre edin veya

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}