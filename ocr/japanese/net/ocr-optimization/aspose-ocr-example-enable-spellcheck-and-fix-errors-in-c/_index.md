---
category: general
date: 2026-03-07
description: Aspose OCR の例で、スペルチェックを有効にし、カスタム辞書を追加し、画像 OCR をロードして OCR エラーを迅速に修正する方法を示しています。
draft: false
keywords:
- aspose ocr example
- how to enable spellcheck
- how to add dictionary
- load image ocr
- how to fix ocr errors
language: ja
og_description: スペルチェックの有効化、カスタム辞書の追加、OCR用画像の読み込み、一般的なOCRエラーの修正方法を案内するAspose OCRのサンプルです。
og_title: Aspose OCR の例 – スペルチェックを有効にしてエラーを修正
tags:
- Aspose
- OCR
- C#
- SpellCheck
title: Aspose OCR の例 – C# でスペルチェックを有効にし、エラーを修正する
url: /ja/net/ocr-optimization/aspose-ocr-example-enable-spellcheck-and-fix-errors-in-c/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR の例 – スペルチェックを有効にして C# でエラーを修正する

画像からテキストを読み取るだけでなく、厄介なスペルミスまでクリーンアップする **Aspose OCR example** が必要だったことはありませんか？ あなただけではありません。実際のプロジェクトでは、元の OCR 出力が誤字だらけになることが多く、特にソース画像に低コントラストのフォントや手書きのメモが含まれている場合に顕著です。  

良いニュースです。Aspose.OCR を使えば、**spellcheck を有効に**し、独自の辞書を組み込んで、数行のコードだけで洗練された文字列を取得できます。以下では、**spellcheck の有効化方法**、**辞書の追加方法**、そして **画像 OCR のロード方法** を具体的に示すので、もう髪を引っ張ることなく **OCR エラーを修正** できるようになります。  

このチュートリアルでは、NuGet のインストールから、修正されたテキストを出力する完全な実行可能プログラムまで、必要なすべてをカバーします。最後まで読むと、任意の .NET プロジェクトにすぐに組み込める堅実な **Aspose OCR example** が手に入ります。

## 前提条件

- .NET 6.0 SDK またはそれ以降（コードは .NET Core および .NET Framework でも動作します）
- Visual Studio 2022 または任意の C# 対応 IDE
- 明瞭な英語のタイプテキストが含まれる画像ファイル（`typed_text.png`）
- Aspose.OCR NuGet パッケージを取得するためのインターネット接続

他のサードパーティライブラリは必要ありません。

---

## ステップ 1 – Aspose.OCR NuGet パッケージのインストール (Load Image OCR)

コードを書く前に、OCR エンジンを動かすライブラリが必要です。

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio を使用している場合、プロジェクトを右クリック → *Manage NuGet Packages* → **Aspose.OCR** を検索して *Install* をクリックしてください。  

パッケージをインストールすると、`OcrEngine`、`ImageStream`、および後で使用する組み込みのスペルチェックユーティリティにアクセスできるようになります。パッケージが配置されたら、**load image OCR** の準備が整います。

## ステップ 2 – OCR エンジン インスタンスの作成

エンジンの作成は、任意の **Aspose OCR example** における最初の具体的なステップです。`OcrEngine` をビットマップを解析しテキストを出力する脳と考えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

// Step 2: Initialize the OCR engine
var ocrEngine = new OcrEngine();
```

`OcrEngine` のコンストラクタはパラメータを必要としないため、クイックプロトタイプに最適です。

## ステップ 3 – Spellcheck の有効化方法（その重要性）

生の OCR 出力には、しばしば “the” の代わりに “teh” のように誤認識された単語が含まれます。組み込みのスペルチェッカーを有効にすると、Aspose が自動的に最も可能性の高い正しい綴りに置き換えてくれます。

```csharp
// Step 3: Turn on spell checking and set the language to English
ocrEngine.Settings.SpellCheck.Enabled = true;
ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;
```

> **なぜ spellcheck を有効にするのか？**  
> - **精度:** 後処理のスペルチェックにより、印刷文書の全体的なテキスト精度が 10‑15 % 向上します。  
> - **ユーザー体験:** クリーンなテキストは、結果を検索インデックスや分析パイプラインに投入する際の下流のクレンジング作業を減らします。

## ステップ 4 – 辞書の追加方法（カスタム単語）

デフォルトの辞書がブランド名、製品コード、またはドメイン固有の用語を認識しないことがあります。そこで **辞書の追加方法** が重要になります。

```csharp
// Step 4: Add custom words that the spell checker should accept
ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
{
    "AsposeOCR",   // our library name
    "OCRify",      // a fictional product
    "CSharpify"    // another custom term
});
```

配列、リスト、または大規模なカスタム語彙がある場合はファイルから読み込むこともできます。スペルチェッカーはこれらのエントリを有効とみなし、誤った修正を防ぎます。

## ステップ 5 – OCR 用画像のロード (Load Image OCR)

エンジンの設定が完了したので、読み取り対象の画像を指定する必要があります。`ImageStream.FromFile` ヘルパーはファイル読み取りの詳細を抽象化します。

```csharp
// Step 5: Load the image that contains the text to be recognized
ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");
```

> **ヒント:** 画像がプロジェクトのサブフォルダーにある場合、*Copy to Output Directory* プロパティを *Copy always* に設定して、実行時にパスが解決されるようにしてください。

## ステップ 6 – 認識を実行し OCR エラーを修正する

すべての設定が完了したら、`Recognize()` を一度呼び出すだけで OCR パイプラインが実行され、スペルチェックが適用され、クリーンな結果が `ocrEngine.Text` に格納されます。

```csharp
// Step 6: Run OCR and let the spell checker clean the output
ocrEngine.Recognize();

// Step 7: Output the corrected text to the console
Console.WriteLine("Corrected text:");
Console.WriteLine(ocrEngine.Text);
```

### 期待される出力

`typed_text.png` に文 `The quick brown fox jumps over teh lazy dog` が含まれていると仮定すると、コンソールに次のように表示されます：

```
Corrected text:
The quick brown fox jumps over the lazy dog
```

“teh” が自動的に “the” に修正されたことに注目してください。カスタム辞書に “OCRify” を追加していて、画像にその単語が含まれていた場合、エンジンはそれをそのまま保持します。

---

## 完全な動作例（コピー＆ペースト可能）

以下は新しいコンソールプロジェクトに貼り付けて使用できる完全なプログラムです。上記のすべての手順に加えて、分かりやすくするためのコメントもいくつか含まれています。

```csharp
// ---------------------------------------------------------------
// Aspose OCR Example – Enable Spellcheck and Fix Errors
// ---------------------------------------------------------------

using System;
using Aspose.OCR;
using Aspose.OCR.SpellCheck;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine
            var ocrEngine = new OcrEngine();

            // 2️⃣ Enable spell checking (how to enable spellcheck)
            ocrEngine.Settings.SpellCheck.Enabled = true;
            ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.English;

            // 3️⃣ Add custom words (how to add dictionary)
            ocrEngine.Settings.SpellCheck.CustomDictionary.AddWords(new[]
            {
                "AsposeOCR",
                "OCRify",
                "CSharpify"
            });

            // 4️⃣ Load the image (load image OCR)
            // Replace the path with the actual location of your image file
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/typed_text.png");

            // 5️⃣ Run OCR – this also fixes common OCR errors (how to fix ocr errors)
            ocrEngine.Recognize();

            // 6️⃣ Show the corrected result
            Console.WriteLine("Corrected text:");
            Console.WriteLine(ocrEngine.Text);
        }
    }
}
```

`Program.cs` として保存し、`dotnet run` を実行すると、修正された文がコンソールに表示されます。

---

## よくある質問とエッジケース

| Question | Answer |
|----------|--------|
| **画像がマルチページ PDF の場合はどうしますか？** | Aspose.OCR は PDF ページを画像として処理できます。`ocrEngine.Image = ImageStream.FromPdf("file.pdf", pageNumber: 1);` を使用し、ページをループしてください。 |
| **英語以外の言語に変更できますか？** | もちろんです。`ocrEngine.Settings.SpellCheck.Language = SpellCheckLanguage.French;` のように設定してください（サポートされている言語であればどれでも構いません）。 |
| **カスタム辞書が非常に大きい場合、パフォーマンスに影響しますか？** | 数千語の追加には多少の初期コストがかかりますが、内部でハッシュセットを使用しているため検索は O(1) です。膨大な語彙の場合は、アプリケーション起動時に一度だけロードすることを検討してください。 |
| **破損した画像で OCR エンジンが例外をスローした場合はどうしますか？** | `Recognize()` を try‑catch ブロックで囲み、`ocrEngine.LastError` を確認してください。また、`ocrEngine.Image.Width` と `Height` で画像サイズを事前に検証することもできます。 |
| **本番環境で使用するにはライセンスが必要ですか？** | 無料評価版はテストに使用できますが、商用ライセンスを取得すると評価用の透かしが除去され、フルパフォーマンスが利用可能になります。 |

---

## 結論

これで、**spellcheck の有効化方法**、**辞書の追加方法**、**画像 OCR のロード**、そして **OCR エラーの修正方法** をクリーンで本番環境向けに示す **完全な Aspose OCR example** が手に入りました。スペルチェッカーを設定しカスタム単語リストを提供するだけで、後処理ロジックを書かずに抽出テキストの品質を大幅に向上させることができます。

次のステップに進む準備はできましたか？ 言語をスペイン語に変更したり、マルチページ PDF を処理したり、出力を検索可能な Azure Cognitive Search インデックスに統合したりしてみてください。同じパターンが適用できます—言語フラグを調整し、必要に応じてカスタム辞書を拡張するだけです。

このガイドが役に立ったと思ったら、GitHub でスターを付けたり、チームメンバーと共有したり、下にコメントを残したりしてください。コーディングを楽しんで、OCR の結果が常にエラーなしであることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}