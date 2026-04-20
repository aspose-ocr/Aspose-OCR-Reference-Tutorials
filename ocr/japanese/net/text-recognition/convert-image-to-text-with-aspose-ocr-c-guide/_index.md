---
category: general
date: 2026-02-14
description: C#で Aspose OCR を使用して画像をテキストに変換します。画像からアラビア語テキストを抽出する方法、OCR 用に画像を読み込む方法、そしてアラビア語を効率的に認識する方法を学びましょう。
draft: false
keywords:
- convert image to text
- extract text from picture
- how to extract arabic text
- load image for ocr
- how to recognize arabic
language: ja
og_description: C#でAspose OCRを使用して画像をテキストに変換する。このチュートリアルでは、画像からアラビア語テキストを抽出し、OCR用に画像を読み込み、アラビア語を認識する方法を示します。
og_title: Aspose OCRで画像をテキストに変換 – C# ガイド
tags:
- OCR
- C#
- Aspose
title: Aspose OCRで画像をテキストに変換 – C# ガイド
url: /ja/net/text-recognition/convert-image-to-text-with-aspose-ocr-c-guide/
---

to keep all placeholders unchanged.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR を使用した画像からテキストへの変換 – C# ガイド

C# アプリケーションで **画像からテキストへ変換** したいですか？画像からテキストへの変換は一般的な作業で、特に非ラテン文字を含む **画像からテキストを抽出** する必要がある場合に重要です。このチュートリアルでは、**アラビア語テキストの抽出方法**、**OCR 用の画像のロード方法**、そして Aspose.OCR ライブラリを使用して **アラビア語文字を認識** するために必要な正確な手順を示す、完全に実行可能なサンプルを順に解説します。

NuGet パッケージのインストールから、フォントが欠如している場合や低解像度スキャンといったエッジケースの処理まで、すべてをカバーします。最後まで読めば、外部ツールを必要とせずに、認識されたアラビア語文字列をコンソールに出力する自己完結型プログラムが手に入ります。

## 学習できること

- .NET プロジェクトに Aspose.OCR を追加する方法（2026 年時点の最新バージョン）
- **画像からテキストへ変換** に必要な正確なコードと各行が重要な理由
- アラビア文字グリフを扱う際の精度向上のヒント
- ファイルパスまたはストリームから **OCR 用の画像をロード** する方法
- 一般的な落とし穴のトラブルシューティング方法（例：言語設定の誤り、サポート外の画像形式）

> **プロのコツ:** .NET 6 以降を対象とする場合、トップレベルステートメントを使用してコードをさらに短くできます。以下の例は最大の互換性を保つために従来の `Program` クラスを使用しています。

## 前提条件

- .NET 6 SDK（または最近の .NET バージョン）
- Visual Studio 2022 または C# 拡張機能付き VS Code
- NuGet パッケージ `Aspose.OCR`（`dotnet add package Aspose.OCR` でインストール）
- アラビア語テキストを含む画像ファイル（例：`arabic_sign.jpg`）

---

## 画像からテキストへの変換 – ステップバイステップ実装

以下は新しいコンソールプロジェクトにコピー＆ペーストできる完全なソースファイルです。**必要なすべての `using` ディレクティブ**、`Main` メソッド、そして各操作の *理由* を説明するインラインコメントが含まれています。

```csharp
// ------------------------------------------------------------
// Program.cs – Complete example to convert image to text
// ------------------------------------------------------------
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

namespace AsposeOcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Create the OCR engine – this object holds the core logic.
            var ocrEngine = new Engine();

            // 2️⃣ Configure OCR options.
            //    We set the language to Arabic because the picture contains Arabic script.
            //    You can replace Language.Arabic with any other supported language.
            var ocrOptions = new OcrOptions
            {
                Language = Language.Arabic
            };

            // 3️⃣ Load the image you want to process.
            //    ImageStream.FromFile reads the file into a stream that Aspose can handle.
            //    If your image is in a different folder, adjust the path accordingly.
            var inputImage = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

            // 4️⃣ Run OCR – the Recognize method returns an OcrResult object.
            var ocrResult = ocrEngine.Recognize(inputImage, ocrOptions);

            // 5️⃣ Output the recognized text to the console.
            Console.WriteLine("=== OCR Result ===");
            Console.WriteLine(ocrResult.Text);
        }
    }
}
```

### 期待される出力

`arabic_sign.jpg` にフレーズ **"مطار دولي"**（意味は “International Airport”）が含まれている場合、コンソールには次のように表示されます。

```
=== OCR Result ===
مطار دولي
```

正確な綴りは画像の品質により若干異なる場合がありますが、文字化けではなくアラビア文字が表示されるはずです。

---

## アラビア語テキストの抽出方法 – 言語設定

`Language = Language.Arabic` を明示的に設定する理由は何ですか？Aspose.OCR は多数の言語をサポートしていますが、デフォルトは英語です。アラビア語は右から左へ書くスクリプトで、文脈依存のグリフ形状があります。エンジンに正しい言語を指定することで、以下が有効になります：

- **合字検出** – 文字が結合する（例: “لا”）
- **右から左への順序付け** – 出力文字列が正しく向きます
- **辞書チェックの強化** – エンジンがアラビア語単語リストと照合し、精度を向上させます

複数言語を含む **画像からテキストを抽出** する必要がある場合は、`OcrOptions.Language` に `Language` 列挙体の配列を渡すことができます（例: `new[] { Language.Arabic, Language.English }`）。

---

## OCR 用の画像ロード – 画像の読み込み

`ImageStream.FromFile(...)` は **OCR 用の画像をロード** する最もシンプルな方法です。ただし、次のようなシナリオに遭遇することがあります：

- 画像がデータベースの BLOB に格納されている。
- HTTP リクエストで画像を受け取る。
- ファイルが非標準形式（例: 複数ページの TIFF）である。

そのような場合は、`MemoryStream` から `ImageStream` を作成できます：

```csharp
byte[] bytes = System.IO.File.ReadAllBytes("path/to/image.png");
using var memStream = new System.IO.MemoryStream(bytes);
var inputImage = ImageStream.FromStream(memStream);
```

どちらのアプローチもエンジンに同じ内部表現を渡すため、OCR の品質は変わりません。

---

## アラビア語を認識する方法 – エンジンの実行

`ocrEngine.Recognize(inputImage, ocrOptions)` を呼び出すと、エンジンは複数の内部ステージを実行します：

1. **前処理** – ノイズ除去、二値化、傾き補正。
2. **セグメンテーション** – 画像を行、単語、文字に分割。
3. **分類** – 各セグメントを既知のアラビア語グリフと照合。
4. **後処理** – 言語規則と信頼度閾値を適用。

信頼度スコアが低い場合は、次の点を検討してください：

- **画像解像度の向上**（アラビア語では最低 300 dpi を推奨）。
- **コントラスト調整**（画像を入力する前に、`System.Drawing` や `ImageSharp` などのシンプルな画像処理ライブラリを使用）。
- **`ocrOptions.UseLanguageDictionary = true` を有効化**して、より厳格な辞書チェックを行う。

---

## よくある落とし穴と回避策

| 症状 | 考えられる原因 | 対策 |
|------|----------------|------|
| 出力が空 | ファイルパスが間違っている、またはサポート外の形式 | パスを確認し、`File.Exists` を使用し、画像が PNG/JPEG/BMP であることを確認する |
| 文字化け | 言語がアラビア語に設定されていない | `OcrOptions` で `Language = Language.Arabic` を設定する |
| 精度が低い | 画像がぼやけている、または dpi が低い | より高解像度のソースを使用するか、シャープフィルタを適用する |
| 例外 `ArgumentNullException` | `inputImage` が null | ファイルが存在すること、ストリームが正しく開かれていることを確認する |

---

## 完全動作例（コピー＆ペースト可能）

名前空間なしの単一ファイルを好む場合、ベストプラクティスを守ったコンパクトなバージョンをご紹介します：

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class ConvertImageToText
{
    static void Main()
    {
        // Engine creation
        var engine = new Engine();

        // Set OCR options – Arabic language
        var options = new OcrOptions { Language = Language.Arabic };

        // Load image – change the path to your actual file
        var image = ImageStream.FromFile("YOUR_DIRECTORY/arabic_sign.jpg");

        // Perform recognition
        var result = engine.Recognize(image, options);

        // Show result
        Console.WriteLine("=== Recognized Arabic Text ===");
        Console.WriteLine(result.Text);
    }
}
```

`dotnet run` でプログラムを実行すると、コンソールにアラビア語テキストが表示されます。

---

## ビジュアルまとめ

以下はコンソール出力を示すプレースホルダー画像です。**alt テキスト** には SEO 対応のための主要キーワードが含まれています。

![convert image to text example – console showing Arabic OCR result](convert-image-to-text-example.png)

---

## 結論

ここでは、C# で Aspose OCR を使用して **画像からテキストへ変換** する方法を実演しました。チュートリアルでは、ライブラリのインストール、言語設定（**アラビア語テキストの抽出方法**）、画像のロード、そして最終的に **アラビア語文字を認識** する単一メソッド呼び出しまでを網羅しました。  

この知識を活用すれば、デスクトップユーティリティ、Web API、またはスキャン文書のバッチ処理を行うバックグラウンドサービスなど、あらゆる .NET プロジェクトに OCR を組み込むことができます。

### 次にやること

- `Language.Arabic` を `Language.French`、`Language.ChineseSimplified` などに変更して、他の言語を試す。
- OCR と **画像からテキストを抽出** パイプラインを組み合わせ、結果をデータベースに保存する。
- `ocrResult.Confidence` プロパティを使用して、低信頼度の行を永続化前にフィルタリングする。

エッジケースやパフォーマンスチューニングに関する質問がありますか？コメントを残すか、ディスカッションスレッドで質問してください。コーディングを楽しんで、画像が常にクリーンで検索可能なテキストを生成しますように！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}