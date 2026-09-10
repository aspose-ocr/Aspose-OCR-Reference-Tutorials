---
description: Aspose.OCR for .NET を使用して OCR 結果を保存する方法を学びましょう – 画像を PDF に変換し、PNG からテキストを抽出し、認識されたテキストを
  DOCX、TXT、PDF、または XLSX に保存します。
linktitle: How to Save OCR Result as Document
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

このチュートリアルでは、Aspose.OCR for .NET を使用して **OCR の保存方法** を学びます。画像内のテキストを認識し、そのテキストを DOCX、TXT、PDF、XLSX といった一般的なドキュメント形式に変換する手順を解説します。最後まで実施すれば、画像からデータを自動的に抽出し、検索可能で編集可能なファイルとして保存できるようになり、アーカイブ、レポート作成、または下流処理に最適です。

## クイック回答
- **“how to save ocr” は何を意味しますか？** 画像から認識されたテキストを DOCX、PDF などのファイル形式に保存することを指します。  
- **どのフォーマットにエクスポートできますか？** DOCX、TXT、PDF、XLSX が標準でサポートされています。  
- **ライセンスは必要ですか？** 評価には無料トライアルが利用でき、商用利用には商用ライセンスが必要です。  
- **画像を直接 PDF に変換できますか？** はい—OCR 結果を PDF として保存すれば、検索可能な PDF ドキュメントが得られます。  
- **PNG はサポートされていますか？** もちろんです。同じ API で **PNG からテキストを抽出** できます。  

## OCR とは何か、そして結果をドキュメントとして保存する理由

光学文字認識 (OCR) は、画像内の印刷文字や手書き文字を機械が読み取れる文字列に変換します。これらの文字列をドキュメントとして保存することで、以下が可能になります：

* コンプライアンスのために検索可能な PDF を作成する。  
* データ分析のためにスプレッドシート (XLSX) を作成する。  
* 編集可能なレポート (DOCX) を生成する。  
* 素早い検索のためにプレーンテキストログ (TXT) をアーカイブする。  

## 前提条件

始める前に、以下が揃っていることを確認してください：

- Aspose.OCR for .NET がインストールされていること。**[here](https://releases.aspose.com/ocr/net/)** からダウンロードできます。  
- ソース画像と出力ドキュメントを格納するフォルダーがマシン上にあること。コード内の `dataDir` 変数をこのフォルダーに合わせて更新してください。  

## 名前空間のインポート

.NET のファイル I/O と Aspose OCR クラスにアクセスするために、いくつかの名前空間が必要です。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### 手順 1: Aspose.OCR の初期化

作業ディレクトリへのパスを設定し、OCR エンジンのインスタンスを作成します。

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### 手順 2: 画像の認識

画像ファイル（例: PNG）を認識器に渡します。ここで **テキスト画像を認識** し、`RecognitionResult` に変換します。

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### 手順 3: 結果をさまざまな形式で保存

ここで認識したテキストをエクスポートします。ワークフローに合った形式を選択してください—**画像を PDF に変換**、**PNG からテキストを抽出**、またはスプレッドシートの生成などが可能です。

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

- **ファイルパス:** 常に絶対パスを使用するか、`dataDir` がパス区切り文字（`\\` または `/`）で終わっていることを確認してください。  
- **画像品質:** 高解像度の画像は精度を向上させます。より良い結果を得るために前処理（傾き補正、ノイズ除去）を検討してください。  
- **ライセンスモード:** 評価モードでは出力に透かしが入る場合があります。有効なライセンスを適用して透かしを除去してください。  

## よくある質問

**Q1. Aspose.OCR はさまざまな画像形式に対応していますか？**  
A1: はい、Aspose.OCR は幅広い画像形式をサポートしており、OCR タスクの柔軟性が確保されています。

**Q2. 精度向上のために認識設定をカスタマイズできますか？**  
A2: もちろんです！Aspose.OCR は `RecognitionSettings` を提供しており、特定の要件に合わせて OCR プロセスを微調整できます。

**Q3. 無料トライアルは利用できますか？**  
A3: はい、無料トライアルは **[here](https://releases.aspose.com/)** から開始できます。

**Q4. Aspose.OCR の一時ライセンスはどこで取得できますか？**  
A4: 一時ライセンスは **[here](https://purchase.aspose.com/temporary-license/)** から取得できます。

**Q5. サポートやコミュニティに参加したい場合はどこへ行けばよいですか？**  
A5: サポートやディスカッションのために **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** の Aspose.OCR コミュニティに参加してください。

---

**最終更新日:** 2026-02-12  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}