---
category: general
date: 2026-05-21
description: Aspose OCR kullanarak aranabilir PDF oluşturun, OCR doğruluğunu artırırken
  C#'ta OCR için resmi nasıl yükleyeceğinizi öğrenin. Adım adım öğretici.
draft: false
keywords:
- create searchable PDF
- improve OCR accuracy
- load image for OCR
- Aspose OCR C#
- PDF output with OCR
language: tr
og_description: Aspose OCR ile aranabilir PDF oluşturun. OCR doğruluğunu artırmayı
  ve OCR için görüntüyü tek bir çalıştırılabilir örnekte nasıl yükleyeceğinizi öğrenin.
og_title: Aspose OCR ile Aranabilir PDF Oluşturma – Tam Rehber
schemas:
- author: Aspose
  dateModified: '2026-05-21'
  description: Create searchable PDF using Aspose OCR while you improve OCR accuracy
    and learn how to load image for OCR in C#. Step‑by‑step tutorial.
  headline: Create Searchable PDF with Aspose OCR – Complete Programming Guide
  type: TechArticle
tags:
- OCR
- Aspose
- PDF
- C#
title: Aspose OCR ile Aranabilir PDF Oluşturma – Tam Programlama Rehberi
url: /tr/net/ocr-optimization/create-searchable-pdf-with-aspose-ocr-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR ile Aranabilir PDF Oluşturma – Tam Programlama Rehberi

Tarama görüntüsünden **searchable PDF** oluşturmanız gerektiğinde nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—birçok geliştirici OCR projelerine ilk kez başladıklarında bu engelle karşılaşıyor. İyi haber şu ki Aspose OCR, tüm süreci—görüntüyü yükleme, daha iyi sonuçlar için resmi iyileştirme ve sonunda aranabilir bir PDF kaydetme—oldukça basit hale getiriyor.

Bu rehberde, sadece **searchable PDF** oluşturmayı göstermekle kalmayıp, aynı zamanda **improve OCR accuracy** ve **load image for OCR** doğru şekilde nasıl yapılacağını gösteren tam bir uçtan‑uca örnek üzerinden ilerleyeceğiz. Sonunda, orijinal görüntüyü gömülü bir şekilde searchable PDF üreten, çalıştırmaya hazır bir C# konsol uygulamanız olacak.

## Öğrenecekleriniz

- Aspose OCR kurulumunu yapmak (isteğe bağlı GPU hızlandırması dahil)  
- Motoru Fransızca (veya herhangi bir dil) için yapılandırarak **improve OCR accuracy**  
- `ImageStream` kullanarak **load image for OCR** doğru şekilde  
- Tanıma öncesinde görüntüyü temizlemek için bir filtre ardışık düzeni oluşturma  
- Kaynak görüntüyü gömülü şekilde searchable PDF olarak sonucu kaydetme  

Aspose OCR dışındaki harici bağımlılıklar gerekmez ve kod .NET 6+ (veya .NET Framework 4.6+) üzerinde çalışır. Hadi başlayalım.

---

![Aspose OCR tarafından oluşturulan örnek searchable PDF – searchable PDF örneği](images/searchable-pdf-sample.png "searchable PDF örneği")

## Adım 1: Searchable PDF Oluşturma – GPU’yu Etkinleştir ve Kaynak Yolunu Ayarla  

Uyumlu bir GPU’nuz varsa, onu etkinleştirmek tanıma süresini önemli ölçüde hızlandırabilir. Bunu atlasanız bile, kodun geri kalanı sorunsuz çalışır.

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// Enable GPU acceleration (optional)
OcrEngine.EnableGpu(true);

// Tell Aspose where to find language data files (offline mode)
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");
```

**Neden önemli:** GPU hızlandırması büyük toplularda gecikmeyi azaltır ve kaynak yolunu ayarlamak motorun internet bağlantısı olmadan çalışmasını sağlar—CI boru hatları veya hava boşluğu ortamları için mükemmeldir.

> **Pro tip:** Başsız bir sunucuda çalışıyorsanız, CUDA sürücülerinin Aspose OCR ile birlikte gelen sürümle eşleştiğini doğrulayın; uyumsuz sürümler sessiz hatalara neden olabilir.

## Adım 2: OCR Doğruluğunu Artırma – Doğru Dili Seçin  

Doğru dil modelini seçmek doğruluk açısından hızlı bir kazançtır. Burada Fransızca’yı seçiyoruz, ancak `OcrLanguage.French` ifadesini desteklenen herhangi bir dil ile değiştirebilirsiniz.

```csharp
var ocrEngine = new OcrEngine
{
    Language = OcrLanguage.French   // improves OCR accuracy for French documents
};
```

**Neden önemli:** Dil‑özgü sözlükler motorun belirsiz karakterleri (ör. “œ” vs “oe”) çözmesine yardımcı olur. Bu adımı atladığınızda motor varsayılan olarak İngilizceyi kullanır ve bu, İngilizce dışı metinlerde **improve OCR accuracy**'yi büyük ölçüde düşürebilir.

## Adım 3: OCR için Görüntüyü Yükleme – ImageStream Kullanımı  

Şimdi **load image for OCR** yapıyoruz. `ImageStream.FromFile` yardımcı sınıfı ham bitmap işleme sürecini soyutlar ve çoğu yaygın formatla (JPG, PNG, TIFF) çalışır.

```csharp
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");
```

**Neden önemli:** Görüntüyü bu şekilde yüklemek, Aspose’un resmi verimli bir biçimde işleyebileceği formatta almasını garanti eder. Ham bir `Bitmap` doğrudan beslemeye çalışırsanız, büyük dosyalarda bellek yönetimi sorunlarıyla karşılaşabilirsiniz.

## Adım 4: Doğruluğu Artırmak İçin Görüntü‑Filtre Ardışık Düzeni Oluşturma  

Temiz bir görüntü savaşın yarısıdır. Aşağıdaki ardışık düzen resmi eğriltir ve arka plan gürültüsünü kaldırır—**improve OCR accuracy**'yi sabote eden iki klasik suçlu.

```csharp
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());   // corrects rotation
filterPipeline.Add(new DenoiseFilter()); // reduces grainy artifacts

// Apply the pipeline and replace the original image
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);
```

**Neden önemli:** Eğrilik düzeltme, metin satırlarının yatay olmasını sağlar, gürültü azaltma ise yanlış karakter lekelerini azaltır. Kaynak taramalarınız özellikle kötü ise daha fazla filtre (ör. `ContrastFilter`) ekleyebilirsiniz.

## Adım 5: OCR Tanıma Gerçekleştirme  

Görüntü ön‑işlemden geçirildikten sonra, motorun sihrini çalıştırıyoruz.

```csharp
ocrEngine.Recognize();
```

Bu tek satır, Aspose OCR’nin arkasındaki derin öğrenme modelini tetikler. `ocrEngine.Text` alanını düz metinle doldurur ve PDF çıktısını da hazırlar.

> **Metin bozuk çıkarsa ne yapmalı?** Adım 2’deki dil ayarını tekrar kontrol edin ve ardışık düzene bir `BinarizeFilter` eklemeyi düşünün.

## Adım 6: Sonucu Searchable PDF Olarak Kaydet  

Son adım, çıkarılan metnin orijinal görüntünün arkasında yer aldığı bir **searchable PDF** kaydetmektir—bu, yasal belgeler veya arşivleme amaçları için tam ihtiyacınız olan şeydir.

```csharp
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });
```

**Neden önemli:** `EmbedOriginalImage = true` taramanın görsel bütünlüğünü korur ve aynı zamanda metin aramasına izin verir. `false` olarak ayarlarsanız, PDF sadece çıkarılan metni içerir; bu, hafif arşivler için faydalı olabilir.

### Opsiyonel: Tanınan Metni ve JSON’u Yazdır  

Ham çıktıyı incelemek istiyorsanız, bu satırlar düz metni ve yapılandırılmış bir JSON yükünü döker.

```csharp
Console.WriteLine(ocrEngine.Text);               // plain text
Console.WriteLine(ocrEngine.GetResultAsJson());  // JSON with layout info
```

**Beklenen çıktı:** Programı çalıştırdıktan sonra, konsolda Fransızca cümle(ler)i göreceksiniz, ardından sınırlama kutuları, güven puanları ve dil meta verilerini içeren bir JSON nesnesi gelecektir.

## Tam Çalışan Örnek (Kopyala‑Yapıştır Hazır)

```csharp
using Aspose.OCR;
using Aspose.OCR.Gpu;          // optional GPU support
using Aspose.OCR.Pdf;          // PDF output
using Aspose.OCR.Filters;     // pre‑processing filters

// 1️⃣ Enable GPU (optional) and set resources path
OcrEngine.EnableGpu(true);
OcrEngine.SetResourcesPath(@"YOUR_DIRECTORY/Resources");

// 2️⃣ Create and configure the OCR engine (improve OCR accuracy)
var ocrEngine = new OcrEngine { Language = OcrLanguage.French };

// 3️⃣ Load the source image (load image for OCR)
ocrEngine.Image = ImageStream.FromFile(@"YOUR_DIRECTORY/input.jpg");

// 4️⃣ Build filter pipeline (deskew + denoise)
var filterPipeline = new ImageFilterPipeline();
filterPipeline.Add(new DeskewFilter());
filterPipeline.Add(new DenoiseFilter());
ocrEngine.Image = filterPipeline.Apply(ocrEngine.Image);

// 5️⃣ Recognize text
ocrEngine.Recognize();

// 6️⃣ Save as searchable PDF (create searchable PDF)
ocrEngine.Save(@"YOUR_DIRECTORY/output.pdf",
    new PdfSaveOptions { EmbedOriginalImage = true });

// Optional: output text and JSON
Console.WriteLine(ocrEngine.Text);
Console.WriteLine(ocrEngine.GetResultAsJson());
```

Programı çalıştırın, `YOUR_DIRECTORY` değişkenini `input.jpg` ve Aspose OCR kaynaklarını içeren bir klasöre yönlendirin ve yanına `output.pdf` oluşturulmuş olarak elde edeceksiniz.

## Sonuç

Artık Aspose OCR ile **searchable PDF** dosyaları oluşturmak için sağlam, üretim‑hazır bir tarifiniz var ve aynı zamanda **improve OCR accuracy** ve **load image for OCR** nasıl yapılacağını öğrenmiş oldunuz. Ardışık düzen—GPU (isteğe bağlı) → dil seçimi → görüntü yükleme → filtre zinciri → tanıma → PDF kaydetme—her kritik adımı kapsar, böylece bunu diğer dillere, daha büyük topluluklara veya farklı çıktı formatlarına uyarlayabilirsiniz.

Sırada ne var? `PdfSaveOptions` yerine `DocxSaveOptions` kullanarak aranabilir Word belgeleri oluşturmayı deneyin, `ContrastFilter` gibi ek filtrelerle denemeler yapın veya bu kodu bir ASP.NET Core API’ye entegre ederek anlık PDF üretimi sağlayın. Olasılıklar sınırsızdır ve burada atılan temel sayesinde herhangi bir OCR‑ile ilgili zorluğun üstesinden gelmeye tamamen hazırsınız.

Sorularınız mı var ya da bir sorunla mı karşılaştınız? Yorum bırakın, iyi kodlamalar!

## İlgili Eğitimler

- [Aspose.OCR ile .NET’te PDF OCR Nasıl Yapılır](/ocr/english/net/text-recognition/recognize-pdf/)
- [Aspose.OCR for .NET ile görüntüden tablo nasıl çıkarılır](/ocr/english/net/text-recognition/recognize-table/)
- [Aspose.OCR ile Dil Kullanarak Görüntü Metni OCR Nasıl Yapılır](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}