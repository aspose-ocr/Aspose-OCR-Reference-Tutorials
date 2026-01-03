---
category: general
date: 2026-01-02
description: Python kullanarak belgelerden tablo çıkarın. PDF'den tabloları nasıl
  okuyacağınızı ve tablo satırlarını temiz, yeniden kullanılabilir bir çözümle nasıl
  yineleyeceğinizi öğrenin.
draft: false
keywords:
- extract table from document
- how to read tables from pdf
- how to iterate table rows
- pdf table extraction python
- document layout detection
language: tr
og_description: Python'da belgelerden tablo çıkarma. Bu kılavuz, PDF'den tabloları
  okuma ve güvenilir bir motorla tablo satırlarını yineleme yöntemini gösterir.
og_title: Belgeden tablo çıkarma – Tam Python Öğreticisi
tags:
- Python
- PDF
- Data Extraction
title: Belgeden tablo çıkarma – Adım adım Python rehberi
url: /tr/python/general/extract-table-from-document-step-by-step-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Belgeden tablo çıkarma – Tam Python Eğitimi

Hiç **belgeden tablo çıkarma** ihtiyacı duydunuz mu ama nereden başlayacağınızı bilemediniz mi? Tek başınıza değilsiniz—birçok geliştirici, verileri tablolar içinde gizleyen PDF'lerle çalışırken aynı duvara çarpıyor. Bu öğreticide, **pdf'den tabloları okuma** yöntemini göstermekle kalmayıp, **tablo satırlarını yineleme** yoluyla verileri istediğiniz yere yönlendirebileceğiniz pratik, uçtan uca bir çözümü adım adım inceleyeceğiz.

Düşünün ki bir dizi fatura var ve her birinde satır kalemlerinin bir özet tablosu bulunuyor. Bu satırları bir CSV'ye aktararak sonraki analizlerde kullanmak istiyorsunuz. Bu rehberin sonunda, tam da bunu yapan yeniden kullanılabilir bir kod parçacığına ve yaygın tuzaklardan kaçınmak için birkaç ipucuna sahip olacaksınız.

## Öğrenecekleriniz

- Bir belgenin düzenini bir layout motoru ile tespit edin.  
- Daha temiz tablo yapıları için ham tespiti bir post‑processor ile iyileştirin.  
- Tespit edilen tablonun her satırını yineleyin ve hücre içeriklerini yazdırın (veya depolayın).  

Harici hizmetler, sihirli kara kutular yok—sadece saf Python ve popüler bir OCR/düzen kütüphanesi (ör. **pdfplumber**, **pdfminer.six** veya zaten kullandığınız bir `engine`). Eğer `recognize_layout()` ve `run_postprocessor()` metodlarını uygulayan bir `engine` nesneniz varsa, kodu doğrudan ekleyebilirsiniz.

> **Pro ipucu:** Ticari bir SDK kullanıyorsanız, “table detection” özelliğini etkinleştirdiğinizden emin olun; aksi takdirde ham layout birleştirilmiş hücreleri kaçırabilir.

---

## Adım 1: Tablo Yapısını Tespit Et – Belgeden tablo çıkarma

İlk olarak, sayfada tabloların nerede bulunduğunu söyleyen ham bir layout elde etmeniz gerekir. Çoğu modern PDF kütüphanesi, bloklar, satırlar ve hücreler hiyerarşisini döndüren `recognize_layout()` benzeri bir metod sunar.

```python
# Step 1 – Detect the document layout using the engine
# ---------------------------------------------------
# `engine` is assumed to be an instantiated object from your PDF library.
# It could be pdfplumber, a custom OCR SDK, or any tool that supports layout detection.
raw_layout = engine.recognize_layout()
```

**Neden önemli:**  
Ham layout, her metin öğesinin koordinatlarını verir, ancak genellikle tablo dışı başlıklar, altbilgiler veya rastgele karakterler gibi gürültü içerir. Bu yüzden bir sonraki adım kritik olur.

> **Sık sorulan soru:** *PDF'im birden fazla sayfa içeriyorsa ne yapmalıyım?*  
> `recognize_layout()` çağrısı genellikle bir sayfa nesnesi listesi döndürür. Bunlar üzerinde döngü kurup aynı post‑processing mantığını her sayfaya uygulayın.

---

## Adım 2: Tespiti İyileştir – Pdf'den tabloları okuma

`raw_layout` elde ettikten sonra onu temizlemeniz gerekir. Çoğu motor, parçalanmış hücreleri birleştiren, alakasız metinleri kaldıran ve düzgün bir `Table` nesnesi oluşturan bir post‑processor ile birlikte gelir.

```python
# Step 2 – Refine the detected layout with the post‑processor
# ----------------------------------------------------------
# The post‑processor returns an enhanced layout where tables are
# represented as a list of rows, each row being a list of Cell objects.
enhanced_layout = engine.run_postprocessor(raw_layout)
```

**Neden buna ihtiyacınız var:**  
Ham layout, tek bir tablo satırını onlarca küçük parçaya ayırabilir. Post‑processor bu parçaları mantıksal hücrelere gruplar, böylece daha sonra yineleme çok kolaylaşır.

> **Köşe durum:** Bazı PDF'ler görünmez kenarlara sahiptir. Eksik satırlar görürseniz, motorunuzda (varsa) “detect invisible lines” bayrağını etkinleştirin.

---

## Adım 3: Tablo Satırlarını Yinele – Tablo satırlarını yineleme

Artık temiz bir `enhanced_layout`'a sahipsiniz, veriyi çekmek çocuk oyuncağı. Aşağıda her satırı dolaşıp hücre metinlerini sekmelerle birleştiriyoruz (çıktının düzgün hizalanması için) ve sonucu yazdırıyoruz. `print` ifadesini istediğiniz depolama mantığıyla (CSV yazıcı, veritabanı ekleme vb.) değiştirebilirsiniz.

```python
# Step 3 – Print the table contents row by row
# --------------------------------------------
# `enhanced_layout.table` is expected to be an iterable of rows.
# Each `row` is a list of Cell objects with a `.text` attribute.
for row in enhanced_layout.table:
    # Join each cell's text with a tab to align columns
    print("\t".join(cell.text for cell in row))
```

**Beklenen çıktı (örnek):**

```
Item	Qty	Price	Total
Widget A	2	$10.00	$20.00
Widget B	1	$15.00	$15.00
Service C	5	$8.00	$40.00
```

Eğer sekme‑ayırmalı bir görünüm yerine CSV istiyorsanız, `"\t".join(...)` ifadesini `",".join(...)` ile değiştirip bir dosyaya yazın.

---

## Tam Çalışan Örnek

Hepsini bir araya getirdiğimizde, bağımsız bir script elde ediyoruz. Kullandığınız kütüphaneye göre import ve motor başlatma kısmını ayarlayın.

```python
# --------------------------------------------------------------
# Full script: extract table from document and iterate rows
# --------------------------------------------------------------
import sys

# -----------------------------------------------------------------
# 1️⃣  Import or instantiate your PDF layout engine.
# Replace the placeholder with the actual library you use.
# -----------------------------------------------------------------
# Example with a fictional `pdf_engine` package:
# from pdf_engine import LayoutEngine
# engine = LayoutEngine(api_key="YOUR_KEY")
# -----------------------------------------------------------------
# For pdfplumber (open‑source) you could do:
# import pdfplumber
# engine = pdfplumber.open("sample.pdf")
# -----------------------------------------------------------------
# We'll keep it generic for the tutorial.
# -----------------------------------------------------------------

def extract_table(engine):
    """
    Detect, refine, and iterate over a table in a PDF document.
    Returns a list of rows, where each row is a list of cell strings.
    """
    # Detect layout
    raw_layout = engine.recognize_layout()

    # Refine layout
    enhanced_layout = engine.run_postprocessor(raw_layout)

    # Collect rows
    rows = []
    for row in enhanced_layout.table:
        rows.append([cell.text for cell in row])
    return rows

def main(pdf_path):
    # Initialise your engine – this will differ per library
    # Below is a stub; replace with real initialization.
    engine = initialize_engine(pdf_path)   # <-- implement this

    try:
        table_rows = extract_table(engine)
        for row in table_rows:
            print("\t".join(row))
    except Exception as e:
        print(f"❌ Extraction failed: {e}", file=sys.stderr)

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python extract_table.py <path-to-pdf>")
    else:
        main(sys.argv[1])
```

**Değiştirmeniz gerekenler:**

- `initialize_engine(pdf_path)`: Seçtiğiniz kütüphane için motor örneğini oluşturun.  
- `engine.recognize_layout()` / `engine.run_postprocessor()`: Eğer farklı isimlendirmeler varsa doğru metod adlarını kullanın.

Scripti `python extract_table.py invoice.pdf` komutuyla çalıştırdığınızda, sonraki işlemler için hazır, sekme‑ayırmalı bir tablo çıktısı alırsınız.

---

## Görsel Açıklama

Aşağıda tespit hattının nasıl göründüğünü gösteren hızlı bir şema yer alıyor.  
![extract table from document diagram showing raw layout → post‑processor → clean table]  

*Alt metin:* *belgeden tablo çıkarma akış diyagramı*  

---

## Sık Sorulan Sorular & Köşe Durumlar

| Soru | Cevap |
|------|-------|
| **PDF birden fazla tablo içeriyorsa ne olur?** | `enhanced_layout.table` yalnızca ilk tespit edilen tabloyu içerebilir. Kütüphane destekliyorsa `enhanced_layout.tables` (çoğul) üzerinden döngü kurup aynı satır‑yineleme mantığını her tabloya uygulayın. |
| **Birleştirilmiş hücrelerle nasıl başa çıkılır?** | Post‑processor genellikle birleştirilmiş hücreleri ayrı girişlere genişletir. Eğer yapmazsa, motorun `merge_cells` bayrağını kontrol edin veya koordinatlarına göre yan yana hücreleri manuel olarak birleştirin. |
| **Taranmış PDF'lerden tablo çıkarabilir miyim?** | Evet, ancak layout tespitinden önce bir OCR adımı gerekir. Birçok SDK, taranmış belgeler için OCR + layout tespitini tek bir çağrıda (`recognize_layout()` taranmış dokümanda) birleştirir. |
| **Büyük toplular için performans sorunları?** | Sayfaları paralel işleyin (ör. `concurrent.futures` kullanarak). En ağır kısım OCR'dir; motor örneğini dosyalar arasında canlı tutarak ağır modellerin yeniden başlatılmasını önleyin. |
| **Ek bağımlılıklar kurmam gerekiyor mu?** | `pdfplumber` kullanıyorsanız `pip install pdfplumber` ile kurun. Ticari SDK'lar için satıcıların kurulum kılavuzunu izleyin. |

---

## Sonuç

Bu yazıda **belgeden tablo çıkarma** sürecini, layout tespiti, iyileştirme ve **tablo satırlarını yineleme** adımlarıyla nasıl gerçekleştireceğinizi gösterdik. Veriyi bir veri‑deposuna, rapor üretimine ya da sadece PDF'yi CSV'ye dönüştürmeye yönlendiriyor olsanız da, desen aynı kalır: tespit → temizle → yinele.

İleride keşfedebileceğiniz adımlar:

- **Pdf'den tabloları okuma** sırasında ek stil bilgileri (fontlar, renkler) elde etme.  
- Analiz için doğrudan **pandas DataFrame**'e aktarma.  
- Aynı hattı kullanarak **tabloları yeni bir PDF'e geri yazma** (ters akış).  

Kendi PDF'lerinizle scripti deneyin ve statik tabloları ne kadar hızlı aksiyon alınabilir verilere dönüştürebileceğinizi görün. İyi çıkarımlar!  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}