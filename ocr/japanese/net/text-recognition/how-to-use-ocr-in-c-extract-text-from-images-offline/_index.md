---
category: general
date: 2026-03-07
description: C#でOCRを使用して画像ファイルからテキストを抽出する方法を学びましょう。このガイドでは、オフラインOCR、画像をテキストに変換する方法、OCR用に画像を読み込む方法を示します。
draft: false
keywords:
- how to use OCR
- extract text from image
- recognize text from png
- convert image to text
- load image for ocr
language: ja
og_description: C#でOCRを使用して画像からオフラインでテキストを抽出する方法。ステップバイステップのコード、ヒント、画像をテキストに変換するための完全な解説。
og_title: C#でOCRを使用する方法 – 完全オフラインガイド
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – オフラインで画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-images-offline/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – オフラインで画像からテキストを抽出する

.NET プロジェクトで **OCR を使用する方法** を、データをクラウドに送信せずに実現したいと考えたことはありませんか？ 同じ悩みを持つ開発者は多いです。画像ファイルからテキストを抽出したいが、ネットワークトラフィックが機密情報を漏らす可能性を恐れるケースです。  

良いニュースです。Aspose.OCR を使えば、PNG、JPEG、PDF からテキストを完全にオフラインで認識できます。このチュートリアルでは、OCR 用に画像を読み込む方法、エンジンをオフラインモードに設定する手順、そして **画像をテキストに変換** するまでの C# コードを数行で紹介します。

このガイドを終える頃には、以下ができるようになります。

* Aspose.OCR NuGet パッケージをインストールする。  
* OCR エンジンをオフライン処理用に設定する。  
* 画像を読み込んでテキストコンテンツを抽出する。  

外部サービス不要、API キー不要 — どの Windows または Linux マシンでも動作する純粋な C# コードです。

---

## 前提条件

作業を始める前に、以下が揃っていることを確認してください。

* .NET 6.0 SDK 以降（コードは .NET Framework 4.7+ でも動作します）。  
* Visual Studio 2022、VS Code、または C# をサポートする任意のエディタ。  
* **Aspose.OCR** ライブラリ — NuGet (`Aspose.OCR`) から取得できます。  
* ライブラリに同梱されている OCR リソースフォルダー（`Resources`、言語データファイルが含まれます）。  
* サンプル画像（例: `offline_test.png`）を既知のディレクトリに配置しておくこと。

> **プロのコツ:** 実行ファイルの隣にリソースフォルダーを置くと、`ResourcesPath` の設定がシンプルになります。

---

## 手順 1: Aspose.OCR NuGet パッケージをインストール

まず、プロジェクトにライブラリを追加します。プロジェクトフォルダーでターミナルを開き、次のコマンドを実行してください。

```bash
dotnet add package Aspose.OCR
```

あるいは Visual Studio の UI を使う場合は、**Dependencies → Manage NuGet Packages** を右クリックし、*Aspose.OCR* を検索して **Install** をクリックします。

> パッケージをインストールすると必要なバイナリがすべて取得されるため、追加の DLL を用意する必要はありません。

---

## 手順 2: OCR エンジンを作成し、オフラインモードに設定 (How to Use OCR – Offline Mode)

次に OCR エンジンのインスタンスを生成し、**オフライン** で動作させるよう指示します。これにより認識中にネットワークトラフィックが発生しません。

```csharp
using Aspose.OCR;
using Aspose.OCR.Settings;

// Initialize the OCR engine
var ocrEngine = new OcrEngine();

// Switch the engine to offline mode – crucial for privacy‑first apps
ocrEngine.Settings.EngineMode = EngineMode.Offline;
```

**なぜオフラインか？**  
`EngineMode` を `Online` にすると、エンジンは Aspose のクラウドに接続して言語パックをその場でダウンロードします。金融や医療など規制の厳しい環境では、このような通信が禁止されることがあります。オフラインモードを強制すれば、すべてローカルマシン内で完結します。

---

## 手順 3: エンジンに OCR リソースフォルダーの場所を指定

OCR エンジンは文字を認識するために言語データ（学習済みモデル）を必要とします。これらのファイルが格納されている場所を設定します。

```csharp
// Replace with the absolute or relative path to your Resources folder
ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";
```

フォルダーの場所が不明な場合は、NuGet パッケージディレクトリ（`%USERPROFILE%\.nuget\packages\aspose.ocr\*\resources`）を確認してください。デプロイを簡単にするため、フォルダー全体をプロジェクトにコピーしておくと便利です。

---

## 手順 4: OCR 用に画像を読み込む (Load Image for OCR)

エンジンはサポートされている任意のビットマップを受け取れます。ここではディスク上の PNG を読み込みます。

```csharp
// Load the image you want to recognize – this is the “load image for OCR” step
ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");
```

**ヒント:** API 経由でストリームから画像を処理したい場合は、`ImageStream.FromStream(yourStream)` を使用してください。

---

## 手順 5: 認識処理を実行し、画像をテキストに変換

すべての準備が整ったら OCR を起動します。`Recognize()` メソッドが本体の処理を行い、抽出されたテキストは `Text` プロパティから取得できます。

```csharp
// Perform OCR – this is where the engine reads the pixels and produces text
ocrEngine.Recognize();

// Grab the result – now you have “convert image to text” completed
string extractedText = ocrEngine.Text;
```

---

## 手順 6: 抽出したテキストを出力

最後に結果を表示します。コンソールアプリなら `Console.WriteLine`、Web API なら JSON 文字列として返すだけです。

```csharp
Console.WriteLine("=== OCR Result ===");
Console.WriteLine(extractedText);
```

プログラムを実行すると `offline_test.png` のテキスト内容が出力されます。たとえば画像に *“Hello, World!”* と書かれていれば、次のように表示されます。

```
=== OCR Result ===
Hello, World!
```

---

## 完全動作サンプル

以下はそのまま実行可能な完全版プログラムです。新規コンソールプロジェクト（`dotnet new console`）に貼り付け、パスを環境に合わせて調整してください。

```csharp
// Program.cs
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize OCR engine
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();

        // -------------------------------------------------
        // Step 2: Set offline mode – no network traffic
        // -------------------------------------------------
        ocrEngine.Settings.EngineMode = EngineMode.Offline;

        // -------------------------------------------------
        // Step 3: Provide path to OCR resource files
        // -------------------------------------------------
        ocrEngine.Settings.ResourcesPath = @"C:\MyProject\Resources";

        // -------------------------------------------------
        // Step 4: Load the image you want to recognize
        // -------------------------------------------------
        ocrEngine.Image = ImageStream.FromFile(@"C:\MyProject\offline_test.png");

        // -------------------------------------------------
        // Step 5: Run recognition and extract text
        // -------------------------------------------------
        ocrEngine.Recognize();
        string extractedText = ocrEngine.Text;

        // -------------------------------------------------
        // Step 6: Show the result
        // -------------------------------------------------
        Console.WriteLine("=== OCR Result ===");
        Console.WriteLine(extractedText);
    }
}
```

> **期待される出力:** コンソールに PNG ファイルに含まれる正確なテキストが表示されます。画像がぼやけている場合は、認識ミスが発生することがあります — 以下のトラブルシューティングセクションをご参照ください。

---

## よくある落とし穴と対策 (Recognize Text from PNG Efficiently)

| Issue | Why it Happens | How to Fix |
|-------|----------------|------------|
| **Empty output** | ResourcesPath が誤ったフォルダーを指している、または言語ファイルが欠如している。 | フォルダーに `eng.traineddata`（または他言語のファイル）が存在するか確認し、パス文字列を再チェックしてください。 |
| **Garbage characters** | 画像解像度が低すぎる、または画像が二値化されていない。 | DPI を上げる、`ImageProcessor` でシャープ化するなど前処理を行う。 |
| **Performance lag** | 大きな画像をフル解像度のまま処理している。 | OCR に渡す前に幅最大 2000 px にリサイズする。 |
| **Unsupported format** | ピクセル形式が特殊な BMP を使用している。 | まず `System.Drawing.Image.Save` で PNG または JPEG に変換する。 |

**プロのコツ:** 複数言語を認識させたい場合は、`ocrEngine.Settings.Language = Language.English | Language.French;` のように `Recognize()` 前に設定してください。

---

## FAQ

**Q: このコードは Linux でも動作しますか？**  
はい。Aspose.OCR はクロスプラットフォーム対応で、ネイティブライブラリは NuGet パッケージに同梱されています。  

**Q: Resources フォルダーが手元にありません。**  
Aspose の公式サイトから無料の言語パックをダウンロードするか、NuGet パッケージ内（`.../aspose.ocr/<version>/resources`）から抽出してください。  

**Q: 信頼度スコアは取得できますか？**  
取得可能です。`Recognize()` 後に `ocrEngine.RecognizedWords` を確認すると、各単語に `Confidence` プロパティが含まれています。

---

## 結論

C# で **OCR を使用する方法** を学び、画像ファイルからテキストを完全オフラインで抽出できるようになりました。Aspose.OCR をインストールし、`EngineMode.Offline` を設定し、リソースを指し示し、画像を読み込んで `Recognize()` を呼び出すだけで、インターネットに一切接続せずに **画像をテキストに変換** できます。  

上記コードを自分の画像パスに置き換えて、検索可能 PDF、データ入力自動化、アクセシビリティツールなどの機能構築に活用してください。次のステップとして、**PNG から大量にテキストを認識** したり、ASP.NET Core API に組み込んでフロントエンドに OCR 結果を提供したりすると良いでしょう。

Happy coding, and feel free to experiment—OCR is surprisingly forgiving once the engine is set up correctly!

--- 

![Diagram showing offline OCR workflow – how to use OCR in a secure environment](https://example.com/ocr-workflow.png "how to use OCR diagram")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}