---
category: general
date: 2026-06-16
description: 快速在 Python 中美化列印 JSON，並學習如何將 JSON 轉換為 dict 或載入 JSON 字串以進行資料操作。逐步教學。
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: zh-hant
og_description: 在 Python 中美化 JSON 輸出，並即時了解如何將 JSON 轉換為 dict 或載入 JSON 字串。數分鐘內掌握 JSON
  處理技巧。
og_title: Python JSON 美化列印 – 完整格式化與轉換指南
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: Python 美化列印 JSON – 完整格式化與轉換指南
url: /zh-hant/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 美化 JSON Python – 完整格式化與轉換指南

是否曾經需要 **pretty print JSON Python**，卻發現輸出總是只有一行、難以閱讀？你並不孤單。在許多專案中，原始的 JSON 字串往往雜亂無章，讓除錯彷彿在大海撈針。  

好消息是？只要使用幾個內建函式，就能把這團混亂的資料轉換成整齊縮排的視圖，接著 **convert JSON to dict** 以便順暢地進行後續處理。在本教學中，我們會一步步說明——從在 Python 中載入 JSON 字串到遍歷其資料——讓你專注於邏輯，而不是與格式奮戰。

## 本教學涵蓋內容

- 如何使用 `json.dumps` 搭配 `indent` 參數 **pretty print JSON Python**。  
- 如何 **load JSON string Python** 成為原生字典。  
- 將得到的字典轉換成實用的 Python 物件，並示範列印每個單字及其信心分數的實作範例。  
- 常見陷阱（例如非 ASCII 字元處理）與快速解決方式。  
- 完整可執行的腳本，直接複製貼上即可使用與客製化。

閱讀完本指南後，你將能將任何 JSON 資料轉換為人類可讀的格式，並以純 Python 操作——不需要額外的函式庫。

---

## 前置條件

- Python 3.8 或更新版本（`json` 模組是標準函式庫的一部份）。  
- 具備字典與迴圈的基本概念。  
- 可選：一個 OCR 引擎或任何會回傳 JSON 的服務——本範例使用模擬的 `engine.recognize()` 呼叫，你也可以自行替換成自己的資料來源。

---

## Step 1: Perform OCR (or Any JSON‑Generating) Recognition

首先，你必須取得可序列化為 JSON 的結果。在許多電腦視覺工作流程中，OCR 引擎會輸出可序列化為 JSON 的結構化物件。以下是一個最小的佔位範例：

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **為什麼這一步很重要：**  
> 即使你不是在做 OCR，通常也會從 API、檔案或訊息佇列收到資料。該物件必須能序列化為 JSON，才能 **pretty print**。

---

## Step 2: Pretty Print JSON Python

現在把原始資料轉成縮排整齊的字串。`indent` 參數負責完成大部分工作。

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

輸出將會是這樣：

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **小技巧：** 若想要更寬的間距，可使用 `indent=4`；若想依字母順序排列鍵，加入 `sort_keys=True`。

---

## Step 3: Load JSON String Python → Native Dictionary

美化後的字串適合人類閱讀，但 Python 在實際運算時更喜歡字典。這一步就是將 **load JSON string Python** 成為原生結構。

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

你會看到：

```
✅ Loaded dict type: <class 'dict'>
```

> **為什麼要這麼做：**  
> 字典提供 O(1) 的查詢、可變動的資料，以及與 Python 生態系的無縫整合。直接操作 JSON 字串會迫使你進行繁瑣的字串解析。

---

## Step 4: Iterate Over Recognized Words – A Real‑World Use Case

讓我們取出每個單字及其信心分數。此範例同時展示 **convert json to dict**（已取得的字典）以及實務的遍歷方式。

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

預期輸出：

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **邊緣案例提示：** 若 JSON 可能缺少 `"words"` 鍵，請防止 `KeyError`：

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## Step 5: Handling Non‑ASCII Characters (Unicode Support)

OCR 引擎常會回傳像 “é” 或 “ü” 之類的字元。預設的 `json.dumps` 會把它們轉成 `\u00e9`。若想保留可讀的字形，請傳入 `ensure_ascii=False`。

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

現在輸出會顯示 **café** 而非轉義字元。這在之後 **convert json to dict** 時尤為重要，因為字典會包含正確的 Unicode 字串。

---

## Step 6: Saving and Reloading the Pretty‑Printed JSON (Optional)

有時你會想把格式化好的 JSON 存檔，以便日後檢視。

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

檔案將會包含縮排整齊的 JSON，而 `json.load` 會自動把它解析回字典。

---

## Step 7: Putting It All Together – A One‑File Solution

以下是一個自包含的腳本，整合了上述所有步驟。可直接存成 `pretty_json_demo.py` 並執行。

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

執行方式：

```bash
python pretty_json_demo.py
```

你會看到美化後的 JSON、字典類型、每個單字與其信心分數，以及保存至 `pretty_output.json` 的 Unicode 友好版本。  

**這就是完整流程**——從原始 OCR 輸出到乾淨、可操作的 Python 字典。

---

## Frequently Asked Questions (FAQs)

| 問題 | 答案 |
|----------|--------|
| **需要額外的函式庫嗎？** | 不需要。內建的 `json` 模組同時支援美化與載入。 |
| **如果我的 JSON 很大怎麼辦？** | 使用 `json.dump` 搭配檔案物件，以避免一次載入全部資料；仍可設定 `indent` 產生美化檔案。 |
| **可以排序鍵嗎？** | 可以——在 `json.dumps` 中加入 `sort_keys=True`，可得到確定的順序，對 diff‑based 測試很有幫助。 |
| **如何處理格式錯誤的 JSON？** | 把 `json.loads` 包在 `try/except json.JSONDecodeError` 區塊，並記錄有問題的字串。 |
| **有更快的替代方案嗎？** | 對於超大負載，可考慮 `orjson` 或 `ujson` 等更快的函式庫，但它們不支援 `indent` 產生美化輸出。 |

## What Should You Learn Next?

以下教學與本指南的技巧密切相關，能幫助你進一步掌握 API 功能並探索其他實作方式：

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cómo usar Aspose OCR para obtener resultados JSON en reconocimiento de imágenes](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Wie man Aspose OCR für JSON‑Ergebnisse bei der Bilderkennung verwendet](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}