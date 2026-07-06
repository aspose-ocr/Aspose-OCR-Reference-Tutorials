---
category: general
date: 2026-06-19
description: OCR'yi adım adım nasıl çalıştırılır ve düz metin OCR teknikleriyle OCR
  doğruluğunu nasıl artırılır. Güvenilir metin çıkarımı için hızlı bir iş akışı öğrenin.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: tr
og_description: OCR'yi verimli bir şekilde çalıştırma. Bu öğreticide, düz metin OCR
  ve AI sonrası işleme kullanarak OCR doğruluğunu nasıl artıracağınız gösteriliyor.
og_title: Python'da OCR Nasıl Çalıştırılır – Tam Kılavuz
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Python'da OCR Nasıl Çalıştırılır – Tam Rehber
url: /tr/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Python'da OCR Nasıl Çalıştırılır – Tam Kılavuz

Hiç **OCR nasıl çalıştırılır** sorusunu, ayarlar üzerinde saatler harcamadan toplu taranmış PDF'lerde merak ettiniz mi? Yalnız değilsiniz. Birçok projede ilk engel, bir görüntüden güvenilir metin elde etmektir ve titiz bir geçiş ile temiz bir çıkarım arasındaki fark genellikle birkaç akıllı adıma dayanır.

Bu rehberde, **OCR çalıştıran** ve aynı zamanda **OCR doğruluğunu artıran** hızlı bir düz metin geçişi, düzen‑duyarlı ikinci bir geçiş ve bir AI‑güçlü post‑işlemciyi birleştiren pratik dört adımlı bir işlem hattını ele alacağız. Sonunda çalıştırmaya hazır bir betiğiniz, her aşamanın neden önemli olduğuna dair net bir açıklamanız ve çok‑sütunlu sayfalar ya da gürültülü taramalar gibi kenar durumlarını ele almanız için ipuçlarınız olacak.

---

## Gerekenler

İlerlemeye başlamadan önce aşağıdakilere sahip olduğunuzdan emin olun:

- **Python 3.9+** – kod tip ipuçları ve f‑string'ler kullanıyor.
- **Tesseract OCR** kurulu ve `tesseract` komut satırı aracılığıyla erişilebilir. (Ubuntu’da: `sudo apt install tesseract-ocr`; Windows’da resmi depodan yükleyiciyi indirin.)
- **pytesseract** sarmalayıcısı (`pip install pytesseract`).
- Bir **AI post‑işleme kütüphanesi** – bu örnek için hafif bir `ai` modülünün `run_postprocessor` sunduğunu varsayacağız. Tercihinize göre OpenAI‑nin GPT‑4 API'si ya da yerel bir LLM ile değiştirin.
- Test etmek için birkaç örnek görüntü ya da PDF.

Hepsi bu. Ağır çerçeveler, Docker akrobatikası yok. Sadece birkaç pip kurulumu ve hazırsınız.

---

## Adım 1: Hızlı Düz‑Metin OCR Geçişi Yapın

Çoğu geliştiricinin gözden kaçırdığı ilk şey, *düz metin* OCR çalıştırmasının ışık hızıyla gerçekleşmesi ve size hızlı bir mantık kontrolü sunmasıdır. `engine.Recognize()` çağrısıyla herhangi bir düzen meta verisi olmadan ham karakterleri çekeceğiz. İşte **düz metin OCR** demek bu demektir.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Neden önemli:*  
- **Hız** – 300 dpi bir sayfada düz geçiş genellikle bir saniyeden az sürer.  
- **Temel Çizgi** – Daha sonraki yapılandırılmış çıktıyı bu temel çizgiyle karşılaştırarak bariz hataları görebilirsiniz.  
- **Hata Yakalama** – Düz geçiş tamamen başarısız olursa (ör. tamamen anlamsız karakterler), görüntü kalitesinin çok düşük olduğunu anlarsınız ve erken çıkabilirsiniz.

---

## Adım 2: Ayrıntılı Düzen‑Duyarlı OCR Geçişi Yapın

Düz metin harika, ama *kelimenin sayfada nerede* olduğunu atar. Faturalar, formlar ya da çok‑sütunlu dergiler için koordinatlar, satır numaraları ve hatta font bilgisi gerekir. İşte `engine.RecognizeStructured()` devreye giriyor.

Aşağıda Tesseract’in **TSV** çıktısını ince bir sarmalayıcı olarak kullanan, sayfalar → satırlar → kelimeler hiyerarşisini koruyan bir örnek bulunuyor.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Bunu yapmamızın nedeni:*  
- **Koordinatlar** sayesinde çıkarılan metni orijinal görüntüde vurgulama ya da kara listeleme gibi işlemler için geri haritalayabilirsiniz.  
- **Satır gruplama** orijinal düzeni korur; bu, tabloları ya da sütunları yeniden oluşturmanız gerektiğinde kritiktir.  
- Bu geçiş düz geçişten biraz daha yavaştır, ama çoğu belge için birkaç saniye içinde tamamlanır.

---

## Adım 3: AI Post‑İşlemciyle OCR Hatalarını Düzeltin

En iyi OCR motoru bile hatalar yapar—“rn” ile “m”, eksik diakritikler ya da bölünmüş kelimeler gibi. Bir AI modeli ham dizeyi ve yapılandırılmış veriyi inceleyerek tutarsızlıkları bulur ve orijinal koordinatları koruyarak metni yeniden yazar.

Aşağıda **mock** bir uygulama var; gerçek bir LLM çağrısı ile gövdeyi değiştirin.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Bu adım OCR doğruluğunu nasıl artırır:*  
- **Bağlamsal düzeltmeler** – AI, çevredeki kelimelere bakarak “l0ve” muhtemelen “love” olduğunu anlayabilir.  
- **Koordinat koruması** – Düzen bilgisi korunur, böylece sonraki görevler (PDF açıklama gibi) doğru kalır.  
- **Yinelemeli iyileştirme** – Post‑işlemciyi birden fazla kez çalıştırarak her geçişte daha fazla hatayı temizleyebilirsiniz.

---

## Adım 4: Düzeltlenmiş, Yapılandırılmış Çıktıyı Döngüyle İşleyin

Artık temizlenmiş bir yapımız olduğuna göre, nihai metni almak çok basit. Aşağıda her satırı yazdırıyoruz, ama aynı zamanda CSV’ye, veritabanına ya da aranabilir bir PDF’ye de yazabilirsiniz.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Beklenen çıktı** (basit tek‑sayfalı bir fatura varsayarak):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Satır sonları ve sütun sırası korunmuş, “$15.00” gibi yaygın OCR hatalarının AI adımıyla “$15,00” yerine doğru şekilde düzeltildiğine dikkat edin.

---

## Bu İş Akışı **OCR Doğruluğunu Nasıl Artırır**?

| Aşama | Ne Düzeltir | Neden Önemlidir |
|------|-------------|-----------------|
| **Plain text OCR** | Okunamayan sayfaları erken tespit eder | Umutsuz girdileri atlayarak zaman tasarrufu sağlar |
| **Structured OCR** | Düzeni, koordinatları yakalar | Sonraki görevleri (vurgulama, kara listeleme) mümkün kılar |
| **AI post‑processor** | Yazım hatalarını düzeltir, bölünmüş kelimeleri birleştirir, sayıları düzeltir | Gürültülü taramalarda karakter‑seviyesi doğruluğu ~%85'ten >%95'e çıkarır |
| **Iteration** | Ayarlanmış parametrelerle yeniden çalıştırmanıza izin verir | Belirli belge tipleri için işlem hattını ince ayar yapar |

Bu üç kavramı—**düz metin OCR**, düzen‑duyarlı çıkarım ve AI düzeltme—birleştirerek, sıfırdan özel bir sinir ağı yazmadan **OCR doğruluğunu önemli ölçüde artıran** sağlam bir çözüm elde edersiniz.

---

## Yaygın Tuzaklar ve Pro İpuçları

- **Tuzak:** Düşük çözünürlüklü bir görüntüyü (≤150 dpi) Tesseract’e vermek, bozuk çıktı üretir.  
  **Pro ipucu:** `Pillow` ile ön‑işlem yapın—`Image.convert('L')` ve `Image.filter(ImageFilter.MedianFilter())` uygulayın OCR’dan önce.

- **Tuzak:** AI post‑işlemci, alan‑spesifik terimleri (ör. “SKU123”) yanlışlıkla yeniden yazar.  
  **Pro ipucu:** Terimlerin bir beyaz listesini oluşturun ve bunu LLM’ye ya da `pyspellchecker` gibi bir yazım denetleyici kütüphanesine iletin.

- **Tuzak:** Çok‑sütunlu sayfalar tek bir satıra birleşir.  
  **Pro ipucu:** Tesseract’in TSV çıktısındaki `block_num` alanını kullanarak sütun sınırlarını tespit edin ve satırları buna göre bölün.

- **Tuzak:** Büyük PDF'ler tüm sayfalar aynı anda yüklendiğinde bellek patlamasına neden olur.  
  **Pro ipucu:** Sayfaları artımlı işleyin—`pdf2image.convert_from_path(..., first_page=n, last_page=n)` döngüsüyle ilerleyin.

---

## İş Akışını Genişletmek

Daha ileri adımlarla ilgileniyorsanız, aşağıdaki iyileştirmeleri değerlendirebilirsiniz:

1. **Toplu işleme** – Tüm betiği bir fonksiyon içinde paketleyin, bir dizini dolaşarak binlerce dosyayı `concurrent.futures` ile paralel işleyin.  
2. **Dil modelleri** – Basit difflib heuristiğini OpenAI‑nin `gpt‑4o` çağrısı ya da yerel bir LLaMA modeli ile değiştirerek daha zengin bağlamsal düzeltmeler elde edin.  
3. **Dışa aktarma formatları** – Düzeltlenmiş yapıyı aranabilir bir PDF’ye yazın.

## Bir Sonraki Öğrenmeniz Gerekenler

Aşağıdaki öğreticiler, bu kılavuzda gösterilen tekniklere dayalı yakın konuları kapsar. Her kaynak, adım‑adım açıklamalar ve tam çalışan kod örnekleri içerir; böylece ek API özelliklerini ustalaşabilir ve projelerinizde alternatif uygulama yaklaşımlarını keşfedebilirsiniz.

- [Aspose.OCR Kullanarak Görüntü Metnini Dil Seçimiyle OCR Yapma](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Aspose.OCR ile Java’da Gelişmiş OCR Teknikleri](/ocr/english/java/advanced-ocr-techniques/)
- [OCR Doğruluğunu Artır – Alanları Algıla Modu](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}