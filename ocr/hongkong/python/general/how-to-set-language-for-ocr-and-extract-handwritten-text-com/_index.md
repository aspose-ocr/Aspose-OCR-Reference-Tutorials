---
category: general
date: 2026-03-26
description: 如何在 OCR 引擎中設定語言並從圖像中提取手寫文字 – 逐步教學將圖像轉換為文字。
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: zh-hant
og_description: 如何在 OCR 引擎中設定語言並從圖像中提取手寫筆記。學習在數分鐘內將圖像轉換為文字。
og_title: 如何設定 OCR 語言 – 輕鬆擷取手寫文字
tags:
- OCR
- Python
- Image Processing
title: 如何設定 OCR 語言並擷取手寫文字 – 完整指南
url: /zh-hant/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何設定 OCR 語言並擷取手寫文字 – 完整指南

有沒有想過 **如何設定語言** 在你的 OCR 引擎上，讓它真的能理解你需要的字元？也許你有一張雜貨清單、會議筆記或是看起來模糊的圖表照片，卻無法擷取文字。好消息是？你不需要電腦視覺博士——只要幾行 Python 以及正確的旗標設定。

在本教學中，我們將逐步說明如何 **擷取手寫文字** 從 PNG 圖片，將該圖像轉換為純文字，並解釋每個設定背後的「原因」。完成後，你將能在任何專案中辨識手寫筆記，無論是筆記應用程式或是批次處理管線。

> **你需要的條件**  
> • Python 3.8+（程式碼同樣支援 3.10）  
> • `ocr` 函式庫（或任何提供 `OcrEngine` 的相容封裝）  
> • 一張範例圖像，例如 `note_handwritten.png`——任何含有擴充拉丁字元的圖像皆可。

讓我們開始吧。

---

## 如何設定語言並啟用手寫辨識

首先，你必須告訴 OCR 引擎它應該預期哪種字母表。如果跳過此步驟，引擎會預設使用通用集合，常會誤認帶重音的字母或特殊符號。

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**為什麼這很重要：**  
- **ExtendedLatin** 包含像 “ñ”、 “ø” 與 “ç” 這類字元，這些在許多歐洲筆記中很常見。  
- `recognize_handwritten` 旗標會將底層模型從印刷文字 OCR 切換為訓練於手寫筆劃的神經網路。若未啟用，引擎會把你的塗鴉當成雜訊。

> **專業提示：** 若你處理多語言文件，請為每種語言建立獨立的引擎，或在每次呼叫前動態切換 `ocr_engine.language`。這樣可避免載入未使用字元集的額外開銷。

![OCR 引擎設定畫面示意圖，說明如何設定語言](/images/ocr-set-language.png "在 OCR 引擎上設定語言")

*圖片替代文字： “在 OCR 引擎設定畫面上設定語言”。*

---

## 從 PNG 圖像擷取手寫文字

既然引擎已知道要尋找什麼，現在是時候提供圖像給它。`recognize_image` 方法會回傳一個豐富的結果物件；`text` 屬性則包含你關心的純文字字串。

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

執行腳本時，你應該會看到類似以下的輸出：

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

此輸出證明你已成功 **將圖像轉換為文字**，且引擎遵守了你提供的語言設定。

**常見陷阱**  
- **路徑錯誤** – 再次確認檔案位置；缺少檔案會拋出 `FileNotFoundError`。  
- **低解析度圖像** – 手寫 OCR 在低於 300 dpi 時表現不佳。若輸出雜亂，請放大或重新掃描。  
- **顏色反轉** – 若背景較暗而墨水較淡，先反轉顏色（可使用 `Pillow` 協助）。

---

## 使用輔助函式將圖像轉換為文字

如果你打算對數十個檔案執行 OCR，請將邏輯封裝成可重用的函式。這也讓程式碼更易於測試與整合至其他管線。

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

此輔助函式將 **如何擷取手寫** 的邏輯抽離，使你能在 Flask 端點、CLI 工具或批次工作中呼叫，而無需每次都重新編寫設定。

---

## 在實務情境中辨識手寫筆記

以下列出幾種情況，你可能需要 **辨識手寫筆記**，以及此設定如何因應：

| 情境 | 為何語言重要 | 建議調整 |
|----------|---------------------|-----------------|
| **多語言雜貨清單** | 項目可能包含重音字元（例如 “crème”） | 依清單切換 `ocr_engine.language`，或若支援則使用 `ocr.Language.AutoDetect` |
| **教室白板照片** | 粉筆可能產生淡淡的筆劃 | 在送入引擎前提升圖像對比度 |
| **醫療處方** | 手寫字跡極度雜亂 | 結合 OCR 與藥品名稱的拼寫校正字典 |

在每種情況下，核心步驟——**如何設定語言**、啟用手寫模式，以及呼叫 `recognize_image`——皆相同。這種一致性使方法既穩健又易於維護。

---

## 邊緣案例與進階調整

1. **批次處理** – 只載入一次引擎，遍歷檔案，僅在需要時變更 `language` 屬性。這可減少初始化的開銷。  
2. **非拉丁文字** – 若需處理西里爾文或阿拉伯文，將 `ExtendedLatin` 替換為相應的列舉（例如 `ocr.Language.Cyrillic`）。同樣的模式適用。  
3. **部分辨識** – 有時對於極短的筆劃，引擎會回傳空字串。快速的合理性檢查（`if not result.text.strip(): …`）可讓你回退至次要模型或請使用者重新掃描。  
4. **效能分析** – 對於大型資料集，計時 `recognize_image` 呼叫。若成為瓶頸，考慮使用 `concurrent.futures.ThreadPoolExecutor` 進行平行化。

---

## 完整範例程式

以下是完整腳本，你可以直接複製貼上至名為 `handwritten_ocr.py` 的檔案。它包含參數解析，讓你可從命令列指向任意圖像。

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

執行方式如下：

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

你應該會看到與前述片段相同的輸出，證實你已成功 **將圖像轉換為文字** 並 **辨識手寫筆記**。

---

## 結論

我們已說明了在 OCR 引擎上 **如何設定語言**、啟用手寫文字旗標，並建立可重用的函式以 **擷取手寫文字** 從任何圖像。依照上述步驟，你即可可靠地 **將圖像轉換為文字**，無論是處理單一筆記或是龐大的掃描文件檔案庫。

接下來，試著使用不同的語言套件、批次處理整個資料夾的圖像，或將此邏輯整合至回傳 JSON 結果的 Web 服務中。基本原則不變，而 `ocr` 函式庫的彈性讓你能因應幾乎所有使用情境。

對於邊緣案例、效能或將腳本擴展至其他語言有任何問題嗎？在 GitHub 留言或私訊我吧——祝開發愉快！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}