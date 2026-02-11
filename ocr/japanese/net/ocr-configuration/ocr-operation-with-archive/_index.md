---
date: 2025-12-19
description: Aspose.OCR for .NET を使用して、アーカイブ画像の OCR を実行し、画像をテキストに変換し、アーカイブファイルからテキストを抽出する方法を学びます。
linktitle: How to Perform OCR on Archive Images with Aspose.OCR for .NET
second_title: Aspose.OCR .NET API
title: .NET 用 Aspose.OCR でアーカイブ画像の OCR を実行する方法
url: /ja/net/ocr-configuration/ocr-operation-with-archive/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose.OCR for .NET を使用したアーカイブ画像の OCR 実行方法

## はじめに

この包括的なチュートリアルでは、Aspose.OCR ライブラリ for .NET を使用して、アーカイブされた画像ファイルに対して **OCR を実行する方法** を学びます。画像をテキストに変換したり、**アーカイブからテキストを抽出**したりする必要がある場合、以下のステップバイステップガイドが開発環境の設定から ZIP アーカイブ内の各画像の認識テキスト取得までをすべて案内します。

## クイックアンサー
- **このチュートリアルでカバーする内容は？** Aspose.OCR for .NET を使用したアーカイブ（ZIP）画像の OCR 実行。  
- **対象の主要キーワードは？** *how to perform ocr*。  
- **ライセンスは必要ですか？** 評価用の無料トライアルで動作しますが、本番環境では商用ライセンスが必要です。  
- **サポートされている .NET バージョンは？** .NET Framework 4.5 以上、.NET Core 3.1 以上、.NET 5/6 以上。  
- **認識設定はカスタマイズできますか？** はい、`RecognitionSettings` を使用して精度を調整できます。

## OCRとは何か、そしてアーカイブでOCRを使用する理由

光学文字認識（OCR）は、スキャン画像や PDF を検索可能で編集可能なテキストに変換します。画像がアーカイブ（例：ZIP ファイル）内にまとめられている場合、各画像を一括で抽出・認識することで時間を節約し、コードの複雑さも軽減できます。Aspose.OCR の `RecognizeMultipleImages` メソッドはこのプロセスをシンプルにします。

## 前提条件

- Visual Studio 2019 以降（または任意の .NET 対応 IDE）。  
- .NET Framework 4.5 以上 または .NET Core 3.1 以上 がインストール済み。  
- Aspose.OCR for .NET ライブラリへのアクセス（以下のダウンロードリンク参照）。  
- 本番利用向けの有効な Aspose.OCR ライセンス（トライアル利用可）。

## 名前空間のインポート

.NET プロジェクトで Aspose.OCR の機能にアクセスするために、必要な名前空間をインポートしてください。

```csharp
using System;
using System.Collections.Generic;
using System.Drawing;
using System.IO;
using Aspose.OCR;
```

## Aspose.OCR for .NETのダウンロードとインストール

最新パッケージはリリースページ **[here](https://releases.aspose.com/ocr/net/)** から取得し、標準の NuGet または手動インストール手順に従ってインストールしてください。

## ライセンスの取得

**[purchase page](https://purchase.aspose.com/buy)** からライセンスを取得するか、**[free trial](https://releases.aspose.com/)** を試してください。ライセンスファイルをプロジェクトのルートに配置し、Aspose のドキュメントに記載の方法で実行時にロードします。

## ステップ1：ドキュメントディレクトリの設定

ドキュメントディレクトリへのパスを初期化します。

```csharp
// ExStart:1
// The path to the documents directory.
string dataDir = "Your Document Directory";
// ExEnd:1
```

> **プロのヒント:** クロスプラットフォームのパス処理には `Path.Combine` を使用してください。

## ステップ 2: Aspose.OCR を初期化する

OCR 操作を開始するために Aspose.OCR クラスのインスタンスを作成します。

```csharp
// ExStart:3
AsposeOcr api = new AsposeOcr();
// ExEnd:3
```

## ステップ 3: 画像パスを指定する

読み取り対象のアーカイブ画像（画像が格納された ZIP ファイル）のフルパスを定義します。

```csharp
// ExStart:4
string fullPath = dataDir + "OCR.zip";
// ExEnd:4
```

## ステップ 4: 画像を認識する

デフォルトまたはカスタム設定で指定したアーカイブの OCR 認識を実行します。この呼び出しは ZIP から各画像を自動的に抽出し、OCR を実行します。

```csharp
// ExStart:5
RecognitionResult[] result = api.RecognizeMultipleImages(fullPath, new RecognitionSettings
{
   //default or custom settings
});
// ExEnd:5
```

> `RecognitionSettings` を調整して、特定の言語や画像品質に合わせた精度向上が可能です。

## ステップ 5: 結果を印刷する

結果をループし、アーカイブ内の各画像に対して認識されたテキストを出力します。

```csharp
// ExStart:6
for (int i = 0; i < result.Length; i++)
{
	 Console.WriteLine($"Image: {i}\n Result:\n {result[i].RecognitionText}");
}
// ExEnd:6
```

出力は各画像インデックスと抽出された文字列を示し、実質的に **画像をテキストに変換** し、**アーカイブからテキストを抽出** することができます。

## よくある問題とトラブルシューティング

| Issue（問題） | Cause（原因） | Solution（解決策） |
|---|---|---|
| No text returned（テキストが返らない） | Image quality too low（画像品質が低すぎる） | Pre‑process images（例：二値化）や `RecognitionSettings.Dpi` の調整を行う |
| Exception on ZIP reading（ZIP 読み取り時の例外） | Invalid archive path（無効なアーカイブパス） | `fullPath` が有効な `.zip` ファイルを指しているか、アプリに読み取り権限があるか確認 |
| License not applied（ライセンスが適用されていない） | License file missing or not loaded（ライセンスファイルが無い、またはロードされていない） | `License license = new License(); license.SetLicense("Aspose.OCR.lic");` を `AsposeOcr` インスタンス作成前に呼び出す |

## よくある質問

**Q: Aspose.OCR for .NET をライセンスなしで使用できますか？**  
A: 評価用の無料トライアルは利用可能ですが、本番環境でのデプロイにはライセンス版が必要です。

**Q: パスワード保護された ZIP アーカイブはサポートされていますか？**  
A: 現在、`RecognizeMultipleImages` は標準的な ZIP ファイルで動作します。暗号化されたアーカイブの場合は、サードパーティ製ライブラリで画像を先に抽出し、抽出した画像配列を OCR エンジンに渡してください。

**Q: 手書き文字の精度を向上させるには？**  
A: `RecognitionSettings.EnableHandwritingRecognition` フラグを有効にし、DPI 設定を高く（例：300）することで改善できます。

**Q: 各認識行の信頼度スコアを取得する方法はありますか？**  
A: 各 `RecognitionResult` には `Confidence` プロパティがあり、これをログに記録したり、低信頼度の結果をフィルタリングしたりできます。

## 結論

これで **アーカイブ画像の OCR を実行**し、**画像をテキストに変換**、**アーカイブからテキストを抽出**するための完全な本番対応ワークフローが完成しました。Aspose.OCR for .NET をアプリケーションに統合すれば、検索可能な文書リポジトリの構築や自動データ入力、バルク画像テキスト抽出が必要なシナリオに対応できます。

## 追加リソース

- **Aspose.OCR Forum:** コミュニティサポートや高度なシナリオについては、[Aspose.OCR forum](https://forum.aspose.com/c/ocr/16) をご覧ください。  
- **Temporary License:** 短期評価が必要な場合は、[temporary license](https://purchase.aspose.com/temporary-license/) をリクエストしてください。  
- **Official Documentation:** 最新の API 変更情報は、[documentation](https://reference.aspose.com/ocr/net/) を確認してください。

---

**Last Updated:** 2025-12-19  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}
