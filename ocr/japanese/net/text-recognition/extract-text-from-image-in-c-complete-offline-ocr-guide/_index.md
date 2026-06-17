---
category: general
date: 2026-03-18
description: C#でAspose OCRを使用して画像からテキストを抽出します。テキストの抽出方法、OCR認識の実行、インターネットなしでキリル文字を認識する方法を学びましょう。
draft: false
keywords:
- extract text from image
- how to extract text
- run OCR recognition
- recognize cyrillic text
- offline OCR with Aspose
language: ja
og_description: Aspose OCRで画像からテキストを抽出します。OCR認識の実行手順、テキスト抽出方法、そしてオフラインでのキリル文字認識に関するステップバイステップガイド。
og_title: C#で画像からテキストを抽出 – オフラインOCRチュートリアル
tags:
- C#
- OCR
- Aspose
- Image Processing
title: C#で画像からテキストを抽出 – 完全オフラインOCRガイド
url: /ja/net/text-recognition/extract-text-from-image-in-c-complete-offline-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – 完全オフライン OCR ガイド

画像からテキストを**抽出する必要があった**が、ネットワーク遅延やライセンス制限が心配だったことはありませんか？ あなただけではありません。サンドボックス環境で動作しなければならず、かつ信頼できる OCR が必要な開発者は多く壁にぶつかります。良いニュースは、Aspose OCR を使用すれば、パイプライン全体をローカルで実行でき、**画像からテキストを抽出**する際にインターネットに接続する必要がありません。

このチュートリアルでは、**テキスト抽出の方法**を実演し、オフラインエンジンを設定し、**OCR 認識を実行**し、さらに **キリル文字の認識**まで行う実用的な例を順に解説します。最後まで進めば、検出された文字列をコンソールに直接出力する C# コンソールアプリが完成します。

## 必要なもの

- .NET 6.0 SDK（または最近の .NET バージョン）  
- Visual Studio 2022 または VS Code – 好みの方  
- Aspose.OCR for .NET NuGet パッケージ  
- Aspose OCR モデルファイルを含むフォルダー（Aspose ポータルから一度ダウンロード）  
- 英語とキリル文字を含む画像ファイル（例: `cyrillic_doc.jpg`）

外部サービスは不要、実行時に隠れたダウンロードもなし – すべてディスク上にあります。

## 手順 1: Aspose.OCR のインストールとリソースの準備

まず、プロジェクトに Aspose.OCR NuGet パッケージを追加します:

```bash
dotnet add package Aspose.OCR
```

次に、マシン上の任意の場所に `AsposeOCRResources` というフォルダーを作成し、Aspose からダウンロードしたモデルファイルをその中にコピーします。OCR エンジンはこのディレクトリ内の言語パックを探すので、パスが正しいことを確認してください。

> **プロのコツ:** リソースフォルダーを `.csproj` ファイルの隣に置くと、開発中のパス処理がシンプルになります。

## 手順 2: オフライン OCR エンジンの構築

今度はエンジンをインスタンス化し、リソースフォルダーを指すように設定します。これが **OCR 認識を完全にオフラインで実行**できる重要なステップです。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // 1️⃣ Create the OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Tell the engine where the language models live
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // 3️⃣ Load the languages you need – English and Cyrillic
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);
```

言語を明示的にロードするのはなぜか？ エンジンにオフラインで動作するよう指示しているため、欠落したパックを取得しに Aspose サーバーへアクセスしません。言語をロードし忘れると、そのスクリプトの文字は無視されます。

## 手順 3: 画像をエンジンに供給する

エンジンの準備ができたら、処理したい画像を提供します。`ImageStream.FromFile` ヘルパーはファイルを OCR エンジンが理解できる形式に読み込みます。

```csharp
        // 4️⃣ Load the target image (make sure the path points to your file)
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");
```

画像が大きい場合は、事前にリサイズして速度と精度を向上させることを検討してください。OCR エンジンは DPI 約 300 が最適です。

## 手順 4: 認識プロセスの実行

`Recognize` を呼び出すと重い処理が実行されます。このメソッドは抽出された文字列や信頼度スコアなどを含む `OcrResult` オブジェクトを返します。

```csharp
        // 5️⃣ Run the OCR recognition
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

内部では、Aspose がビットマップを解析し、言語固有のニューラルネットを走らせ、文字をつなぎ合わせます。英語とキリル文字の両方をロードしているため、混在スクリプトの文書もシームレスに処理されます。

## 手順 5: 抽出されたテキストの表示

最後に結果を出力します。実際のアプリではデータベースに保存したり別サービスに渡したりするかもしれませんが、このデモではコンソールに印字するだけです。

```csharp
        // 6️⃣ Show the extracted text on the console
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行すると、次のような出力が得られるはずです:

```
=== OCR Output ===
This is an English line.
Это строка на кириллице.
```

文字化けが見られる場合は、キリル文字の言語パックがリソースフォルダーに正しく配置されているか、画像がぼやけていないかを再確認してください。

![画像からテキストを抽出した例](extract_text_image.png "画像からテキストを抽出")

*画像の代替テキスト: 画像からテキストを抽出 – 英語とキリル文字の行を示す OCR 結果。*

## 一般的な落とし穴の対処

### 言語パックが見つからない場合

「Language data not found」という例外が出た場合、エンジンはモデルファイルを見つけられませんでした。`ResourcesPath` を確認し、フォルダーに `english.dat` と `cyrillic.dat`（または同等の名前のファイル）が含まれていることを確かめてください。

### 信頼度が低いスコア

画像にノイズがあると、OCR エンジンが特定の文字に対して低い信頼度を返すことがあります。精度向上のために次を試してください:

- エンジンに供給する前に画像をグレースケールに変換する  
- ノイズを減らすためにメディアンフィルタを適用する  
- テキストが水平に揃っていることを確認する（必要に応じて回転）

### 大きな画像

10 MP の写真を処理すると遅くなることがあります。アスペクト比を保ちつつ幅を最大 2000 px に縮小してください。エンジンは依然としてほとんどの文字を正確に捕捉します。

## 例の拡張

- **バッチ処理:** ディレクトリ内のすべてのファイルをループで回し、認識ロジックをラップする。  
- **出力形式:** `OcrResult` は `TextLines` コレクションも提供し、バウンディングボックスを含む – UI アプリでテキストをハイライトするのに便利。  
- **追加言語:** 他のサポートされている enum 値（例: `Language.French`）で `LoadLanguage` を呼び出すだけです。  

これらすべての拡張は **テキスト抽出の方法** の原則に従います – 適切な言語パックをロードし、残りはエンジンに任せるだけです。

## 完全なソースコードまとめ

以下はコピー＆ペーストで使用できる完全版プログラムです。`YOUR_DIRECTORY` を実際のパスに置き換えてください。

```csharp
using Aspose.OCR;
using Aspose.OCR.Enums;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Step 2: Point the engine to the folder that contains OCR model files
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";

        // Step 3: Load the languages you need (no automatic download will occur)
        ocrEngine.LoadLanguage(Language.English);
        ocrEngine.LoadLanguage(Language.Cyrillic);

        // Step 4: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/cyrillic_doc.jpg");

        // Step 5: Run the recognition process
        OcrResult ocrResult = ocrEngine.Recognize(image);

        // Step 6: Display the extracted text
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.Text);
    }
}
```

これを `Program.cs` として保存し、`dotnet run` を実行すると、エンジンが画像から取得したテキストがコンソールに表示されます。これで、オフラインで **画像からテキストを抽出**することに成功しました。

## 結論

Aspose OCR を使用して、完全にオフラインのシナリオで **画像からテキストを抽出**するために必要なすべてを網羅しました。本ガイドは **テキスト抽出の方法** を示し、**OCR 認識の実行** をデモし、ネットワーク呼び出しなしで英語とキリル文字の **認識** が可能であることを実証しました。

NuGet パッケージの設定から言語パックが見つからないといったエッジケースの対処まで、.NET アプリケーションで OCR 機能を構築するための堅実な基盤が手に入りました。

次は何をしますか？ PDF を入力にしたり、複数ページをスキャンしたり、出力を検索インデックスに統合したりしてみてください。オフライン OCR をマスターすれば、可能性は無限です。

Happy coding, and may your images always be crystal‑clear!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}