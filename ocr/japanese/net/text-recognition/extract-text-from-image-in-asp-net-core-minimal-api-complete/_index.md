---
category: general
date: 2026-05-25
description: 最小限の ASP.NET Core API で画像からテキストを抽出する方法を学びましょう。POST で画像をアップロードし、マルチパートフォームデータを読み取って画像に
  OCR を実行します。
draft: false
keywords:
- extract text from image
- upload image via post
- read multipart form data
- how to recognize text from image
- perform OCR on image
language: ja
og_description: 最小限の ASP.NET Core API を使用して画像からテキストを抽出します。このガイドでは、POST で画像をアップロードし、マルチパートフォームデータを読み取り、画像に対して
  OCR を実行する方法を示します。
og_title: ASP.NET Coreで画像からテキストを抽出する – ステップバイステップ
schemas:
- author: Aspose
  dateModified: '2026-05-25'
  description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  headline: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  type: TechArticle
- description: Learn how to extract text from image with a minimal ASP.NET Core API.
    Upload image via POST, read multipart form data and perform OCR on image.
  name: Extract Text from Image in ASP.NET Core Minimal API – Complete Guide
  steps:
  - name: Breaking Down the Logic
    text: '| Step | What Happens | Why It Matters | |------|--------------|----------------|
      | **ReadFormAsync** | Parses the incoming *multipart/form-data* request. | Without
      this, you can’t access the uploaded files. | | **form.Files["image"]** | Retrieves
      the file whose form‑field name is `image`. | Guarant'
  - name: 1. Large Files
    text: 'The default request body limit is 30 MB. For larger scans you might need
      to adjust:'
  - name: 2. Asynchronous OCR
    text: Some OCR libraries expose async methods (`RecognizeAsync`). If yours does,
      replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the
      lambda as `async`.
  - name: 3. Security Considerations
    text: '- **Validate file size** before loading it into memory. - **Sanitize the
      filename** if you ever write it to disk. - **Rate‑limit** the endpoint to avoid
      denial‑of‑service attacks.'
  - name: 4. GPU Acceleration
    text: If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your
      hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially
      on high‑resolution images.
  type: HowTo
tags:
- ASP.NET Core
- OCR
- Minimal API
title: ASP.NET Core Minimal APIで画像からテキストを抽出する – 完全ガイド
url: /ja/net/text-recognition/extract-text-from-image-in-asp-net-core-minimal-api-complete/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ASP.NET Core Minimal APIで画像からテキストを抽出する – 完全ガイド

重厚なフレームワークと格闘せずに **画像からテキストを抽出** したいと思ったことはありませんか？ あなたは一人ではありません。多くの開発者が、ユーザーが画像をドロップして生の文字列を取得できる迅速な方法を必要としています。レシートのスキャン、手書きメモのデジタル化、検索インデックスの構築など、さまざまな用途があります。

このチュートリアルでは、**POSTで画像をアップロード**し、*multipart/form‑data* ペイロードを解析し、シングルトンの `OcrEngine` を使って **画像上で OCR を実行** する小さな ASP.NET Core Minimal API を作成します。最後までで、任意の .NET 8 プロジェクトに組み込んですぐに画像からテキストを抽出できる、完全に実行可能なアプリが手に入ります。

## 作成するもの

- `/ocr` をリッスンするミニマルな Web アプリ。
- `multipart/form-data` の POST リクエストで送信された画像ファイルを受け取るエンドポイント。
- アップロードされたファイルを読み取り、OCR エンジンに渡してプレーンテキストの結果を返すロジック。
- 対応カードを持つ方向けの、GPU 加速スニペット（コメントアウト済み）オプション。

**前提条件**  
- .NET 8 SDK（またはそれ以降）。  
- C# とコマンドラインの基本的な知識。  
- `OcrEngine` クラスを提供する OCR ライブラリ（サンプルでは仮想の NuGet パッケージを想定）。

これらが揃っているなら、さっそく始めましょう。

## ステップ 1: プロジェクトのセットアップと OCR パッケージの追加

First, create a new web project and pull in the OCR library.

```bash
dotnet new web -n ImageOcrApi
cd ImageOcrApi
dotnet add package Awesome.Ocr --version 1.3.0   # replace with your actual OCR package
```

> **プロのコツ:** 依存関係は常に最新に保ちましょう。新しいバージョンは、特に GPU 加速推論においてパフォーマンス向上をもたらすことが多いです。

## ステップ 2: シングルトン OCR エンジンの登録（主要サービス）

We want a single `OcrEngine` instance for the whole app—no need to spin up a new engine per request. Register it in the builder’s service container.

```csharp
using Awesome.Ocr;               // <-- the OCR library namespace
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using System.Drawing;            // System.Drawing.Common for Image handling

var builder = WebApplication.CreateBuilder(args);

// Register a singleton OCR engine (English language)
// Uncomment the GPU line if you have a compatible GPU and the library supports it.
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU acceleration
    return engine;
});
```

**なぜシングルトンか？**  
OCR エンジンの作成はコストがかかります—例えばニューラルネットワークの重みをメモリにロードすることを考えてください。同じインスタンスを再利用することで CPU サイクルと RAM の両方を節約でき、すべての `/ocr` 呼び出しの応答時間が速くなります。

## ステップ 3: アプリケーションの構築

Now we materialize the `WebApplication` object.

```csharp
var app = builder.Build();
```

この行はほぼ魔法のように見えますが、内部ではルーティング、ミドルウェア、そして先ほど設定した DI コンテナを接続しています。

## ステップ 4: POST エンドポイントの定義 – “POST で画像をアップロード”

Here’s the heart of the tutorial: an endpoint that **upload image via POST**, reads the multipart payload, and hands the data to the OCR engine.

```csharp
app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    // Step 5: Read multipart form data and extract the uploaded image
    var form = await request.ReadFormAsync();               // <-- read multipart/form-data
    var file = form.Files["image"];                         // expects a field named "image"

    if (file is null || file.Length == 0)
    {
        return Results.BadRequest("No image file provided.");
    }

    // Guard against unsupported content types
    if (!file.ContentType.StartsWith("image/"))
    {
        return Results.BadRequest("Uploaded file is not an image.");
    }

    // Load the image into a System.Drawing.Image
    using var img = Image.FromStream(file.OpenReadStream());

    // Step 6: Perform OCR on the image
    string text = ocr.Recognize(img);                       // <-- perform OCR on image

    // Step 7: Return the extracted text as plain‑text
    return Results.Text(text);
});
```

### ロジックの分解

| ステップ | 何が起こるか | 重要な理由 |
|------|--------------|----------------|
| **ReadFormAsync** | 受信した *multipart/form-data* リクエストを解析します。 | これがなければ、アップロードされたファイルにアクセスできません。 |
| **form.Files["image"]** | フィールド名が `image` のファイルを取得します。 | 呼び出し側に予測可能な契約を保証します。 |
| **Content‑type check** | ファイルが画像かどうか（例: `image/png`）を確認します。 | 画像でないデータで OCR エンジンがエラーになるのを防ぎます。 |
| **Image.FromStream** | 生のストリームを `System.Drawing.Image` に変換します。 | OCR ライブラリはバイト配列ではなく `Image` オブジェクトを期待します。 |
| **ocr.Recognize(img)** | OCR エンジンを呼び出して **画像からテキストを認識** します。 | これが **画像上で OCR を実行** する核心のステップです。 |
| **Results.Text** | プレーンテキストのレスポンスを返します。 | 下流サービスが扱いやすいシンプルな形式です。 |

## ステップ 5: API の実行

Finally, start the web server.

```csharp
app.Run();
```

When you execute `dotnet run`, the API will listen on `http://localhost:5000` (or a port of your choosing). You can test it with `curl`:

```bash
curl -X POST http://localhost:5000/ocr \
  -F "image=@/path/to/receipt.png" \
  -H "Accept: text/plain"
```

**Expected output:** The console will print the recognized characters, e.g.:

```
Total: $23.45
Date: 2026-05-20
Item A  $12.00
Item B  $11.45
```

If the image is blurry or the language isn’t supported, the OCR engine will return an empty string or an error message—handle those cases in production code.

## エッジケースとベストプラクティス

### 1. 大きなファイル

The default request body limit is 30 MB. For larger scans you might need to adjust:

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 100 * 1024 * 1024; // 100 MB
});
```

### 2. 非同期 OCR

Some OCR libraries expose async methods (`RecognizeAsync`). If yours does, replace `ocr.Recognize(img)` with `await ocr.RecognizeAsync(img)` and mark the lambda as `async`.

### 3. セキュリティ上の考慮点

- メモリにロードする前に **ファイルサイズを検証** する。  
- ディスクに書き込む場合は **ファイル名をサニタイズ** する。  
- **レートリミット** を設定し、DoS 攻撃を防止する。

### 4. GPU 加速

If you uncomment the `engine.GpuDevice = new GpuDevice(0);` line and your hardware supports CUDA or DirectML, you’ll see a noticeable speed boost, especially on high‑resolution images.

## 完全動作例

Below is the complete `Program.cs` you can copy‑paste into a fresh Minimal API project.

```csharp
using Awesome.Ocr;
using Microsoft.AspNetCore.Builder;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Http.Features;
using System.Drawing;

var builder = WebApplication.CreateBuilder(args);

// Optional: increase multipart limit for big images
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});

// Register the OCR engine as a singleton
builder.Services.AddSingleton<OcrEngine>(sp =>
{
    var engine = new OcrEngine { Language = OcrLanguage.English };
    // engine.GpuDevice = new GpuDevice(0); // enable GPU if available
    return engine;
});

var app = builder.Build();

app.MapPost("/ocr", async (HttpRequest request, OcrEngine ocr) =>
{
    var form = await request.ReadFormAsync();
    var file = form.Files["image"];

    if (file is null || file.Length == 0)
        return Results.BadRequest("No image file provided.");

    if (!file.ContentType.StartsWith("image/"))
        return Results.BadRequest("Uploaded file is not an image.");

    using var img = Image.FromStream(file.OpenReadStream());

    // Core OCR operation
    string text = ocr.Recognize(img);

    return Results.Text(text);
});

app.Run();
```

Save, run `dotnet run`, and you’re ready to **extract text from image** on demand.

## 結論

We’ve walked through a **complete, end‑to‑end solution** for extracting text from image using ASP.NET Core Minimal API. Starting from project scaffolding, we **registered a singleton OCR engine**, built an endpoint that **uploads image via POST**, **read multipart form data**, and finally **perform OCR on image** to return clean plain‑text. 

From here you can:

- よりリッチなレスポンスのために JSON ラッパーを追加。  
- 抽出したテキストを保存するデータベースを組み込む。  
- 複数言語（`OcrLanguage.Spanish` など）への対応を拡張。

The pattern scales nicely—just drop the same endpoint into a larger microservice or expose it behind an API gateway.

Got questions about handling PDFs, batch processing, or GPU tuning? Drop a comment, and happy coding!

## 関連チュートリアル

- [Aspose.OCR .NET を使用した画像からテキストを抽出](/ocr/english/net/image-and-drawing-recognition/)
- [Aspose.OCR for .NET による画像テキスト抽出 – OCR 最適化](/ocr/english/net/ocr-optimization/)
- [Aspose.OCR を使用した C# での画像テキスト抽出（言語選択）](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}