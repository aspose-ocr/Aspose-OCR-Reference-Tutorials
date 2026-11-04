---
category: general
date: 2026-04-04
description: OCR を迅速かつ安全に使用する方法。画像からテキストを抽出し、DJVU をテキストに変換し、Aspose.OCR で画像を OCR にロードする方法を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert djvu to text
- load image for OCR
- extract text from djvu
language: ja
og_description: C#でOCRを使用して画像ファイルやDJVU文書からテキストを抽出する方法。フルコード付きのステップバイステップチュートリアル。
og_title: C#でOCRを使用する方法 – 完全ガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – 画像とDJVUファイルからテキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-and-djvu-files/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C#でOCRを使用する方法 – 画像とDJVUファイルからテキストを抽出する

スキャンしたページから手動で入力せずに単語を抽出する **how to use OCR** を考えたことがありますか？ あなただけではありません。古い本をデジタル化したり、レシートからデータを抽出したりする多くのプロジェクトで、画像からテキストを取得することは日常的な課題です。良いニュースは、Aspose.OCR を使えば、たった数行のコードで、ソースが DJVU ファイルであっても実行できることです。

このガイドでは、C# を使用して **extract text from image** ファイル、**load image for OCR**、さらには **convert DJVU to text** を行うために必要なすべてを説明します。最後まで読むと、認識されたテキストをコンソールに直接出力する、すぐに実行できるコンソールアプリが手に入ります。謎も余計な依存関係もなく、純粋な C# と Aspose だけです。

## 学べること

- Aspose.OCR ライブラリのインストールと参照方法。
- PNG、JPEG、または DJVU ページであっても **load image for OCR** に必要な正確なコード。
- エンジンを呼び出して結果を取得する方法。
- 大きなドキュメントの処理や一般的な落とし穴に関するヒント。
- Visual Studio にコピー＆ペーストできる、完全な実行可能サンプル。

> **前提条件:** .NET 6.0 以降と有効な Aspose.OCR ライセンス（または無料トライアル）。まだライブラリが無い場合は、`dotnet add package Aspose.OCR` で NuGet から取得してください。

---

## Aspose を使用した C# での OCR の使い方

これは、C# プロジェクトで **how to use OCR** の質問に実際に答えるコアステップです。以下のコードは完全なプログラムで、新しいコンソールアプリに貼り付けて F5 キーを押すだけで実行できます。

```csharp
using System;
using Aspose.OCR;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 1: Create the OCR engine instance.
            var ocrEngine = new OcrEngine();

            // Step 2: Load the image (or DJVU page) you want to analyze.
            // Replace the path with your own file location.
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/book-page.djvu");

            // Step 3: Run the recognition process.
            OcrResult ocrResult = ocrEngine.Recognize();

            // Step 4: Output the extracted text.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

**なぜこれが機能するのか:**  
- `OcrEngine` はエントリーポイントで、画像前処理、言語検出、文字分類という重い処理を抽象化します。  
- `ImageStream.FromFile` は多数のフォーマットに対応しており、DJVU も含まれるため、余分な変換ステップなしで **convert DJVU to text** が可能です。  
- `Recognize()` はプレーンテキスト出力、信頼度スコア、必要に応じてバウンディングボックスを保持する `OcrResult` オブジェクトを返します。

プログラムを実行すると、次のような出力が表示されます。

```
=== OCR Result ===
In the beginning God created the heavens and the earth.
```

これで完了です—最初の成功した **extract text from DJVU** 操作です。

![OCR の使用例](/images/ocr-demo.png "C# コンソールアプリで OCR を使用する様子のスクリーンショット")

*Alt text: “how to use OCR” のコンソール出力スクリーンショット。*

## OCR 用に画像をロードする

エンジンが何かを読み取る前に、**load image for OCR** を正しく行う必要があります。Aspose はほとんどのラスタ形式を標準でサポートしていますが、認識をスムーズにするためのいくつかのヒントがあります：

- **Resize large images** を最長辺 2000 px にリサイズします。サイズが大きすぎるとメモリ使用量が増え、エンジンが遅くなる可能性があります。  
- **Convert color images to grayscale** を行い、ノイズの多い背景を抑えます。`ocrEngine.Image = ImageStream.FromFile(path).ConvertToGrayscale();` を使用してください。  
- **Set DPI manually** で低解像度スキャンに対応します（`ocrEngine.Image.DpiX = 300; ocrEngine.Image.DpiY = 300;`）。

これらの調整は任意ですが、スキャンした領収書などの **extract text from image** ファイルの精度を向上させることが多いです。

## 画像からテキストを抽出する – ベストプラクティス

PNG、JPEG、BMP などの一般的な画像形式を扱う場合でも手順は同じですが、エンジンを微調整できます：

```csharp
ocrEngine.Image = ImageStream.FromFile("sample.png");

// Optional: enable language packs for better accuracy.
ocrEngine.Language = Language.English;

// Optional: set recognition mode to auto.
ocrEngine.RecognitionMode = RecognitionMode.Auto;
```

- **Language selection** は重要です。多言語文書を処理する場合は `ocrEngine.Language = Language.Multilingual;` を設定してください。  
- **RecognitionMode** は `Auto`、`Fast`、`Accurate` のいずれかに設定できます。`Accurate` は速度を犠牲にして高品質を提供するため、アーカイブ作業に使用します。

## DJVU をテキストに変換する – マルチページファイルの処理

DJVU ファイルは複数ページを含むことが多いです。Aspose は各ページを個別の画像ストリームとして扱うため、ループで処理できます：

```csharp
using Aspose.OCR;
using System.Collections.Generic;

var ocrEngine = new OcrEngine();
List<string> allPagesText = new List<string>();

int pageCount = ImageStream.GetPageCount("book.djvu");
for (int i = 1; i <= pageCount; i++)
{
    ocrEngine.Image = ImageStream.FromFile("book.djvu", i); // Load page i
    OcrResult result = ocrEngine.Recognize();
    allPagesText.Add(result.Text);
}

// Combine all pages into a single string.
string fullText = string.Join("\n--- Page Break ---\n", allPagesText);
Console.WriteLine(fullText);
```

**なぜループするのか:**  
DJVU ファイルは本質的に画像のスタックです。各ページを順に反復処理することで、**extract text from DJVU** を順序通りに行い、元の文書の流れを保持します。

## よくある落とし穴とプロのコツ

| 問題 | 発生原因 | 対策 |
|------|----------------|-----|
| **ゴミ文字** | 低 DPI または高圧縮 | 画像を拡大し、`ocrEngine.Image.DpiX/Y = 300` を設定する |
| **処理が遅い** | `Accurate` モードを大きなファイルで使用している | 大量処理では `Fast` モードに切り替える |
| **言語サポートが不足している** | デフォルト言語が英語のみ | 追加の言語パックをロードする（`ocrEngine.Language = Language.Spanish;`） |
| **メモリ不足エラー** | 高解像度ページを多数同時に読み込んでいる | ページを1つずつ処理し、リソースを解放する（`ocrEngine.Dispose();`） |

簡単な **pro tip**: ページの処理が終わったら必ず `ocrEngine.Dispose()` を呼び出してください。これによりネイティブリソースが解放され、長時間稼働するサービスでの微細なメモリリークによるクラッシュを防げます。

## OCR パイプラインのテスト

すべてが正しく動作することを確認するために、以下の簡単なチェックを試してください：

1. 認識された文字列の **長さを出力** する: `Console.WriteLine($"Characters recognized: {ocrResult.Text.Length}");`
2. 既知のテキストがある場合は、シンプルな diff ライブラリを使って **既知テキストと比較** する。
3. **信頼度スコアを記録**（`ocrResult.Confidence`）して、低品質ページを自動的に検出する。

信頼度が常に 0.7 未満の場合は、前述の画像前処理手順を見直してください。

## 次のステップ

**how to use OCR** が分かったので、ワークフローの拡張を検討してください：

- **Batch processing**: ループを `Parallel.ForEach` でラップして、大規模コレクションの処理速度を向上させます。  
- **Export to PDF**: Aspose.PDF を使用して、認識されたテキストを検索可能な PDF 用の隠しレイヤーとして埋め込みます。  
- **Integrate with AI**: 抽出した文字列を言語モデルに渡し、要約やエンティティ抽出を行います。

これらすべては、先ほど構築した同じ基盤の上に成り立っており、各ステップは我々が取り上げた **extract text from image** の原則から恩恵を受けます。

## 結論

我々は Aspose を使用した C# における **how to use OCR** を徹底的に解説し、画像のロード、**extracting text from image**、**DJVU** ファイルの処理、一般的な問題のトラブルシューティングまで網羅しました。上記の完全な実行可能サンプルは堅実な出発点を提供し、散りばめられたヒントは実務プロジェクトへの適用を助けるでしょう。  

ぜひ試してみて、特定の文書に合わせて設定を調整すれば、スキャンしたページをすぐに検索可能なテキストに変換できます。質問や協力しにくいファイルがあればコメントを残してください—ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}