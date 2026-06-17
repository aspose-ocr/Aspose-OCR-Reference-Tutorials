---
category: general
date: 2026-05-06
description: Aspose OCR'i Java'da kullanarak bir görüntüden aranabilir PDF oluşturun.
  Görüntüyü PDF'ye dönüştürmeyi, yazım düzeltmesini etkinleştirmeyi ve hızlı sonuçlar
  için OCR GPU'yu kullanmayı öğrenin.
draft: false
keywords:
- create searchable pdf
- convert image to pdf
- enable spell correction
- use ocr gpu
- process image ocr
language: tr
og_description: Aspose OCR'i Java'da kullanarak bir görüntüden aranabilir PDF oluşturun.
  Bu kılavuz, görüntüyü PDF'ye dönüştürmeyi, yazım düzeltmeyi etkinleştirmeyi ve OCR
  GPU'yu kullanmayı gösterir.
og_title: Java OCR ile Görüntüden Aranabilir PDF Oluştur
tags:
- OCR
- Java
- PDF
title: Java OCR ile Görüntüden Aranabilir PDF Oluştur
url: /tr/java/ocr-operations/create-searchable-pdf-from-image-with-java-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Görüntüden Java OCR ile Aranabilir PDF Oluşturma

Hiç taranmış bir resimden **create searchable PDF** oluşturmanız gerekti, ancak nereden başlayacağınızı bilemediniz mi? Yalnız değilsiniz—çoğu geliştirici, görüntü‑tabanlı PDF'lerle ilk kez uğraşırken bu engelle karşılaşır. Neyse ki, Aspose OCR for Java ile **convert image to PDF** yapabilir, metni seçilebilir içeriğe dönüştürebilir ve hatta daha düzgün bir sonuç için yazım düzeltmesi ekleyebilirsiniz.

Bu öğreticide, kullanılabilir olduğunda **use OCR GPU** nasıl kullanılacağını, **process image OCR**'ı verimli bir şekilde nasıl gerçekleştireceğimizi ve yazım düzeltmesini etkinleştirmenin sonraki aramalarda neden önemli olduğunu gösteren eksiksiz, çalıştırmaya hazır bir örnek üzerinden ilerleyeceğiz. Sonunda, kullanıcılarla paylaşabileceğiniz veya uyumluluk için arşivleyebileceğiniz bir searchable PDF oluşturmak için tek tıklamalı bir yönteme sahip olacaksınız.

> **Pro tip:** GPU'siz bir makinede çalışıyorsanız, kod sorunsuz bir şekilde CPU'ya geri döner, böylece bir şeyleri yeniden yazmanız gerekmez.

---

## Gereksinimler

- **Java 8+** (kod JDK 8 ve üzeri ile derlenir)
- **Aspose OCR for Java** kütüphanesi (en son JAR'ı Aspose sitesinden indirin)
- **input image** (JPEG, PNG, TIFF vb.) searchable PDF'ye dönüştürmek istediğiniz bir resim
- (Opsiyonel) En hızlı tanıma için CUDA desteği olan bir **GPU**

Ekstra framework yok, Maven/Gradle sihri yok—sadece sınıf yolunda tek bir JAR ve hazırsınız.

## Adım 1: OCR Motorunu Başlatın – İşlemin Kalbi  

İlk olarak bir `OcrEngine` örneği oluşturur ve kaynak dosyaya işaret ederiz. Bu nesne, görüntüyü okuyacak, sinir ağını çalıştıracak ve bize metni geri verecek iş gücüdür.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Initialise the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the image you want to convert
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));
```

*Neden önemli:* Motoru bir kez başlatıp tekrar kullanmak, yerel kütüphanelerin tekrar tekrar yüklenmesi yükünü ortadan kaldırır—bu, onlarca dosyayı toplu işlediğinizde birikerek performans kazancı sağlar.

## Adım 2: İşleme Aygıtını Seçin – Mümkünse OCR GPU'yu Kullanın  

İş istasyonunuzda uyumlu bir GPU varsa, Aspose'a ağır işi GPU üzerinde çalıştırmasını söyleyebilirsiniz. Aksi takdirde motor otomatik olarak CPU'ya geçer.

```java
        // Prefer GPU; fall back to CPU if no compatible device is found
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);
```

*Faydası nedir?* GPU hızlandırması, özellikle yüksek çözünürlüklü taramalarda her sayfadan saniyeler kazandırabilir. Geri dönüş, aynı kodun her yerde çalışmasını sağlar; bu yüzden **use OCR GPU**'yu varsayılan ayar olarak öneririz.

## Adım 3: Tarama Hızını Artırın – Tüm CPU Çekirdeklerini Kullanın  

GPU meşgul olduğunda bile, çevresindeki ön işleme adımları paralelleştirilebilir. İş parçacığı sayısını mevcut işlemci sayısına ayarlamak, motorun birden fazla parçayı aynı anda işleyebilmesini sağlar.

```java
        // Use all logical cores for preprocessing and language detection
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());
```

*Not:* 4 çekirdekli bir dizüstü bilgisayarda bu dört iş parçacığı oluşturur; 16 çekirdekli bir iş istasyonunda tam faydayı elde edersiniz. Ancak daha fazla iş parçacığının daha yüksek bellek kullanımı anlamına geldiğini unutmayın.

## Adım 4: Görüntüyü Temizleyin – Ön‑İşleme Filtreleri  

Bulanık veya gürültülü bir tarama, çöp metin üretir. Birkaç yerleşik filtre eklemek doğruluğu büyük ölçüde artırır.

```java
        // Deskew the image so text lines are horizontal
        ocrEngine.getPreprocessing().add(new DeskewFilter());

        // Remove speckles and background noise
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());
```

*Neden bu filtreler?* `DeskewFilter`, bir belge tarayıcıya açıyla verildiğinde sıkça oluşan rotasyonu düzeltir. `NoiseRemovalFilter` ise karakter olarak yanlış yorumlanabilecek rastgele pikselleri ortadan kaldırır. Bunu, OCR motoruna okunacak temiz bir kağıt vermek gibi düşünün.

## Adım 5: Akıllı Özellikleri Açın – Yazım Düzeltmesini ve Otomatik Dil Algılamayı Etkinleştirin  

Çok dilli belgelerle çalışıyorsanız ya da sadece daha az yazım hatası istiyorsanız, yerleşik yazım denetleyicisini açın ve motorun dili tahmin etmesine izin verin.

```java
        // Activate spell correction to fix common OCR mistakes
        ocrEngine.getSettings().setEnableSpellCorrection(true);

        // Let the engine automatically detect the language of the input
        ocrEngine.getSettings().setAutoDetectLanguage(true);
```

*Ne zaman faydalıdır?* Diyelim ki taramanızda hem İngilizce hem de İspanyolca bölümler var. Otomatik algılama özelliği sözlükleri anlık değiştirirken, yazım düzeltmesi “0” gibi “O” yerine okunmuş karakterleri temizler. Bu adım, gerçek sonuçlar döndüren bir **searchable PDF** üretmek için esastır.

## Adım 6: Sonucu Kaydedin – Görüntüyü PDF'ye Dönüştürün ve Aranabilir Hale Getirin  

Son olarak motoru, orijinal görüntünün görünmez bir metin katmanının arkasında yer aldığı bir PDF oluşturması için yönlendiririz. Bu klasik **convert image to PDF** iş akışıdır, ancak PDF artık aranabilir.

```java
        // Generate a searchable PDF – the text layer sits behind the original image
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

Çıktı dosyası (`output-searchable.pdf`) herhangi bir PDF görüntüleyicide açılabilir; metni yerel bir PDF gibi seçebilir, kopyalayabilir ve arayabilirsiniz. Ek bir araç gerekmez.

## Tam Çalışan Örnek – Kopyala‑Yap ve Çalıştır  

Aşağıda, derlemeye hazır tam program yer alıyor. `YOUR_DIRECTORY` ifadesini `input.jpg` dosyasının bulunduğu klasörle değiştirin.

```java
import com.aspose.ocr.*;

public class QuickStart {
    public static void main(String[] args) throws Exception {
        // Step 1: Create the OCR engine and load the source image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/input.jpg"));

        // Step 2: Select the processing device (GPU if available, otherwise CPU)
        ocrEngine.getDevice().setDeviceType(OcrDeviceType.GPU);

        // Step 3: Use all available CPU cores to speed up recognition
        ocrEngine.setThreadCount(Runtime.getRuntime().availableProcessors());

        // Step 4: Add preprocessing filters to improve image quality
        ocrEngine.getPreprocessing().add(new DeskewFilter());
        ocrEngine.getPreprocessing().add(new NoiseRemovalFilter());

        // Step 5: Enable spell correction and automatic language detection
        ocrEngine.getSettings().setEnableSpellCorrection(true);
        ocrEngine.getSettings().setAutoDetectLanguage(true);

        // Step 6: Perform OCR and save the result as a searchable PDF
        ocrEngine.save("YOUR_DIRECTORY/output-searchable.pdf", OcrSaveFormat.PDF_SEARCHABLE);

        System.out.println("Searchable PDF generated successfully.");
    }
}
```

**Beklenen çıktı:** Programı çalıştırdığınızda konsolda *“Searchable PDF generated successfully.”* satırını göreceksiniz. `output-searchable.pdf` dosyasını Adobe Reader’da açtığınızda, orijinal görüntüden bir kelimeyi arama kutusuna yazıp konumuna anında gidebileceksiniz.

## Yaygın Sorular ve Kenar Durumları  

- **GPU algılanmazsa ne olur?**  
  `setDeviceType(OcrDeviceType.GPU)` çağrısı bir istisna atmaz; sadece motoru önce GPU'yu denemeye yönlendirir. Başarısız olursa, motor sessizce CPU'ya geri döner.

- **Bir çalıştırmada birden fazla görüntüyü işleyebilir miyim?**  
  Evet. Kodu bir döngü içinde sarın, her yinelemede dosya adını değiştirin ve aynı `OcrEngine` örneğini yeniden kullanarak bellek kullanımını düşük tutun.

- **PDF'im çok büyük—nasıl küçültebilirim?**  
  OCR sonrası Aspose’un PDF optimizasyon API’lerini çalıştırabilir ya da motorun önüne beslemeden önce kaynak görüntüyü küçültebilirsiniz (`ImageStream.fromFile(...).setResolution(150)` 150 DPI için).

- **Yasal uyumluluk için orijinal görüntü çözünürlüğünü korumam gerekiyor.**  
  `PDF_SEARCHABLE` formatı orijinal bitmap'i tam olarak korur; görünmez metin katmanı, görsel kalitede değişiklik yapmadan üzerine eklenir.

## Görsel Özet  

![searchable pdf örneği oluşturma](placeholder-image.png "searchable pdf örneği oluşturma")

*Alt metin:* *searchable pdf örneği oluşturma – Java OCR motoru taranmış bir JPG'yi aranabilir bir PDF'ye dönüştürüyor.*

## Sonuç  

Artık Aspose OCR for Java kullanarak herhangi bir görüntüyü **searchable PDF**'ye dönüştürmek için **tam, uçtan uca bir çözüm** elde ettiniz. **convert image to PDF**, **spell correction'ı etkinleştirerek** ve mümkün olduğunda **OCR GPU'yu kullanarak**, platformlar arasında çalışan hızlı, doğru ve aranabilir sonuçlar elde edersiniz.

Sonraki adım ne? Şunları deneyin:

- **Farklı çıktı formatları** (`PDF`, `DOCX`, `HTML`) metin katmanının nasıl davrandığını görmek için.
- **Özel sözlükler** alan‑spesifik jargon işliyorsanız.
- **Toplu işleme** binlerce taramayı otomatik olarak işlemek için.

İş parçacığı sayısını ayarlamaktan, filtreleri değiştirmekten veya kendi ön‑işleme hattınızı eklemekten çekinmeyin. Temel desen aynı kalır: yükle → ön‑işle → yapılandır → OCR → kaydet.

Kodlamaktan keyif alın, ve PDF'lerinizin her zaman aranabilir olmasını dileriz!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}