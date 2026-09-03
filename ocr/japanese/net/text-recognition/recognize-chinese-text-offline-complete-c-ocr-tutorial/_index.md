---
category: general
date: 2026-01-02
description: Aspose.OCR を使用したオフライン文字認識で、中国語テキストを認識し、PNG ファイルからテキストを抽出する方法を学びましょう。インターネットは不要です
  – 数ステップで画像の OCR を実行できます。
draft: false
keywords:
- recognize chinese text
- extract text from png
- offline text recognition
- perform OCR on image
language: ja
og_description: インターネットなしで中国語テキストを認識します。このチュートリアルでは、オフライン文字認識を使用してPNGからテキストを抽出し、C#で画像に対してOCRを実行する方法を示します。
og_title: オフラインで中国語テキストを認識する – ステップバイステップ C# ガイド
tags:
- OCR
- C#
- Aspose
title: オフラインで中国語テキストを認識 – 完全なC# OCRチュートリアル
url: /ja/net/text-recognition/recognize-chinese-text-offline-complete-c-ocr-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# オフラインで中国語テキストを認識 – 完全な C# OCR チュートリアル

スキャンした PNG から **中国語テキストを認識** したいが、アプリがインターネットに接続できないマシンで動作する必要がありますか？ あなたは一人ではありません。多くのエンタープライズシナリオ—たとえばエアギャップされたサーバーやフィールドデバイス—では、クラウドサービスに依存することは選択肢になりません。

このガイドでは、**png からテキストを抽出** し、**オフラインでテキスト認識** を実行し、Aspose.OCR を使用して **画像アセットで OCR を実行** する自己完結型ソリューションを順を追って説明します。最後には、コンソールに中国語文字を直接出力する C# コンソールプログラムが完成します。

## 前提条件

- .NET 6 SDK（または任意の最新 .NET バージョン）がローカルにインストールされていること。  
- Visual Studio 2022 または VS Code のいずれか。  
- Aspose.OCR for .NET の NuGet パッケージ（`Aspose.OCR`）のコピー。  
- 英語と簡体字中国語用の言語リソースファイル（チュートリアルで自動ダウンロード方法を示します）。  
- `chinese_doc.png` という名前の画像を、参照できるフォルダー（`YOUR_DIRECTORY` プレースホルダー）に配置しておくこと。

追加のサービスや API キーは不要です—ローカル DLL と数個のリソースファイルだけで完結します。

---

## 手順 1 – 必要な言語リソースをダウンロード（1 回だけ）

Aspose.OCR は言語パックをディスクに保存します。アプリを初めて実行する際にそれらを取得する必要があります。`ResourceManager.DownloadResources` 呼び出しがまさにそれを行い、英語と簡体字中国語の両方を指定することで、後でネットワークトラフィックなしにエンジンが切り替えられます。

```csharp
using Aspose.OCR;

// Download English and Simplified Chinese language packs (run once)
ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);
```

> **プロのコツ:** ダウンロードしたフォルダー（`Aspose.OCR.Resources`）をソース管理下に置いておくと、複数マシンで再現可能なビルドが容易になります。

## 手順 2 – オフラインモードで OCR エンジンを初期化

`OfflineMode = true` を設定すると、ライブラリは HTTP 呼び出しを行わなくなります。これが真の **オフラインテキスト認識** の鍵です。

```csharp
// Initialise the OCR engine for offline use
var ocrEngine = new OcrEngine()
{
    OfflineMode = true   // Guarantees no network traffic
};
```

> **重要な理由:** 言語パックが欠如している場合にクラウドサービスへフォールバックする OCR ライブラリがあります。オフラインモードを強制することで、決定的なパフォーマンスとデータプライバシーポリシーへの準拠が保証されます。

## 手順 3 – 処理したい PNG を読み込む

画像の読み取りには `System.Drawing.Bitmap` を使用します。プロジェクトが .NET 6+ で非 Windows プラットフォームを対象とする場合は、代替として `SkiaSharp` を検討してください。ほとんどの Windows 中心のデプロイでは `Bitmap` で問題ありません。

```csharp
using System.Drawing;

// Load the PNG that contains Chinese characters
var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
var image = new Bitmap(imagePath);
```

> **エッジケース:** PNG が非常に大きい（5 MP 超）場合は、認識速度向上とメモリ使用量削減のために先に縮小するとよいでしょう。

```csharp
// Optional downscale for huge images
if (image.Width * image.Height > 5_000_000)
{
    var scaled = new Bitmap(image, new Size(image.Width / 2, image.Height / 2));
    image.Dispose();
    image = scaled;
}
```

## 手順 4 – 簡体字中国語で認識を実行

ここでエンジンに使用する言語を明示します。`RecognitionOptions` オブジェクトは `DetectOrientation` や `PreserveFormatting` などの調整も可能ですが、既定設定でほとんどの印刷文書に対して十分に機能します。

```csharp
using Aspose.OCR;

// Perform OCR using Simplified Chinese language pack
var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
{
    Language = Language.ChineseSimplified
});
```

## 手順 5 – 抽出したテキストを表示（またはさらに処理）

`OcrResult.Text` プロパティにプレーンテキストが格納されます。コンソールへの出力、ファイルへの書き込み、あるいは下流の NLP パイプラインへの入力として利用できます。

```csharp
// Output the recognized Chinese text to the console
Console.WriteLine("=== Recognized Chinese Text ===");
Console.WriteLine(ocrResult.Text);
```

### 期待される出力

`chinese_doc.png` に「你好，世界！」というフレーズが含まれている場合、コンソールは次のように表示します：

```
=== Recognized Chinese Text ===
你好，世界！
```

> **注記:** OCR の精度は画像の品質、フォントの明瞭さ、コントラストに依存します。最高の結果を得るには、300 dpi 以上の高解像度スキャンを使用し、テキストが歪んでいないことを確認してください。

---

## 完全動作サンプル

以下はコピー＆ペーストで使用できる完全版プログラムです。新しいコンソールプロジェクト内に `Program.cs` として保存し、`dotnet run` を実行してください。リソースダウンロードから最終出力までのすべての手順がひとつにまとめられています。

```csharp
// Program.cs
using Aspose.OCR;
using System;
using System.Drawing;

class OfflineExample
{
    static void Main()
    {
        // 1️⃣ Download language resources (only needed once)
        ResourceManager.DownloadResources(Language.English, Language.ChineseSimplified);

        // 2️⃣ Initialise OCR engine in offline mode
        var ocrEngine = new OcrEngine()
        {
            OfflineMode = true
        };

        // 3️⃣ Load the PNG image
        var imagePath = @"YOUR_DIRECTORY\chinese_doc.png";
        using var image = new Bitmap(imagePath);

        // 4️⃣ Recognise Simplified Chinese text
        var ocrResult = ocrEngine.Recognize(image, new RecognitionOptions
        {
            Language = Language.ChineseSimplified
        });

        // 5️⃣ Print the result
        Console.WriteLine("=== Recognized Chinese Text ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

> **ヒント:** インターネットが完全に利用できない状況でも優雅に処理したい場合は、`ResourceManager.DownloadResources` 呼び出しを `try/catch` ブロックでラップし、`NetworkException` がスローされたときに適切に対処してください。

---

## よくある質問 (FAQ)

| 質問 | 回答 |
|----------|--------|
| **繁体字中国語も認識できますか？** | はい—`Language.ChineseSimplified` を `Language.ChineseTraditional` に置き換え、対応するパックをダウンロードしてください。 |
| **PNG ではなく JPEG からテキストを抽出したい場合は？** | 同じコードで動作します。ファイル拡張子を変更するだけです。`Bitmap` はほとんどの一般的なラスタ形式をサポートしています。 |
| **各文字のバウンディングボックスを取得する方法はありますか？** | `RecognitionOptions.DetectRegions = true` を設定します。`OcrResult` に座標情報を持つ `Region` オブジェクトが含まれます。 |
| **Linux で実行するにはどうすればよいですか？** |`System.Drawing.Common` パッケージ（1.0 以上）を使用します。ヘッドレス Linux 環境では `libgdiplus` のネイティブ依存関係が必要になることがあります。 |
| **画像フォルダーをバッチ処理できますか？** | もちろんです—認識ロジックを `foreach (var file in Directory.GetFiles(folder, "*.png"))` ループでラップすれば実現できます。 |

---

## 次のステップ & 関連トピック

- **精度向上**: `RecognitionOptions.PreprocessImage = true` を試して、エンジンに自動コントラスト強調を任せましょう。  
- **複数言語の組み合わせ**: `ResourceManager.DownloadResources` に言語配列を渡すことで、エンジンに自動検出させることができます。  
- **UI への統合**: コンソールコードを WinForms や WPF アプリに組み込み、テキストボックスに OCR 結果を表示させましょう。  
- **他の Aspose ライブラリの活用**: PDF 生成には `Aspose.PDF`、スライド自動化には `Aspose.Slides` などがあります。  

他の画像形式からテキストを抽出したい場合も、同様のパターンが適用できます—ファイルパスを差し替え、必要に応じて前処理オプションを調整してください。コーディングを楽しんでください！

---

![recognize chinese text example](/images/recognize-chinese-text.png "コンソールに表示された中国語テキスト認識結果のスクリーンショット")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}