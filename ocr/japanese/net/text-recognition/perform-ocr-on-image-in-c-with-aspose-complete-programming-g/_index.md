---
category: general
date: 2026-06-16
description: C#でAspose OCRを使用して画像のOCRを実行します。JSON結果の取得方法、ファイルの扱い方、一般的な問題のトラブルシューティングをステップバイステップで学びましょう。
draft: false
keywords:
- perform OCR on image
- Aspose OCR C#
- JSON result handling
- C# image recognition
- OCR engine configuration
language: ja
og_description: C#でAspose OCRを使用して画像のOCRを実行します。このガイドでは、JSON出力、エンジンの設定、実用的なヒントをご紹介します。
og_title: C#で画像のOCRを実行する – 完全なAspose OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Perform OCR on image using Aspose OCR in C#. Learn step‑by‑step how
    to get JSON results, handle files, and troubleshoot common issues.
  headline: Perform OCR on Image in C# with Aspose – Complete Programming Guide
  type: TechArticle
- questions:
  - answer: Aspose.OCR handles PNG, JPEG, BMP, TIFF, and GIF. If you need to work
      with PDFs, convert each page to an image first (Aspose.PDF can help).
    question: What image formats are supported?
  - answer: Yes – set `ocrEngine.Settings.ResultFormat = ResultFormat.Text;`. JSON
      is preferred when you need more metadata.
    question: Can I get plain text instead of JSON?
  - answer: Feed each page image to `RecognizeImage` in a loop and concatenate the
      results, or use `RecognizePdf` which returns a combined JSON structure.
    question: How do I handle multi‑page documents?
  - answer: For batch processing, reuse a single `OcrEngine` instance rather than
      creating a new one per image. Also, enable `RecognitionMode.Fast` if accuracy
      can be traded for speed.
    question: Performance concerns?
  - answer: Without a license, the output JSON will include a watermark field. Apply
      your license early in `Main` with `License license = new License(); license.SetLicense("Aspose.OCR.lic");`.
    question: License warnings?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
title: Aspose を使用した C# で画像の OCR を実行する – 完全プログラミングガイド
url: /ja/net/text-recognition/perform-ocr-on-image-in-c-with-aspose-complete-programming-g/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で画像に OCR を実行する – 完全プログラミングガイド

画像ファイルに **OCR を実行** したいけど、生のピクセルをテキストに変換する方法が分からない…という経験はありませんか？領収書のスキャン、パスポートからのデータ抽出、古い文書のデジタル化など、**画像に OCR を実行** できることは .NET 開発者にとって大きな変化をもたらします。

このチュートリアルでは、Aspose.OCR ライブラリを使って **画像に OCR を実行** し、結果を JSON で取得し、下流処理のために保存するハンズオン例をステップバイステップで解説します。最後まで読めば、すぐに実行できるコンソールアプリ、各設定項目の明確な説明、そして一般的な落とし穴を回避するためのプロのコツが手に入ります。

## 前提条件

始める前に以下を用意してください：

- .NET 6.0 SDK 以降（Microsoft のサイトからダウンロード可能）。  
- 有効な Aspose.OCR ライセンスまたは無料トライアル – ライセンスなしでも動作しますが透かしが入ります。  
- **画像に OCR を実行** したい画像ファイル（PNG、JPEG、TIFF） – 本ガイドでは `receipt.png` を使用します。  
- Visual Studio 2022、VS Code、またはお好みのエディタ。

`Aspose.OCR` 以外の NuGet パッケージは必要ありません。

## 手順 1: プロジェクトの作成と Aspose.OCR のインストール

まず、コンソールプロジェクトを新規作成し、OCR ライブラリを導入します。

```bash
dotnet new console -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

> **プロのコツ:** Visual Studio を使用している場合は、NuGet パッケージマネージャ UI からパッケージを追加できます。依存関係が自動で復元されるため、後で手動で `dotnet restore` を実行する手間が省けます。

次に `Program.cs` を開き、内容を **画像に OCR を実行** するコードに置き換えます。

## 手順 2: OCR エンジンの作成と設定

Aspose OCR ワークフローの中心は `OcrEngine` クラスです。以下ではインスタンス化し、エンジンに JSON 形式で結果を出力させる設定を行います。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 2.1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2.2: Tell the engine we want JSON output.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: tweak language or recognition speed.
        // ocrEngine.Settings.Language = Language.English; // default is English
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Fast; // or Accurate
```

**`ResultFormat` を JSON に設定する理由**  
JSON は言語に依存せず、C#、JavaScript、Python など任意の環境で強く型付けされたオブジェクトにデシリアライズできます。また、信頼度スコアやバウンディングボックス座標も保持できるため、下流の検証に便利です。

## 手順 3: 画像に OCR を実行し JSON を取得

エンジンが準備できたら、`RecognizeImage` を呼び出して **画像に OCR を実行** します。このメソッドは JSON ペイロードを文字列で返します。

```csharp
        // Step 3: Perform OCR on the image and capture the JSON output.
        // Replace the path with the location of your own image file.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);
```

> **エッジケース:** 画像が破損している、またはパスが間違っている場合、`RecognizeImage` は `FileNotFoundException` をスローします。エラーハンドリングが必要な場合は `try/catch` でラップしてください。

## 手順 4: JSON 結果を保存して後続処理に備える

OCR の出力を保存すれば、データベースや API、UI コンポーネントに後から流し込むことができます。以下は JSON をディスクに書き込むシンプルな方法です。

```csharp
        // Step 4: Save the JSON result for later use.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);
```

クラウド環境で実行する場合は、`File.WriteAllText` を Azure Blob Storage や AWS S3 への書き込みに置き換えても同様に扱えます。

## 手順 5: ユーザーへ通知しクリーンアップ

小さなコンソールメッセージで処理が正常に完了したことを確認します。実際のアプリではファイルにログを残したり、監視サービスに送信したりすることも考えられます。

```csharp
        // Step 5: Inform the user that the JSON file has been saved.
        Console.WriteLine("JSON result saved to " + outputPath);
    }
}
```

以上で一連の流れは完了です！`dotnet run` でプログラムを実行すると、確認メッセージとともに `receipt.json` が生成され、内容は次のようになります。

```json
{
  "Pages": [
    {
      "Blocks": [
        {
          "Text": "Total: $23.45",
          "Confidence": 0.98,
          "Rectangle": { "X": 120, "Y": 340, "Width": 150, "Height": 20 }
        }
      ]
    }
  ]
}
```

## 完全実行可能サンプル

参考までに、`Program.cs` にそのまま貼り付けられる **完全版** を掲載します。抜けはありません。

```csharp
using Aspose.OCR;
using System;
using System.IO;

class JsonResultDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance.
        var ocrEngine = new OcrEngine();

        // Step 2: Configure the engine to return results in JSON format.
        ocrEngine.Settings.ResultFormat = ResultFormat.Json;

        // Optional: adjust language or recognition mode if needed.
        // ocrEngine.Settings.Language = Language.English;
        // ocrEngine.Settings.RecognitionMode = RecognitionMode.Accurate;

        // Step 3: Perform OCR on the image and capture the JSON output.
        string imagePath = "YOUR_DIRECTORY/receipt.png";
        string jsonResult = ocrEngine.RecognizeImage(imagePath);

        // Step 4: Save the JSON result for further processing.
        string outputPath = "YOUR_DIRECTORY/receipt.json";
        File.WriteAllText(outputPath, jsonResult);

        // Step 5: Notify that the JSON file has been saved.
        Console.WriteLine($"JSON result saved to {outputPath}");
    }
}
```

> **ヒント:** `YOUR_DIRECTORY` を絶対パスまたはプロジェクトルートからの相対パスに置き換えてください。`Path.Combine(Environment.CurrentDirectory, "receipt.png")` を使うと、Windows と Linux のパス区切りの違いを意識せずに済みます。

## よくある質問と落とし穴

- **対応している画像形式は？**  
  Aspose.OCR は PNG、JPEG、BMP、TIFF、GIF をサポートします。PDF を扱いたい場合は、各ページを画像に変換してから処理してください（Aspose.PDF が便利です）。

- **JSON ではなくプレーンテキストが欲しい場合は？**  
  `ocrEngine.Settings.ResultFormat = ResultFormat.Text;` と設定すれば取得できます。メタデータが不要な場合に有効です。

- **マルチページ文書はどう扱う？**  
  各ページ画像を `RecognizeImage` にループで渡して結果を結合するか、`RecognizePdf` を使用して一括で JSON 構造を取得します。

- **パフォーマンス面の注意点は？**  
  バッチ処理では画像ごとに新しい `OcrEngine` を作らず、同一インスタンスを再利用してください。また、精度を犠牲にして速度を優先したい場合は `RecognitionMode.Fast` を有効にします。

- **ライセンス警告は？**  
  ライセンス未取得の場合、出力 JSON に透かしフィールドが含まれます。`Main` の冒頭で以下を実行してライセンスを設定してください。  
  `License license = new License(); license.SetLicense("Aspose.OCR.lic");`

## ビジュアル概要

以下の図は「画像ファイル → OCR エンジン → JSON 出力 → 保存」のデータフローを視覚化したものです。全体パイプラインの中で各ステップがどこに位置するかを把握しやすくなります。

![画像に OCR を実行するワークフロー図](https://example.com/ocr-workflow.png "画像に OCR を実行する")

*Alt text: Aspose OCR を使用して画像に OCR を実行し、JSON に変換してファイルに保存する流れを示す図。*

## サンプルの拡張

**画像に OCR を実行** して JSON ペイロードを取得できたので、次のような拡張が考えられます：

- `System.Text.Json` や `Newtonsoft.Json` で JSON をパースし、特定フィールドを抽出。  
- テキストをデータベースに挿入して検索可能なアーカイブを構築。  
- Web API と統合し、クライアントが画像をアップロードして即座に OCR 結果を取得できるようにする。  
- `Aspose.Imaging` を使って画像の前処理（デスキュー、コントラスト強化）を行い、認識精度を向上させる。

これらのトピックはすべて、本章で構築した `OcrEngine` インスタンスを再利用して実装できます。

## 結論

C# と Aspose OCR を用いて **画像に OCR を実行** し、エンジンを JSON 出力に設定し、結果を永続化する方法を学びました。コードの各行を丁寧に解説し、設定の意図や本番環境で遭遇しやすいエッジケースにも触れました。

ここからは、`ocrEngine.Settings.Language` で言語を変えてみたり、`RecognitionMode` を調整したり、JSON を下流の分析パイプラインに流し込んだりして、さらに実験を広げてみてください。信頼性の高い OCR と最新の .NET ツールを組み合わせれば、可能性は無限大です。

本ガイドが役立ったと思ったら、Aspose.OCR の GitHub リポジトリにスターを付けたり、チームメンバーとシェアしたり、コメントで独自のコツを共有してください。Happy coding!

## 次に学ぶべきこと

以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを扱っています。各リソースには完全なコード例とステップバイステップの解説が含まれているので、API の追加機能をマスターしたり、別の実装アプローチを探求したりする際に役立ちます。

- [Aspose OCR で JSON 結果を取得する方法](/ocr/english/net/text-recognition/get-result-as-json/)
- [Aspose.OCR for .NET で画像からテキストを抽出する方法](/ocr/english/net/text-recognition/get-recognition-result/)
- [画像を URL から取得して OCR を実行する](/ocr/english/net/ocr-optimization/perform-ocr-on-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}