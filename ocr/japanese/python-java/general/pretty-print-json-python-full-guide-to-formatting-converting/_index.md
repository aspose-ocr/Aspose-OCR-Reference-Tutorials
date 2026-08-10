---
category: general
date: 2026-06-16
description: PythonでJSONをすばやく整形表示し、JSONを辞書に変換する方法やデータ操作のためにJSON文字列をロードする方法を学びましょう。ステップバイステップのチュートリアルです。
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: ja
og_description: PythonでJSONを整形表示し、JSONをdictに変換する方法やJSON文字列をロードする方法をすぐに確認できます。数分でJSON操作をマスターしましょう。
og_title: PythonでJSONを整形表示 – 完全フォーマット＆変換ガイド
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
title: PythonでJSONを整形表示 – フォーマットと変換の完全ガイド
url: /ja/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Pretty Print JSON Python – Full Guide to Formatting & Converting

JSON を **pretty print** したいとき、出力が一行の読めない文字列になってしまうことはありませんか？ 多くのプロジェクトで、生の JSON 文字列はごちゃごちゃした状態で、デバッグがまるで干し草の中の針を探すように困難です。  

良いニュースは、組み込み関数を数個使うだけで、混沌としたデータをきれいにインデントされた表示に変換でき、さらに **convert JSON to dict** してスムーズに後続処理が行えるようになることです。このチュートリアルでは、JSON 文字列を Python で読み込み、データをイテレートするまでのすべての手順を解説します。フォーマットに悩む代わりにロジックに集中できるようになります。

## What This Tutorial Covers

- `json.dumps` の `indent` 引数を使って **pretty print JSON Python** する方法。  
- **load JSON string Python** してネイティブな辞書に変換する正確な手順。  
- 辞書を便利な Python オブジェクトに変換し、各単語と信頼度スコアを出力する実用例。  
- 非 ASCII 文字の扱いなど、よくある落とし穴とその即効対策。  
- コピー＆ペーストしてすぐに使える、完全に実行可能なスクリプト。

このガイドを読み終えると、任意の JSON ペイロードを人間が読みやすい形式に変換し、外部ライブラリなしで純粋な Python だけで操作できるようになります。

---

## Prerequisites

- Python 3.8 以上（`json` モジュールは標準ライブラリに含まれます）。  
- 辞書とループの基本的な理解。  
- 任意で OCR エンジンや JSON を返すサービス。例ではモックの `engine.recognize()` を使用していますが、独自のデータソースに置き換えて構いません。

---

## Step 1: Perform OCR (or Any JSON‑Generating) Recognition

まずは JSON 互換の結果が必要です。多くのコンピュータビジョンワークフローでは OCR エンジンが構造化オブジェクトを出力し、JSON にシリアライズできます。最小限のプレースホルダーは次の通りです：

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

> **Why this step matters:**  
> OCR を実行しなくても、API、ファイル、メッセージキューなどからデータを受け取ることが多いです。オブジェクトは **pretty print** できるように JSON にシリアライズ可能である必要があります。

---

## Step 2: Pretty Print JSON Python

生データをきれいにインデントされた文字列に変換します。`indent` パラメータが主役です。

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

出力例は以下のようになります：

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

> **Pro tip:** 幅広いインデントが欲しい場合は `indent=4`、キーをアルファベット順に並べたい場合は `sort_keys=True` を追加してください。

---

## Step 3: Load JSON String Python → Native Dictionary

人間には pretty‑printed 文字列が見やすいですが、実際の処理は辞書が便利です。ここで **load JSON string Python** してネイティブ構造に変換します。

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

結果は次のようになります：

```
✅ Loaded dict type: <class 'dict'>
```

> **Why we do this:**  
> 辞書は O(1) の検索、可変データ、Python エコシステムとのシームレスな統合を提供します。JSON 文字列のままで作業すると、面倒な文字列解析が必要になります。

---

## Step 4: Iterate Over Recognized Words – A Real‑World Use Case

各単語とその信頼度スコアを抽出してみましょう。これにより **convert json to dict**（既に取得した dict）と実践的なイテレーションの両方を示します。

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

期待される出力は次の通りです：

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **Edge case tip:** JSON に `"words"` キーが存在しない可能性がある場合は、`KeyError` を防ぐために以下のようにガードしてください：

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## Step 5: Handling Non‑ASCII Characters (Unicode Support)

OCR エンジンは “é” や “ü” といった文字を返すことがあります。デフォルトの `json.dumps` は `\u00e9` のようにエスケープします。可読性を保つには `ensure_ascii=False` を指定します。

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

これで出力はエスケープされた形ではなく **café** と表示されます。後で **convert json to dict** する際にも、辞書は正しい Unicode 文字列を保持します。

---

## Step 6: Saving and Reloading the Pretty‑Printed JSON (Optional)

フォーマット済み JSON をファイルに保存して後で確認したいことがあります。

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

ファイルにはインデントされた JSON が保存され、`json.load` が自動的に dict にパースします。

---

## Step 7: Putting It All Together – A One‑File Solution

以下は本記事で説明したすべての手順を組み込んだ、単体スクリプトです。`pretty_json_demo.py` という名前で保存し、実行してみてください。

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

実行方法：

```bash
python pretty_json_demo.py
```

実行すると、pretty‑printed JSON、辞書型の表示、各単語と信頼度、そして Unicode 対応版が `pretty_output.json` に保存されます。  

**これで完了です**—生の OCR 出力から、きれいで操作しやすい Python 辞書への変換までの全工程を網羅しました。

---

## Frequently Asked Questions (FAQs)

| Question | Answer |
|----------|--------|
| **Do I need an external library?** | No. The built‑in `json` module handles both pretty printing and loading. |
| **What if my JSON is huge?** | Use `json.dump` with a file handle to avoid loading everything into memory; you can still set `indent` for a pretty file. |
| **Can I sort the keys?** | Yes—add `sort_keys=True` to `json.dumps` for deterministic ordering, which helps with diff‑based testing. |
| **How do I handle malformed JSON?** | Wrap `json.loads` in a `try/except json.JSONDecodeError` block and log the problematic string. |
| **Is there a faster alternative?** | For massive payloads, libraries like `orjson` or `ujson` are faster, but they don’t support `indent` out‑of‑ |

## What Should You Learn Next?

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれており、API の追加機能を習得したり、独自プロジェクトで代替実装を試したりするのに役立ちます。

- [How to Use Aspose OCR for JSON Result in Image Recognition](/ocr/english/net/text-recognition/get-result-as-json/)
- [Cómo usar Aspose OCR para obtener resultados JSON en reconocimiento de imágenes](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [Wie man Aspose OCR für JSON‑Ergebnisse bei der Bilderkennung verwendet](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}