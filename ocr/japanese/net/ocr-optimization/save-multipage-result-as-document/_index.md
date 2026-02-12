---
date: 2025-12-30
description: Aspose.OCR を使用して C# で画像を PDF に変換し、マルチページ OCR 結果をドキュメントとして保存し、画像からテキストを抽出する方法を学びましょう。
linktitle: Convert Images to PDF C# – Save Multipage OCR Result
second_title: Aspose.OCR .NET API
title: 画像をPDFに変換 C# – 複数ページのOCR結果を保存
url: /ja/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像を PDF に変換 C# – マルチページ OCR 結果の保存

## はじめに

このチュートリアルでは、Aspose.OCR for .NET を使用して **画像を PDF C# に変換** し、生成されたマルチページ OCR 出力をドキュメントとして保存する方法を学びます。アーカイブ用に **スキャン画像を PDF に変換** したい場合や、データ処理のために **画像からテキストを抽出 C#** したい場合でも、本ガイドは実践的な例とベストプラクティスのヒントを交えて、すべての手順を丁寧に解説します。

## クイック回答
- **このチュートリアルで扱う内容は？** Aspose.OCR を使用した C# における画像の複数枚を PDF/Docx/Txt/Pdf/Xlsx に変換する方法。
- **対応フォーマットは？** Docx、Text、Pdf、Xlsx（PDF へ直接出力も可能）。
- **ライセンスは必要ですか？** 評価用の無料トライアルで動作しますが、本番環境では永続ライセンスが必要です。
- **対応 .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6/7。
- **変換時にテキスト抽出は可能ですか？** はい。OCR 結果を利用して保存前にテキストを取得できます。

## 「画像を PDF に変換 C#」とは？

C# で画像を PDF に変換するとは、1 枚または複数枚のビットマップファイル（PNG、JPEG、TIFF など）をプログラム上で取得し、視覚的レイアウトを保持しつつ、必要に応じて OCR による検索可能テキストを埋め込んだ PDF ドキュメントを生成することです。Aspose.OCR を使うと、このプロセスがシンプルかつ高度にカスタマイズ可能になります。

## なぜ Aspose.OCR を選ぶのか？

- **高精度** OCR エンジンで多数の言語に対応。
- **マルチページ対応** – 画像バッチを一括で処理可能。
- **直接保存** – 余分な変換ステップなしで一般的な Office フォーマットへ出力。
- **完全な .NET 統合** – ネイティブ依存や外部ツールが不要。

## 前提条件

作業を始める前に、以下を準備してください。

1. Aspose.OCR for .NET をインストールします。ダウンロードは [こちら](https://releases.aspose.com/ocr/net/)。
2. 無料トライアルまたは購入済みライセンスを取得します – トライアルは [こちら](https://releases.aspose.com/)、購入は [こちら](https://purchase.aspose.com/buy)。
3. 公式 [ドキュメント](https://reference.aspose.com/ocr/net/) を確認し、API の概要を把握します。
4. 問題が発生した際は [サポートフォーラム](https://forum.aspose.com/c/ocr/16) でコミュニティに参加してください。

準備が整ったら、コーディングを開始しましょう。

## 名前空間のインポート

C# ファイルに必要な名前空間を追加します。

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

これらのインポートにより、コレクション、ファイル操作、LINQ、そして Aspose OCR クラスへのアクセスが可能になります。

## 手順 1: ドキュメントディレクトリの設定

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` を、ソース画像が格納されている絶対パスまたは相対パス、そして出力ファイルを保存したい場所に置き換えてください。

## 手順 2: Aspose.OCR の初期化

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` オブジェクトを作成すると、**画像を PDF C# に変換** ワークフローを含むすべての OCR 操作にアクセスできます。

## 手順 3: 画像の認識

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` メソッドはリスト内の各ファイルを処理し、`RecognitionResult` のコレクションを返します。任意の枚数の画像を入力できるため、**スキャン画像を PDF に変換** するシナリオに最適です。

## 手順 4: 好みの形式で結果を保存

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

下記の形式から、次工程に最も適したものを選択してください。

- **Docx** – 検索可能テキスト付きの編集可能 Word 文書。
- **Text** – クイックなデータマイニング向けのプレーンテキスト抽出（**画像からテキストを抽出 C#**）。
- **Pdf** – アーカイブに最適な従来型 PDF 出力。
- **Xlsx** – 表形式データ用のスプレッドシート表現。

## 主なユースケース

- **デジタルアーカイブ:** スキャンした紙の契約書を検索可能 PDF に変換。
- **データ入力の自動化:** 領収書や請求書からテキストを抽出し、データベースに取り込む。
- **バッチ処理:** 数千枚の画像を最小限のコードで単一ジョブとして処理。

## トラブルシューティングとヒント

- **大量画像セット:** メモリ使用量の急増を防ぐため、画像を小さなバッチに分割して処理。
- **画像品質:** OCR 精度を最大化するには、最低でも 300 dpi を確保。
- **ライセンスエラー:** OCR メソッド呼び出し前に、ライセンスファイルが正しくロードされているか確認。

## 追加のよくある質問

**Q: OCR を使用せずに画像を PDF C# に変換できますか？**  
A: はい、Aspose.PDF や他のライブラリを使って純粋な画像→PDF 変換は可能ですが、OCR を利用すると検索可能テキストが付加されます。

**Q: 変換後に画像からテキストを抽出 C# するには？**  
A: `RecognizeMultipleImages` が返す `result` リストの各要素に `Text` プロパティがあり、これを `.txt` ファイルに書き出すか直接処理できます。

**Q: カスタムページ余白や向きを設定できますか？**  
A: PDF や Docx に保存する前に、Aspose.Words または Aspose.PDF API を使用してドキュメントレイアウトを変更できます。

**Q: 画像が読み取れなかった場合はどうなりますか？**  
A: そのページに対して OCR エンジンは空の `RecognitionResult` を返します。`result[i].Text` が null または空文字列かどうかを確認し、適切にハンドリングしてください。

**Q: API はクラウド展開に対応していますか？**  
A: はい、Azure Functions や AWS Lambda など、.NET ランタイムが要件を満たす環境であればどこでも動作します。

---

**最終更新日:** 2025-12-30  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}