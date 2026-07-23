---
date: 2026-02-22
description: Aspose.OCR for .NET を使用して画像からテキストを抽出し、PNG をテキストに変換し、C# アプリケーションで OCR
  の精度を向上させる方法を学びましょう。
linktitle: Extract Text from Image – Recognize Line with Aspose.OCR
second_title: Aspose.OCR .NET API
title: 画像からテキストを抽出 – Aspose.OCRで行を認識
url: /ja/net/image-and-drawing-recognition/recognize-line/
weight: 14
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出 – Aspose.OCRで行を認識

## はじめに

Optical character recognition (OCR) は、テキストの画像を検索可能で編集可能なコンテンツに変換するための定番ソリューションとなっています。画像ファイルから **extract text from image** を迅速かつ確実に行いたい場合、Aspose.OCR for .NET は、フル .NET Framework と **ASP OCR .NET Core** プロジェクトの両方で動作する強力で開発者に優しい API を提供します。このチュートリアルでは、画像内の行を認識し、テキストに変換し、結果を表示するまでの手順を、シンプルで分かりやすい C# コードとともに解説します。

## Quick Answers
- **Aspose.OCRは何をしますか？** 画像形式から印刷されたテキストまたは手書きテキストを読み取り、プレーン文字列として返します。  
- **対応している画像形式は？** PNG、JPEG、BMP、GIF、TIFF など。  
- **テストにライセンスは必要ですか？** 開発には無料トライアルで動作しますが、本番環境ではライセンスが必要です。  
- **.NET Coreで実行できますか？** はい – ライブラリは .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 をサポートしています。  
- **シンプルな行認識にかかる時間は？** 標準的な PNG で通常 1 秒未満です。

## “画像からテキストを抽出” とは？

画像からテキストを抽出するとは、OCR 技術を用いてビジュアルピクセルを解析し、文字を識別して機械可読なテキストとして出力することを指します。これにより、スキャンした文書のデジタル化、レシートからのデータ入力自動化、検索可能なアーカイブの構築などが可能になります。

## .NET 用 Aspose.OCR を使用する理由

- **高精度**：複数の言語とフォントに対応。  
- **外部依存なし** – 純粋なマネージドコードで、統合が簡単です。  
- **包括的なフォーマットサポート** – PNG、JPEG、BMP などに対応。  
- **シンプルな API** – 数行のコードで画像からテキストへ変換できます。  

### これが **PNG をテキストに変換** するのに役立つ理由

Aspose.OCR は PNG ファイルを直接読み取れるため、スキャンした PNG 画像を `RecognizeLine` メソッドに渡すだけで、途中の変換ステップなしにクリーンな文字列を取得できます。

## 前提条件

- **開発環境** – Visual Studio 2022（または好みの .NET IDE）。  
- **Aspose.OCR for .NET** – [download link](https://releases.aspose.com/ocr/net/) からダウンロードしてください。  
- **ドキュメントディレクトリ** – マシン上のフォルダで、サンプル画像（`sample_line.png`）が保存されている場所です。コード内の “Your Document Directory” を実際のパスに置き換えてください。

## 名前空間のインポート

.NET では、名前空間を使用して必要なクラスにアクセスします。C# ファイルの先頭に以下の using 文を追加してください。

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

## Aspose.OCR を使用して画像からテキストを抽出する方法

以下にステップバイステップの実装例を示します。各コードブロックは元のチュートリアルと同一で、ロジックはそのままです。

### 手順 1: Aspose.OCR の初期化

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
// ExEnd:1
```

> **プロのコツ:** 絶対パスまたは `Path.Combine` を使用して、OS 間のパス区切り問題を回避してください。

### 手順 2: 画像の行を認識する

```csharp
// ExStart:3
// Recognize image
string result = api.RecognizeLine(dataDir + "sample_line.png");
// ExEnd:3
```

`RecognizeLine` メソッドは単一行のテキストに焦点を当てるため、画像のレイアウトが分かっている場合に最適です。ドキュメントに重要なデータが1行だけ含まれているときの **read scanned image text** にも有効です。

### 手順 3: 認識されたテキストの表示

```csharp
// ExStart:4
// Display the recognized text
Console.WriteLine(result);
// ExEnd:4
```

プログラムを実行すると、抽出された行がコンソールに出力され、**extract text from image** 操作が成功したことが確認できます。

### 手順 4: 完了メッセージ

```csharp
Console.WriteLine("RecognizeLine executed successfully");
```

このメッセージが表示されれば、OCR プロセスがエラーなく完了したことを意味します。

## Aspose.OCR で OCR 精度を向上させる方法

- **高解像度画像を使用**（300 dpi 以上）。  
- **画像前処理を適用** 例: `api.PreprocessImage` を使用した二値化やノイズ除去。  
- **正しい言語を選択** `api.Language = OcrLanguage.English;`（または適切な言語列挙体）を使用。  
- **余分な背景を除去** ために境界をトリミング。

## よくある問題と解決策

| 問題 | 原因 | 対策 |
|-------|--------|-----|
| `FileNotFoundException` | `dataDir` パスが間違っている | フォルダパスを確認し、`sample_line.png` が存在することを確認してください。 |
| 精度が低い | 低解像度画像 | 高解像度の画像を使用するか、画像を前処理（例: 二値化）してください。 |
| 未対応フォーマット | 画像がサポートリストにない | `RecognizeLine` を呼び出す前に画像を PNG または JPEG に変換してください。 |

## よくある質問

### Q1: Aspose.OCR はすべての画像形式に対応していますか？

A1: Aspose.OCR は PNG、JPEG、GIF、BMP など幅広い画像形式をサポートしています。詳細な一覧は [documentation](https://reference.aspose.com/ocr/net/) を参照してください。

### Q2: トライアル期間中に商用プロジェクトで Aspose.OCR を使用できますか？

A2: はい、トライアル期間中に商用プロジェクトで Aspose.OCR の機能を検証できます。長期利用の場合は、[purchasing a license](https://purchase.aspose.com/buy) の取得をご検討ください。

### Q3: Aspose.OCR コミュニティへの支援や貢献はどうすればよいですか？

A3: 支援やコラボレーションは、[support forum](https://forum.aspose.com/c/ocr/16) で活発に行われています。質問や提案を投稿してください。

### Q4: Aspose.OCR の一時ライセンスは利用可能ですか？

A4: はい、機能評価用の一時ライセンスを取得できます。詳細は [here](https://purchase.aspose.com/temporary-license/) をご覧ください。

### Q5: Aspose.OCR for .NET のシステム要件は何ですか？

A5: 包括的なシステム要件は [documentation](https://reference.aspose.com/ocr/net/) に記載されています。

## 結論

これらの手順に従うことで、Aspose.OCR for .NET を使用して画像ファイルから **extract text from image** を実現し、個々の行を認識できるようになりました。この機能により、データキャプチャの自動化、検索可能なアーカイブの構築、任意の .NET アプリケーションへの OCR 統合が容易になります。フルフレームワークでも **ASP OCR .NET Core** でも、同様に活用できます。

---

**最終更新日:** 2026-02-22  
**テスト環境:** Aspose.OCR 24.12 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}