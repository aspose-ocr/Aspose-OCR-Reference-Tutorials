---
category: general
date: 2026-10-30
description: Java'da Aspose OCR ile görüntüleri ön işleyerek OCR'yi nasıl geliştireceğinizi
  öğrenin. Bu kılavuz, görüntü kontrastını artırmayı, kontrast seviyesini ayarlamayı
  ve metni verimli bir şekilde çıkarmayı gösterir.
draft: false
keywords:
- how to improve OCR
- how to boost contrast
- preprocess image OCR
- extract text image Java
- recognize text image Java
lastmod: 2026-10-30
og_description: Java'da Aspose OCR ile görüntüleri ön işleyerek OCR'yi nasıl geliştireceğinizi
  öğrenin. Kılavuz, kontrastı artırmayı, kontrast seviyesini ayarlamayı ve metni hızlı
  bir şekilde çıkarmayı açıklar.
og_image_alt: Screenshot of a Java OCR preprocessing pipeline showing before‑and‑after
  contrast enhancement
og_title: OCR'yi Nasıl Geliştirirsiniz – Java Görüntü Ön İşleme Kılavuzu
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  headline: How to improve OCR – preprocess image for OCR in Java with Aspose
  type: TechArticle
- description: Learn how to improve OCR by preprocessing images in Java with Aspose
    OCR. This guide shows how to boost image contrast, set contrast level, and extract
    text efficiently.
  name: How to improve OCR – preprocess image for OCR in Java with Aspose
  steps:
  - name: '**Deskew** – corrects slight rotations.'
    text: '**Deskew** – corrects slight rotations.'
  - name: '**Denoise** – removes speckles that confuse character segmentation.'
    text: '**Denoise** – removes speckles that confuse character segmentation.'
  - name: '**Contrast enhancement** – makes dark text stand out against the background.'
    text: '**Contrast enhancement** – makes dark text stand out against the background.'
  type: HowTo
- questions:
  - answer: Yes—load the appropriate language pack with `engine.setLanguage("fr")`
      or any supported ISO code to improve accuracy for non‑English text.
    question: Can I use this approach for languages other than English?
  - answer: It does not read PDF pages natively; you should extract images from the
      PDF first (e.g., with Aspose PDF) and then feed them to the OCR engine.
    question: Does Aspose OCR support PDF input directly?
  - answer: The library handles images up to 30 MP without needing to load the whole
      file into memory, thanks to its streaming architecture.
    question: How large an image can I process?
  - answer: Absolutely—iterate over the files, reuse the same `OcrEngine` instance,
      and add each file to `OcrInput`. This reduces per‑image overhead dramatically.
    question: Is there a way to batch‑process a folder of images?
  - answer: Try adjusting `setContrastLevel` in smaller increments, experiment with
      `setDenoiseMode`, or enable `setUseAdaptiveThreshold(true)` for difficult backgrounds.
    question: What if the OCR output still contains errors?
  type: FAQPage
tags:
- Java
- OCR
- Image Processing
title: OCR'yi Nasıl Geliştirirsiniz – Java'da Aspose ile OCR için Görüntü Ön İşleme
url: /tr/java/advanced-ocr-techniques/preprocess-image-for-ocr-complete-java-guide-to-boost-contra/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüyü OCR için Ön İşleme – Tam Java Rehberi

Hiç **görüntüyü OCR için ön işleme** yapmanız gerekti ama hangi ayarların gerçekten fark yarattığından emin olmadınız mı? Yalnız değilsiniz. Çoğu geliştirici bir görüntüyü OCR motoruna atar ve sihrin gerçekleşmesini umar, ancak bozuk bir çıktı alır. Bu öğreticide, Aspose OCR for Java kullanarak **görüntü kontrastını artıran**, **kontrast seviyesini** ayarlayan ve sonunda **görüntüden metin tanıyan** pratik, uçtan uca bir örnek üzerinden ilerleyeceğiz.

Tamamladığınızda, gürültülü taramalarda bile **OCR kullanarak metin çıkaran** yeniden kullanılabilir bir kod parçacığına sahip olacaksınız. Gizli hileler yok, sadece net adımlar ve her birinin ardındaki mantık.

## Hızlı cevaplar
- **OCR'ı iyileştirmenin ilk adımı nedir?** Motoru oluşturmadan önce Aspose OCR lisansınızı yükleyin.  
- **Hangi üç ön işleme seçeneği en çok önemlidir?** Eğikliği düzeltme, gürültü giderme ve kontrast artırma.  
- **Çoğu basılı belge için hangi kontrast seviyesi işe yarar?** Yaklaşık 1.3 f iyi bir denge sağlar.  
- **İşlenmiş görüntüyü görebilir miyim?** Evet—ara bitmap'i PNG olarak dışa aktarın.  
- **Üretim için lisansa ihtiyacım var mı?** Kesinlikle; deneme sürümü sınırlı modda çalışır ve filigran ekler.

## Java’da Görüntüleri Ön İşleyerek OCR’ı Nasıl İyileştirirsiniz?
Görüntüyü yükleyin, eğikliği düzeltin, gürültüyü giderin ve kontrastı ayarlayın, ardından tanıyıcıyı çalıştırın. Aspose OCR’ın işlem hattı görüntüyü tam bu sırayla işler, böylece her dönüşüm sinir ağı tanıyıcısı görmeden önce mümkün olan en temiz veriler üzerinde çalışır. Bu iki adımlı yaklaşım—ön işleme ardından tanıma—tipik taranmış belgelerde karakter doğruluğunu %30’a kadar artırır.

## Aspose OCR for Java Nedir?
Aspose OCR for Java, **30+ görüntü formatını** (JPEG, PNG, TIFF, BMP dahil) destekleyen bir kütüphanedir ve standart 8 çekirdekli bir sunucuda 200 sayfalık çoklu‑görüntü toplu işlemini 2 saniyenin altında gerçekleştirebilir. Programatik olarak yapılandırabileceğiniz yerleşik eğikliği düzeltme, gürültü giderme ve kontrast artırma filtreleri sunar.

## Gerekenler
- Java 17 veya daha yeni (herhangi bir güncel JDK çalışır)
- Aspose OCR for Java kütüphanesi (resmi Aspose sitesinden indirin)
- Geçerli bir Aspose OCR lisans dosyası (`Aspose.OCR.lic`)
- Okumak istediğiniz giriş görüntüsü (`input.jpg`)
- Tercih ettiğiniz IDE veya basit bir komut satırı kurulumu

Eğer bunlara sahipseniz harika—hadi hemen başlayalım.

## İlk adım nedir: Aspose OCR lisansını yüklemek?
Herhangi bir OCR nesnesi oluşturmadan önce lisansı yükleyin, böylece motor deneme modunda değil tam özellik modunda çalışır. Bu, filigranları önler, tüm ön işleme seçeneklerinin kilidini açar ve OCR motorunun doğru metin çıkarımı için gerekli lisanslı dil paketlerine ve performans iyileştirmelerine erişmesini sağlar.

```java
import com.aspose.ocr.*;

public class PreprocessDemo {
    public static void main(String[] args) throws Exception {

        // Load the Aspose OCR license – this disables the evaluation limits
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**Neden önemli:** Uygun bir lisans olmadan motor değerlendirme modunda çalışır, bu da sonuçları kısaltabilir veya filigran ekleyebilir. Lisansı erken ayarlamak, sonraki tüm ön işleme seçeneklerinin tam özellik modunda uygulanmasını da sağlar.

## OCR motorunu nasıl başlatırsınız?
`OcrEngine` sınıfı, OCR gerçekleştiren ve ön işleme kontrolleri sağlayan temel bileşendir. Tek bir `OcrEngine` örneği oluşturun ve her görüntü için yeniden kullanın, böylece modelin tekrar tekrar yüklenmesinden kaçınılır. Motoru yeniden kullanmak, dahili sinir ağı modellerini önbelleğe alır, bu da görüntü başına gecikmeyi %40’a kadar azaltır ve bellek tüketimini düşürür, toplu işleme daha verimli hale gelir.

```java
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
```

**İpucu:** Bir toplu işlemde birçok görüntü işlemek istiyorsanız motoru tek bir örnek (singleton) olarak tutun; dahili kaynakları önbelleğe alır ve sonraki çağrıları hızlandırır.

## Ön işleme nasıl yapılandırılır – eğikliği düzeltme, gürültü giderme ve kontrast artırma
İşte **görüntüyü OCR için ön işleme** yaptığımız yer. Döndüreceğimiz üç ayar şunlardır:
1. **Deskew** – hafif döndürmeleri düzeltir.
2. **Denoise** – karakter segmentasyonunu karıştıran lekeleri giderir.
3. **Contrast enhancement** – koyu metnin arka plana karşı öne çıkmasını sağlar.

```java
        // Access preprocessing settings
        PreprocessingSettings preprocessing = ocrEngine.getPreprocessing();

        // Enable automatic deskew (helps with scanned pages that are a few degrees off)
        preprocessing.setDeskew(true);
        preprocessing.setDeskewAngleTolerance(0.1); // tolerance in degrees

        // Turn on denoising – median works well for salt‑and‑pepper noise
        preprocessing.setDenoise(true);
        preprocessing.setDenoiseMode(DenoiseMode.MEDIAN); // alternatives: GAUSSIAN

        // Boost contrast – this is the “boost image contrast” step
        preprocessing.setContrastEnhance(true);
        preprocessing.setContrastLevel(1.3f); // 1.0 = no change, >1.0 = stronger contrast
```

### Neden kontrast seviyesini ayarlamalıyız?
Kontrast seviyesini artırmak, görüntünün histogramını genişletir, karanlık pikselleri daha da karartır ve parlak pikselleri daha parlak hâle getirir. Pratikte, `1.3f` **kontrast seviyesi** çoğu basılı belge için en iyi dengeyi sağlar, `1.5f` üzerindeki bir değer ise ince çizgileri aşırı aydınlatabilir. Denemekten çekinmeyin; bu ayar değiştirmesi ucuzdur ve **görüntüden metin tanıma** başarısını büyük ölçüde artırabilir.

## Giriş görüntüsünü nasıl hazırlamalısınız?
`OcrInput` sınıfı, OCR motorunun işleyeceği bir görüntü koleksiyonunu temsil eder. `OcrInput` sınıfı dosya yönetimini soyutlar, toplu işleme için bir veya birden fazla görüntü eklemenize olanak tanır. Tek tek dosya yolları, akışlar veya bayt dizileri belirtebilir ve motor her girişi ayrı bir sayfa olarak ele alır, gerektiğinde format algılamayı ve dönüşümü otomatik olarak gerçekleştirir.

```java
        // Prepare the image for OCR – you can add more files to the same OcrInput
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/input.jpg");
```

**Köşe durum:** Görüntünüz standart dışı bir formatta ise (ör. çok sayfalı TIFF), her sayfayı ayrı ayrı yükleyebilir veya önce PNG/JPEG’e dönüştürebilirsiniz.

## Tanıma adımı nasıl çalışır?
`recognize` metodunu çağırdığınızda, motor önce yapılandırılmış ön işleme hattını—deskew, denoise ve kontrast artırma—tam bu sırayla uygular. Görüntü temizlendikten sonra sinir ağı tanıyıcısına gönderilir; bu tanıyıcı karakter şekillerini analiz eder ve çıkarılan metni bir dize olarak döndürür.

```java
        // Run OCR – this returns a result object containing the extracted text
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);
```

**Arka planda ne oluyor?** Aspose OCR önce deskew dönüşümünü uygular, ardından denoise filtresini çalıştırır ve son olarak görüntüyü sinir ağı tabanlı tanıyıcısına beslemeden önce kontrastı ayarlar. Sıra kasıtlıdır; değiştirmek alt‑optimum sonuçlara yol açabilir.

## Tanınan metni nasıl çıktılarız?
Tanıma tamamlandıktan sonra sonucu `getText` veya `getTextLines` ile alabilirsiniz. Bu örnekte çıkarılan dizeyi sadece konsola yazdırıyoruz, ancak üretimde bir dosyaya yazabilir, bir veritabanına kaydedebilir veya ağ üzerinden aşağı akış hizmetlerine gönderebilirsiniz.

```java
        // Print the recognized text to the console
        System.out.println(ocrResult.getText());
    }
}
```

### Beklenen çıktı
`input.jpg` dosyası “Hello World!” ifadesini içeriyorsa, konsol şu şekilde görüntülenmelidir:

```
Hello World!
```

Çıktı bozuk görünüyorsa, ön işleme değerlerini—özellikle **kontrast seviyesi** ve **denoise modu**—iki kez kontrol edin ve farklı bir görüntü formatı deneyin.

## Ön‑işlenmiş görüntüyü nasıl görselleştirirsiniz (isteğe bağlı)?
Ön işleme sonrası OCR motorunun ne gördüğünü incelemeniz gerekiyorsa, ara bitmap'i `saveProcessedImage` yöntemiyle PNG dosyası olarak dışa aktarabilirsiniz. Bu görsel kontrol, tanımadan önce deskew, denoise ve kontrast ayarlarının doğru uygulanıp uygulanmadığını doğrulamanıza yardımcı olur.

```java
        // Export the pre‑processed image for debugging
        BufferedImage processed = preprocessing.getProcessedImage();
        ImageIO.write(processed, "png", new File("processed.png"));
```

![OCR için görüntü ön işleme örneği](/images/ocr-preprocess-example.png "OCR için görüntü ön işleme – kontrast artırmadan önce ve sonra")
[OCR için görüntü ön işleme örneği](/images/ocr-preprocess-example.png "OCR için görüntü ön işleme – kontrast artırmadan önce ve sonra")

*Yukarıdaki görüntü, kontrast artırma ve gürültü giderme işlemlerinin bulanık bir taramayı temiz, OCR‑hazır bir resme nasıl dönüştürdüğünü gösterir.*

## Yaygın tuzaklar ve nasıl kaçınılır
| Tuzak | Neden olur | Çözüm |
|---------|----------------|-----|
| **Aşırı kontrast** (`setContrastLevel` çok yüksek) | Açık arka plan beyazlaşır, soluk karakterler silinir | Çoğu basılı metin için seviyeyi 1.1 ile 1.4 arasında tutun |
| **Deskew toleransı çok düşük** | Küçük döndürmeler düzeltilmez | `setDeskewAngleTolerance` değerini taranmış kitaplar için 0.2 veya 0.3'e yükseltin |
| **İkili görüntülerde GAUSSIAN denoise kullanmak** | Kenarları bulanıklaştırır, karakterleri birleştirir | Siyah‑beyaz taramalarda `DenoiseMode.MEDIAN` kullanın |
| **Lisans eksik** | Motor deneme moduna geri döner, çıktıyı kısaltır | `Aspose.OCR.lic` yolunu ve dosyanın okunabilir olduğunu doğrulayın |

## Sıkça sorulan sorular
**S: Bu yaklaşımı İngilizce dışındaki diller için kullanabilir miyim?**  
C: Evet—`engine.setLanguage("fr")` gibi uygun dil paketini yükleyin veya desteklenen herhangi bir ISO kodunu kullanın; bu, İngilizce dışı metinlerde doğruluğu artırır.

**S: Aspose OCR doğrudan PDF girişi destekliyor mu?**  
C: PDF sayfalarını yerel olarak okuyamaz; önce PDF’den görüntüleri çıkarmanız gerekir (ör. Aspose PDF ile) ve ardından OCR motoruna beslemelisiniz.

**S: Ne kadar büyük bir görüntüyü işleyebilirim?**  
C: Kütüphane, akış mimarisi sayesinde tüm dosyayı belleğe yüklemeye gerek kalmadan 30 MP’ye kadar görüntüyü işleyebilir.

**S: Görüntü klasörünü toplu olarak işlemek mümkün mü?**  
C: Kesinlikle—dosyalar üzerinde döngü kurun, aynı `OcrEngine` örneğini yeniden kullanın ve her dosyayı `OcrInput`a ekleyin. Bu, görüntü başına ek yükü büyük ölçüde azaltır.

**S: OCR çıktısı hâlâ hatalar içeriyorsa ne yapmalıyım?**  
C: `setContrastLevel` değerini daha küçük adımlarla ayarlamayı deneyin, `setDenoiseMode` ile deney yapın veya zor arka planlar için `setUseAdaptiveThreshold(true)` özelliğini etkinleştirin.

## Sonraki adımlar: temel ön işlemeyi aşmak
Artık **görüntüyü OCR için ön işleyebilir** ve **OCR kullanarak metin çıkarabilirsiniz**, şu uzantıları göz önünde bulundurun:
- **Dil paketleri** – İngilizce dışı metinlerde doğruluğu artırmak için belirli dil sözlüklerini yükleyin.
- **İlgi bölgesi (ROI) kırpma** – sayfanın sadece bir kısmına ihtiyacınız varsa görüntünün bir alt bölümüne odaklanın.
- **Toplu işleme** – bir dizindeki görüntüler üzerinde döngü kurun, hız için aynı `OcrEngine` örneğini yeniden kullanın.
- **PDF ile bütünleştirme** – taranmış PDF’leri tek bir işlem hattında aranabilir PDF’lere dönüştürmek için Aspose OCR’ı Aspose PDF ile birleştirin.

Bu konular doğal olarak ikincil anahtar kelimelerimizi içerir: hâlâ **görüntü kontrastını artıracak**, **kontrast seviyesini ayarlayacak** ve birçok senaryoda **görüntüden metin tanıyacaksınız**.

## Sonuç
Aspose OCR for Java kullanarak **görüntüyü OCR için ön işleme** yapmanız için gereken her şeyi kapsadık: lisansı yükleme, deskew, denoise ve kontrast artırma yapılandırması, görüntüyü besleme ve sonunda **görüntüden metin tanıma**. Yukarıdaki eksiksiz, çalıştırılabilir örnekle artık **OCR kullanarak metin çıkarabilirsiniz** herhangi bir uygun şekilde hazırlanmış resimde.

Kodu çalıştırın, **kontrast seviyesini** ayarlayın ve doğruluğun nasıl yükseldiğini izleyin. Hazır olduğunuzda, dil‑spesifik modelleri veya toplu işlem hatlarını keşfederek bu tek‑görüntü demosunu üretim‑düzeyinde bir çözüme dönüştürün.

*Kodlamaktan keyif alın ve taramalarınız her zaman net olsun!*

---

**Son Güncelleme:** 2026-10-30  
**Test Edilen Versiyon:** Aspose OCR for Java 24.11  
**Yazar:** Aspose

## İlgili Öğreticiler

- [Aspose Ocr Java Rehberi ile Görüntüden Metin Çıkarma](/ocr/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/)
- [Aspose Ocr Gpu Java Kullanarak Metin Görüntüsü Tanıma](/ocr/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/)
- [Ocr Engine Java Oluşturma – Büyük Görüntülerden Metin Tanıma](/ocr/java/advanced-ocr-techniques/create-ocr-engine-java-recognize-text-from-large-images/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}