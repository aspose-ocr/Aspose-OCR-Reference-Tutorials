---
date: 2026-06-29
description: Aspose.OCR for .NET を使用して OCR 結果を保存する方法を学びます – OCR 出力の保存、画像を検索可能な PDF
  に変換、PNG からテキスト抽出、そして DOCX、TXT、PDF、または XLSX へのエクスポート方法をステップバイステップで解説します。
keywords:
- how to save ocr
- image to searchable pdf
- extract text from png
- create searchable pdf
- ocr result to txt
linktitle: OCR結果をドキュメントとして保存する方法
schemas:
- author: Aspose
  dateModified: '2026-06-29'
  description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  headline: How to Save OCR Result as Document
  type: TechArticle
- description: Learn how to save OCR results with Aspose.OCR for .NET – a step‑by‑step
    guide on how to save ocr output, convert image to searchable pdf, extract text
    from png, and export to DOCX, TXT, PDF, or XLSX.
  name: How to Save OCR Result as Document
  steps:
  - name: Initialize Aspose.OCR
    text: AsposeOcr is the primary class that performs OCR operations. Set the path
      to your working directory and create an instance of the OCR engine.
  - name: Recognize Image
    text: RecognitionResult holds the text and layout information extracted from the
      image. Pass the image file (e.g., a PNG) to the recognizer. This is where we
      **recognize text images** and turn them into a `RecognitionResult`.
  - name: Save Result in Different Formats
    text: Now we export the recognized text. Choose the format that fits your workflow—whether
      you need to **convert image to searchable pdf**, **extract text from png**,
      or generate a spreadsheet.
  - name: Display Success Message
    text: A simple console message confirms that the process completed without errors.
  type: HowTo
- questions:
  - answer: It refers to persisting the text recognized from an image into a file
      format like DOCX, PDF, etc.
    question: What does “how to save ocr” mean?
  - answer: DOCX, TXT, PDF, and XLSX are supported out‑of‑the‑box.
    question: Which formats can I export to?
  - answer: A free trial works for evaluation; a commercial license is required for
      production use.
    question: Do I need a license?
  - answer: Yes—save the OCR result as PDF to get a searchable PDF document.
    question: Can I convert image to PDF directly?
  - answer: Absolutely; you can **extract text from PNG** images with the same API.
    question: Is PNG supported?
  type: FAQPage
second_title: Aspose.OCR .NET API
title: OCR結果をドキュメントとして保存する方法
url: /ja/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR結果をドキュメントとして保存する方法

## はじめに

このチュートリアルでは、Aspose.OCR for .NET を使用して **OCR の保存方法** を学びます。画像内のテキストを認識し、そのテキストを DOCX、TXT、PDF、XLSX などの一般的なドキュメント形式に変換する手順を解説します。最後まで実施すれば、画像からデータを自動的に抽出し、検索可能で編集可能なファイルとして保存できるようになります。アーカイブ、レポート作成、または下流処理に最適です。

## クイック回答
- **“OCR の保存方法” は何を意味しますか？** 画像から認識されたテキストを DOCX、PDF などのファイル形式に保存することを指します。  
- **どの形式にエクスポートできますか？** DOCX、TXT、PDF、XLSX が標準でサポートされています。  
- **ライセンスは必要ですか？** 評価には無料トライアルが利用できますが、本番環境で使用するには商用ライセンスが必要です。  
- **画像を直接 PDF に変換できますか？** はい。OCR 結果を PDF として保存すれば、検索可能な PDF ドキュメントが得られます。  
- **PNG はサポートされていますか？** もちろんです。同じ API で **PNG からテキストを抽出** できます。

## OCRとは何か、そして結果をドキュメントとして保存する理由

OCR（Optical Character Recognition）は、画像内の印刷文字や手書き文字を機械が読み取れる文字列に変換します。これらの文字列をドキュメントとして保存することで、**検索可能な PDF** を作成したり、スプレッドシートにデータを入力したり、編集可能なレポートを生成したり、プレーンテキストのログをアーカイブしたりできます。Aspose.OCR を使用すれば、スキャンした画像を **検索可能な PDF** にワンステップで変換でき、別途 PDF 作成ツールを使用する必要がなくなります。

## 前提条件

開始する前に、以下が揃っていることを確認してください：

- .NET 用 Aspose.OCR がインストールされていること。**[here](https://releases.aspose.com/ocr/net/)** からダウンロードできます。  
- ソース画像と出力ドキュメントを格納するフォルダーがマシン上にあること。コード内の `dataDir` 変数をこのフォルダーのパスに更新してください。

## 名前空間のインポート

.NET のファイル I/O と Aspose OCR クラスにアクセスするために、いくつかの名前空間が必要です。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 手順 1: Aspose.OCR の初期化

AsposeOcr は OCR 処理を実行する主要クラスです。作業ディレクトリのパスを設定し、OCR エンジンのインスタンスを作成します。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 手順 2: 画像を認識する

RecognitionResult は画像から抽出されたテキストとレイアウト情報を保持します。画像ファイル（例: PNG）を認識器に渡します。ここで **テキスト画像を認識** し、`RecognitionResult` に変換します。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 手順 3: 結果をさまざまな形式で保存する

ここで認識されたテキストをエクスポートします。ワークフローに合わせた形式を選択してください—**画像を検索可能な PDF に変換** したり、**PNG からテキストを抽出** したり、スプレッドシートを生成したりできます。

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### 手順 4: 成功メッセージの表示

シンプルなコンソールメッセージで、エラーなく処理が完了したことを確認できます。

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## よくある落とし穴とヒント

- **ファイルパス:** 常に絶対パスを使用するか、`dataDir` がパス区切り文字（`\` または `/`）で終わっていることを確認してください。  
- **画像品質:** 解像度の高い画像は精度を向上させます。より良い結果を得るために、前処理（傾き補正、ノイズ除去）を検討してください。  
- **ライセンスモード:** 評価モードでは出力に透かしが入る場合があります。透かしを除去するには有効なライセンスを適用してください。

## よくある質問

**Q1. Aspose.OCR はさまざまな画像形式に対応していますか？**  
A1: はい、Aspose.OCR は PNG、JPEG、TIFF、BMP、GIF など 30 以上の画像形式をサポートしており、OCR タスクの柔軟性を確保します。

**Q2. 精度向上のために認識設定をカスタマイズできますか？**  
A2: もちろんです！Aspose.OCR は `RecognitionSettings` を提供しており、特定の要件に合わせて OCR プロセスを微調整できます。

**Q3. 無料トライアルは利用可能ですか？**  
A3: はい、無料トライアルは **[here](https://releases.aspose.com/)** から開始できます。

**Q4. Aspose.OCR の一時ライセンスはどこで取得できますか？**  
A4: 一時ライセンスは **[here](https://purchase.aspose.com/temporary-license/)** で取得できます。

**Q5. サポートやコミュニティとの交流はどこでできますか？**  
A5: サポートやディスカッションは **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** の Aspose.OCR コミュニティに参加してください。

---

**最終更新日:** 2026-06-29  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 関連チュートリアル

- [Aspose.OCR .NET を使用した画像からのテキスト抽出](/ocr/net/image-and-drawing-recognition/)
- [画像を PDF に変換 C# – マルチページ OCR 結果の保存](/ocr/net/ocr-optimization/save-multipage-result-as-document/)
- [テキスト画像抽出 – OCR 設定](/ocr/net/ocr-settings/)


{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}