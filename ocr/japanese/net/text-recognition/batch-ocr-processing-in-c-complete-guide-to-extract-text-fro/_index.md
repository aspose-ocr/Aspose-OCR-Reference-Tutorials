---
category: general
date: 2026-06-16
description: C# のバッチ OCR 処理を使用すると、画像をテキストに迅速に変換できます。Aspose.OCR を使ったステップバイステップのコードで、画像からテキストを抽出する方法を学びましょう。
draft: false
keywords:
- batch OCR processing
- extract text from images
- convert images to text
language: ja
og_description: C#でのバッチOCR処理は画像をテキストに変換します。このガイドに従って、Aspose.OCRを使用して画像からテキストを抽出してください。
og_title: C#によるバッチOCR処理 – 画像からテキストを抽出
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  headline: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  type: TechArticle
- description: Batch OCR processing in C# lets you convert images to text quickly.
    Learn how to extract text from images using Aspose.OCR with step‑by‑step code.
  name: Batch OCR Processing in C# – Complete Guide to Extract Text from Images
  steps:
  - name: Expected Output
    text: 'Assuming you have three images (`invoice1.png`, `receipt2.jpg`, `form3.tif`)
      in the input folder, the output folder will contain:'
  - name: What if some images fail to process?
    text: '`OcrBatchProcessor` logs errors to the console by default and continues
      with the next file. For production use, you can subscribe to the `OnError` event
      to collect failed filenames and retry later.'
  - name: Can I process PDFs directly?
    text: Yes. Aspose.OCR treats each page of a PDF as an image internally. Just point
      `InputFolder` to a directory containing PDFs, and the processor will extract
      text from every page—effectively **convert images to text** even when the source
      is a PDF.
  - name: How do I handle multi‑language documents?
    text: Set `Language` to `OcrLanguage.Multilingual` or specify a list of languages
      if the library version supports it. The engine will attempt to recognize characters
      from all provided languages, which is handy for international invoices.
  - name: What about memory consumption?
    text: The batch processor streams each image, so memory usage stays low even with
      thousands of files. However, enabling a high `MaxDegreeOfParallelism` on a memory‑constrained
      machine could cause spikes. Monitor your RAM and adjust the thread count accordingly.
  type: HowTo
tags:
- OCR
- C#
- Aspose
title: C#でのバッチOCR処理 – 画像からテキストを抽出する完全ガイド
url: /ja/net/text-recognition/batch-ocr-processing-in-c-complete-guide-to-extract-text-fro/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# におけるバッチ OCR 処理 – 画像からテキストを抽出する完全ガイド

C# で **バッチ OCR 処理** を、画像ごとに個別のループを書かずに行う方法を考えたことはありませんか？ あなただけではありません。スキャンした領収書、請求書、手書きメモが数十、あるいは数百枚もあると、各ファイルを手動で OCR エンジンに渡す作業はすぐに悪夢のようになります。  

良いニュースです。Aspose.OCR を使えば、*画像をテキストに変換* する操作を1回のシンプルな処理で行えます。このチュートリアルでは、ライブラリのインストールから、**画像からテキストを抽出**し、必要な形式で結果を保存する本番対応のバッチジョブの実行まで、全工程を順を追って解説します。

> **得られるもの:** フォルダー全体を処理し、元の画像と同じ場所にプレーンテキスト（または JSON、XML、HTML、PDF）ファイルを書き出すすぐに実行できるコンソールアプリと、最大スループットのために並列処理を調整する方法を示します。

## 前提条件

- .NET 6.0 SDK またはそれ以降（コードは .NET Core と .NET Framework の両方で動作します）
- Visual Studio 2022、VS Code、またはお好みの C# エディタ
- Aspose.OCR の NuGet ライセンス（評価用に無料トライアルが利用可能）
- 画像ファイル（`.png`、`.jpg`、`.tif` など）のフォルダーで、**画像をテキストに変換**したいもの

これらの項目が揃っているなら、さっそく始めましょう。

![Diagram illustrating batch OCR processing flow](batch-ocr-workflow.png "Batch OCR processing flow")

## ステップ 1: NuGet で Aspose.OCR をインストール

まず、Aspose.OCR パッケージをプロジェクトに追加します。プロジェクトディレクトリでターミナルを開き、以下を実行してください：

```bash
dotnet add package Aspose.OCR
```

または、Visual Studio 内であれば、*Dependencies → Manage NuGet Packages* を右クリックし、**Aspose.OCR** を検索して *Install* をクリックします。この1行で **バッチ OCR 処理** に必要なすべてが取得されます。

> **プロのコツ:** パッケージのバージョンは常に最新に保ちましょう。最新リリース（2026年6月時点）では新しい画像フォーマットのサポートが追加され、多言語の精度が向上しています。

## ステップ 2: コンソールの雛形を作成

新しい C# コンソールアプリを作成します（まだ作成していない場合）。生成された `Program.cs` を以下の雛形に置き換えてください。上部の `using Aspose.OCR;` ディレクティブに注目してください—これが `OcrBatchProcessor` クラスを提供する名前空間です。

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // We'll fill this in later.
    }
}
```

この時点ではファイルは単なるプレースホルダーですが、**バッチ OCR 処理** ロジックのクリーンな出発点となります。

## ステップ 3: OcrBatchProcessor の初期化

`OcrBatchProcessor` はフォルダーを走査し、サポートされている各画像に OCR を実行して出力を書き込む主役です。インスタンス化は以下のようにシンプルです：

```csharp
// Step 3: Create an OCR batch processor instance
var ocrBatchProcessor = new OcrBatchProcessor();
```

単一画像 API ではなくバッチプロセッサを使用する理由は何でしょうか？ バッチクラスはファイル列挙、エラーロギング、さらには並列実行まで自動で処理するため、ループの実装に費やす時間が減り、精度の微調整により多くの時間を割くことができます。

## ステップ 4: 入力フォルダーと出力フォルダーを指定

プロセッサに画像の読み取り元と結果の出力先を指示します。プレースホルダーのパスを実際のディレクトリに置き換えてください。

```csharp
// Step 4: Configure the input folder containing images to process
ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

// Step 5: Set the folder where OCR results will be saved
ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";
```

アプリを実行する前に両方のフォルダーが存在している必要があります。存在しない場合は `DirectoryNotFoundException` がスローされます。プログラムで作成することも簡単ですが、分かりやすさのため例はシンプルにしています。

## ステップ 5: 出力形式を選択

Aspose.OCR はプレーンテキスト、JSON、XML、HTML、さらには PDF を出力できます。ほとんどの **画像からテキストを抽出** シナリオではプレーンテキストで十分ですが、必要に応じて変更してください。

```csharp
// Step 6: Choose the desired output format (e.g., plain text)
ocrBatchProcessor.OutputFormat = ResultFormat.Text;   // alternatives: Json, Xml, Html, Pdf, etc.
```

下流処理のために構造化データが必要な場合は、`ResultFormat.Json` が堅実な選択です。ライブラリは各ページのテキストを自動的に JSON オブジェクトでラップし、レイアウト情報を保持します。

## ステップ 6: 言語と並列度を設定

OCR の精度は適切な言語モデルに依存します。英語は多くの西洋文書で機能しますが、サポートされている任意の言語（アラビア語、中国語など）を選択できます。さらに、プロセッサに起動させるスレッド数を指定できます—デフォルトは最大 4 です。

```csharp
// Step 7: Specify the language for OCR recognition
ocrBatchProcessor.Language = OcrLanguage.English;

// Step 8: Define the level of parallelism (up to 4 concurrent threads)
ocrBatchProcessor.MaxDegreeOfParallelism = 4;
```

**並列処理が重要な理由:** クアッドコア CPU を持っている場合、`MaxDegreeOfParallelism` を `4` に設定すると処理時間が約 75 % 短縮できます。2 コアのラップトップでは `2` が安全です。ハードウェアに最適な設定を見つけるために試行錯誤してください。

## ステップ 7: バッチジョブを実行

いよいよ本格的な処理が始まります。1 行でパイプライン全体が起動し、入力フォルダー内のすべての画像を処理して結果を出力フォルダーに書き込みます。

```csharp
// Step 9: Execute the batch processing of all supported image files
ocrBatchProcessor.Execute();

Console.WriteLine("Batch OCR completed.");
```

コンソールに *Batch OCR completed.* と表示されたら、各元画像の横に `.txt` ファイル（または選択した形式）が作成されています。ファイル名は元画像と一致するため、OCR 出力と元画像の対応が簡単です。

## 完全な動作例

すべてをまとめると、以下が `Program.cs` にコピーしてすぐに実行できる完全なプログラムです：

```csharp
using Aspose.OCR;
using System;

class BatchDemo
{
    static void Main()
    {
        // Step 1: Create an OCR batch processor instance
        var ocrBatchProcessor = new OcrBatchProcessor();

        // Step 2: Configure the input folder containing images to process
        ocrBatchProcessor.InputFolder = @"C:\MyProjects\OCRDemo\Images\Batch";

        // Step 3: Set the folder where OCR results will be saved
        ocrBatchProcessor.OutputFolder = @"C:\MyProjects\OCRDemo\Results\Batch";

        // Step 4: Choose the desired output format (plain text is default)
        ocrBatchProcessor.OutputFormat = ResultFormat.Text; // alternatives: Json, Xml, Html, Pdf, etc.

        // Step 5: Specify the language for OCR recognition
        ocrBatchProcessor.Language = OcrLanguage.English;

        // Step 6: Define the level of parallelism (up to 4 concurrent threads)
        ocrBatchProcessor.MaxDegreeOfParallelism = 4;

        // Step 7: Execute the batch processing of all supported image files
        ocrBatchProcessor.Execute();

        Console.WriteLine("Batch OCR completed.");
    }
}
```

### 期待される出力

入力フォルダーに 3 枚の画像（`invoice1.png`、`receipt2.jpg`、`form3.tif`）があると仮定すると、出力フォルダーには以下が含まれます：

```
invoice1.txt
receipt2.txt
form3.txt
```

各 `.txt` ファイルには対応する画像から抽出された生の文字列が格納されています。Notepad で任意のファイルを開くと、元のスキャンのプレーンテキスト表現が確認できます。

## よくある質問とエッジケース

### 画像の処理に失敗した場合は？

`OcrBatchProcessor` はデフォルトでエラーをコンソールに記録し、次のファイルへ処理を続行します。本番環境では、`OnError` イベントを購読して失敗したファイル名を収集し、後で再試行することができます。

```csharp
ocrBatchProcessor.OnError += (sender, args) =>
{
    Console.WriteLine($"Failed on {args.FileName}: {args.Exception.Message}");
};
```

### PDF を直接処理できますか？

はい。Aspose.OCR は PDF の各ページを内部的に画像として扱います。`InputFolder` を PDF を含むディレクトリに設定すれば、プロセッサはすべてのページからテキストを抽出します—ソースが PDF であっても実質的に **画像をテキストに変換** できます。

### 多言語文書を処理するには？

`Language` を `OcrLanguage.Multilingual` に設定するか、ライブラリバージョンがサポートしていれば言語リストを指定してください。エンジンは指定されたすべての言語の文字認識を試みるため、国際的な請求書に便利です。

### メモリ消費はどうですか？

バッチプロセッサは各画像をストリーム処理するため、数千ファイルでもメモリ使用量は低く抑えられます。ただし、メモリが限られたマシンで `MaxDegreeOfParallelism` を高く設定するとスパイクが発生する可能性があります。RAM を監視し、スレッド数を適宜調整してください。

## 精度向上のヒント

- **画像の前処理**: ノイズ除去、傾き補正、グレースケール変換を OCR 前に行います。Aspose.OCR は `ImagePreprocessOptions` を提供しており、`ocrBatchProcessor` に付与できます。
- **適切な形式を選択**: レイアウト保持が必要な場合は、`ResultFormat.Html` や `Pdf` が改行や基本的なスタイリングを維持します。
- **結果の検証**: 空の出力ファイルをチェックするシンプルなポストプロセスを実装します—空ファイルは認識失敗を示すことが多いです。

## 次のステップ

これで **バッチ OCR 処理** による **画像からテキストを抽出** の方法を習得したので、次のようなことを検討できるでしょう：

- **データベースと統合** – 各 OCR 結果をメタデータと共に保存し、検索可能にします。
- **UI を追加** – 小規模な WPF または WinForms のフロントエンドを作成し、ユーザーがフォルダーをドラッグ＆ドロップできるようにします。
- **スケールアウト** – バッチジョブを Azure Functions や AWS Lambda 上で実行し、クラウドネイティブな処理を実現します。

これらのトピックはすべて本稿で扱ったコア概念に基づいているため、ソリューションを拡張する準備は整っています。

---

**コーディングを楽しんでください！** 問題が発生したり改善案があれば、下にコメントを残してください。会話を続けて、OCR 自動化をさらにスムーズにしましょう。

## 次に学ぶべきことは？

以下のチュートリアルは、本ガイドで示した手法に基づく密接に関連したトピックを取り上げています。各リソースには、ステップバイステップの解説と完全な動作コード例が含まれており、追加の API 機能を習得し、プロジェクトで代替実装アプローチを検討するのに役立ちます。

- [フォルダー上で OCR 操作を使用して画像からテキストを抽出](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Aspose.OCR for .NET でリストを使用して画像をバッチ OCR する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)
- [Aspose.OCR for .NET を使用して ZIP アーカイブからテキストを抽出する方法](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}