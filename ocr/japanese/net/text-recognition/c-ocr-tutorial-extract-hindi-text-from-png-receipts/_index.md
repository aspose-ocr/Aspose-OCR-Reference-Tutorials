---
category: general
date: 2026-01-09
description: C# OCRチュートリアル：PNGからテキストを読み取り、画像をテキストに変換し、Aspose OCRを使用してレシートのヒンディー語テキストを認識する。
draft: false
keywords:
- c# ocr tutorial
- read text from png
- convert image to text
- recognize hindi text
- extract text from receipt
language: ja
og_description: PNGからテキストを読み取り、画像をテキストに変換し、Aspose OCRで領収書のヒンディー語テキストを認識する方法を教えるC#
  OCRチュートリアル。
og_title: c# OCR チュートリアル – PNG領収書からヒンディー語テキストを抽出
tags:
- OCR
- C#
- Aspose
- Image Processing
title: C# OCR チュートリアル – PNG領収書からヒンディー語テキストを抽出
url: /ja/net/text-recognition/c-ocr-tutorial-extract-hindi-text-from-png-receipts/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# c# OCR チュートリアル – PNG レシートからヒンディー語テキストを抽出

PNG ファイルからテキストを **読み取る** 方法を考えたことはありますか？たとえばヒンディー語のレシートが多数あり、金額を自動で取得したいとします。この c# OCR チュートリアルでは、画像を数行のコードだけで検索可能なテキストに変換する方法を解説します。

このガイドでは Aspose OCR のインストール、PNG レシートの読み込み、ヒンディー文字の認識、そして抽出した文字列をコンソールに出力する手順を順に見ていきます。最後まで読めば、**画像をテキストに変換**、**ヒンディー語テキストの認識**、さらに **レシート画像からテキストを抽出** できるようになります。

> **前提条件:** 有効な Aspose OCR ライセンス（または無料トライアル）と .NET 6+ がインストールされている必要があります。NuGet が初めてでも心配はいりません—こちらでも説明します。

---

## 必要なもの

- **Visual Studio 2022**（または任意の C# 対応エディタ）
- **.NET 6 SDK**（以降のバージョンでも可）
- **Aspose.OCR** NuGet パッケージ  
  ```bash
  dotnet add package Aspose.OCR
  ```
- サンプルレシート画像（例: `hindi-receipt.png`）をプロジェクトフォルダーに保存

これらが揃っていれば、最終コードをコピー＆ペーストして **F5** で実行できます。

---

## 手順 1: プロジェクトの作成と名前空間のインポート

まだコンソールプロジェクトがない場合は作成します:

```bash
dotnet new console -n HindiReceiptOcr
cd HindiReceiptOcr
dotnet add package Aspose.OCR
```

次に `Program.cs` を開き、冒頭で Aspose OCR の名前空間をインポートします。これによりコンパイラがクラスを認識できるようになります:

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;
```

> **ポイント:** `OcrEngine` は `Aspose.OCR` にあり、言語関連の列挙型は `Aspose.OCR.Settings` にあります。どちらかを忘れるとコンパイルエラーになります。

---

## 手順 2: OCR エンジンの初期化と言語モデルの選択

OCR エンジンには **対象言語** を指定する必要があります。Aspose には多数の言語パックが同梱されており、`OcrLanguage.Hindi` を指定すると、エンジンはヒンディー語モデルをダウンロード（未取得の場合）して使用します。

```csharp
// Step 2: Create and configure the OCR engine
var ocrEngine = new OcrEngine
{
    // The library will auto‑download the model the first time it runs.
    Language = OcrLanguage.Hindi
};
```

> **プロのコツ:** 複数言語のレシートを処理する場合は、実行時に `Language` を切り替えるか、`MultiLanguage` モードを有効にできます。

---

## 手順 3: PNG レシートをエンジンに渡す

ここで **PNG からテキストを読み取ります**。実行ファイルからの相対パスでも問題ありません。メソッドはエンジンが解読できた文字列全体を返します。

```csharp
// Step 3: Perform OCR on the target image file
string imagePath = @"hindi-receipt.png";   // adjust if your file lives elsewhere
string recognizedText = ocrEngine.RecognizeImage(imagePath);
```

画像が高解像度で文字がはっきりしていれば、ほぼ完璧な結果が得られます。ノイズが多いスキャンの場合は、前処理（例: 二値化）を検討してください—Aspose には `PreprocessImage` メソッドが用意されています。

---

## 手順 4: 抽出したテキストの表示または保存

テスト時はコンソールに結果をダンプするのが一般的です。実運用ではデータベースや CSV ファイルに書き出すこともあります。

```csharp
// Step 4: Show the OCR result
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(recognizedText);
```

サンプルレシートでプログラムを実行すると、次のような出力が得られます:

```
=== OCR Output ===
दिनांक: 09/01/2026
बिल no: 12345
रक्कम: ₹ 1,250.00
धन्यवाद!
```

これが **画像をテキストに変換** した実例です—手作業の転記は不要です。

---

## 完全動作サンプル（コピー＆ペースト可能）

以下は単一ファイルで完結するプログラムです。`Program.cs` に貼り付け、`hindi-receipt.png` をビルドされた `.exe` と同じディレクトリに置き、**Ctrl + F5** で実行してください。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace HindiReceiptOcr
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Initialize the OCR engine with Hindi language
            var ocrEngine = new OcrEngine
            {
                Language = OcrLanguage.Hindi
            };

            // 2️⃣ Path to the PNG receipt (adjust if needed)
            string imagePath = @"hindi-receipt.png";

            // 3️⃣ Run OCR – this will download the Hindi model on first run
            string recognizedText = ocrEngine.RecognizeImage(imagePath);

            // 4️⃣ Output the result – you can also write to a file or DB
            Console.WriteLine("=== OCR Output ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

### 期待される出力

レシート画像にクリアなヒンディー文字が含まれていれば、コンソールに抽出された行が改行付きで表示されます。認識できない単語がある場合は文字化けした断片が出力されます—画像品質の改善や前処理の調整が必要であるサインです。

---

## 手順 5: 発展編 – レシートから項目をプログラム的に抽出

**レシートからテキストを抽出** して日付、合計、請求番号といったフィールドを取得したい場合は、OCR 文字列を正規表現で後処理します:

```csharp
using System.Text.RegularExpressions;

// Example: pull the amount (₹) from the OCR result
var amountMatch = Regex.Match(recognizedText, @"रक्कम:\s*₹\s*([\d,]+\.\d{2})");
if (amountMatch.Success)
{
    Console.WriteLine($"Detected amount: {amountMatch.Groups[1].Value}");
}
```

この小さなスニペットは、生の OCR 出力を構造化データに変換する方法を示しています—会計ソフトへの入力に最適です。

---

## よくある落とし穴と回避策

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **空の出力** | 画像パスが間違っている、またはファイルが出力フォルダーにコピーされていない | `Path.GetFullPath` を使用し、`File.Exists` で存在を確認 |
| **文字化け** | 低解像度 PNG または圧縮カラー | 画像を拡大し、DPI を 300+ に設定、または `ocrEngine.ImagePreprocessor` を使用 |
| **言語モデルが未ダウンロード** | 初回実行時にインターネット接続がない | Aspose ポータルで事前にヒンディー語モデルをダウンロード、またはローカルにホスト |
| **パフォーマンス低下** | ループで多数ページを処理し、解放しないまま使用 | `using` ブロックで `OcrEngine` を囲むか、インスタンスを再利用 |

---

## 画像イラスト

![c# ocr tutorial reading Hindi text from PNG receipt](https://example.com/placeholder-image.png "c# ocr tutorial – read text from png receipt")

*スクリーンショットは、OCR 前後のヒンディー語レシートを示しています。*

---

## まとめ: 本チュートリアルで学んだこと

- C# コンソール アプリを作成し、Aspose OCR NuGet パッケージを追加  
- **ヒンディー語テキストを認識** するために `OcrEngine` を初期化  
- `RecognizeImage` を使って **PNG からテキストを読み取る**  
- **画像をテキストに変換** し、結果をコンソールに出力  
- 正規表現で **レシートからテキストを抽出** する簡易パターンを実演  

以上すべてが単一ファイルで実行可能な **c# OCR チュートリアル** の形で提供されました。

---

## 次のステップと関連トピック

1. **バッチ処理** – フォルダー内のレシート画像をすべて走査し、結果を CSV に保存  
2. **前処理** – `ocrEngine.ImagePreprocessor` を活用してノイズ除去、傾き補正、コントラスト強化  
3. **マルチ言語 OCR** – `OcrLanguage.Multilingual` を有効にし、ヒンディー語と英語が混在するレシートに対応  
4. **統合** – 抽出データを Entity Framework Core モデルに保存し、永続化  

これらに興味がある方は、**C# で画像をテキストに変換** と **OCR 結果から構造化データを抽出** に関する他のチュートリアルもご覧ください。

---

### Happy Coding!

実装中に問題が発生したり、独自に拡張した事例があればぜひコメントで共有してください。OCR は最初のステップに過ぎません—クリーンなデータが本当の魔法を生み出します。🚀

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}