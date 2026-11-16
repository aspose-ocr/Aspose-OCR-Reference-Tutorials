---
category: general
date: 2026-04-11
description: Aspose OCR for C# で OCR を無効にしてオフラインで実行し、インターネットなしで画像からテキストを抽出し、OCR 用に画像を正しく読み込む方法を学びましょう。
draft: false
keywords:
- how to disable OCR
- extract text from image
- load image for OCR
- offline OCR C#
- Aspose OCR resources
language: ja
og_description: Aspose OCR for C#でOCRを無効にし、オフラインで実行し、インターネット不要で画像からテキストを抽出し、OCR用に画像を簡単に読み込む方法。
og_title: C#でOCRを無効にする方法 – オフライン Aspose OCR ガイド
tags:
- C#
- OCR
- Aspose
- Offline Processing
title: C#でOCRを無効化する方法 – オフライン Aspose OCR ガイド
url: /ja/net/ocr-configuration/how-to-disable-ocr-in-c-offline-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を無効化する方法 – オフライン Aspose OCR ガイド

本当にオフラインで動作させたいとき、**OCR を無効化する方法** を知りたくありませんか？たとえば、ネットワークに依存できないセキュアなデスクトップアプリを作成している場合や、予期せぬダウンロードを避けたい場合です。幸い、Aspose OCR では自動リソース取得をオフにし、ローカルフォルダーを指定してすべてをオンプレミスで管理できます。このチュートリアルでは、**画像からテキストを抽出** する方法と、**OCR 用に画像をロード** する正しい手順も併せて紹介します。

エンジンの初期化から認識した日本語テキストの出力まで、外部ドキュメントや隠されたマジックは一切不要の、すぐに実行できる完全なサンプルを順を追って解説します。最後まで読むと、自動ダウンロード機能を無効化する重要性、リソースパスの設定方法、注意すべき落とし穴が理解できるようになります。

## 前提条件

- .NET 6.0（またはそれ以降の .NET バージョン）がマシンにインストールされていること。  
- Aspose.OCR for .NET NuGet パッケージ（`Install-Package Aspose.OCR`）。  
- 必要な言語リソース（例：日本語モデル）が既に格納されたフォルダー。  
- OCR を実行したい画像ファイル（`japan_doc.png`）。

言語パックが不足している場合は、Aspose ポータルから一度だけダウンロードし、`AsposeOCRResources` などのフォルダーに解凍してください。自動ダウンロード機能を無効化すれば、以降は追加のダウンロードは発生しません。

![OCR をオフラインで無効化する方法](/images/how-to-disable-ocr.png "how to disable OCR illustration")

## Step 1 – OCR エンジン インスタンスの作成  

最初に行うのは `OcrEngine` のインスタンス化です。このオブジェクトが画像を読み取る「脳」の役割を担います。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Settings;

class OfflineDemo
{
    static void Main()
    {
        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

> **重要ポイント:** エンジンがなければ設定はできません。オブジェクトはすべての設定を保持し、ライブラリがインターネットにアクセスできるかどうかを決める重要なフラグも含まれます。

## Step 2 – 自動リソース ダウンロードの無効化  

デフォルトでは Aspose OCR は不足している言語ファイルをオンデマンドで取得しようとします。オフライン環境を保つために、`AutoDownloadResources` スイッチを `false` に切り替えます。

```csharp
        // Step 2: Disable automatic resource download to work offline
        ocrEngine.Settings.AutoDownloadResources = false;
```

> **プロのコツ:** これをオフにするとプライバシーが保護されるだけでなく、エンジンが更新チェックに時間を費やさないため、最初の認識が高速化します。

## Step 3 – ローカルリソース フォルダーの指定  

事前にダウンロードしておいた言語パックが格納されているフォルダーへのパスをエンジンに教えます。前提条件で設定したパスです。

```csharp
        // Step 3: Point the engine to the folder containing pre‑downloaded resources
        ocrEngine.Settings.ResourcesPath = @"YOUR_DIRECTORY/AsposeOCRResources";
```

> **起こり得る問題:** パスが間違っている、または必要な言語ファイルが欠如していると `ResourceNotFoundException` がスローされます。フォルダー名の綴りと日本語モデル（`jpn.traineddata`）が存在するかを必ず確認してください。

## Step 4 – ローカル言語モデルの選択  

ディスク上にある実際の言語を選択します。例では日本語を使用していますが、ダウンロード済みの他言語に置き換えることも可能です。

```csharp
        // Step 4: Select the language model that is available locally
        ocrEngine.Settings.Language = Language.Japanese;
```

> **エッジケース:** 一部の言語（例: 中国語）では追加の辞書が必要です。補助ファイルも同じリソースフォルダーに入れておきましょう。

## Step 5 – OCR 用に画像をロード  

ここで **OCR 用に画像をロード** します。`ImageStream.FromFile` メソッドはファイルをストリームに読み込み、Aspose が処理できる形に変換します。

```csharp
        // Step 5: Load the image you want to recognize
        ImageStream image = ImageStream.FromFile(@"YOUR_DIRECTORY/japan_doc.png");
```

> **ヒント:** 対応フォーマットは PNG、JPEG、BMP、TIFF です。PDF を扱う場合は、各ページを画像に変換してから処理してください。

## Step 6 – 認識プロセスの実行  

エンジンが実際にピクセルを読み取り、テキストへ変換しようとします。

```csharp
        // Step 6: Run the OCR process
        OcrResult ocrResult = ocrEngine.Recognize(image);
```

> **このステップが遅くなる理由:** OCR は CPU 集中型処理です。特に高解像度画像では時間がかかります。パフォーマンスが問題になる場合は、認識前に画像を縮小することを検討してください。

## Step 7 – 抽出したテキストの出力  

最後に **画像からテキストを抽出** し、コンソールに表示します。

```csharp
        // Step 7: Output the recognized text
        Console.WriteLine(ocrResult.Text);
    }
}
```

プログラムを実行すると、`japan_doc.png` に含まれていた日本語文字がコンソールに表示されます。設定が正しければ、Unicode テキストのブロックがきれいに出力されます。

### 期待される出力

```
これはサンプルの日本語テキストです。
```

(実際の出力は画像の内容に依存します。)

## よくある落とし穴と回避策  

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **言語ファイルが欠如** | `AutoDownloadResources` が false のためエンジンが取得できない | `ResourcesPath` が `jpn.traineddata` を含むフォルダーを指しているか確認 |
| **画像パスが誤っている** | `ImageStream.FromFile` が `FileNotFoundException` をスロー | 絶対パスを使用するか、作業ディレクトリを正しく設定 |
| **未対応画像形式** | Aspose が読み取れる形式は限定的 | `FromFile` 呼び出し前に画像を PNG または JPEG に変換 |
| **大画像でメモリ不足** | OCR は画像全体をメモリに展開する | 画像をリサイズ／タイル化するか、プロセスのメモリ上限を増やす |

## サンプルの拡張例  

- **バッチ処理:** ディレクトリ内の画像をループで処理し、各結果を個別の `.txt` ファイルに書き出す。  
- **他言語対応:** `Language.Japanese` を `Language.English`（または他の言語）に置き換え、対応するリソースファイルを配置。  
- **カスタム前処理:** Aspose.Imaging を使ってデスキューやコントラスト調整を行い、OCR の精度を向上させる。

## 結論  

これで **C# の Aspose OCR で OCR を無効化** し、完全にオフラインで動作させる方法が分かりました。`AutoDownloadResources` を `false` に設定し、ローカルリソースフォルダーを指し示し、正しく **OCR 用に画像をロード** すれば、インターネットに一切接続せずに **画像からテキストを抽出** できます。この手法はセキュアな環境、CI パイプライン、ネットワークアクセスが制限されたシナリオに最適です。

次のステップに進みませんか？スキャンした PDF フォルダー全体を処理したり、別の言語パックで実験したり、OCR 結果を検索可能なデータベースに統合したりしてみてください。今日構築したオフライン設定は、オンプレミスの文書処理ワークフローの堅実な基盤となります。

Happy coding, and feel free to drop a comment if you hit any snags!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}