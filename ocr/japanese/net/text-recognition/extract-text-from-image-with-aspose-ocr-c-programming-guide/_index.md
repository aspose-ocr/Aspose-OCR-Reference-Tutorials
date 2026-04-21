---
category: general
date: 2026-03-13
description: C# で Aspose OCR を使用して画像からテキストを抽出します。OCR 用に画像を読み込む方法、画像で OCR を実行する方法、そしてステップバイステップのコードでキリル文字テキストを抽出する方法を学びましょう。
draft: false
keywords:
- extract text from image
- load image for ocr
- run ocr on image
- extract cyrillic text
- recognize cyrillic text
language: ja
og_description: C#でAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、OCR用に画像をロードし、画像でOCRを実行し、キリル文字テキストを効率的に抽出する方法を示します。
og_title: Aspose OCRで画像からテキストを抽出 – C# ガイド
tags:
- Aspose OCR
- C#
- Image Processing
title: Aspose OCRで画像からテキストを抽出する – C#プログラミングガイド
url: /ja/net/text-recognition/extract-text-from-image-with-aspose-ocr-c-programming-guide/
---

Check for italic "*Why this matters:*" we kept same.

Now produce final output with all translated content.

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する（Aspose OCR） – C# プログラミングガイド

画像から **テキストを抽出** したいと思ったことはありますか？しかし、キリル文字を問題なく処理できるライブラリがどれか分からない場合も多いでしょう。請求書のスキャン、パスポートの検証、または簡単なメモ取りなど、画像から信頼できるテキストを取得することは重要です。

このガイドでは、**load image for OCR**、Aspose OCR の設定、**run OCR on image**、そして最終的に **extract Cyrillic text** を数行の C# で実行する手順を詳しく説明します。最後まで実行すれば、認識されたテキストをコンソールに出力する実行可能なスニペットが手に入ります。

## 学べること

- Aspose OCR NuGet パッケージのインストールと参照方法。  
- エンジンに言語パックリソースを指す正しい方法。  
- `Language.Cyrillic` を選択することがラテン文字以外のスクリプトで重要な理由。  
- 一般的な落とし穴（リソースが見つからない、サポートされていない画像形式）とその回避策。  
- 任意の .NET プロジェクトに貼り付け可能な、完全な実行可能サンプル。

OCR の事前経験は不要ですが、C# と Visual Studio の基本的な知識があるとスムーズに進められます。

## 前提条件

1. **.NET 6.0** 以上がインストールされていること（コードは .NET Core と .NET Framework の両方で動作します）。  
2. **Visual Studio 2022**（または C# をサポートする任意のエディタ）。  
3. **Aspose.OCR** NuGet パッケージ。Package Manager Console からインストールします：  

   ```powershell
   Install-Package Aspose.OCR
   ```

4. OCR 言語パックが格納されたフォルダー（Aspose のサイトからダウンロード可能）。  
5. 例で使用する画像ファイル（`cyrillic.png`）で、読み取りたいキリル文字が含まれています。

> **プロのコツ:** 言語パックフォルダーをプロジェクトの `bin` ディレクトリの隣に置くと、パス処理が簡単になります。

## ステップ 1 – OCR 用に画像をロード

最初に行うべきことは、エンジンにビットマップ画像を渡すことです。Aspose OCR は `ImageStream` を受け付け、これはファイルパスから直接作成できます。

```csharp
using Aspose.OCR;

// Step 1: Load the image you want to process
string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
ImageStream image = ImageStream.FromFile(imagePath);
```

*Why this matters:* 画像を早めにロードすることで、ファイルが存在し、サポートされている形式（PNG、JPEG、BMP など）であることを確認できます。ファイルが見つからない場合、`FromFile` 呼び出しは明確な例外をスローし、後の曖昧な OCR エラーを防ぎます。

## ステップ 2 – OCR エンジンとリソースの設定

次に、OCR エンジンをインスタンス化し、言語パックが格納されたフォルダーを指定します。正しいリソースが無いと、エンジンはキリル文字の字形を解釈できません。

```csharp
// Step 2: Create the OCR engine instance
OcrEngine ocrEngine = new OcrEngine();

// Tell Aspose where the language resources live
string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
ocrEngine.SetResourcesPath(resourcesPath);
```

*Why this matters:* `SetResourcesPath` メソッドは、コードと各言語の文字形状データファイルをつなぐ橋渡しです。この手順を忘れると、出力が文字化けしたり `ResourceNotFoundException` が発生したりします。

## ステップ 3 – 言語を選択し **Run OCR on Image**

ここで、期待する言語を選択します。例ではキリル文字を扱うので `Language.Cyrillic` を設定します。複数のスクリプトを扱う必要がある場合は、ビット単位 OR（`|`）演算子で組み合わせることができます。

```csharp
// Step 3: Select the language you want to recognize
ocrEngine.Language = Language.Cyrillic;

// Assign the previously loaded image to the engine
ocrEngine.Image = image;

// Finally, perform the recognition
ocrEngine.Recognize();
```

*Why this matters:* 言語を指定することで OCR アルゴリズムの検索空間が狭まり、速度と精度が大幅に向上します。正しい言語フラグで **Run OCR on image** を実行すれば、誤認識が格段に減ります。

## ステップ 4 – 抽出されたキリル文字テキストの取得と利用

認識が完了すると、エンジンは結果を `Text` プロパティに格納します。これをコンソールに表示したり、ファイルに書き出したり、別のシステムに渡したりできます。

```csharp
// Step 4: Output the recognized text
string recognizedText = ocrEngine.Text;
Console.WriteLine("=== Extracted Cyrillic Text ===");
Console.WriteLine(recognizedText);
```

典型的なコンソール出力は次のようになります：

```
=== Extracted Cyrillic Text ===
Привет, мир! Это тестовое изображение.
```

出力に予期しない記号が含まれる場合は、言語パックがインストールした Aspose OCR のバージョンと一致しているか再確認してください。

## 完全動作例 – すべてのステップを統合

以下は新しいコンソールプロジェクトにコピー＆ペーストできる完全なプログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えてください。

```csharp
using System;
using Aspose.OCR;

namespace ExtractCyrillicDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // 1️⃣ Load the image you want to process
            string imagePath = @"YOUR_DIRECTORY\cyrillic.png";
            ImageStream image = ImageStream.FromFile(imagePath);

            // 2️⃣ Initialize OCR engine and point to language resources
            OcrEngine ocrEngine = new OcrEngine();
            string resourcesPath = @"YOUR_DIRECTORY\OcrResources";
            ocrEngine.SetResourcesPath(resourcesPath);

            // 3️⃣ Choose Cyrillic language and run OCR on image
            ocrEngine.Language = Language.Cyrillic;
            ocrEngine.Image = image;
            ocrEngine.Recognize();

            // 4️⃣ Extract and display the text
            string result = ocrEngine.Text;
            Console.WriteLine("=== Extracted Cyrillic Text ===");
            Console.WriteLine(result);
        }
    }
}
```

### 期待される結果

プログラムを実行すると、`cyrillic.png` に表示されているテキストがそのままコンソールに出力されます。画像に “Привет, мир!” というフレーズが含まれていれば、余計な記号なしでその行が表示されます。

## エッジケースとトラブルシューティング

| 状況 | 確認項目 | 推奨修正 |
|-----------|---------------|---------------|
| **言語パックが欠如** | `resourcesPath` が `.dat` ファイルを含むフォルダーを指していますか？ | Aspose からパックを再ダウンロードし、指定フォルダーに配置してください。 |
| **サポート外の画像形式** | ファイルは PNG、JPEG、BMP、または TIFF ですか？ | `FromFile` を呼び出す前に、サポートされている形式のいずれかに画像を変換してください。 |
| **出力にゴミ文字** | `ocrEngine.Language` を正しく設定しましたか？ | `Language.Cyrillic` を使用してください（複数言語の場合はフラグを組み合わせます）。 |
| **大画像でのパフォーマンス低下** | 画像解像度が 3000 px を超えていますか？ | OCR 前に画像を適切なサイズ（例: 幅 1024 px）に縮小してください。 |

## 次に探求できる関連トピック

- **Extract text from image** を PDF で Aspose PDF + OCR を使用して抽出。  
- `Stream` から **Load image for OCR**（Web API から画像が来る場合に便利）。  
- バッチ処理を高速化するために **run OCR on image** を並列で使用。  
- 手書きメモから **Extract cyrillic text** を Aspose OCR の手書きモードで抽出。  
- データベースで検索インデックス用に **recognize cyrillic text** と統合。

## 結論

ここでは Aspose OCR を使用して **extract text from image** を行う方法を示しました。画像のロードから認識されたキリル文字のコンソール出力までを網羅しています。短く自己完結型のプログラムは必要最小限のコードを示し、トラブルシューティング表は最も一般的な問題からあなたを守ります。

ぜひご自身のスクリーンショットで試してみて、言語パックをアラビア語や中国語に差し替えて、同じパターンが世界中でどのように機能するか確認してください。コーディングを楽しみ、OCR の結果が常にクリアでありますように！

![Extract text from image example](extract-text-from-image.png "Extract text from image example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}