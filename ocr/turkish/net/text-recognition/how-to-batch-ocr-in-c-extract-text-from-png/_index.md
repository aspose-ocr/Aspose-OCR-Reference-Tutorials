---
category: general
date: 2026-03-26
description: C#'ta toplu OCR nasıl yapılır, PNG dosyalarından metin çıkarmayı kolaylaştırır.
  Aspose OCR ile toplu metin çıkarımı için bu adım adım C# OCR öğreticisini izleyin.
draft: false
keywords:
- how to batch OCR
- extract text from png
- c# ocr tutorial
- how to create OCR
- batch text extraction
language: tr
og_description: C#'ta toplu OCR nasıl yapılır, PNG dosyalarından hızlıca metin çıkarmanızı
  sağlar. Bu rehber, toplu metin çıkarma ile tam bir C# OCR öğreticisi sunar.
og_title: C#'ta toplu OCR nasıl yapılır – PNG'den metin çıkarma
tags:
- OCR
- C#
- Aspose
title: C#'ta toplu OCR nasıl yapılır – PNG'den metin çıkarma
url: /tr/net/text-recognition/how-to-batch-ocr-in-c-extract-text-from-png/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#'ta toplu OCR nasıl yapılır – PNG'den metin çıkarma

Hiç **toplu OCR nasıl yapılır** diye bir ekran görüntüsü yığınına ayrı ayrı program yazmadan metin çıkarmayı düşündünüz mü? Yalnız değilsiniz. Birçok projede, metinlerinin toplanması gereken onlarca PNG dosyasıyla karşılaşıyoruz ve bunları tek tek işlemek can sıkıcı.

İyi haber? Aspose OCR ile tüm bu görüntüleri paralel olarak işleyen küçük bir C# konsol uygulaması oluşturabilirsiniz; bu da size hızlı **batch text extraction** ve temiz bir sonuç kümesi sunar. Bu rehberde tam bir **c# ocr tutorial** üzerinden geçecek, her parçanın neden önemli olduğunu açıklayacak ve çıktının tam olarak nasıl göründüğünü göstereceğiz.

Bu makalenin sonunda şunları yapabilecek duruma geleceksiniz:

* PNG dosyalarının (veya desteklenen herhangi bir görüntünün) listesini tek seferde yüklemek.  
* Paylaşılan bir `OcrEngine` yapılandırarak ayarların toplu işlem boyunca tutarlı kalmasını sağlamak.  
* Kuyruğu en fazla dört paralel çalışanla çalıştırmak.  
* Her sayfa için tanınan metni alıp konsola yazdırmak.

Sihir yok, sadece bugün çözümünüze ekleyebileceğiniz sağlam bir kod.

## Gereksinimler

Başlamadan önce şunların olduğundan emin olun:

* .NET 6 SDK (veya daha yeni bir .NET sürümü).  
* Geçerli bir Aspose OCR lisansı ya da geçici bir değerlendirme anahtarı.  
* İşlemek istediğiniz PNG dosyalarını içeren bir klasör.  
* Visual Studio 2022 ya da tercih ettiğiniz editör.

Hepsi bu—`Aspose.OCR` ve standart `System.Collections.Generic` dışındaki ekstra NuGet paketine gerek yok.

## Toplu OCR Nasıl Yapılır – Projeyi Kurma

İlk olarak yeni bir konsol projesi oluşturun ve Aspose OCR kütüphanesini ekleyin.

```bash
dotnet new console -n BatchOcrDemo
cd BatchOcrDemo
dotnet add package Aspose.OCR
```

Geri yükleme tamamlandıktan sonra **Program.cs** dosyasını (veya yeni bir dosya) açın ve gerekli `using` yönergelerini ekleyin:

```csharp
using System;
using System.Collections.Generic;
using Aspose.OCR;
```

Bu basit iskelet, daha sonra ihtiyaç duyacağımız `OcrEngine`, `RecognitionQueue` ve yardımcı sınıflara erişim sağlar.

## PNG'den Metin Çıkarma – Görüntü Listesini Hazırlama

Şimdi programa **hangi PNG'leri** OCR'dan geçireceğimizi söylememiz gerekiyor. En basit yol, mutlak ya da göreli yolları tutan bir `List<string>` oluşturmaktır.

```csharp
// Step 1: Define the image files to be processed
var imagePaths = new List<string>
{
    @"YOUR_DIRECTORY/page1.png",
    @"YOUR_DIRECTORY/page2.png",
    @"YOUR_DIRECTORY/page3.png",
    @"YOUR_DIRECTORY/page4.png"
};
```

`YOUR_DIRECTORY` kısmını gerçek klasör yolu ile değiştirin. Dinamik bir kümeniz varsa, `Directory.GetFiles(@"YOUR_DIRECTORY", "*.png")` kullanıp sonucu listeye ekleyebilirsiniz. Önemli nokta, **extract text from PNG** işleminin sadece doğru dosya adlarını kuyruğa beslemek olduğudur.

![Toplu OCR iş akışı](https://example.com/placeholder.png "PNG dosyaları koleksiyonunda toplu OCR'un nasıl yapılacağını gösteren diyagram")

*Görsel alt metni: toplu OCR iş akışı diyagramı*

## C# OCR öğreticisi – Tanıma kuyruğunu yapılandırma

Toplu işlemin kalbi `RecognitionQueue`'dur. Bunu, her görüntüyü paylaşılan bir `OcrEngine`'e teslim eden bir taşıma bandı gibi düşünün. Motoru paylaşarak bellek kullanımını düşük tutar ve her sayfa için aynı ayarların uygulanmasını garantiler.

```csharp
// Step 2: Create a recognition queue with shared OCR engine and parallelism
var recognitionQueue = new RecognitionQueue
{
    MaxDegreeOfParallelism = 4,          // run up to 4 images at the same time
    Engine = new OcrEngine()            // shared configuration for all images
};
```

`MaxDegreeOfParallelism` değerini 4 olarak ayarlamamızın nedeni nedir? Tipik bir dört çekirdekli dizüstü bilgisayarda bu, işletim sistemini zorlamadan en iyi verimi verir. Daha fazla çekirdeğe sahip bir sunucuda çalışıyorsanız, sayıyı buna göre artırabilirsiniz.

### Pro ipucu

Özel dil paketlerine, DPI ayarlarına ya da ilgi bölgesi kırpmasına ihtiyacınız varsa, görüntüleri kuyruğa eklemeden **bir kez** paylaşılan `Engine` üzerinde ayarlayın. Örneğin:

```csharp
recognitionQueue.Engine.Language = Language.English;
recognitionQueue.Engine.Dpi = 300;
```

Sonraki tüm tanıma işlemleri bu seçenekleri otomatik olarak devralır—bu, **how to create OCR** hatları tutarlı kalmasını sağlayan özettir.

## Toplu Metin Çıkarma – Görüntüleri Kuyruğa Eklemek ve Kuyruğu Çalıştırmak

Kuyruk hazır olduğunda, bir sonraki adım her görüntüyü kuyruğa itmek olur. `Enqueue` metodu bir `OcrImage` örneği alır; bu örneği dosya yolundan oluştururuz.

```csharp
// Step 3: Enqueue each image for OCR processing
foreach (var path in imagePaths)
    recognitionQueue.Enqueue(OcrImage.FromFile(path));
```

Tüm dosyalar kuyruğa alındıktan sonra işleme başlarız:

```csharp
// Step 4: Run the queue and collect OCR results
List<OcrResult> ocrResults = recognitionQueue.ExecuteAll();
```

`ExecuteAll` her görüntü bitene kadar bloklanır, ardından her öğenin giriş sırasına karşılık geldiği bir liste döndürür. Bu, sayfa 1 sonucunun indeks 0, sayfa 2 sonucunun indeks 1 vb. olmasını garantiler—sonuçları kaynak dosyalarla eşleştirmeniz gerektiğinde çok kullanışlıdır.

## OCR Nasıl Oluşturulur – Sonuçları Görüntüleme

Son olarak, tanınan metni konsola yazdıralım. İşte **batch text extraction**'ın gerçek anlamda çalıştığını göreceğiniz yer.

```csharp
// Step 5: Output the recognized text for each page
for (int i = 0; i < ocrResults.Count; i++)
{
    Console.WriteLine($"--- Page {i + 1} ---");
    Console.WriteLine(ocrResults[i].Text);
}
```

Programı çalıştırdığınızda (`dotnet run`) aşağıdakine benzer bir çıktı görmelisiniz:

```
--- Page 1 ---
Welcome to the quarterly report.
--- Page 2 ---
Revenue increased by 12% YoY.
--- Page 3 ---
All figures are provisional.
--- Page 4 ---
Contact finance@example.com for details.
```

Bir görüntü başarısız olursa (ör. bozuk dosya), ilgili `OcrResult` boş bir `Text` özelliğine sahip olur ve tanılayıcılar için `ocrResults[i].Exception` değerini inceleyebilirsiniz.

## OCR Nasıl Oluşturulur – İpuçları, Kenar Durumları ve En İyi Uygulamalar

### Büyük topluları işleme

Yüzlerce PNG'yi işlemek, tüm `OcrResult` nesnelerini bellekte tutarsanız hâlâ bellek tüketebilir. Bu gibi durumlarda, her sonuç geldiğinde çıktıyı bir dosyaya ya da veritabanına akıtın:

```csharp
recognitionQueue.OnResultReady += (sender, args) =>
{
    File.AppendAllText("OcrOutput.txt",
        $"--- {args.Image.Path} ---{Environment.NewLine}{args.Result.Text}{Environment.NewLine}");
};
```

### PNG dışı formatlarla başa çıkma

Aspose OCR JPEG, BMP ve TIFF formatlarını da kutudan çıkar çıkmaz destekler. Listedeki dosya uzantısını değiştirin ya da joker karakter araması yapın. Aynı **c# ocr tutorial** adımları geçerlidir—kodda değişiklik yapmanıza gerek yok.

### Boş sayfaları atlama

Bazen boş sayfalar içeren taranmış PDF'leriniz varsa, sonuçları şu şekilde filtreleyebilirsiniz:

```csharp
if (!string.IsNullOrWhiteSpace(result.Text))
    // process non‑empty text
```

### Lisans hususları

Değerlendirme sürümü her sayfaya bir filigran ekler. Üretim ortamında, `Main` metodunun başında lisans dosyanızı gömmeniz gerekir:

```csharp
License lic = new License();
lic.SetLicense("Aspose.OCR.lic");
```

### Paralellik ayarı

`MaxDegreeOfParallelism` varsayılan olarak `Environment.ProcessorCount` değerindedir. CPU kullanımı ya da bellek baskısı yüksekse değeri düşürün. Tam tersine, çok çekirdekli bir bulut VM'inde değeri artırarak donanımı tam olarak değerlendirin.

## Özet

Artık C#'ta **how to batch OCR** çözümüne sahipsiniz; **extract text from PNG** dosyalarını paralel olarak işleyebilir, temiz ve sıralı sonuçlar elde edebilirsiniz. Tek bir `OcrEngine` paylaşarak **how to create OCR** hatlarını hem bellek açısından verimli hem de bakım kolaylığı sağlayacak şekilde oluşturmayı öğrendiniz. Bu **c# ocr tutorial** aynı zamanda **batch text extraction**'ı yüzlerce görüntüye ölçeklendirmek için sadece birkaç ek satırla nasıl yapılacağını gösteriyor.

---

### Sırada ne var?

* Dil algılamayı ekleyin (`Engine.Language = Language.AutoDetect`).  
* Çıktı formatlarıyla deney yapın—sonuçları JSON ya da CSV olarak yazarak sonraki analizlere hazırlayın.  
* Bu toplu OCR'ı bir PDF‑to‑image dönüşüm adımıyla birleştirerek tam taranmış belgeleri işleyin.

Paralelliği ayarlamaktan, kendi görüntü kaynaklarınızı eklemekten ya da sonuçları bir arama indeksine bağlamaktan çekinmeyin. **how to batch OCR** konusunda uzmanlaştığınızda sınır yok.

İyi kodlamalar, OCR işlemleriniz hızlı ve hatasız olsun!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}