---
category: general
date: 2026-05-28
description: ASP.NET CoreでOCRを実行する方法—画像のアップロード、画像からのテキスト抽出、そしてファイルアップロードを効率的に処理する方法を学びましょう。
draft: false
keywords:
- how to perform OCR
- extract text from image
- handle file upload
- how to upload file
- upload image OCR
language: ja
og_description: ASP.NET CoreでOCRを実行する方法。画像のアップロード、画像からのテキスト抽出、そしてAspose OCRを使用したファイルアップロードの処理をステップバイステップで学びましょう。
og_title: ASP.NET CoreでOCRを実行する方法 – 完全ガイド
schemas:
- author: Aspose
  dateModified: '2026-05-28'
  description: How to perform OCR in ASP.NET Core—learn to upload image, extract text
    from image, and handle file upload efficiently.
  headline: How to Perform OCR in ASP.NET Core – Full Guide
  type: TechArticle
tags:
- OCR
- ASP.NET Core
- C#
- file upload
title: ASP.NET CoreでOCRを実行する方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-perform-ocr-in-asp-net-core-full-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# ASP.NET Core で OCR を実行する方法 – 完全ガイド

最新の Web API で **how to perform OCR** を実行することを考えたことはありますか？ 髪の毛が抜けるほど悩む必要はありません。開発者は常に、ユーザーが画像（レシート、パスポートのスキャン、手書きメモなど）をアップロードできるようにし、JSON で生のテキストを取得する必要があります。  

このチュートリアルでは、**how to upload file** を示す完全な本番対応ソリューションを順を追って解説します。ファイルの検証、Aspose OCR の実行、最終的に **extract text from image** を行います。最後まで読むと、任意の ASP.NET Core プロジェクトに貼り付けられるコントローラが手に入ります。

## 作成するもの

- multipart/form‑data アップロードを受け付ける `OcrController`
- ファイルが実際に存在し、空でないことを検証
- Aspose OCR エンジンを使用した非同期 OCR 処理
- 認識されたテキストを含むシンプルな JSON 応答

外部サービスや隠されたマジックは不要です—ローカルで実行できる純粋な C# コードだけです。

## 前提条件（開始前に必要なもの）

| Requirement | Why It Matters |
|-------------|----------------|
| .NET 6 SDK or later | ASP.NET Core 6+ はミニマル API 機能と非同期サポートを提供します。 |
| Visual Studio 2022 (or VS Code) | IDE はデバッグを容易にしますが、任意のエディタでも動作します。 |
| Aspose.OCR NuGet package (`dotnet add package Aspose.OCR`) | 実際に OCR 処理を行うエンジンです。 |
| Basic knowledge of ASP.NET Core MVC | `ControllerBase` とルーティング属性を使用します。 |

これらが揃っていれば、さあ始めましょう。

## 手順 1: プロジェクトのセットアップと Aspose OCR のインストール

ターミナルを開き、最新の Web API プロジェクトを作成します：

```bash
dotnet new webapi -n OcrDemo
cd OcrDemo
dotnet add package Aspose.OCR
```

その単一コマンドで OCR ライブラリとすべての依存関係が取得されます。追加の設定は不要です。Aspose は一般的な画像フォーマットに対してすぐに使えます。

## 手順 2: OCR コントローラの追加（**how to perform OCR** の核心）

`Controllers/OcrController.cs` という新しいファイルを作成し、以下のコードを貼り付けます。完全な実行可能サンプルで、欠けている部分はありません。

```csharp
using Aspose.OCR;
using Microsoft.AspNetCore.Mvc;
using System.Threading.Tasks;

namespace OcrDemo.Controllers
{
    [ApiController]
    [Route("[controller]")]
    public class OcrController : ControllerBase
    {
        // Step 1: Receive the uploaded file from the request
        [HttpPost("upload")]
        public async Task<IActionResult> Upload([FromForm] IFormFile uploadedFile)
        {
            // Step 2: Validate that a file was actually provided
            if (uploadedFile == null || uploadedFile.Length == 0)
                return BadRequest("No file supplied.");

            // Step 3: Open a read‑only stream for the file content
            await using var fileStream = uploadedFile.OpenReadStream();

            // Step 4: Create the OCR engine and load the image from the stream
            var ocrEngine = new OcrEngine();
            ocrEngine.Image = ImageStream.FromStream(fileStream);

            // Step 5: Perform asynchronous text recognition
            string extractedText = await ocrEngine.RecognizeAsync();

            // Step 6: Return the recognized text in the response
            return Ok(new { extractedText });
        }
    }
}
```

### Why This Works

- **`[FromForm] IFormFile`** は ASP.NET Core にマルチパートのファイル部分を `uploadedFile` にバインドさせます。これは Web API で **handle file upload** を行う古典的な方法です。
- `if` ガードにより **handle file upload** エラーを優雅に処理し、クライアントがファイルを送信し忘れた場合は 400 Bad Request を返します。
- `using var fileStream = uploadedFile.OpenReadStream();` は*読み取り専用*ストリームを開きます。大きなファイルに必須で、画像全体をメモリに読み込む必要はありません。
- `ocrEngine.Image = ImageStream.FromStream(fileStream);` はストリームを直接 Aspose OCR に渡し、パイプラインをシンプルに保ちます。
- `await ocrEngine.RecognizeAsync();` はバックグラウンドスレッドで重い処理を実行し、API の応答性を保ちます。これは **how to perform OCR** を非同期で行う核心です。
- 最後に結果を JSON オブジェクト（`{ extractedText }`）でラップします—フロントエンドでの利用に最適です。

## 手順 3: リクエストサイズ制限の設定（任意だが便利）

高解像度のスキャンを想定する場合は、デフォルトのリクエストサイズを拡大します。`Program.cs` に以下を追加してください：

```csharp
builder.Services.Configure<FormOptions>(options =>
{
    options.MultipartBodyLengthLimit = 50 * 1024 * 1024; // 50 MB
});
```

これで API は 10 MB のレシート画像でも問題なく処理できます。使用ケースに応じて制限を調整してください。

## 手順 4: エンドポイントを cURL または Postman でテスト

ターミナルから実行できる簡単な cURL コマンドを示します：

```bash
curl -X POST http://localhost:5000/ocr/upload \
  -F "uploadedFile=@/path/to/your/image.png"
```

以下のような JSON ペイロードが表示されるはずです：

```json
{
  "extractedText": "Sample text that was on the image."
}
```

画像に認識可能な文字が含まれていない場合、文字列は空になります—エラーは起きず、空の結果が返ります。これは覚えておくべき重要なエッジケースです。

## 手順 5: ビジュアル確認（任意の画像）

以下は、OCR リクエストが成功した後に受け取る JSON 応答を示すプレースホルダー画像です。

![How to perform OCR result – screenshot of JSON response showing extracted text](/images/ocr-result.png)

*Alt text:* **how to perform OCR の結果スクリーンショット（画像から抽出されたテキスト）**

## よくある落とし穴とプロのコツ

| Pitfall | Solution |
|---------|----------|
| **Unsupported image format**（例: 複数ページの TIFF） | まず PNG/JPEG に変換するか、`OcrEngine` に渡す前に Aspose の `ImageConverter` を使用してください。 |
| **Large files cause memory pressure** | 示したようにファイルをストリーム処理し、`IFormFile.CopyToAsync` で `MemoryStream` にコピーするのは避けてください。 |
| **OCR returns garbled text** | 画像が高コントラストで正しい向きであることを確認してください。必要に応じて `ocrEngine.Preprocess()` で前処理を行います。 |
| **Multiple concurrent requests** | Aspose OCR はスレッドセーフですが、サーバーのメモリが制限されている場合はセマフォで同時実行数を制限すると良いでしょう。 |

## 例の拡張: バルクアップロードと並列処理

複数の画像を同時に **handle file upload** する必要がある場合は、アクションのシグネチャをリスト受け取りに変更します：

```csharp
[HttpPost("batch")]
public async Task<IActionResult> BatchUpload([FromForm] List<IFormFile> files)
{
    if (files == null || !files.Any())
        return BadRequest("No files supplied.");

    var results = new List<object>();

    foreach (var file in files)
    {
        await using var stream = file.OpenReadStream();
        var engine = new OcrEngine { Image = ImageStream.FromStream(stream) };
        var text = await engine.RecognizeAsync();
        results.Add(new { fileName = file.FileName, extractedText = text });
    }

    return Ok(results);
}
```

これで **upload image OCR** をバルクで実行でき、フォルダ内のレシートを一括でスキャンするのに最適です。

## セキュリティ上の考慮事項

- **Validate file extensions**（`.png`, `.jpg`, `.jpeg`）を処理前に検証し、悪意あるアップロードを防止します。
- **Scan for viruses** を実施し、API がインターネットに公開されている場合は ClamAV などのサービスと統合してください。
- **Rate‑limit** を設定し、エンドポイントへの DoS 攻撃を防止します。

## 期待される出力と検証方法

`/ocr/upload` エンドポイントに「Hello」という単語がはっきり写った画像でリクエストすると、レスポンスは以下のようになるはずです：

```json
{
  "extractedText": "Hello"
}
```

ブラウザの開発者ツール → Network タブを開くか、cURL の出力を確認することで簡単に検証できます。

## まとめ – カバーした内容

- ASP.NET Core プロジェクトをセットアップし、Aspose OCR NuGet パッケージを追加しました。
- **how to perform OCR**、**handle file upload**、**extract text from image** を示すクリーンなコントローラを実装しました。
- エラーハンドリング、パフォーマンス調整、セキュリティのベストプラクティスについて議論しました。
- 実行可能なコードサンプルとバルクアップロードのバリエーションを提供しました。

## 次にやること

- **Add language support**: Aspose OCR は異なる言語に設定可能です（`ocrEngine.Language = Language.English;`）。
- **Integrate with a database**: 抽出したテキストとメタデータを保存し、後で検索できるようにします。
- **Front‑end UI**: ユーザーが画像をドラッグ＆ドロップし、OCR 結果を即座に確認できるシンプルな React または Blazor ページを作成します。

自由に実験してください—OCR エンジンを入れ替えたり、異なる画像前処理を試したり、結果を下流の AI モデルに連携したりできます。最新の .NET スタックで **how to perform OCR** を知っていれば、可能性は無限です。

コーディングを楽しんで、テキストが常に読みやすい状態でありますように！

## 関連チュートリアル

- [画像の OCR 方法 – OCR 画像認識で画像に OCR を実行する](/ocr/english/net/image-and-drawing-recognition/perform-ocr-on-image/)
- [Aspose を使用してストリームから画像を認識する方法 – OCR 画像認識](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [OCR 画像認識でしきい値を設定する方法](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}