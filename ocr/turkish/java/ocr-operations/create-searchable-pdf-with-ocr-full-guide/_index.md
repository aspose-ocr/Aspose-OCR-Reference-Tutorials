---
category: general
date: 2026-06-22
description: Java’da OCR kullanarak aranabilir PDF oluşturun. Sıkıştırmayı nasıl devre
  dışı bırakacağınızı ve taranmış görüntü PDF’sini hızlıca aranabilir PDF’ye dönüştüreceğinizi
  öğrenin.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- ocr to searchable pdf
- how to disable compression
- pdf without compression
language: tr
og_description: OCR kullanarak Java’da aranabilir PDF oluşturun. Bu kılavuz, sıkıştırmayı
  nasıl devre dışı bırakacağınızı, taranmış görüntü PDF’sini nasıl dönüştüreceğinizi
  ve sıkıştırmasız bir PDF nasıl oluşturulacağını gösterir.
og_title: OCR ile Aranabilir PDF Oluşturma – Tam Java Öğreticisi
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  headline: Create Searchable PDF with OCR – Full Guide
  type: TechArticle
- description: Create searchable PDF using OCR in Java. Learn how to disable compression
    and convert scanned image PDF to a searchable PDF quickly.
  name: Create Searchable PDF with OCR – Full Guide
  steps:
  - name: Set the output format to `PDF_SEARCHABLE`.
    text: Set the output format to `PDF_SEARCHABLE`.
  - name: Turn off PDF compression with `PdfCompression.NONE`.
    text: Turn off PDF compression with `PdfCompression.NONE`.
  - name: Run OCR and capture the `PdfDocument`.
    text: Run OCR and capture the `PdfDocument`.
  - name: Save the file to disk.
    text: Save the file to disk.
  type: HowTo
tags:
- OCR
- PDF
- Java
- Document Processing
title: OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz
url: /tr/java/ocr-operations/create-searchable-pdf-with-ocr-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR ile Aranabilir PDF Oluşturma – Tam Kılavuz

Tarama görüntülerinden oluşan bir topluluktan **aranabilir PDF** oluşturmanız gerektiğinde, hangi ayarları değiştirmeniz gerektiğinden emin olmadınız mı? Tek başınıza değilsiniz—çoğu geliştirici, çıktının devasa ve okunamaz bir yığın haline gelmesiyle aynı duvara çarpıyor.  

Bu öğreticide, bir Java OCR motoru kullanarak **aranabilir PDF oluşturmayı**, **tarama görüntüsü PDF'yi dönüştürmeyi** ve kritik olarak **sıkıştırmayı nasıl devre dışı bırakacağınızı** gösteren temiz, uçtan uca bir örnek üzerinden geçeceğiz, böylece ortaya çıkan dosya orijinal boyutlarına sadık kalır. Sonunda çalıştırmaya hazır bir kod parçacığına ve her yapılandırmanın neden önemli olduğuna dair sağlam bir anlayışa sahip olacaksınız.

## Öğrenecekleriniz

* OCR motorunu **aranabilir pdf oluşturacak şekilde** yapılandırmayı.  
* PDF sıkıştırmasını kapatmanın nedenini ve **sıkıştırmasız pdf** elde etmeyi.  
* Tarama görüntüsü alıp OCR çalıştıran ve **aranabilir PDF** kaydeden tam bir Java programı.  
* Çok sayfalı taramalar veya düşük çözünürlüklü kaynaklar gibi uç durumları ele almak için ipuçları.  

**Önkoşullar** – Java 8+ yüklü, uyumlu bir OCR SDK'sı (kod ABBYY FineReader Engine API'sini kullanıyor, ancak kavramlar `setOutputFormat` ve `setPdfCompression` sunan herhangi bir kütüphane için geçerlidir). IntelliJ IDEA veya Eclipse gibi bir IDE işleri kolaylaştırır, ancak basit bir metin düzenleyicisi de yeterlidir.

![Aranabilir PDF oluşturma iş akışı](image-placeholder.png "Tarama görüntülerinden son PDF'ye aranabilir pdf sürecini gösteren diyagram")

## Adım 1: OCR Motorunu **Aranabilir PDF Oluşturacak Şekilde** Ayarlama

OCR motoruna söylemeniz gereken ilk şey, hangi tür çıktıyı beklediğinizdir. Varsayılan olarak birçok SDK düz metin veya raster PDF üretir, bu da aranabilir değildir. Formatı değiştirmek sizin yerinize ağır işi yapar.

```java
// Step 1: Tell the engine we want a searchable PDF
engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);
```

*Neden önemli*: `PDF_SEARCHABLE` bayrağı, motoru tarama görüntüsünün altına görünmez bir metin katmanı eklemeye yönlendirir. Arama araçları daha sonra belgeyi indeksleyebilir, böylece Adobe Reader'da açtığınız herhangi bir yerel PDF gibi davranır.

## Adım 2: Sıkıştırmayı Devre Dışı Bırakma – **Sıkıştırmayı Nasıl Devre Dışı Bırakılır** Doğru Şekilde

Bu adımı atladığınızda motor, alan tasarrufu için her sayfayı sıkıştırır, ancak sıkıştırma ince detayları bulanıklaştırabilir—özellikle daha sonra yüksek çözünürlüklü görüntüler çıkarmanız gerektiğinde sorun yaratır.

```java
// Step 2: Turn off PDF compression to keep original image quality
engine.getConfig().setPdfCompression(PdfCompression.NONE);
```

**Pro ipucu**: Sıkıştırmayı devre dışı bırakmak, her pikselin önemli olduğu yasal belgeler veya tıbbi taramaları arşivlemeyi planladığınızda esastır. Ortaya çıkan dosya daha büyük olabilir, ancak orijinal boyutları ve netliği korursunuz.

## Adım 3: OCR'ı Çalıştırın ve Oluşan Belgeyi Alın

Motor artık ne çıktıyı vereceğini ve görüntüleri nasıl işleyeceğini bildiğine göre, tanıma işlemini çalıştırabilirsiniz. Çağrı, kaydedilmeye veya daha fazla işlenmeye hazır bir `PdfDocument` nesnesi döndürür.

```java
// Step 3: Run OCR and capture the searchable PDF in memory
PdfDocument pdf = engine.recognizeToPdf();
```

*Arka planda ne oluyor?* Motor, her giriş sayfasını işler, karakter tanıma yapar ve gizli metin katmanını görüntüye ekler. Birden fazla sayfanız varsa, otomatik olarak birleştirilir.

## Adım 4: **Aranabilir PDF**'yi Diske Kaydetme

Son olarak, bellek içindeki PDF'yi bir dosyaya yazın. Yazma izniniz olan bir konum seçin ve dosyaya anlamlı bir ad verin.

```java
// Step 4: Persist the searchable PDF on disk
pdf.save("YOUR_DIRECTORY/searchable.pdf");
```

`searchable.pdf` dosyasını bir görüntüleyicide açtığınızda, metni seçip arayabileceğinizi fark edeceksiniz—görünür içerik hâlâ orijinal tarama görüntüsü olsa da.

### Tam Çalışan Örnek

Aşağıda, dört adımı bir araya getiren bağımsız bir Java sınıfı bulunuyor. Kopyalayıp yapıştırmaktan, giriş yolunu ayarlamaktan ve olduğu gibi çalıştırmaktan çekinmeyin.

```java
import com.abbyy.ocrsdk.Engine;
import com.abbyy.ocrsdk.OcrOutputFormat;
import com.abbyy.ocrsdk.PdfCompression;
import com.abbyy.ocrsdk.PdfDocument;

/**
 * Demonstrates how to create searchable PDF from scanned images.
 * This example uses the ABBYY FineReader Engine Java API.
 */
public class SearchablePdfCreator {

    public static void main(String[] args) {
        // ---- 1. Initialize the OCR engine -------------------------------------------------
        Engine engine = new Engine();
        // (Assume license activation and engine initialization are handled elsewhere)

        // ---- 2. Configure output to be a searchable PDF ----------------------------------
        engine.getConfig().setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE);

        // ---- 3. Disable compression for a PDF without compression -------------------------
        engine.getConfig().setPdfCompression(PdfCompression.NONE);

        // ---- 4. Load the scanned image(s) --------------------------------------------------
        // For simplicity, we let the engine auto‑detect images in the working folder.
        // You could also call engine.addImage("path/to/image.tif") for explicit control.
        engine.addImage("YOUR_DIRECTORY/scanned-page.tif");

        // ---- 5. Perform OCR and retrieve the PDF -----------------------------------------
        PdfDocument pdf = engine.recognizeToPdf();

        // ---- 6. Save the result -----------------------------------------------------------
        pdf.save("YOUR_DIRECTORY/searchable.pdf");

        System.out.println("✅ Searchable PDF created successfully at YOUR_DIRECTORY/searchable.pdf");
    }
}
```

**Beklenen çıktı** – Programı çalıştırdıktan sonra yukarıdaki konsol mesajını göreceksiniz ve `searchable.pdf` dosyası `YOUR_DIRECTORY` içinde görünecek. Herhangi bir PDF okuyucuda açtığınızda şunları yapabilmelisiniz:

* Metni vurgulama.
* Yerleşik aramayı (Ctrl + F) kullanarak kelimeleri bulma.
* Gerekirse gizli metin katmanını dışa aktarma.

---

## Neden Sıkıştırma Devre Dışı Bırakılır? **Sıkıştırmasız PDF**'yi Anlamak

Şöyle düşünebilirsiniz: “Sıkıştırma her zaman iyi bir fikir değil mi?” Cevap nüanslıdır:

| Durum | Sıkıştırmayı Koru (`NORMAL`) | Sıkıştırmayı Devre Dışı Bırak (`NONE`) |
|-----------|-----------------------------|------------------------------|
| Hukuki sözleşmelerin arşivlenmesi | ❌ Piksel doğruluğunu değiştirebilir | ✅ Orijinal görünümü garantiler |
| Düşük çözünürlüklü büyük tarama topluluğu | ✅ Depolamayı tasarruf eder | ❌ Faydası olmadan boyutu artırır |
| Küçük fontlarda OCR doğruluğu ihtiyacı | ❌ İnce detayları bulanıklaştırır | ✅ Her darbeyi korur |

Kısacası, **sıkıştırmanın nasıl devre dışı bırakılacağı** depolama ile doğruluk arasında bir denge meselesidir. Metni yeniden yazdırmak yerine aramayı amaçladığınız çoğu aranabilir PDF iş akışı için sıkıştırmayı kapatmak en güvenli seçenektir.

## **Tarama Görüntüsü PDF**'yi Doğrudan Dönüştürme

Bazen içinde tarama görüntüleri bulunan bir PDF'niz (“sadece görüntü PDF”i) olabilir. **Tarama görüntüsü PDF'yi** aranabilir bir sürüme **dönüştürmek** için, tek tek görüntüler yerine tüm PDF'yi motorun içine besleyebilirsiniz:

```java
engine.addPdf("YOUR_DIRECTORY/scanned-image-only.pdf");
PdfDocument searchable = engine.recognizeToPdf();
searchable.save("YOUR_DIRECTORY/searchable-from-pdf.pdf");
```

Aynı yapılandırma bayrakları (`PDF_SEARCHABLE` ve `PdfCompression.NONE`) geçerlidir, böylece bir PDF konteynerinden başlasa bile **sıkıştırmasız pdf** elde edersiniz.

## Yaygın Tuzaklar ve Nasıl Kaçınılır

* **Çıktı formatını ayarlamayı unutmak** – Motor varsayılan olarak raster PDF üretir, bu da aranabilir değildir. `recognizeToPdf()`'den önce her zaman `setOutputFormat(OcrOutputFormat.PDF_SEARCHABLE)` çağırın.
* **Büyük toplularda bellek tükenmesi** – Sayfaları parçalar halinde yükleyip işleyin veya SDK'nız bir streaming API sağlıyorsa onu kullanın.
* **Yanlış dosya yolları** – Mutlak yollar kullanın veya çalışma dizininizin doğru ayarlandığından emin olun; aksi takdirde `pdf.save()` bir `IOException` fırlatır.
* **Lisans etkinleştirilmemiş** – Çoğu ticari OCR SDK'sı geçerli bir lisans gerektirir; lisans eksikse motor bir runtime istisnası fırlatır.

---

## Sonuç

Artık tarama görüntülerinden **aranabilir PDF** dosyaları oluşturmayı, **tarama görüntüsü PDF'yi dönüştürmeyi** ve **sıkıştırmanın nasıl devre dışı bırakılacağını** gösteren eksiksiz, çalıştırmaya hazır bir çözümünüz var. Temel adımlar şunlardır:

1. Çıktı formatını `PDF_SEARCHABLE` olarak ayarlayın.  
2. PDF sıkıştırmasını `PdfCompression.NONE` ile kapatın.  
3. OCR'ı çalıştırın ve `PdfDocument`'i yakalayın.  
4. Dosyayı diske kaydedin.

Buradan itibaren fontlarla deney yapabilir, filigran ekleyebilir veya tüm klasörleri toplu işleyebilirsiniz. OCR dil paketleri eklemek, çok sayfalı TIFF'leri işlemek veya bu iş akışını bir web servisine entegre etmekle ilgileniyorsanız, “Java'da OCR dil seçimi” ve “Büyük belge setleri için Streaming OCR” adlı yaklaşan öğreticilerimize göz atın.

Sorularınız mı var, yoksa bir sorun mu fark ettiniz? Aşağıya yorum bırakın—iyi kodlamalar ve yeni aranabilir PDF'lerinizin tadını çıkarın!

## Sonra Ne Öğrenmelisiniz?

Aşağıdaki öğreticiler, bu rehberde gösterilen tekniklere dayanarak yakından ilgili konuları kapsar. Her kaynak, ek API özelliklerini öğrenmenize ve kendi projelerinizde alternatif uygulama yaklaşımlarını keşfetmenize yardımcı olmak için adım adım açıklamalar içeren tam çalışan kod örnekleri sunar.

- [PDF Metnini Tanıma – Aspose.OCR for Java ile OCR İşlemleri](/ocr/english/java/ocr-operations/)
- [Aspose.OCR for Java'da PDF Belgelerini OCR ile Tanıma](/ocr/english/java/ocr-operations/recognize-pdf/)
- [Görüntüleri PDF C#'a Dönüştür – Çok Sayfalı OCR Sonucunu Kaydet](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}