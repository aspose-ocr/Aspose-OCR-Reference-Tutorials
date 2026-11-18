---
category: general
date: 2026-03-23
description: Aspose OCR を使用してフォームからテキストを迅速に抽出します。領域内のテキスト認識方法と、画像の OCR 部分を処理する完全な
  C# サンプルをご紹介します。
draft: false
keywords:
- extract text from form
- recognize text in area
- ocr part of image
- Aspose OCR C#
- region based OCR
language: ja
og_description: Aspose OCR を使用してフォームからテキストを抽出します。このチュートリアルでは、領域内のテキストを認識し、C# で画像の
  OCR 部分を処理する方法を示します。
og_title: Aspose OCRでフォームからテキストを抽出する – 完全ガイド
tags:
- C#
- OCR
- Aspose
- Image Processing
title: Aspose OCRでフォームからテキストを抽出する – ステップバイステップガイド
url: /ja/net/text-recognition/extract-text-from-form-with-aspose-ocr-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# フォームからテキストを抽出する Aspose OCR – ステップバイステップガイド

**フォームからテキストを抽出**したいのに、ページ全体がノイズだらけだったことはありませんか？ 開発者は PDF、スキャンした請求書、手書きアンケートなど、1つのフィールドだけが重要なケースと格闘しています。 良いニュースは、Aspose OCR に必要な部分だけを見させ、残りは無視させることができるということです。

このガイドでは、スキャンしたフォームの **領域内のテキストを認識**し、必要な値を取り出し、画像の他の部分はそのままにする方法を詳しく解説します。 最後まで読めば、外部サービスを呼び出すことなく、**画像の OCR 部分**だけを処理する実行可能な C# プログラムが手に入ります。

## 本チュートリアルで得られるもの

- フォーム画像からフィールドを抽出する、完全に実行可能な C# コンソールアプリ  
- なぜ矩形領域を対象にする方が高速かつ高精度になるのかの明確な説明  
- 空結果、異なる DPI 設定、マルチページフォームの取り扱いに関するヒント  
- 数分で自分のプロジェクトにコードを適用できるチェックリスト  

**前提条件** – .NET 6 以上、Visual Studio 2022（またはお好みの IDE）、そして最初に Aspose.OCR NuGet パッケージを取得するためのインターネット接続が必要です。その他のライブラリは不要です。

---

## フォームからテキストを抽出 – プロジェクトのセットアップ

コードに入る前に、環境が整っていることを確認しましょう。手順は意図的にシンプルにしています。実際の魔法は OCR エンジンをインスタンス化したときに始まります。

1. **新しいコンソールプロジェクトを作成**  
   ```bash
   dotnet new console -n FormOcrDemo
   cd FormOcrDemo
   ```

2. **NuGet で Aspose.OCR を追加**  
   ```bash
   dotnet add package Aspose.OCR
   ```

3. **スキャンしたフォームをプロジェクトフォルダーにコピーし、`form.png` にリネーム**  
   （ファイルが PDF の場合は、必要なページを PNG にエクスポートしてください。Aspose OCR はラスタ画像で最適に動作します）

以上です。残りのチュートリアルはこの 3 つの手順が完了していることを前提とします。

![extract text from form example](form-region.png "extract text from form example")

*画像の代替テキスト: スキャンした文書上でハイライトされた領域を示す、フォームからテキストを抽出する例*

---

## 領域内テキスト認識 – 関心領域の定義

なぜ矩形を使うのでしょうか？ たとえば 2 MB の税務申告書全体をスキャンしたとします。全体に OCR をかけると CPU が無駄に消費され、関係のないフィールドから誤検出が出やすくなります。対象となる座標だけに絞ることで、次の効果が得られます。

- **処理時間を最大 80 % 短縮**（大きな画像の場合）  
- **精度向上**：エンジンが不要なグラフィックを無視  
- **後処理が簡素化**：期待するテキストが何か正確に分かる  

矩形は `x`, `y`, `width`, `height` の 4 つの数値で定義します。これらは画像左上隅からのピクセル単位です。フィールドの位置が分からない場合は、Paint で画像を開き、左上隅にマウスを合わせて X/Y 値を確認し、幅と高さをドラッグで測定してください。

---

## 画像の OCR 部分 – フォームの読み込みとエンジン設定

領域が決まったら、エンジン自体について説明します。`OcrEngine` は Aspose OCR の中心です。言語自動検出、傾き補正、プレーンテキスト文字列の返却を自動で行います。フォームが非ラテン文字を使用している場合は `Resolution` や `Language` などのプロパティを調整できます。英語のフォームであればデフォルトで十分です。

以下は **完全かつ自己完結型のプログラム** です。`Program.cs` に貼り付けて **F5** を押すだけで動作します。

```csharp
using Aspose.OCR;
using System;
using System.Drawing; // for Rectangle

class RegionExample
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Create the OCR engine (using ensures disposal)
        // -------------------------------------------------
        using (OcrEngine ocrEngine = new OcrEngine())
        {
            // -------------------------------------------------
            // Step 2: Load the image that contains the form
            // -------------------------------------------------
            // ImageStream.FromFile reads the file into Aspose's internal format
            // Replace "YOUR_DIRECTORY/form.png" with the actual path if needed
            ocrEngine.Image = ImageStream.FromFile("form.png");

            // -------------------------------------------------
            // Step 3: Define the region that holds the desired field
            // -------------------------------------------------
            // (x, y, width, height) – adjust these numbers for your form
            Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);

            // -------------------------------------------------
            // Step 4: Recognize text only inside the defined region
            // -------------------------------------------------
            bool success = ocrEngine.Recognize(regionOfInterest);
            string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;

            // -------------------------------------------------
            // Step 5: Display the extracted field value
            // -------------------------------------------------
            Console.WriteLine("Field value: " + (string.IsNullOrEmpty(recognizedText)
                ? "[No text detected]"
                : recognizedText));
        }

        // Keep the console window open when debugging
        Console.WriteLine("\nPress any key to exit...");
        Console.ReadKey();
    }
}
```

### 期待される出力

矩形が「Invoice # 12345」というフィールドを正しく囲んでいる場合、コンソールは次のように表示します。

```
Field value: Invoice # 12345
```

領域が空であるか OCR が失敗した場合は、次のように表示されます。

```
Field value: [No text detected]
```

---

## ステップバイステップ コード解説

以下ではプログラムを小さなチャンクに分割し、各行の **理由** を説明し、必要に応じてコードを調整するポイントを示します。

### Step 1: Install Aspose.OCR via NuGet *(H3)*

```bash
dotnet add package Aspose.OCR
```

*Why?* NuGet パッケージにはネイティブ OCR エンジン、言語データファイル、.NET ラッパーがすべて含まれています。これが無いと `OcrEngine` クラスは存在しません。

### Step 2: Initialize OcrEngine *(H3)*

```csharp
using (OcrEngine ocrEngine = new OcrEngine())
```

*Why use `using`?* `OcrEngine` はアンマネージドリソース（ネイティブ DLL、画像バッファ）を保持します。`using` 文により確実に解放され、長時間稼働するサービスでのメモリリークを防げます。

### Step 3: Load the Form Image *(H3)*

```csharp
ocrEngine.Image = ImageStream.FromFile("form.png");
```

*Why `ImageStream`?* ファイル I/O を抽象化し、PNG、JPEG、TIFF などの一般的なフォーマットを Aspose OCR が内部で必要とするビットマップ表現に自動変換します。

### Step 4: Specify the Region to Extract Text *(H3)*

```csharp
Rectangle regionOfInterest = new Rectangle(120, 350, 400, 80);
```

*Why a `Rectangle`?* OCR エンジンは `System.Drawing.Rectangle` を受け取ります。4 つのパラメータで正確にフィールドを特定し、ページ全体をトリミングできます。

*Tip:* 複数フィールドに対応する場合は、`Dictionary<string, Rectangle>` に各矩形を格納し、ループで処理すると便利です。

### Step 5: Run Recognition and Retrieve Result *(H3)*

```csharp
bool success = ocrEngine.Recognize(regionOfInterest);
string recognizedText = success ? ocrEngine.Text.Trim() : string.Empty;
```

*Why check `success`?* ぼやけた画像、未対応言語、空領域などさまざまな理由で OCR が失敗することがあります。ブール値を確認しておくことで、古いデータを誤って使用するリスクを回避できます。

### Step 6: Handle Edge Cases and Common Pitfalls *(H3)*

- **異なる DPI**：スキャンが低解像度（< 150 DPI）の場合、`ocrEngine.Image.DpiX` と `ocrEngine.Image.DpiY` を認識前に上げてください。  
- **複数ページ**：マルチページ PDF の場合、各ページを個別の PNG に抽出し、ページごとに矩形ロジックを繰り返します。  
- **非英語テキスト**：認識前に `ocrEngine.Language = Language.Thai;`（またはサポートされている任意の言語）を設定します。  
- **ノイズ除去**：`ocrEngine.Image.Filters.Add(new GaussianBlurFilter(1.2f));` を使用すると、粒状スキャンで結果が改善されることがあります。

---

## さらに踏み込む – 実務でのバリエーション

### 同一フォームから複数フィールドを抽出

「氏名」「日付」「金額」など複数項目を取得したい場合は、次のようにコレクションを作成します。

```csharp
var fields = new Dictionary<string, Rectangle>
{
    { "Name",   new Rectangle(50, 200, 300, 60) },
    { "Date",   new Rectangle(400, 200, 200, 60) },
    { "Amount", new Rectangle(650, 200, 250, 60) }
};

foreach (var kvp in fields)
{
    bool ok = ocrEngine.Recognize(kvp.Value);
    Console.WriteLine($"{kvp.Key}: {(ok ? ocrEngine.Text.Trim() : "[Not found]")}");
}
```

### データベースとの統合

抽出後に結果を SQL Server に保存したい場合のサンプルです。

```csharp
using (var conn = new SqlConnection(connectionString))
{
    conn.Open();
    var cmd = new SqlCommand(
        "INSERT INTO FormResults (FieldName, FieldValue) VALUES (@name, @value)", conn);
    cmd.Parameters.AddWithValue("@name", "InvoiceNumber");
    cmd.Parameters.AddWithValue("@value", recognizedText);
    cmd.ExecuteNonQuery();
}
```

### サーバー上での自動化

バックグラウンドサービスとして実行する場合は、ロジックを `async` メソッドにラップし、`Task.Run` で UI の応答性を保ちます。マルチコアでの高速化のために `ocrEngine.ParallelProcessing = true;` を設定することも忘れずに。

---

## 結論

これで Aspose OCR を使って **フォーム画像からテキストを抽出**する、堅牢で本番環境向けの手法が手に入りました。特定の矩形に焦点を当てることで、不要な領域を無視し、効率的かつ正確に目的のデータを取得できます。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}