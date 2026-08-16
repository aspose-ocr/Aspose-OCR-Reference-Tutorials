---
category: general
date: 2026-04-03
description: C#でOCRを実行し、Aspose OCRを使用して画像からテキストを抽出し、ロシア語のスペルチェックを行う方法を学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- convert image to text
- how to spell check
- ocr russian language
language: ja
og_description: C#でOCRを実行し、Aspose OCRを使用して画像からテキストを抽出する方法を学び、ロシア語のスペルチェックも行います。
og_title: C#でOCRを実行する方法 – 画像からテキストを抽出
tags:
- OCR
- C#
- Aspose
- SpellCheck
title: C#でOCRを実行する方法 – 画像からテキストを抽出
url: /ja/net/text-recognition/how-to-perform-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを実行する方法 – 画像からテキストを抽出する

手書きメモの写真に **OCRを実行する方法** を知りたくありませんか？スキャンしたレシートや、外国語の看板、コピー＆ペーストできないPDFページなど、さまざまなケースが考えられます。朗報です！C#の数行と Aspose OCR ライブラリさえあれば、その画像をすぐに編集可能なテキストに変換できます。

このガイドでは **OCRを実行する方法** を示すだけでなく、 **画像からテキストを抽出する**、 **画像をテキストに変換する**、さらにロシア語文書を扱う際の **スペルチェックの方法** まで解説します。たくさんあるように見えても安心してください。ステップバイステップで丁寧に説明します。

## 学べること

このチュートリアルを終えると、以下ができるようになります。

* ロシア語サポート用に Aspose OCR を設定する。  
* 画像ファイルを読み込み、光学文字認識で **画像からテキストを抽出する**。  
* 組み込みのスペルチェッカーを使って誤字を自動修正する – OCR 出力の **スペルチェックの方法** に最適です。  
* 整形された文字列をコンソールに出力し、さらに処理や保存に利用できるようにする。

**前提条件** – 必要なもの：

* .NET 6.0 以降（.NET Framework 4.8 でも動作します）。  
* 有効な Aspose OCR ライセンス、または一時的な評価キー。  
* ロシア語テキストが含まれる画像ファイル（デモでは `russian_note.jpg` と呼びます）。  

これらが馴染みのないものでも心配はいりません。以下の手順には Aspose OCR を取得する正確な NuGet コマンドが含まれており、コードは完全に自己完結しています。

![OCR実行例](/images/ocr-demo.png "C#でOCRを実行する例")

## 手順 1 – Aspose OCR をインストールし名前空間を追加

まずはライブラリが必要です。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行します。

```bash
dotnet add package Aspose.OCR
```

このコマンドは最新の安定版（2026年4月時点で 22.9）を取得します。パッケージが復元されたら、C# ファイルの先頭に必要な `using` ディレクティブを追加します。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;
```

*プロのコツ*：Visual Studio を使用している場合、最初のクラス名を入力すると IDE が自動的に追加を提案してくれます。

## 手順 2 – ロシア語用に OCR エンジンを初期化

**OCRを実行する方法** は `OcrEngine` インスタンスの作成から始まります。`OcrLanguage.Russian` を指定することで、エンジンにキリル文字セットとロシア語固有のヒューリスティックをロードさせます。

```csharp
// Step 2: Initialise OCR engine for Russian
OcrEngine ocrEngine = new OcrEngine
{
    Language = OcrLanguage.Russian   // Enables Russian language support
};
```

なぜ重要かというと、言語を設定しないとエンジンはデフォルトで英語になり、キリル文字を誤認識して文字化けした出力になります。言語を明示的に設定することで精度が大幅に向上します。

## 手順 3 – 画像を読み込み **画像をテキストに変換する**

次に画像をメモリに取り込みます。`Image.FromFile` メソッドは JPG、PNG、BMP などの一般的なフォーマットに対応しています。読み込み後、`Recognize` を呼び出して **画像をテキストに変換する** 処理を行います。

```csharp
// Step 3: Load the image that contains Russian text
Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

// Step 4: Perform OCR – this is the core “how to perform OCR” call
string rawText = ocrEngine.Recognize(sourceImage);
```

`rawText` 変数には OCR の生データが格納されますが、まだ誤字や認識ミスが含まれている可能性があります。実際にエンジンが取得した内容を確認したい場合は、次のように出力できます。

```csharp
Console.WriteLine("Raw OCR output:");
Console.WriteLine(rawText);
```

## 手順 4 – OCR 結果の **スペルチェックの方法**

ロシア語 OCR は特に低解像度のスキャンでノイズが多くなりがちです。Aspose にはロシア語辞書を標準で備えた `SpellChecker` クラスがあります。使用例は以下の通りです。

```csharp
// Step 5: Initialise the spell checker
SpellChecker spellChecker = new SpellChecker();

// Step 6: Correct spelling mistakes in the recognized text
string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);
```

`CheckAndCorrect` メソッドは、誤字が検出された単語を最も妥当と思われる正しい形に置き換えた新しい文字列を返します。句読点も考慮されるため、テキストが壁のように連続することはありません。

*エッジケース*：OCR の出力が空（例: 画像が真っ白）だった場合、`CheckAndCorrect` は空文字列を返します。結果をファイルに書き込む予定がある場合は、空文字列かどうかのチェックを入れておくと安全です。

## 手順 5 – 整形済み結果を表示

最後に修正済み文字列を出力します。実際のアプリケーションではデータベースや JSON API、Word 文書に書き込むことも考えられますが、デモではコンソールへのダンプで十分です。

```csharp
// Step 7: Show the corrected result
Console.WriteLine("\nCorrected text:");
Console.WriteLine(correctedText);
```

プログラムを実行すると、次のような出力が得られるはずです。

```
Raw OCR output:
Привeт мир! Этo тeкcт c русcкoй оcнoвнoй.

Corrected text:
Привет мир! Это текст с русской основой.
```

スペルチェッカーが「Привeт」（ラテン文字の ‘e’ が混在）を正しいキリル文字の「Привет」に変換しているのが分かります。これが **OCR 出力のスペルチェックの方法** の魔法です。

## 完全動作サンプル

以下は、すべての手順をひとつにまとめた完全な実行可能プログラムです。新しいコンソールプロジェクトに貼り付けて **F5** キーで実行してください。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;
using System.Drawing;

class SpellCheckDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine configured for Russian language
        OcrEngine ocrEngine = new OcrEngine { Language = OcrLanguage.Russian };

        // Step 2: Load the image that contains the text to be recognized
        Image sourceImage = Image.FromFile(@"YOUR_DIRECTORY/russian_note.jpg");

        // Step 3: Perform OCR to extract raw text from the image
        string rawText = ocrEngine.Recognize(sourceImage);

        // Optional: Show raw OCR output
        System.Console.WriteLine("Raw OCR output:");
        System.Console.WriteLine(rawText);

        // Step 4: Initialise the spell checker
        SpellChecker spellChecker = new SpellChecker();

        // Step 5: Correct spelling mistakes in the recognized text
        string correctedText = spellChecker.CheckAndCorrect(rawText, OcrLanguage.Russian);

        // Step 6: Display the corrected result
        System.Console.WriteLine("\nCorrected text:");
        System.Console.WriteLine(correctedText);
    }
}
```

### 期待される出力

ロシア語手書きの高解像度写真を使用した場合、クリーンで人が読める文が得られます。画像がぼやけている場合でも、一部正しく認識できない単語が出ることがありますが、スペルチェッカーがほとんどの明らかなエラーを補正してくれます。

## よくある落とし穴と対策

| 問題 | 発生理由 | 対処法 / 回避策 |
|------|----------|----------------|
| **文字化け** | DPI が低い、または背景がノイズが多い | `Recognize` 前に画像を前処理（コントラスト上げ、解像度を ≥ 300 dpi にリサイズ） |
| **出力が空** | ファイルパスが間違っている、または未対応フォーマット | パスを確認し、`Image.FromFile` を `try/catch` で囲んでエラーを可視化 |
| **スペルチェッカーがエラーを見逃す** | 辞書にない固有名詞や専門用語 | `spellChecker.AddUserDictionary("mywords.txt")` でカスタム単語リストを読み込む |
| **大量バッチで遅延** | OCR は CPU 集中型処理 | バックグラウンドスレッドで実行、または `Parallel.ForEach` を使って複数画像を同時処理 |
| **ライセンス例外** | 評価版の有効期限切れ | ライセンスを購入し、`License license = new License(); license.SetLicense("Aspose.Total.lic");` を `OcrEngine` 作成前に呼び出す |

## 次のステップ – シンプル OCR を超えて

**OCRを実行する方法** を習得した今、以下の拡張を検討してください。

* **バッチ処理** – フォルダー内の画像をループし、各テキストを `.txt` ファイルに書き出す。  
* **PDF 変換** – Aspose PDF を使って抽出したテキストを検索可能な PDF に埋め込む。  
* **言語検出** – 複数言語に対応する必要がある場合、OCR 結果を先に解析してから `OcrLanguage` を切り替える。  
* **Azure Cognitive Services との統合** – Aspose の結果と Microsoft の OCR API を比較し、ハイブリッドアプローチを構築する。

これらすべてのトピックは、二次キーワード **extract text from image**、**convert image to text**、そして **how to spell check** を自然に含んでいますので、ぜひ活用してください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}