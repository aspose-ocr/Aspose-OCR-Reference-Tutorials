---
date: 2026-04-23
description: Aspose.OCR を使用して C# で画像を PDF に変換する方法、マルチページ OCR 結果をドキュメントとして保存する方法、そして画像からテキストを抽出する方法を学びましょう。
keywords:
- extract text from images
- batch image to pdf
- convert scanned images pdf
linktitle: 画像をPDFに変換 C# – 複数ページのOCR結果を保存
second_title: Aspose.OCR .NET API
title: 画像からテキストを抽出 – 画像をPDFに変換 C#
url: /ja/net/ocr-optimization/save-multipage-result-as-document/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – 画像を PDF に変換 C#

## はじめに

このチュートリアルでは、Aspose.OCR for .NET を使用して **画像からテキストを抽出** しながら **画像を PDF に変換 C#** する方法を学び、マルチページ OCR 結果をドキュメントとして保存します。アーカイブのために **画像をバッチで PDF に変換** が必要な場合や、コンプライアンスのために **スキャン画像を PDF に変換** が必要な場合、あるいは単に画像から検索可能なテキストを取得したい場合でも、明確な説明と実践的なヒント、ベストプラクティスの推奨とともに、すべての手順を順を追って解説します。

## クイック回答
- **このチュートリアルでカバーする内容は何ですか？** C# で Aspose.OCR を使用して、複数の画像を PDF/Docx/Txt/Xlsx に変換し、画像からテキストを抽出します。
- **サポートされている出力形式はどれですか？** Docx、Text、Pdf、Xlsx（PDF を直接出力することも可能です）。
- **ライセンスは必要ですか？** 評価には無料トライアルが利用できますが、本番環境では永続ライセンスが必要です。
- **.NET の対応バージョンは何ですか？** .NET Framework 4.5 以降、.NET Core 3.1 以降、.NET 5/6/7。
- **変換しながらテキストを抽出できますか？** はい—OCR 結果を使用して保存前にテキストを取得できます。

## 「画像からテキストを抽出」とは何か、そして PDF 変換と組み合わせる理由

画像からテキストを抽出するとは、OCR（光学文字認識）を使用して視覚的な文字を検索可能で編集可能な文字列に変換することを意味します。**画像を PDF に変換 C#** すると、これらの文字列が PDF に埋め込まれ、ドキュメントが検索可能かつインデックス可能になります—デジタルアーカイブやデータマイニングに最適です。

## このタスクに Aspose.OCR を使用する理由

- **多数の言語にわたる高精度**。  
- **マルチページ対応** – 1 回の呼び出しで画像バッチを処理できます（**画像をバッチで PDF に変換** シナリオに最適）。  
- **余分な変換ステップなしで、一般的な Office 形式へ直接保存**。  
- **完全な .NET 統合** – ネイティブ依存性がなく、Windows、Linux、クラウドランタイムで動作します。

## 前提条件

1. Aspose.OCR for .NET をインストールしましたか。ダウンロードは[here](https://releases.aspose.com/ocr/net/)から可能です。  
2. 無料トライアルまたは購入ライセンスを取得しましたか – トライアルは[here](https://releases.aspose.com/)、購入は[here](https://purchase.aspose.com/buy)から取得できます。  
3. 公式[documentation](https://reference.aspose.com/ocr/net/)を確認し、API の概要を把握してください。  
4. サポートフォーラム[support forums](https://forum.aspose.com/c/ocr/16)に参加し、問題解決の助けを得てください。  

すべての準備が整ったので、コーディングを始めましょう。

## 名前空間のインポート

C# ファイルに必要な名前空間を追加します：

```csharp
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using Aspose.OCR;
```

これらのインポートにより、コレクション、ファイル操作、LINQ、そして Aspose OCR クラスにアクセスできます。

## 手順 1: ドキュメントディレクトリの設定

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";
```

`"Your Document Directory"` を、ソース画像が存在する絶対パスまたは相対パス、そして出力ファイルを保存したい場所に置き換えてください。

## 手順 2: Aspose.OCR の初期化

```csharp
// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

`AsposeOcr` オブジェクトを作成すると、**画像を PDF に変換 C#** ワークフローを含むすべての OCR 操作にアクセスできます。

## 手順 3: 画像の認識

```csharp
// Recognize image
List<RecognitionResult> result = api.RecognizeMultipleImages(
    new List<string> { dataDir + "sample.png", dataDir + "sample_bad.png" },
    new RecognitionSettings { }
).ToList();
```

`RecognizeMultipleImages` メソッドはリスト内の各ファイルを処理し、`RecognitionResult` のコレクションを返します。任意の数の画像を入力でき、**スキャン画像を PDF に変換** シナリオに最適です。

## 手順 4: 好みの形式で結果を保存

```csharp
// Save the result in your preferred format
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR()+"sample.docx", SaveFormat.Docx, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf, result);
AsposeOcr.SaveMultipageDocument(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx, result);
```

下流のワークフローに最適な形式を選択してください：

- **Docx** – 検索可能なテキストを含む編集可能な Word ドキュメント。  
- **Text** – 迅速なデータマイニングのためのプレーンテキスト抽出（**画像からテキストを抽出**）。  
- **Pdf** – アーカイブに最適な従来の PDF 出力。  
- **Xlsx** – 表形式データのスプレッドシート表現。

## 一般的な使用例

- **デジタルアーカイブ:** スキャンした紙の契約書を検索可能な PDF に変換します。  
- **データ入力の自動化:** 領収書や請求書からテキストを抽出し、データベースに取り込みます。  
- **バッチ処理:** 最小限のコードで数千枚の画像を単一ジョブで処理し、**画像をバッチで PDF に変換** のニーズに最適です。

## トラブルシューティング &amp; ヒント

- **大量の画像セット:** メモリスパイクを防ぐために、画像を小さなバッチに分けて処理してください。  
- **画像品質:** OCR の精度を最大化するため、画像は最低でも 300 dpi にしてください。  
- **ライセンスエラー:** OCR メソッドを呼び出す前に、ライセンスファイルが正しくロードされていることを確認してください。  
- **空結果:** 読めないページに対して OCR エンジンは空の `RecognitionResult` を返します。`result[i].Text` が null または空文字列でないか確認し、適切に処理してください。

## よくある質問

**Q: OCR を使用せずに画像を PDF C# に変換できますか？**  
A: はい、Aspose.PDF や他のライブラリを使用して純粋な画像→PDF 変換が可能ですが、OCR を使用すると検索可能なテキストが追加されます。

**Q: 変換後に C# で画像からテキストを抽出するにはどうすればよいですか？**  
A: `RecognizeMultipleImages` が返す `result` リストには `Text` プロパティが含まれており、これを `.txt` ファイルに書き出すか、直接処理できます。

**Q: カスタムページ余白や向きを設定できますか？**  
A: PDF や Docx に保存する際、`SaveMultipageDocument` を呼び出す前に Aspose.Words または Aspose.PDF API を使用してドキュメントレイアウトを変更できます。

**Q: 画像が読めない場合はどうなりますか？**  
A: OCR エンジンはそのページに対して空の `RecognitionResult` を返します。`result[i].Text` が null または空文字列かどうかを確認し、適切に処理してください。

**Q: API はクラウド展開をサポートしていますか？**  
A: はい、ランタイムがバージョン要件を満たす限り、Azure Functions や AWS Lambda など、任意の .NET ランタイムで動作します。

**最終更新日:** 2026-04-23  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**著者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}