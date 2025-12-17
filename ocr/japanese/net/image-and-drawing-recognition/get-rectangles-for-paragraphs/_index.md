---
date: 2025-12-17
description: .NET 用 Aspose.OCR を使用して OCR 画像から段落の矩形を抽出する方法を学びましょう – 矩形の抽出と段落座標の取得に関する決定版ガイドです。
linktitle: Get Rectangles for Paragraphs in OCR Image Recognition
second_title: Aspose.OCR .NET API
title: OCR画像認識における段落の矩形抽出方法
url: /ja/net/image-and-drawing-recognition/get-rectangles-for-paragraphs/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR画像認識で段落の矩形を抽出する方法

## はじめに

Aspose.OCR for .NET を使用した **段落の矩形を抽出する方法** に関する包括的なガイドへようこそ。ドキュメント処理パイプラインを強化し、段落の境界を取得してデータ抽出を自動化したい方に最適です。環境設定から矩形座標の出力まで、すべての手順を順を追って解説しますので、すぐに OCR 結果を活用できます。

## クイック回答
- **「矩形を抽出する」とは何ですか？** 検出されたテキスト領域のバウンディングボックス (x, y, width, height) を返します。  
- **どの API メソッドが矩形を提供しますか？** `AsposeOcr.GetRectangles` と `AreasType.PARAGRAPHS` を使用します。  
- **開発時にライセンスは必要ですか？** テスト用の無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **複数画像を一度に処理できますか？** はい。画像リストをループし、各ファイルに対して `GetRectangles` を呼び出します。  
- **対応フォーマットは何ですか？** PNG、JPEG、TIFF、BMP など多数。

## OCR で「矩形を抽出する」とは？
OCR 用語で矩形を抽出するとは、画像内の各段落または行を囲む幾何学的境界を特定することです。これらの座標を使って、スキャンした文書の特定部分をハイライト、切り抜き、あるいはさらに分析できます。

## なぜ段落座標を抽出するのか？
- **正確な後処理** – 各矩形を下流のワークフロー（例: 翻訳、マスク処理）に渡すことができます。  
- **UI/UX の向上** – 元画像上にバウンディングボックスをオーバーレイして、テキストが検出された場所をユーザーに示せます。  
- **バッチ自動化** – 大量の文書セットで段落を素早く検出・分離できます。

## 前提条件

- C# と .NET 開発の基本知識。  
- Aspose.OCR for .NET がインストールされた開発環境 – ダウンロードは [here](https://releases.aspose.com/ocr/net/) から。  
- 画像処理の概念と、スキャンファイルからテキストを抽出する際の OCR の重要性に関する基本的な理解。

## 名前空間のインポート

C# ファイルで必要な名前空間をインポートし、OCR クラスを利用できるようにします:

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## 手順 1: ドキュメントディレクトリの設定

解析対象の画像が格納されているフォルダーを定義します:

```csharp
string dataDir = "Your Document Directory";
```

## 手順 2: AsposeOcr インスタンスの初期化

`AsposeOcr` オブジェクトを作成します – これによりすべての OCR 機能にアクセスできます:

```csharp
AsposeOcr api = new AsposeOcr();
```

## 手順 3: 画像パスの指定

処理したい画像ファイルへの正確なパスを指定します:

```csharp
string fullPath = dataDir + "sample.png";
```

## 手順 4: 画像を認識し段落矩形を取得

`GetRectangles` メソッドを呼び出します。`detect_areas` を `true` に設定すると、エンジンは **段落** の矩形を返します:

```csharp
List<Rectangle> rectangles = api.GetRectangles(fullPath, AreasType.PARAGRAPHS, true);
```

## 手順 5: 結果の出力

検出された **段落座標** を表示し、抽出結果を確認します:

```csharp
Console.WriteLine("Areas coordinates:");
rectangles.ForEach(a => Console.WriteLine($"x:{a.X} y:{a.Y} width:{a.Width} height:{a.Height}"));
```

## よくある問題と解決策

| 問題 | 原因 | 対策 |
|------|------|------|
| 矩形が返ってこない | 画像品質が低い、または `AreasType` が誤っている | 画像が鮮明であることを確認し、`AreasType.PARAGRAPHS` を使用してください。 |
| 座標が 1 ピクセルずれる | DPI スケーリングの不一致 | 画像読み込み時に正しい DPI を設定するか、`api.Config.Dpi` を使用してください。 |
| ライセンス例外 | 本番環境で有効なライセンスがない | `api.SetLicense` で一時的または永続的なライセンスを適用してください。 |

## FAQ

**Q: Aspose.OCR はさまざまな画像フォーマットに対応していますか？**  
A: はい、PNG、JPEG、TIFF、BMP など多数の一般的なフォーマットをサポートしています。

**Q: 複数画像のバッチ処理は可能ですか？**  
A: もちろんです。ファイルパスのコレクションをループし、各画像に対して `GetRectangles` を呼び出してください。

**Q: Aspose.OCR for .NET の無料トライアルはありますか？**  
A: はい、無料トライアルは [here](https://releases.aspose.com/) から入手できます。

**Q: Aspose.OCR の一時ライセンスはどこで取得できますか？**  
A: 一時ライセンスは [here](https://purchase.aspose.com/temporary-license/) から取得できます。

**Q: Aspose.OCR に関する追加サポートやディスカッションはどこで行えますか？**  
A: コミュニティサポートやディスカッションは [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) でご利用ください。

## 結論

本チュートリアルでは、Aspose.OCR for .NET を使用して段落の **矩形を抽出する方法** を示し、各コードスニペットを解説し、返される座標の解釈方法を説明しました。これらの手順をアプリケーションに組み込むことで、段落境界を確実に取得し、文書ワークフローを強化し、よりスマートな OCR 主導のソリューションを構築できます。

---

**最終更新日:** 2025-12-17  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}