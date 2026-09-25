---
category: general
date: 2026-01-15
description: Aspose OCR を使用してアラビア語テキストを OCR し、ヒンディー語テキストを認識する方法を学びましょう。このステップバイステップガイドでは、画像からテキストを抽出し、画像をテキストに効率的に変換する方法を示します。
draft: false
keywords:
- how to ocr arabic
- recognize arabic text
- extract text from image
- convert image to text
- recognize hindi text
language: ja
og_description: 単一のC#プログラムでアラビア語テキストをOCRし、ヒンディー語テキストを認識する方法。画像からテキストを抽出し、画像をテキストに変換する完全ガイドをご覧ください。
og_title: Aspose OCRでアラビア語とヒンディー語のテキストをOCRする方法
tags:
- Aspose OCR
- C#
- Multilingual OCR
title: Aspose OCRでアラビア語とヒンディー語のテキストをOCRする方法
url: /ja/net/text-recognition/how-to-ocr-arabic-and-hindi-text-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# アラビア語とヒンディー語のテキストを Aspose OCR で OCR する方法

右から左へ流れる**how to ocr arabic**文字を OCR したり、レシートからヒンディー文字を抽出したりする方法を考えたことはありますか？ あなたは一人ではありません。同じワークフローで**recognize arabic text**と**recognize hindi text**が必要になる開発者は多くいます。  

このチュートリアルでは、完全に実行可能な C# のサンプルを通して、**extract text from image** ファイルからテキストを抽出し、**convert image to text** を行い、Aspose OCR でアラビア語とヒンディー語の両方のスクリプトを処理する方法を説明します。曖昧な参照は一切なく、コピー＆ペーストできるコードと各行の背後にある考え方だけを提供します。

> **Pro tip:** Aspose OCR をまだ使用したことがない場合は、まず NuGet パッケージ `Aspose.OCR` をインストールしてください。Visual Studio でワンクリックでインストールでき、CPU ベースの認識に必要なすべてのネイティブバイナリが自動的に取得されます。

![アラビア語 OCR の例](/images/arabic-ocr-sample.png "アラビア語 OCR – サンプル アラビア語サイン")

*画像の代替テキスト:* **how to ocr arabic – sample Arabic sign**  

## アラビア語 OCR – 環境設定

コードに入る前に、開発環境が整っていることを確認しましょう。

1. **Target framework** – .NET 6.0 以降。古いバージョンでもコンパイルは可能ですが、最新の言語機能は利用できません。  
2. **Package** – ターミナルで `dotnet add package Aspose.OCR` を実行するか、NuGet パッケージ マネージャー UI を使用してください。  
3. **Images** – 参照できるフォルダーにサンプル画像を 2 枚配置します。例: `C:\OCRSamples\arabic_sign.jpg` と `C:\OCRSamples\hindi_receipt.png`。アラビア語画像ははっきりとした高コントラストのアラビア文字を含み、ヒンディー語画像はスキャンしたレシートまたは看板の写真で構いません。  

以上です。余分な設定ファイルや GPU ドライバーは不要で、シンプルな CPU ベースの OCR エンジンだけです。

## アラビア語テキストの認識 – 読み込みと処理

ここで実際に**recognize arabic text**を行います。重要なのはエンジンに期待する言語を指定することです。指定しない場合、エンジンはデフォルトでラテン文字とみなし、文字化けした出力になります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine (CPU‑based by default)
        var ocrEngine = new OcrEngine();

        // 2️⃣ Load an image that contains Arabic script
        var arabicImage = OcrImage.FromFile(@"C:\OCRSamples\arabic_sign.jpg");

        // 3️⃣ Recognize the Arabic text – note the Language.Arabic enum
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);

        // 4️⃣ Print the result to the console
        System.Console.WriteLine("Arabic: " + arabicResult.Text);
```

**Why this works:**  
* `OcrEngine` は前処理、セグメンテーション、文字分類といった重い処理をすべて担当します。  
* `Language.Arabic` を渡すことで、右から左へのレイアウトエンジンとアラビア文字セットが有効になります。これを指定しないと、エンジンは画像を左から右のラテン文字として扱い、ダイアクリティックが欠落したり単語が壊れたりします。  

**Expected output**（実際のテキストは画像により異なります）:

```
Arabic: مرحبا بكم في متجرنا
```

空文字列が出力された場合は、画像が暗すぎないか、ファイルパスが正しいかを再確認してください。  

## 画像からテキスト抽出 – 右から左スクリプトの処理

アラビア語だけが特別な処理を必要とするわけではありません。右から左（RTL）言語は、認識後に OCR エンジンが視覚的順序を逆転させる必要があります。`Language.Arabic` を指定すれば Aspose が自動的に処理しますが、将来的な拡張（例: ヘブライ語）を考えると覚えておく価値があります。

*ヒント:* 後で UI に OCR 結果を表示する際は、コントロールが RTL 表示に対応していることを確認してください。対応していないとテキストが乱れたように表示されます。

## 画像をテキストに変換 – ヒンディー語の処理

次に、ヒンディー語のレシートに対して**convert image to text**を行いましょう。手順はアラビア語の場合と同様ですが、代わりに `Language.Hindi` を使用します。

```csharp
        // 5️⃣ Load the Hindi (Devanagari) image
        var hindiImage = OcrImage.FromFile(@"C:\OCRSamples\hindi_receipt.png");

        // 6️⃣ Recognize Hindi text – Language.Hindi tells the engine to use Devanagari models
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);

        // 7️⃣ Output the Hindi OCR result
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Why we reuse the same `ocrEngine` instance:**  
言語ごとに新しいエンジンを作成すると、メモリと初期化時間が無駄になります。Aspose のエンジンはシーケンシャル呼び出しに対してスレッドセーフなので、再利用する方が効率的でクリーンです。

**Sample console output**（こちらも画像に依存します）:

```
Hindi: कुल राशि: ₹ 1,250.00
```

ヒンディー語テキストが文字化けしたラテン文字のように見える場合、言語列挙子を省略したか、画像解像度が低すぎる（<300 dpi）可能性があります。画像を拡大したり、シンプルな二値化フィルタを適用することで精度が大幅に向上します。

## ヒンディー語テキストの認識 – よくある落とし穴とエッジケース

正しい言語フラグを設定していても、いくつかの問題でつまずくことがあります。

| Issue | Symptom | Fix |
|-------|---------|-----|
| 低コントラスト | 多くの文字が “?” になるか省略される | `OcrImage.AdjustContrast(1.5)` で前処理 |
| 画像の傾き | テキストが回転して表示され、OCR が空文字列を返す | `ocrEngine.PreprocessImage(arabicImage, ImageProcessingOptions.Rotate)` を呼び出す |
| 混在言語 | アラビア語行の後に英数字が続く | 2 回実行: まず `Language.Arabic`、次に同じ画像で `Language.English` を使用し結果を結合 |
| ファイルサイズが大きい | 認識が遅い、またはメモリ不足エラー | `OcrImage.Resize(2000, 0)` で幅最大 2000 px に縮小 |

これらのヒントは、完璧にスキャンされていない**extract text from image**ファイルの処理に役立ちます。実務プロジェクトではよくあるケースです。

## すべてをまとめる – 完全な動作例

以下は、すぐに新しいコンソールプロジェクトにコピーできる完全なプログラムです。隠れた依存関係や余分な設定はなく、純粋な C# だけです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

class MultiLangDemo
{
    static void Main()
    {
        // Initialize the OCR engine (CPU‑based)
        var ocrEngine = new OcrEngine();

        // -------------------- Arabic --------------------
        var arabicPath = @"C:\OCRSamples\arabic_sign.jpg";
        var arabicImage = OcrImage.FromFile(arabicPath);
        var arabicResult = ocrEngine.Recognize(arabicImage, Language.Arabic);
        System.Console.WriteLine("Arabic: " + arabicResult.Text);

        // -------------------- Hindi --------------------
        var hindiPath = @"C:\OCRSamples\hindi_receipt.png";
        var hindiImage = OcrImage.FromFile(hindiPath);
        var hindiResult = ocrEngine.Recognize(hindiImage, Language.Hindi);
        System.Console.WriteLine("Hindi: " + hindiResult.Text);
    }
}
```

**Running the program** を実行すると、コンソールにアラビア語とヒンディー語の文字列が出力され、**recognize arabic text** と **recognize hindi text** を単一の実行で正常に行えたことが確認できます。  

## 結論

これで、**how to ocr arabic** の質問に対する包括的な解決策が手に入り、ヒンディー語も同時に処理できるようになりました。単一の `OcrEngine` を作成し、各画像を読み込み、適切な `Language` 列挙体を渡すだけで、**extract text from image**、**convert image to text**、そして **recognize arabic text** と **recognize hindi text** を余分なライブラリなしで実現できます。

ここからは以下のようなことを検討できます：

* **Batch processing** – 画像フォルダーをループし、結果をデータベースに保存する。  
* **Post‑processing** – 正規表現を使ってヒンディー語レシートの通貨記号をクリーンアップする。  
* **Hybrid language detection** – 列挙体を選択する前に、生のビットマップを言語識別モデルに渡す。  

ぜひ試してみて、前処理ステップを調整すれば OCR 精度がすぐに向上するのが分かります。問題が発生したら、  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}