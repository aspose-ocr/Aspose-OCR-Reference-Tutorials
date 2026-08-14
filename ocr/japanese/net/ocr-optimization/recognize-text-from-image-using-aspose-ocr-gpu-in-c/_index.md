---
category: general
date: 2026-02-20
description: Aspose OCR の GPU 加速を使用して画像からテキストを高速に認識します。完全な実行可能サンプルで、C# でスキャンからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- recognize text from image
- extract text from scan
- Aspose OCR GPU
- C# OCR tutorial
- image to text conversion
language: ja
og_description: GPUアクセラレーションを使用して画像からテキストを認識します。このチュートリアルでは、Aspose OCR を利用して C# でスキャンからテキストを抽出する方法を、コードとヒントとともに紹介します。
og_title: Aspose OCR GPU を使用して画像からテキストを認識する – C# ガイド
tags:
- Aspose
- OCR
- C#
- GPU
title: C#でAspose OCR GPUを使用して画像からテキストを認識する
url: /ja/net/ocr-optimization/recognize-text-from-image-using-aspose-ocr-gpu-in-c/
---

acceleration you can turn a massive scanned TIFF into clean, searchable text in seconds."

Translate to Japanese.

Proceed.

Will keep code block placeholders unchanged.

Now produce final answer.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU を使用した C# での画像からテキスト認識

画像からテキストを **認識** したいけれど、ファイルが巨大で CPU がパンクしたことはありませんか？従来の OCR ライブラリを試して、処理に時間がかかりすぎたり、結果が断片的だったりした経験があるかもしれません。朗報です！Aspose OCR の GPU 加速を使えば、巨大なスキャン TIFF を数秒でクリーンな検索可能テキストに変換できます。

このガイドでは、GPU 対応マシン上で **スキャンファイルからテキストを抽出** するための、コピー＆ペーストだけで動く完全なサンプルを順を追って解説します。曖昧な説明は省き、必要なコード、各行の意味、そしてトラブル回避のポイントを紹介します。

## 必要な環境

- **.NET 6+**（または .NET Framework 4.7+ – API は同じです）
- **Aspose.OCR for .NET** NuGet パッケージ（バージョン 23.12 以降）
- CUDA 対応 **GPU**（任意ですが、劇的に高速化します）
- 高解像度のスキャン画像（例: `large_doc.tif`）

GPU がなくても、エンジンは自動的に CPU にフォールバックするので、例は実行できますが少し遅くなります。

## Step 1 – Aspose.OCR パッケージのインストール

ターミナルまたは Package Manager Console で次を実行します:

```bash
dotnet add package Aspose.OCR
```

または Visual Studio の NuGet UI で **Aspose.OCR** を検索し、*Install* をクリックします。これによりコア OCR ライブラリとオプションの GPU 加速アセンブリが取得されます。

> **プロのコツ:** インストール後、`packages` フォルダーに `Aspose.OCR.Acceleration.dll` があるか確認してください。GPU サポートに必須です。ヘッドレスサーバーの場合は省略してもコンパイルは通ります。

## Step 2 – GPU 加速 OCR エンジンの初期化

`GpuOcrEngine` クラスは互換性のある GPU を自動検出します。デバイスが複数ある場合は特定のものを選択できますが、ほとんどの開発者は自動選択に任せます。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration;   // <-- enables GPU support

class GpuExample
{
    static void Main()
    {
        // Step 2.1: Create the OCR engine. It will look for a CUDA‑compatible GPU.
        GpuOcrEngine ocrEngine = new GpuOcrEngine();

        // Step 2.2 (optional): Force a particular GPU device.
        // Uncomment the line below if you know the device ID you want to use.
        // ocrEngine.Device = GpuDevice.GetById(0);
```

**重要ポイント:** GPU エンジンは一度だけ初期化すればオーバーヘッドが低く抑えられます。ループ内でエンジンを繰り返し生成・破棄すると、パフォーマンス向上が失われます。

## Step 3 – 高解像度スキャン画像の読み込み

Aspose OCR は `System.Drawing.Image` を使用します。ファイルパスが実際の画像を指していることを確認してください。存在しない場合は `FileNotFoundException` がスローされます。

```csharp
        // Step 3: Load the image you want to process.
        // Replace YOUR_DIRECTORY with the actual folder on your machine.
        var scannedImage = Image.FromFile(@"YOUR_DIRECTORY/large_doc.tif");
```

> **エッジケース:** 画像が 10 000 × 10 000 px を超える場合は、まずダウンサンプリングを検討してください。GPU メモリは有限で、巨大ビットマップの読み込みは `OutOfMemoryException` を引き起こす可能性があります。

## Step 4 – デフォルト（ラテン文字）言語設定で OCR 実行

`Recognize` メソッドはプレーン文字列を返します。別言語やカスタム前処理が必要な場合は `OcrOptions` オブジェクトを渡せます。

```csharp
        // Step 4: Run OCR. By default it assumes Latin script.
        string recognizedText = ocrEngine.Recognize(scannedImage);
```

**デフォルトが有効な理由:** 契約書、請求書、レポートなど、ほとんどのスキャン文書はラテン系アルファベットです。キリル文字、アラビア文字、中文が必要な場合は、`ocrEngine.Language = "ru"`（または該当する ISO コード）を `Recognize` 呼び出し前に設定してください。

## Step 5 – 抽出したテキストの表示または保存

簡易的な確認としてコンソールに結果を書き出します。実際のアプリではデータベース、`.txt` ファイル、あるいは検索インデックスに保存することが考えられます。

```csharp
        // Step 5: Output the OCR result.
        Console.WriteLine(recognizedText);

        // Optional: Save to a file.
        // File.WriteAllText(@"output.txt", recognizedText);
    }
}
```

### 期待される出力

`large_doc.tif` にシンプルな段落「Hello, world!」が含まれている場合、次のように表示されます:

```
Hello, world!
```

複数ページのスキャンでは、エンジンは読み取り順にテキストを連結します。ページ境界が必要な場合は改行 (`\n`) で分割できます。

## 共通の落とし穴と対策

| 問題 | 症状 | 対策 |
|-------|---------|-----|
| **GPU が検出されない** | `ocrEngine.Device` が `null` で処理が遅い | 最新の NVIDIA ドライバと CUDA Toolkit（v11 以上）をインストールし、`nvidia-smi` で確認 |
| **ガベージコレクションの遅延** | 多数の画像処理後にメモリが急増 | OCR 後に `scannedImage.Dispose()` を呼ぶか、`using` ブロックで画像を囲む |
| **言語設定ミス** | ラテン文字以外が文字化け | `Recognize` 前に `ocrEngine.Language` を正しい ISO 639‑1 コードに設定 |
| **極端に大きなファイル** | `OutOfMemoryException` | `Image.GetThumbnailImage` でダウンサンプリングするか、スキャンをタイルに分割 |

## 完全な実行可能サンプル

以下に、`using` ディレクティブ、エラーハンドリング、画像用の tidy `using` ブロックを含む全プログラムを示します:

```csharp
using System;
using System.Drawing;
using System.IO;
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Acceleration; // GPU support

class GpuOcrDemo
{
    static void Main()
    {
        try
        {
            // Initialize the GPU‑accelerated OCR engine.
            GpuOcrEngine ocrEngine = new GpuOcrEngine();

            // OPTIONAL: Choose a specific GPU device.
            // ocrEngine.Device = GpuDevice.GetById(0);

            // Load the high‑resolution scanned image.
            string imagePath = @"YOUR_DIRECTORY/large_doc.tif";
            if (!File.Exists(imagePath))
                throw new FileNotFoundException($"Image not found: {imagePath}");

            using (Image scannedImage = Image.FromFile(imagePath))
            {
                // Perform OCR (defaults to Latin script).
                string text = ocrEngine.Recognize(scannedImage);

                // Output the extracted text.
                Console.WriteLine("=== OCR Result ===");
                Console.WriteLine(text);

                // Save to a text file (optional).
                string outputPath = Path.ChangeExtension(imagePath, ".txt");
                File.WriteAllText(outputPath, text);
                Console.WriteLine($"Text saved to {outputPath}");
            }
        }
        catch (Exception ex)
        {
            Console.Error.WriteLine($"Error: {ex.Message}");
        }
    }
}
```

### コードの概要

1. **作成**: 最適な GPU を自動選択する `GpuOcrEngine` を生成  
2. **読み込み**: `using` ブロックで対象 TIFF をロードし、確実に破棄  
3. **呼び出し**: `Recognize` でビットマップを文字列に変換  
4. **書き出し**: コンソールと、ソース画像と同じフォルダーにある `.txt` ファイルの両方に結果を書き込む  
5. **例外処理**: 例外を捕捉し、分かりやすいエラーメッセージを表示  

## 更なる展開 – 「画像からテキスト認識」からフルスケール文書パイプラインへ

テキスト抽出ができたら、次のステップを検討してください:

- **バッチ処理**: フォルダー内の TIFF をループし、結果を単一の検索可能インデックスに集約  
- **言語検出**: `ocrEngine.DetectLanguage()`（利用可能な場合）で自動的に言語を切り替え  
- **後処理**: スペルチェッカーや正規表現フィルタで OCR アーティファクトをクリーンアップ  
- **Azure Cognitive Search との統合**: 抽出テキストをクラウド検索インデックスにプッシュし、即時検索を実現  

これらはすべて、今回学んだ「エンジンを一度初期化 → 画像を供給 → テキストを取得」のパターンに基づいています。

## 結論

Aspose OCR の GPU 加速エンジンを C# で使用し、**画像からテキストを認識**する方法を学びました。完全な実行例は、エンジンのセットアップ、高解像度スキャンの読み込み、OCR の実行、出力の処理方法を示しています。上記のヒントとエッジケース対策を守れば、開発者ノートパソコンでも本番サーバーでも、信頼性の高い結果が得られます。

さらに多くのスキャンを検索可能データに変換したいですか？フォルダー全体を処理したり、非ラテン言語に挑戦したり、全文検索エンジンに結果を流し込んだりしてみてください。可能性は無限大です。今回書いたコードがその堅実な基盤となります。

Happy coding! 🚀

![画像からテキスト認識の例](/images/ocr-gpu

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}