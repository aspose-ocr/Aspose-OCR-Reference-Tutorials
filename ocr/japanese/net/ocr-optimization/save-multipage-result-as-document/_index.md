---
date: 2026-04-29
description: Aspose.OCR を使用して画像を PDF に変換する方法（C#）、マルチページ OCR 結果をドキュメントとして保存する方法、画像からテキストを抽出する方法（C#）を学びましょう。
keywords:
- convert images to pdf
- extract text from images
- c# ocr library
- convert images to xlsx
- generate pdf from tiff
linktitle: 画像をPDFに変換 C# – 複数ページのOCR結果を保存
second_title: Aspose.OCR .NET API
title: 画像をPDFに変換（C#） – 複数ページのOCR結果を保存
url: /ja/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像をPDFに変換 C# – 複数ページのOCR結果を保存

## はじめに

このチュートリアルでは、強力な **Aspose.OCR** ライブラリ for .NET を使用して **convert images to PDF C#** の方法を学びます。**convert scanned TIFF files to searchable PDFs** が必要な場合や、画像からテキストを抽出してデータマイニングを行う場合、または画像のバッチから Excel ワークブックを生成する場合でも、本ガイドは明確な説明、実践的なヒント、ベストプラクティスの推奨とともに、すべての手順を丁寧に案内します。

## クイック回答

- **What does this tutorial cover?** 複数の画像を PDF、Docx、Text、Xlsx に変換し、C# の Aspose.OCR を使用して OCR 結果を複数ページのドキュメントとして保存します。  
- **Which output formats are supported?** Docx、Text、Pdf、Xlsx（PDF を直接出力することも可能）  
- **Do I need a license?** 無料トライアルで評価は可能ですが、本番環境では永続ライセンスが必要です。  
- **What .NET versions are compatible?** .NET Framework 4.5+、.NET Core 3.1+、.NET 5/6/7  
- **Can I extract text while converting?** はい—保存前に OCR 結果を使用して検索可能なテキストを取得できます。

## 「convert images to PDF C#」とは何ですか？

C# で画像を PDF に変換することは、プログラム上で 1 つまたは複数のビットマップファイル（PNG、JPEG、TIFF など）を取得し、視覚的レイアウトを保持しつつ、必要に応じて OCR による検索可能なテキストを埋め込んだ PDF ドキュメントを生成することを意味します。Aspose.OCR は **c# ocr library** を提供し、マルチページ対応や一般的なオフィス形式への直接保存など、エンドツーエンドの処理を行います。

## このタスクで Aspose.OCR を使用する理由

- **High‑accuracy OCR** は数十言語をサポートします。  
- **Multipage processing** – 画像フォルダー全体を入力し、単一の検索可能な PDF を取得します。  
- **Direct export** to Docx、Text、Pdf、Xlsx へ、二次変換ステップ不要でエクスポートできます。  
- **Pure .NET** – ネイティブ依存がなく、Windows、Linux、クラウドランタイムで動作します。

## 前提条件

1. .NET 用 Aspose.OCR をインストールします。ダウンロードは [here](https://releases.aspose.com/ocr/net/) から。  
2. 無料トライアルまたは購入ライセンスを取得します – トライアルは [here](https://releases.aspose.com/) から、購入は [here](https://purchase.aspose.com/buy) から。  
3. 公式 [documentation](https://reference.aspose.com/ocr/net/) を確認し、API の概要に慣れます。  
4. [support forums](https://forum.aspose.com/c/ocr/16) でコミュニティに参加し、問題解決の支援を受けます。

すべての準備が整ったので、コーディングを始めましょう。

## 名前空間のインポート

C# ファイルに必要な名前空間を追加します:

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

これらのインポートにより、コレクション、ファイル操作、LINQ、そして Aspose OCR クラスにアクセスできます。

## ステップ 1: ドキュメントディレクトリの設定

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` を、ソース画像がある絶対パスまたは相対パス、そして出力ファイルを保存したい場所に置き換えます。

## ステップ 2: Aspose.OCR の初期化

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` オブジェクトを作成することで、**convert images to PDF C#** ワークフローを含むすべての OCR 操作にアクセスできます。

## ステップ 3: 画像の認識

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` メソッドはリスト内の各ファイルを処理し、`RecognitionResult` のコレクションを返します。任意の数の画像を入力でき、**convert scanned images to PDF** のシナリオに最適です。

## ステップ 4: 好みの形式で結果を保存

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

下流のワークフローに最適な形式を選択してください：

- **Docx** – 検索可能なテキストを含む編集可能な Word 文書。  
- **Text** – 簡易データマイニング用のプレーンテキスト抽出（**extract text from images**）。  
- **Pdf** – アーカイブに最適な従来の PDF 出力。  
- **Xlsx** – 表形式データのスプレッドシート表現（**convert images to xlsx**）。

## 画像をPDFに変換 C# の手順 – ステップバイステップまとめ

1. **変換したい画像が入ったフォルダーを用意する**  
2. **`AsposeOcr` インスタンスを作成**して OCR 機能にアクセスする  
3. **`RecognizeMultipleImages` を呼び出し**、各ファイルの OCR 結果を取得する  
4. **`SaveMultipageDocument` を使用して** 必要な形式でマルチページ結果を保存する

## 一般的な使用例

- **Digital archiving:** スキャンした紙の契約書を検索可能な PDF に変換します。  
- **Data entry automation:** 領収書や請求書からテキストを抽出し、データベースに取り込みます。  
- **Batch processing:** 数千枚の画像を単一のジョブで最小限のコードで処理します。  
- **Generate PDF from TIFF:** 元の高解像度スキャン文書を忠実に保持する必要がある場合に最適です。

## トラブルシューティングとヒント

- **Large image sets:** メモリスパイクを防ぐため、画像を小さなバッチに分けて処理します。  
- **Image quality:** OCR の精度を最適化するため、画像は最低 300 dpi であることを確認してください。  
- **License errors:** OCR メソッドを呼び出す前に、ライセンスファイルが正しくロードされているか確認します。  
- **Empty results:** 画像が読めない場合、対応する `RecognitionResult` の `Text` プロパティは空になります—保存前に null または空文字列かチェックしてください。

## よくある質問

**Q: Can I convert images to PDF C# without using OCR?**  
A: はい、純粋な画像‑to‑PDF 変換には Aspose.PDF や他のライブラリを使用できますが、OCR を使用すると検索可能なテキストが追加され、PDF がはるかに有用になります。

**Q: How do I extract text from images C# after conversion?**  
A: `RecognizeMultipleImages` が返す `result` リストには各ページの `Text` プロパティが含まれています。これらの文字列を `.txt` ファイルに書き出すか、アプリケーション内で直接処理できます。

**Q: Is it possible to set custom page margins or orientation?**  
A: PDF や Docx に保存する際、`SaveMultipageDocument` を呼び出す前に Aspose.Words または Aspose.PDF API を使用して文書レイアウト（余白や向き）をカスタマイズできます。

**Q: What happens if an image cannot be read?**  
A: OCR エンジンはそのページに対して空の `RecognitionResult` を返します。これを検出して、問題のあるファイルをスキップまたはログに記録できます。

**Q: Does the API support cloud deployment?**  
A: はい、ランタイムがバージョン要件を満たす限り、Azure Functions や AWS Lambda など、任意の .NET ランタイムで動作します。

## 結論

これで、**convert images to PDF C#**、検索可能なテキストの抽出、さらには画像バッチから Word、プレーンテキスト、Excel ファイルを生成する完全な本番対応ワークフローが手に入ります。さまざまな出力形式を試したり、特定言語向けに OCR 設定を調整したり、コードを大規模な文書処理パイプラインに統合したりして自由に活用してください。

---

**最終更新日:** 2026-04-29  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}