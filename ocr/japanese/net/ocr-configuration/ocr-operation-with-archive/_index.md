---
date: 2026-04-12
description: Aspose.OCR for .NET を使用してアーカイブ画像に OCR を実行し、ZIP ファイルからテキストを抽出する方法を、セットアップ、コード、トラブルシューティングを含めて学びましょう。
keywords:
- extract text from zip
- read images from zip
- Aspose OCR .NET
linktitle: .NET 用 Aspose.OCR を使用して ZIP アーカイブからテキストを抽出する方法
second_title: Aspose.OCR .NET API
title: Aspose.OCR for .NET を使用して ZIP アーカイブからテキストを抽出する方法
url: /ja/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR for .NET を使用して ZIP アーカイブからテキストを抽出する方法

## はじめに

## クイック回答
- **このチュートリアルの内容は何ですか？** Aspose.OCR for .NET を使用した ZIP アーカイブからのテキスト抽出。  
- **対象となる主要キーワードは何ですか？** *extract text from zip*。  
- **ライセンスは必要ですか？** 評価には無料トライアルで動作しますが、製品環境では商用ライセンスが必要です。  
- **サポートされている .NET バージョンは何ですか？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **認識設定をカスタマイズできますか？** はい。`RecognitionSettings` を使用して、言語や画像品質に合わせて精度を調整できます。

## OCR とは何か、そして ZIP アーカイブで使用する理由

光学文字認識（OCR）は、スキャン画像や PDF を検索可能で編集可能なテキストに変換します。これらの画像が ZIP ファイル内にまとめられている場合、1 回の処理で各画像を抽出して認識できるため、時間の節約とコードの複雑さの削減につながります。Aspose.OCR の `RecognizeMultipleImages` メソッドを使用すれば、**zip から画像を読み取り**、すぐにテキストコンテンツを取得できます。

## 前提条件

- Visual Studio 2019 以降（または任意の .NET 対応 IDE）。  
- .NET Framework 4.5 以上または .NET Core 3.1 以上がインストールされていること。  
- Aspose.OCR for .NET ライブラリへのアクセス（以下のダウンロードリンク）。  
- 本番利用のための有効な Aspose.OCR ライセンス（トライアル利用可能）。

## 名前空間のインポート

.NET プロジェクトで、Aspose.OCR が提供する機能にアクセスするために必要な名前空間をインポートします：

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Aspose.OCR for .NET のダウンロードとインストール

リリースページ **[here](https://releases.aspose.com/ocr/net/)** から最新パッケージを取得し、標準的な NuGet または手動インストール手順に従ってください。

## ライセンスの取得

**[purchase page](https://purchase.aspose.com/buy)** からライセンスを取得するか、**[free trial](https://releases.aspose.com/)** を試してください。ライセンスファイルをプロジェクトのルートに配置し、Aspose のドキュメントに記載された方法で実行時にロードします。

## 手順 1: ドキュメントディレクトリの設定

まず、ドキュメントディレクトリへのパスを初期化します。このフォルダーには処理対象の ZIP アーカイブを配置します：

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **プロのコツ:** クロスプラットフォームのパス処理には `Path.Combine` を使用してください。

## 手順 2: Aspose.OCR の初期化

OCR 操作を開始するために Aspose.OCR クラスのインスタンスを作成します：

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## 手順 3: ZIP アーカイブのパスを指定

読み取り対象の画像（画像が含まれる ZIP ファイル）へのフルパスを定義します：

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## 手順 4: ZIP 内の画像を認識

既定またはカスタム設定を使用して、指定したアーカイブに対して OCR 認識を実行します。この呼び出しは ZIP から各画像を自動的に抽出し、OCR を実行します：

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> 特定の言語、DPI、または手書き認識を有効にするために `RecognitionSettings` を調整して精度を向上させることができます。

## 手順 5: 抽出されたテキストを出力

結果をループし、アーカイブ内の各画像に対して認識されたテキストを出力します。ここが実際に **extract text from zip** を行う部分です：

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

出力は各画像インデックスと抽出された文字列を示し、実質的に **画像をテキストに変換** し、**アーカイブからテキストを抽出** する単一操作となります。

## このアプローチが重要な理由

- **バッチ処理:** 手動で抽出することなく、ZIP 内の任意の数の画像を処理します。  
- **パフォーマンス:** アーカイブから直接読み取ることで I/O オーバーヘッドを削減します。  
- **スケーラビリティ:** 大規模な ZIP ファイルでも動作し、非同期パターンと組み合わせて高スループットシナリオに対応できます。  

## よくある問題とトラブルシューティング

| 問題 | 原因 | 解決策 |
|------|------|--------|
| テキストが返されない | 画像品質が低すぎる | 画像を前処理（例: 二値化）するか、`RecognitionSettings.Dpi` を調整してください |
| ZIP 読み取り時の例外 | アーカイブパスが無効 | `fullPath` が有効な `.zip` ファイルを指し、アプリに読み取り権限があることを確認してください |
| ライセンスが適用されない | ライセンスファイルが欠如またはロードされていない | `AsposeOcr` インスタンスを作成する前に `License license = new License(); license.SetLicense("Aspose.OCR.lic");` を呼び出してください |

## よくある質問

**Q: Aspose.OCR for .NET をライセンスなしで使用できますか？**  
A: はい、評価用の無料トライアルは利用可能ですが、本番環境での展開にはライセンス版が必要です。

**Q: ライブラリはパスワード保護された ZIP アーカイブをサポートしていますか？**  
A: 現在、`RecognizeMultipleImages` は標準的な ZIP ファイルで動作します。暗号化されたアーカイブの場合は、サードパーティ製ライブラリで画像を先に抽出し、OCR エンジンに画像配列を渡してください。

**Q: 手書きテキストの精度を向上させるには？**  
A: `RecognitionSettings.EnableHandwritingRecognition` フラグを有効にし、より高い DPI 設定（例: 300）を提供してください。

**Q: 認識された各行の信頼度スコアを取得する方法はありますか？**  
A: 各 `RecognitionResult` には `Confidence` プロパティが含まれており、これをログに記録したり、低信頼度の結果をフィルタリングしたりできます。

## 追加リソース

- **Aspose.OCR フォーラム:** コミュニティサポートや高度なシナリオについては、[Aspose.OCR フォーラム](https://forum.aspose.com/c/ocr/16)をご覧ください。  
- **一時ライセンス:** 短期評価が必要な場合は、[temporary license](https://purchase.aspose.com/temporary-license/) をリクエストしてください。  
- **公式ドキュメント:** 最新の API 変更情報は、[documentation](https://reference.aspose.com/ocr/net/) を確認してください。

---

**最終更新日:** 2026-04-12  
**テスト環境:** Aspose.OCR 24.11 for .NET  
**作者:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}