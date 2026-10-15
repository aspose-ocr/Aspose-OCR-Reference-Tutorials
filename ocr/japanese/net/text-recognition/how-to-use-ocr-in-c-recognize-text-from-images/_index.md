---
category: general
date: 2026-02-09
description: C#でOCRを使用して画像からテキストを認識し、抽出し、Aspose OCRで画像をテキストに変換する方法。完全なステップバイステップガイド。
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from image
- convert image to text
- load image stream
language: ja
og_description: C#でOCRを使用して画像からテキストを認識し、テキストを抽出し、Aspose OCRで画像をテキストに変換する方法。コード付きの完全ガイド。
og_title: C#でOCRを使用する方法 – 画像からテキストを認識する
tags:
- C#
- Aspose OCR
- Image Processing
title: C#でOCRを使用する方法 – 画像からテキストを認識する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-recognize-text-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – 画像からテキストを認識する

スクリーンショットを編集可能なテキストに変換する **OCR の使い方** が気になったことはありませんか？ あなたは一人ではありません。画像ファイルから *テキストを認識* したいが、すぐに実行できるサンプルが見つからずに壁にぶつかる開発者は多いです。  

このチュートリアルでは、ライセンスの読み込み、エンジンの作成、画像ストリームの供給、そして最終的にプレーンテキストを取得するまでの一連の流れを順を追って解説します。最後まで読めば、**画像からテキストを抽出**、**画像をテキストに変換**、さらには **画像ストリームの読み込み** のコツも理解できるようになります。

> **得られるもの:** Aspose.OCR を使用した完全な実行可能 C# プログラム、各ステップの解説、そして一般的な落とし穴を回避するためのヒント。

---

## 前提条件

- .NET 6.0 以上（API は .NET Framework 4.6+ でも動作します）  
- Aspose.OCR for .NET NuGet パッケージ（`Aspose.OCR`）がインストール済み  
- 有効な Aspose OCR ライセンスファイル（`Aspose.OCR.lic`） – 無料トライアルでも動作しますが、透かしが入ります。  
- 明瞭で機械可読なテキストが含まれる画像（`sample.jpg`）。

> **ヒント:** Visual Studio を使用している場合、NuGet コンソールでのコマンドは  
> `Install-Package Aspose.OCR -Version 23.10`（最新バージョンに置き換えてください）。

---

## OCR の使い方: ライセンスの読み込みとエンジンの初期化

最初に行うべきことは、Aspose に対してライセンスを所有していることを伝えることです。このステップを省略すると実行は可能ですが、出力に透かしが入り、トライアルモードのチェックに余計な処理時間がかかります。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // Step 1 – Load the Aspose OCR license (replace with your .lic file path)
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // Step 2 – Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // The rest of the steps follow...
    }
}
```

**重要性:** `License` オブジェクトはトライアル透かしを無効化し、精度の高いモデルや多言語サポートなどフル機能を解放します。  

> **プロのコツ:** ライセンスファイルはソース管理リポジトリの外に置きましょう。環境変数や安全なボールトを使って実行時にパスを注入するのがベストプラクティスです。

---

## 手順 2 – 画像ストリームの読み込み（ファイルパスより優れている理由）

`ImageStream` を **画像ストリームとして読み込む** と、データベース、Web リクエスト、またはメモリ上のバイト配列から画像を取得できる柔軟性が得られます。  

```csharp
// Step 3 – Load the image you want to recognize
// Using ImageStream.FromFile is the simplest way for local files.
ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

// Alternative: load from a byte array (e.g., when the image is uploaded via HTTP)
// byte[] imageBytes = ... // get from request
// ImageStream imageStream = ImageStream.FromBytes(imageBytes);
```

**解説:** `ImageStream` は基になるソースを抽象化し、OCR エンジンがすべてを同一視できるようにします。後でクラウドストレージバケットに切り替える場合でも、`ImageStream` の生成方法だけを変更すれば、残りのコードはそのままです。

---

## 手順 3 – 画像からテキストを認識する

いよいよ本題です: **画像からテキストを認識** します。`OcrEngine.Recognize` メソッドは Aspose に同梱されたニューラルネットワークモデルを実行し、複数の便利なプロパティを持つ `OcrResult` オブジェクトを返します。

```csharp
// Step 4 – Run the OCR process on the image
OcrResult ocrResult = ocrEngine.Recognize(imageStream);
```

**`OcrResult` に含まれるもの:**  
- `PlainText` – 検出された文字をすべて連結した単一文字列。  
- `Words` – バウンディングボックスを持つ単語オブジェクトのコレクション（ハイライトに便利）。  
- `Lines` – 行単位のグルーピングで、段落区切りを保持しやすい。

純粋なテキストだけが必要な場合は `PlainText` が最速のルートです。画像上に結果をオーバーレイしたいなど高度なシナリオでは `Words` や `Lines` を活用してください。

---

## 手順 4 – 抽出したテキストの表示または永続化

最後に、認識結果をコンソールに出力します。実際のアプリではデータベースやファイル、あるいは API 経由で送信することになるでしょう。

```csharp
// Step 5 – Display the recognized plain text (watermark omitted with a full license)
Console.WriteLine("=== OCR Output ===");
Console.WriteLine(ocrResult.PlainText);
Console.WriteLine("==================");

// Optional: Save to a .txt file
System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
```

**期待される出力:**  
`sample.jpg` に文 *“Hello World!”* が含まれている場合、次のように表示されます。

```
=== OCR Output ===
Hello World!
==================
```

トライアルライセンスを使用していると、テキストの末尾に小さな “Aspose OCR Demo” 透かしが付加されます。フルライセンスでは透かしは完全に消えます。

---

## 完全動作サンプル（コピー＆ペーストで使用可）

以下はコンパイル可能なフルプログラムです。パスを自分の環境に合わせて置き換えればすぐに動作します。

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;
using Aspose.OCR.Licensing;

class LicenseExample
{
    static void Main()
    {
        // 1️⃣ Load license – required for production use
        License ocrLicense = new License();
        ocrLicense.SetLicense(@"C:\Licenses\Aspose.OCR.lic");

        // 2️⃣ Create OCR engine – the core processing object
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Load image – you can also use ImageStream.FromBytes for in‑memory data
        ImageStream imageStream = ImageStream.FromFile(@"C:\Images\sample.jpg");

        // 4️⃣ Recognize text – this is where the magic happens
        OcrResult ocrResult = ocrEngine.Recognize(imageStream);

        // 5️⃣ Output the plain text – perfect for further processing
        Console.WriteLine("=== OCR Output ===");
        Console.WriteLine(ocrResult.PlainText);
        Console.WriteLine("==================");

        // Optional: persist the result
        System.IO.File.WriteAllText(@"C:\Output\extracted.txt", ocrResult.PlainText);
    }
}
```

> **覚えておくべきこと:** 上記コードは **画像からテキストを抽出** し、**画像をテキストに変換** する処理を 1 回の呼び出しで実行します。余計なループやピクセル操作は不要で、すべて Aspose が内部で処理します。

---

## よくある質問とエッジケース

### 画像がぼやけている、またはコントラストが低い場合は？

Aspose OCR には前処理オプション（例: `ocrEngine.ImagePreprocessor`）が用意されています。二値化やデスケューを有効にしてから認識すると効果的です。

```csharp
ocrEngine.ImagePreprocessor = new ImagePreprocessor
{
    Binarization = true,
    Deskew = true
};
```

### 複数言語に対応させるには？

エンジンの `Language` プロパティを設定します。

```csharp
ocrEngine.Language = OcrLanguage.English | OcrLanguage.Spanish;
```

設定後、エンジンは自動的に両言語を検出しようとします。

### JPEG ではなく PDF を処理したい場合は？

可能です。Aspose OCR は PDF を直接読み取れますが、各ページを画像に変換するには Aspose.PDF ライブラリが必要です。その画像ストリームを OCR エンジンに渡します。

### 大量バッチ処理は？

認識ロジックをループで回し、同じ `OcrEngine` インスタンスを再利用してください。画像ごとにエンジンを新規作成すると不要なオーバーヘッドが発生します。

---

## 本番環境向け OCR のプロ・ティップス

- **ライセンスオブジェクトをキャッシュ**: アプリ起動時に一度だけロードし、リクエストごとに再読込しない。  
- **`OcrEngine` を再利用**: エンジンは内部バッファを保持しているため、再利用すると GC 圧力が減ります。  
- **画像サイズを制限**: 5 MP 超の超大型画像は処理時間が大幅に増加します。高解像度が不要な場合は 150‑300 DPI にダウンサンプルしてください。  
- **出力の検証**: OCR は完璧ではありません。簡易的な信頼度チェック（`ocrResult.Words.Average(w => w.Confidence)`）を実装し、低信頼度の結果は手動レビューへ回す仕組みを入れましょう。  
- **スレッド安全性**: `OcrEngine` はスレッドセーフではありません。スレッドごとに別インスタンスを作成するか、プールパターンを採用してください。

---

## まとめ

C# での **OCR の使い方** を、ライセンスの読み込みからクリーンな検索可能テキストの抽出まで網羅しました。上記手順に従えば **画像からテキストを認識**、**画像からテキストを抽出**、そして **画像をテキストに変換** がシンプルに実現でき、将来的にデータソースを変更しても柔軟に対応できる **画像ストリームの読み込み** パターンも習得できます。

次のステップに挑戦してみませんか？ ROI（領域指定）での切り取り、Azure Blob Storage との統合、あるいは OCR 出力を自然言語処理パイプラインに流し込むなど、可能性は無限です。今や堅実な基盤が整ったので、思いのままに拡張していきましょう。

---

![画像からテキストを認識する OCR フロー: ライセンス読み込み → エンジン作成 → 画像ストリーム読み込み → 認識 → テキスト出力](image-placeholder.png "画像からテキストを認識する OCR フロー")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}