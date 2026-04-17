---
category: general
date: 2026-03-26
description: 學習如何對阿拉伯語 PNG 圖像執行 OCR，快速提取阿拉伯文字。本指南示範如何使用一步一步的 Python 程式碼將圖像轉換為文字。
draft: false
keywords:
- how to run ocr
- extract arabic text
- recognize arabic text
- convert image to text
- extract text from png
language: zh-hant
og_description: 如何在阿拉伯語 PNG 圖像上執行 OCR？請參考本完整指南，學習如何擷取阿拉伯語文字、辨識阿拉伯語文字，並使用 Python 將圖像轉換為文字。
og_title: 如何對阿拉伯文 PNG 進行 OCR – 從圖片提取文字
tags:
- OCR
- Python
- Arabic
title: 如何對阿拉伯語 PNG 圖片執行 OCR – 從圖像中提取文字
url: /zh-hant/python-java/general/how-to-run-ocr-on-arabic-png-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 如何在阿拉伯語 PNG 上執行 OCR – 從圖像提取文字

有沒有想過 **如何在包含阿拉伯文字的圖像上執行 OCR**？也許你手上有掃描的收據、歷史手稿，或只是社交媒體貼文的螢幕截圖，且需要將文字轉成可搜尋的格式。你並不孤單——全球的開發者在處理從右至左語言時都會遇到這個問題。

在本教學中，我們將逐步示範一個完整且可執行的範例，說明 **如何在 PNG 檔案上執行 OCR**、擷取阿拉伯文字，並將結果印出到主控台。沒有模糊的「請參考文件」連結；只有你可以直接複製貼上的程式碼，以及每一行程式碼意義的說明。完成後，你將能可靠地 **將圖像轉換為文字**，即使來源是棘手的阿拉伯語 PNG。

> **你將學會**
> - 為阿拉伯語設定 Python OCR 引擎
> - 載入 PNG 圖像並處理常見陷阱
> - 辨識阿拉伯文字並驗證輸出
> - 提供 **擷取阿拉伯文字** 從不同影像品質的技巧

在開始之前，請確保已安裝 Python 3.8 以上，且有最新版本的 `ocr` 套件（即範例中使用的那個）。如果你使用虛擬環境，請立即啟動它——這樣可以保持相依性整潔。

## 前置條件

- Python 3.8 或更新版本  
- `ocr` 套件（`pip install ocr‑engine` – 請以實際套件名稱取代）  
- 一張阿拉伯語 PNG 圖像（`arabic_doc.png`），放在可參照的位置  
- 基本熟悉 Python 函式與類別  

就這樣。沒有重量級框架，沒有 Docker 容器——只有純粹的 Python。

## 步驟 1：安裝與匯入 OCR 函式庫

首先，我們需要 OCR 引擎本身。這個函式庫提供一個 `OcrEngine` 類別，具有直觀的 API。

```python
# Install the library (run once in your terminal)
# pip install ocr-engine   # <-- replace with the correct package name

# Import the necessary classes
import ocr
from ocr import Imaging
```

*為什麼要單獨匯入 `Imaging`？* `Imaging` 子模組提供便利的 `Image.load` 方法，能直接支援 PNG、JPEG 與 TIFF。若省略此步驟，必須自行處理原始位元組，對大多數使用情境而言是多餘的。

## 步驟 2：建立 OCR 引擎實例

現在我們建立引擎的實例。可以把這個物件想像成會處理圖像的「大腦」。

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

> **專業提示：** 若打算連續處理多張圖像，請重複使用同一個 `ocr_engine` 實例。它會快取語言模型，從而加速後續的辨識。

## 步驟 3：設定語言為阿拉伯語

阿拉伯語不是拉丁字母；它有自己的字元集、從右至左的書寫方向，以及依上下文變形的特性。因此必須明確告訴引擎要載入哪個語言模型。

```python
# Step 3: Set the language to Arabic (language code "ar")
ocr_engine.set_language("ar")
```

如果忘記這行程式碼，引擎會預設使用英文模型，導致輸出亂碼——這是我常見到的問題。

## 步驟 4：載入 PNG 圖像

這裡才是真正開始 **將圖像轉換為文字** 的部分。我們將載入包含阿拉伯文字的 PNG 檔案。

```python
# Step 4: Load the image that contains the Arabic text
image_path = "YOUR_DIRECTORY/arabic_doc.png"   # replace with your actual path
ocr_engine.set_image(Imaging.Image.load(image_path))
```

### 常見邊緣案例

| 問題 | 徵狀 | 解決方法 |
|-------|---------|-----|
| 圖像太暗 | 輸出包含大量空白 | 使用 Pillow 前處理 (`ImageEnhance.Brightness`) |
| PNG 含有 Alpha 通道 | 某些 OCR 引擎會誤讀透明像素 | 載入前先轉換為 RGB (`image.convert("RGB")`) |
| 文字旋轉 | 辨識出的文字上下顛倒 | 在傳遞給引擎前旋轉圖像 (`image.rotate(90, expand=True)`) |

## 步驟 5：執行辨識程序

所有設定完成後，我們最終請引擎執行辨識工作。

```python
# Step 5: Run the recognition process
ocr_result = ocr_engine.recognize()
```

`recognize` 方法會回傳一個物件，內含原始 Unicode 字串、信心分數與邊界框。對大多數開發者而言，純文字已足夠。

## 步驟 6：輸出辨識出的阿拉伯文字

現在我們將結果印出。在實際應用中，你可能會寫入檔案、資料庫，或傳給翻譯 API。

```python
# Step 6: Output the recognized text
print(ocr_result.get_text())
```

執行腳本後，應該會在主控台看到阿拉伯字元（請確認終端機支援 Unicode）。若出現問號或空字串，請再次檢查語言設定與圖像品質。

### 預期輸出

```
هذا نص عربي من صورة PNG تم استخراجها باستخدام OCR.
```

如果輸出與上方範例相似，恭喜你——已成功 **從 PNG 擷取阿拉伯文字**！

## 完整範例程式

以下是完整腳本，可直接複製貼上。請將 `YOUR_DIRECTORY/arabic_doc.png` 替換為你自己的檔案路徑。

```python
import ocr
from ocr import Imaging

def main():
    # Create OCR engine
    ocr_engine = ocr.OcrEngine()
    
    # Set Arabic language
    ocr_engine.set_language("ar")
    
    # Load the PNG image
    image_path = "YOUR_DIRECTORY/arabic_doc.png"
    ocr_engine.set_image(Imaging.Image.load(image_path))
    
    # Recognize text
    ocr_result = ocr_engine.recognize()
    
    # Print the extracted Arabic text
    print(ocr_result.get_text())

if __name__ == "__main__":
    main()
```

使用 `python run_ocr.py`（或你命名的檔案）執行。若所有套件正確安裝，將會在主控台看到阿拉伯語句子。

## 如何在不同影像格式上執行 OCR

相同程式碼同樣適用於 JPEG、TIFF 或 BMP——只要更改檔案副檔名即可。`Image.load` 方法會自動偵測格式，讓你可以 **將圖像轉換為文字**，無需額外程式碼。

```python
# Example for a JPEG file
ocr_engine.set_image(Imaging.Image.load("sample.jpg"))
```

請記住，來源圖像的品質會極大影響 **辨識阿拉伯文字** 步驟的準確度。高解析度、低壓縮的圖像能提供最佳結果。

## 從 PNG 擷取文字：提升準確度的技巧

1. **DPI 重要** – 目標至少 300 dpi。較低 DPI 常導致遺漏字元。  
2. **對比度為王** – 使用影像處理工具（例如 OpenCV）在送入 OCR 引擎前提升對比度。  
3. **除噪** – 小雜點會干擾模型，使用中值濾波可改善。  

以下是一段使用 Pillow 在 OCR 前改善 PNG 的快速程式碼：

```python
from PIL import Image, ImageEnhance, ImageFilter

def preprocess_png(path):
    img = Image.open(path).convert("L")          # grayscale
    img = ImageEnhance.Contrast(img).enhance(2)  # boost contrast
    img = img.filter(ImageFilter.MedianFilter()) # denoise
    return img

# Use the preprocessed image
prepped = preprocess_png("arabic_doc.png")
ocr_engine.set_image(Imaging.Image.from_pil(prepped))
```

## 常見問答

**Q: 這能用於除阿拉伯語之外的其他從右至左語言嗎？**  
A: 當然可以。只要將語言代碼改成相應的（`"ar"` → `"he"` 代表希伯來語，`"fa"` 代表波斯語），引擎就會載入對應模型。

**Q: 若要從資料夾中的多個 PNG 擷取文字該怎麼做？**  
A: 迭代檔案，重複使用同一個 `ocr_engine` 實例，將結果收集到列表或寫入各自的 `.txt` 檔案。

**Q: 能取得每個單字的信心分數嗎？**  
A: 可以。`ocr_result` 通常提供 `get_confidences()` 方法，將每個分數與相對應的單字配對，即可進行品質控制。

## 往後的步驟

既然你已掌握 **如何在阿拉伯語 PNG 上執行 OCR**，可以考慮以下後續想法：

- **批次處理：** 結合 `os.listdir` 於腳本中，**從整個目錄擷取阿拉伯文字**。  
- **後處理：** 使用 `arabic_reshaper` 與 `python-bidi` 套件，正確在 PDF 中顯示從右至左的輸出。  
- **整合：** 將擷取的文字輸入搜尋索引（例如 Elasticsearch），使掃描文件可被搜尋。  

上述每個主題皆以本教學的基礎為出發點，能協助你將簡單的 **將圖像轉換為文字** 程式碼升級為可投入生產的工作流程。

---

![如何在阿拉伯語 PNG 上執行 OCR](

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}