---
category: general
date: 2026-04-01
description: C#でOCR出力をJSONとXMLに変換する方法 – 画像からテキストを抽出し、Aspose.OCRを使用してC#でJSONファイルを書き出す方法を学ぶ。
draft: false
keywords:
- how to convert ocr
- extract text from image
- write json file c#
- write xml file c#
- how to extract text
language: ja
og_description: C#でOCR結果を構造化されたJSONおよびXMLファイルに変換する方法。画像からテキストを抽出し、JSONファイルを書き出すステップバイステップガイド（C#）。
og_title: C#でOCRをJSONおよびXMLに変換する方法 – JSONファイルの書き込み
tags:
- OCR
- C#
- Aspose
title: C#でOCRをJSONとXMLに変換する方法 – JSONファイルを書き込む
url: /ja/net/text-recognition/how-to-convert-ocr-to-json-xml-in-c-write-json-file/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を JSON と XML に変換する方法 – JSON ファイルの書き込み

**How to convert OCR** の結果を実際に使える形にすることは、多くの開発者が抱える質問です。このガイドでは、画像からテキストを抽出し、OCR の出力を整形された JSON と XML に変換し、C# でそれらのファイルを書き出す方法を示します。

生の OCR 文字列を見て「もっと良い保存方法があるはずだ」と思ったことがあるなら、ここが正解です。最後まで読むと、画像ファイルから **extracts text from image** できるだけでなく、**write JSON file C#** と **write XML file C#** を簡単に実行できる、完全に動作するプログラムが手に入ります。

## 必要なもの

- **.NET 6.0** 以上（コードは .NET Framework 4.6 以降でも動作します）。  
- **Aspose.OCR** NuGet パッケージ – `dotnet add package Aspose.OCR` でインストールします。  
- テキストを含む画像（例: `invoice.png`）。  
- お好みの IDE – Visual Studio、Rider、または VS Code で構いません。

> **Pro tip:** 画像ファイルは `Resources/` のような専用フォルダーに入れておくと、パスがすっきりします。

## ステップ 1: OCR エンジンのセットアップ – How to Convert OCR

まず、`OcrEngine` インスタンスを作成し、対象言語を指定します。多くの場合は英語で十分ですが、`Language.English` を任意のサポート言語に置き換えることができます。

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Step 1: Initialise the OCR engine for English text
        var ocrEngine = new OcrEngine { Language = Language.English };
```

> **Why this matters:** 正しい言語でエンジンを初期化すると、特にラテン文字以外のスクリプトに対して精度が大幅に向上します。

## ステップ 2: テキスト認識 – Extract Text from Image

画像をエンジンに渡します。`Recognize` メソッドは `OcrResult` オブジェクトを返し、生テキストと位置情報を含みます。

```csharp
        // Step 2: Recognise text from the supplied image
        // Replace "YOUR_DIRECTORY/invoice.png" with your actual file path
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");
```

画像が見つからない場合、`Recognize` は `FileNotFoundException` をスローします。デモを簡潔に保つためパスが正しい前提としていますが、実運用では try‑catch で囲むことを推奨します。

## ステップ 3: 結果を JSON に変換 – Write JSON File C#

Aspose.OCR のシリアライズはとても簡単です。`ToJson` メソッドは `indent` フラグを受け取り、整形された出力を生成します。テキストエディタで開くことを想定した場合に便利です。

```csharp
        // Step 3: Convert OCR result to formatted JSON
        string jsonOutput = ocrResult.ToJson(indent: true);
```

### 期待される JSON サンプル

```json
{
  "Text": "Invoice #12345\nDate: 2024‑03‑31\nTotal: $250.00",
  "Regions": [
    {
      "Bounds": { "X": 10, "Y": 20, "Width": 200, "Height": 30 },
      "Text": "Invoice #12345"
    }
    // … more regions …
  ]
}
```

> **How to extract text**: `Text` プロパティから取得できる文字列は、検索インデックスやデータベースなど他のサービスへそのまま渡すことができます。

## ステップ 4: JSON を永続化 – Write JSON File C# (Continued)

JSON 文字列が用意できたら、`File.WriteAllText` でファイルに書き込みます。デフォルトで UTF‑8 エンコーディングが使用されます。

```csharp
        // Step 4: Save JSON to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);
```

これで画像と同じディレクトリに `invoice.json` が作成され、次の処理にすぐ使える状態になります。

## ステップ 5: 結果を XML に変換 – Write XML File C#

レガシーシステムで XML が必要な場合は、`ToXml` メソッドがその役割を担います。`ToJson` と同様に整形出力をサポートしています。

```csharp
        // Step 5: Convert OCR result to formatted XML
        string xmlOutput = ocrResult.ToXml(indent: true);
```

### 期待される XML サンプル

```xml
<OcrResult>
  <Text>Invoice #12345
Date: 2024-03-31
Total: $250.00</Text>
  <Regions>
    <Region>
      <Bounds X="10" Y="20" Width="200" Height="30" />
      <Text>Invoice #12345</Text>
    </Region>
    <!-- … more regions … -->
  </Regions>
</OcrResult>
```

## ステップ 6: XML を永続化 – Write XML File C# (Continued)

XML の保存は JSON と同じ手順です。拡張子を `.xml` に変えるだけで完了します。

```csharp
        // Step 6: Save XML to disk
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

### 完全動作サンプル

以下に、コンソールアプリにコピペできる完全なプログラムを示します。

```csharp
using Aspose.OCR;
using System.IO;

class JsonXmlOcrDemo
{
    static void Main()
    {
        // Initialise OCR engine for English
        var ocrEngine = new OcrEngine { Language = Language.English };

        // Recognise text from image
        var ocrResult = ocrEngine.Recognize("YOUR_DIRECTORY/invoice.png");

        // Convert to JSON and save
        string jsonOutput = ocrResult.ToJson(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.json", jsonOutput);

        // Convert to XML and save
        string xmlOutput = ocrResult.ToXml(indent: true);
        File.WriteAllText("YOUR_DIRECTORY/invoice.xml", xmlOutput);
    }
}
```

プログラムを実行すると、指定した場所に `invoice.json` と `invoice.xml` の 2 つの新しいファイルが生成されます。ファイルを開いて、サンプルと同じ構造になっていることを確認してください。

## よくある質問とエッジケース

| 質問 | 回答 |
|----------|--------|
| **画像に複数言語が含まれている場合は？** | 言語ごとに別々の `OcrEngine` インスタンスを作成するか、サポートされていれば `Language.Multi` を使用します。 |
| **出力フォーマット（例: 領域データを除外）を制御できますか？** | はい。`ToJson` と `ToXml` はオプションパラメータでフィールドをフィルタリングできます。`ExportOptions` を参照してください。 |
| **ページ数の多い PDF を処理するには？** | 各ページを個別に処理し、結果を集約してから一度だけシリアライズします。 |
| **出力は UTF‑8 で安全ですか？** | 完全に安全です。Aspose.OCR は内部で Unicode を使用し、`File.WriteAllText` はデフォルトで UTF‑8 で書き込みます。 |
| **パフォーマンスは？** | OCR は CPU 集中型です。バッチ処理の場合はコア間で並列化するか、Aspose のクラウド API の利用を検討してください。 |

## まとめ

これで **how to convert OCR** の結果を JSON と XML の両方に変換し、C# で **extract text from image**、**write JSON file C#**、**write XML file C#** を数行のコードで実現できました。この手法は高速で信頼性が高く、Aspose.OCR がサポートするすべての画像タイプで動作します。

次のチャレンジに挑戦してみませんか？ぜひ以下の内容を試してみてください。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}