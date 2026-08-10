---
category: general
date: 2026-02-22
description: OCR metnini nasıl çıkaracağınızı ve AI sonrası işleme ile OCR doğruluğunu
  nasıl artıracağınızı öğrenin. Python'da adım adım bir örnekle OCR metnini kolayca
  temizleyin.
draft: false
keywords:
- how to extract OCR
- improve OCR accuracy
- clean OCR text
- OCR post‑processing
- AI OCR enhancement
language: tr
og_description: Basit bir Python iş akışı ve AI sonrası işleme kullanarak OCR metnini
  nasıl çıkaracağınızı, OCR doğruluğunu nasıl artıracağınızı ve OCR metnini nasıl
  temizleyeceğinizi keşfedin.
og_title: OCR Metnini Nasıl Çıkarılır – Adım Adım Rehber
tags:
- OCR
- AI
- Python
title: OCR Metnini Nasıl Çıkarılır – Tam Rehber
url: /tr/python/general/how-to-extract-ocr-text-complete-guide/
---

any images: none.

All good.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR Metni Nasıl Çıkarılır – Tam Programlama Öğreticisi

Hiç **OCR nasıl çıkarılır** diye merak ettiniz mi, taranmış bir belgeden yazım hataları ve kırık satırlarla dolu bir karmaşa elde etmeden? Yalnız değilsiniz. Birçok gerçek‑dünya projesinde OCR motorundan gelen ham çıktı karışık bir paragraf gibi görünür ve temizlemek bir iş gibi hissettirir.  

İyi haber? Bu rehberi izleyerek yapılandırılmış OCR verilerini çekmenin, bir AI post‑işlemcisi çalıştırmanın ve **temiz OCR metni** elde etmenin pratik bir yolunu göreceksiniz, bu metin sonraki analizler için hazır olacak. Ayrıca **OCR doğruluğunu artırma** tekniklerine de değineceğiz, böylece sonuçlar ilk seferde güvenilir olacak.

Önümüzdeki birkaç dakikada ihtiyacınız olan her şeyi ele alacağız: gerekli kütüphaneler, tam çalıştırılabilir bir betik ve yaygın tuzaklardan kaçınma ipuçları. Belirsiz “belgelere bak” kısayolları yok—sadece kopyalayıp yapıştırıp çalıştırabileceğiniz eksiksiz, bağımsız bir çözüm.

## Gereksinimler

- Python 3.9+ (kod tip ipuçları kullanıyor ancak daha eski 3.x sürümlerinde de çalışır)
- Yapılandırılmış bir sonuç döndürebilen bir OCR motoru (ör. `pytesseract` ile Tesseract ve `--psm 1` bayrağı, ya da blok/ satır meta verileri sunan ticari bir API)
- Bir AI post‑işlem modeli – bu örnek için basit bir fonksiyonla taklit edeceğiz, ancak OpenAI’nin `gpt‑4o-mini`, Claude veya metin kabul edip temizlenmiş çıktı dönen herhangi bir LLM ile değiştirebilirsiniz
- Test etmek için birkaç örnek görüntü satırı (PNG/JPG)

Bunlar hazırsa, başlayalım.

## OCR Nasıl Çıkarılır – İlk Alım

İlk adım, OCR motorunu çağırmak ve ona düz bir dize yerine **yapılandırılmış bir temsil** istemektir. Yapılandırılmış sonuçlar blok, satır ve kelime sınırlarını korur, bu da sonradan temizlemeyi çok daha kolay hâle getirir.

```python
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List

# Simple data classes mirroring a typical structured OCR response
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

def recognize_structured(image_path: str) -> StructuredResult:
    """
    Run Tesseract with the `--psm 1` layout mode to get block/line info.
    In a real engine you would get JSON directly; here we simulate it.
    """
    img = Image.open(image_path)

    # Tesseract's TSV output includes level, page_num, block_num, par_num, line_num, word_num, text…
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    current_block_idx = -1
    current_line_idx = -1

    for i, level in enumerate(tsv["level"]):
        if level == 3:  # block level
            result.blocks.append(Block())
            current_block_idx += 1
            current_line_idx = -1
        elif level == 4:  # line level
            result.blocks[current_block_idx].lines.append(Line(text=""))
            current_line_idx += 1

        # level 5 is word; concatenate words into the current line
        if level == 5:
            word = tsv["text"][i]
            if word.strip():
                line_obj = result.blocks[current_block_idx].lines[current_line_idx]
                line_obj.text += (word + " ")

    # Trim trailing spaces
    for block in result.blocks:
        for line in block.lines:
            line.text = line.text.strip()
    return result
```

> **Neden önemli:** Blokları ve satırları koruyarak paragrafların nerede başladığını tahmin etmek zorunda kalmayız. `recognize_structured` fonksiyonu, daha sonra bir AI modeline besleyebileceğimiz temiz bir hiyerarşi sağlar.

```python
# Demo call – replace with your own image path
structured_result = recognize_structured("sample_scan.png")
print("Before AI:", structured_result.blocks[0].lines[0].text)
```

Kod parçacığını çalıştırmak, OCR motorunun gördüğü gibi ilk satırı tam olarak yazdırır; bu genellikle “OCR” yerine “0cr” gibi hatalı tanımalara sahiptir.

## AI Post‑İşleme ile OCR Doğruluğunu Artırma

Şimdi ham yapılandırılmış çıktıya sahibiz, bunu bir AI post‑işlemcisine verelim. Amaç, yaygın hataları düzelterek, noktalama işaretlerini normalleştirerek ve gerektiğinde satırları yeniden bölerek **OCR doğruluğunu artırmaktır**.

```python
import openai  # Example: using OpenAI's API; replace with your provider

def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    """
    Sends each line to an LLM that returns a cleaned version.
    This simple loop can be parallelized for large documents.
    """
    api_key = "YOUR_OPENAI_API_KEY"
    openai.api_key = api_key

    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "You are an OCR cleanup assistant. Fix any spelling, spacing, "
                "or punctuation errors in the following line while preserving the original meaning:\n\n"
                f"\"{line.text}\""
            )
            response = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=200,
            )
            cleaned = response.choices[0].message.content.strip()
            line.text = cleaned
    return structured
```

> **Pro ipucu:** Bir LLM aboneliğiniz yoksa, çağrıyı yerel bir transformer (ör. `sentence‑transformers` + ince ayarlı düzeltme modeli) ya da kural‑tabanlı bir yaklaşımla değiştirebilirsiniz. Temel fikir, AI’nın her satırı izole şekilde görmesidir; bu genellikle **OCR metnini temizlemek** için yeterlidir.

```python
# Apply the AI post‑processor
structured_result = run_postprocessor(structured_result)
print("After AI:", structured_result.blocks[0].lines[0].text)
```

Şimdi çok daha temiz bir cümle görmelisiniz—yazım hataları düzeltildi, ekstra boşluklar kaldırıldı ve noktalama işaretleri düzeltildi.

## Daha İyi Sonuçlar İçin OCR Metnini Temizleme

AI düzeltmesinden sonra bile, son bir temizlik adımı uygulamak isteyebilirsiniz: ASCII olmayan karakterleri temizlemek, satır sonlarını birleştirmek ve birden fazla boşluğu tek bir boşluğa indirmek. Bu ekstra geçiş, çıktının NLP veya veritabanı alımı gibi sonraki görevler için hazır olmasını sağlar.

```python
import re

def final_cleanup(structured: StructuredResult) -> str:
    """
    Flattens the hierarchy into a single string and performs
    additional regex‑based cleaning.
    """
    lines = []
    for block in structured.blocks:
        for line in block.lines:
            # Remove any lingering non‑printable characters
            cleaned = re.sub(r"[^\x20-\x7E]", "", line.text)
            # Collapse multiple spaces
            cleaned = re.sub(r"\s+", " ", cleaned).strip()
            lines.append(cleaned)
    # Join blocks with double newline to preserve paragraph breaks
    return "\n\n".join(lines)

clean_text = final_cleanup(structured_result)
print("\n=== Cleaned OCR Text ===\n")
print(clean_text)
```

`final_cleanup` fonksiyonu, doğrudan bir arama indeksine, bir dil modeline veya CSV dışa aktarımına besleyebileceğiniz düz bir dize verir. Blok sınırlarını koruduğumuz için paragraf yapısı korunur.

## Kenar Durumları ve Ne‑Olursa‑Senaryoları

- **Çok‑sütun düzenleri:** Kaynağınızda sütunlar varsa, OCR motoru satırları karıştırabilir. TSV çıktısından sütun koordinatlarını tespit edebilir ve AI'ye göndermeden önce satırları yeniden sıralayabilirsiniz.
- **Latin dışı yazı sistemleri:** Çince veya Arapça gibi diller için, LLM'nin istemini dil‑spesifik düzeltme talep edecek şekilde değiştirin veya o yazı sisteminde ince ayarlı bir model kullanın.
- **Büyük belgeler:** Her satırı ayrı ayrı göndermek yavaş olabilir. Satırları toplu gönderin (ör. istekte 10 satır) ve LLM'nin temizlenmiş satırların bir listesini döndürmesine izin verin. Token limitlerine uymayı unutmayın.
- **Eksik bloklar:** Bazı OCR motorları sadece düz bir kelime listesi döndürür. Bu durumda, benzer `line_num` değerlerine sahip kelimeleri gruplayarak satırları yeniden oluşturabilirsiniz.

## Tam Çalışan Örnek

Her şeyi bir araya getirerek, uçtan uca çalıştırabileceğiniz tek bir dosya burada. Yer tutucuları kendi API anahtarınız ve görüntü yolunuzla değiştirin.

```python
# ocr_cleanup.py
import re
import pytesseract
from PIL import Image
from dataclasses import dataclass, field
from typing import List
import openai

# ---------- Data structures ----------
@dataclass
class Line:
    text: str

@dataclass
class Block:
    lines: List[Line] = field(default_factory=list)

@dataclass
class StructuredResult:
    blocks: List[Block] = field(default_factory=list)

# ---------- Step 1: Extract OCR ----------
def recognize_structured(image_path: str) -> StructuredResult:
    img = Image.open(image_path)
    tsv = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT)

    result = StructuredResult()
    cur_block = -1
    cur_line = -1

    for i, lvl in enumerate(tsv["level"]):
        if lvl == 3:                # block
            result.blocks.append(Block())
            cur_block += 1
            cur_line = -1
        elif lvl == 4:              # line
            result.blocks[cur_block].lines.append(Line(text=""))
            cur_line += 1
        elif lvl == 5:              # word
            word = tsv["text"][i]
            if word.strip():
                result.blocks[cur_block].lines[cur_line].text += word + " "

    # Trim spaces
    for blk in result.blocks:
        for ln in blk.lines:
            ln.text = ln.text.strip()
    return result

# ---------- Step 2: AI post‑processor ----------
def run_postprocessor(structured: StructuredResult) -> StructuredResult:
    openai.api_key = "YOUR_OPENAI_API_KEY"
    for block in structured.blocks:
        for line in block.lines:
            prompt = (
                "Correct OCR errors (spelling, spacing, punctuation) in this line:\n"
                f"\"{line.text}\""
            )
            resp = openai.ChatCompletion.create(
                model="gpt-4o-mini",
                messages=[{"role": "user", "content": prompt}],
                temperature=0.0,
                max_tokens=150,
            )
            line.text = resp.choices[0].message.content.strip()
    return structured

# ---------- Step 3: Final cleanup ----------
def final_cleanup(structured: StructuredResult) -> str:
    out = []
    for block in structured.blocks:
        for line in block.lines:
            txt = re.sub(r"[^\x20-\x7E]", "", line.text)   # strip non‑ASCII
            txt = re.sub(r"\s+", " ", txt).strip

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}