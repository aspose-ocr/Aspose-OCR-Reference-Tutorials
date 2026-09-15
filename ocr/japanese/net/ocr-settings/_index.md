---
date: 2026-05-19
description: Aspose.OCR for .NET を使用して画像からテキストを抽出し、画像をドキュメントに変換し、アプリケーションでの OCR 精度を向上させる方法を学びます。
keywords:
- extract text from images
- convert image to document
- improve ocr accuracy
- ocr image to txt
- save ocr as pdf
linktitle: OCR 設定
second_title: Aspose.OCR .NET API
title: 画像からテキストを抽出 – Aspose.OCR の OCR 設定
url: /ja/net/ocr-settings/
weight: 26
---

{{< blocks/products/pf/main-wrap-class >}}  
{{< blocks/products/pf/main-container >}}  
{{< blocks/products/pf/tutorial-page-section >}}  

# 画像からテキストを抽出 – Aspose.OCR の OCR 設定  

## はじめに  

今日の急速に変化するデジタル社会において、**画像からテキストを抽出**は、請求書処理から検索可能なアーカイブまで、あらゆる場面で重要な機能です。Aspose.OCR for .NET は、任意の画像を編集可能なテキスト、PDF、DOCX、またはプレーンテキストファイルに変換できる強力で即使用可能なエンジンを提供します。本ガイドでは、最も一般的な OCR 設定を解説し、*なぜ*各設定が重要なのかを説明し、実際のシナリオでの適用方法を示すことで、アプリケーションの精度、速度、柔軟性を向上させる方法をご紹介します。  

## クイック回答  
- **“extract text from images” とは何ですか？** 画像ファイル内の文字を認識し、編集可能なテキストとして出力するプロセスです。  
- **.NET でこれを最もうまく処理できるライブラリはどれですか？** Aspose.OCR for .NET は業界トップクラスの精度と多言語サポートを提供します。  
- **OCR の結果を PDF や DOCX に変換できますか？** はい – “Save Result as Document” チュートリアルでは、単一の呼び出しで PDF、DOCX、または TXT にエクスポートする方法を示しています。  
- **大量バッチの OCR を高速化するにはどうすればよいですか？** スレッド数を増やす（“Set Threads Count” を参照）ことで並列認識を実行できます。  
- **ファインチューニングは可能ですか？** もちろんです – 閾値を設定し、許可文字のホワイトリスト、無視文字のブラックリストを指定し、言語パックをロードして最適な結果を得ることができます。  

## “extract text from images” とは何か？  

ピクセルパターンを解析し、二値化やノイズ除去などの前処理を適用した上で、学習済み言語モデルを使用して各グリフを認識することで、文字の視覚的表現を編集可能な Unicode テキストに変換します。生成された文字列は、アプリケーション内で保存、検索、インデックス付け、またはさらに処理することができます。  

## なぜ Aspose.OCR for .NET を使用するのか？  

Aspose.OCR ライブラリをロードすると、すぐに **50 以上の入力および出力フォーマット** のサポートが得られます – JPEG、PNG、BMP、TIFF、PDF から画像への変換などを含み、**500 MB** までのファイルをメモリを使い果たすことなく処理できます。エンジンはクリーンなスキャンで **最大 98 % の精度** を提供し、低コントラストやノイズの多い画像をほぼ完璧な結果に引き上げる組み込み前処理機能も備えています。  

## OCR 画像認識でドキュメントとして結果を保存  

`SaveResultAsDocument` は OCR の出力を直接ドキュメントファイルに保存します。  

`ocrEngine.SaveResultAsDocument(outputPath, SaveFormat.Pdf)` を呼び出すと、Aspose.OCR はテキストを選択可能なテキストレイヤーを持つ PDF に書き込み、追加の後処理なしで検索やコピー＆ペースト機能を実現します。  

## OCR 画像認識でスレッド数を設定  

スレッドプールを調整することで、同時に処理される画像ページ数を制御します。  

**定義:** `ThreadsCount` プロパティは、エンジンが生成する並列 OCR ワーカースレッドの最大数を決定します。  

この値をデフォルトの **1** から **4**（マルチコアサーバーではそれ以上）に増やすと、大量バッチで処理時間を **30‑70 %** 短縮でき、アプリケーション設定で指定したメモリ上限も遵守されます。  

## OCR 画像認識で閾値を設定  

閾値処理はグレースケール画像を白黒ビットマップに変換し、低コントラストのソースにとって重要です。  

**定義:** `Threshold` プロパティは二値化時に使用される輝度カットオフ（0‑255）を設定します。  

薄くなったスキャンの場合、閾値 **180** に設定すると、文字エッジがよりクリアになり、デフォルトの自動設定と比較して誤検出を最大 **15 %** 減少させることが多いです。  

## OCR 画像認識で許可文字を指定  

場合によっては、シリアル番号の数字など、文字のサブセットだけが必要になることがあります。  

**定義:** `AllowedCharacters` コレクションはホワイトリストとして機能し、指定した文字だけの認識に制限します。  

エンジンを `"0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZ"` に限定することで、句読点のノイズを除去し、英数字コードの精度を **20 %** 向上させることができます。  

## OCR 画像認識で無視文字を指定  

逆に、ノイズとして頻繁に現れる文字を無視したい場合があります。  

**定義:** `IgnoredCharacters` コレクションはブラックリストで、認識時に一致するシンボルを OCR エンジンが破棄するよう指示します。  

対象データに含まれない “#” や “$” などの一般的なアーティファクトを除去することで、特にスキャンしたフォームにおいて誤認識率が劇的に低下します。  

## OCR 画像認識で異なる言語を扱う  

Aspose.OCR には、ラテン文字からキリル文字、アラビア文字、アジア文字まで、**30 以上のスクリプト** 用の言語パックが同梱されています。  

**定義:** `Language` プロパティは文字形状解析を導く言語モデルを選択します。  

適切なパックをロード（例: `ocrEngine.Language = Language.French`）することで、エンジンがスクリプト固有のヒューリスティックを適用し、多言語文書の精度が **10‑25 %** 向上します。  

## OCR 設定チュートリアル  
### [OCR 画像認識でドキュメントとして結果を保存](./save-result-as-document/)  
Aspose.OCR for .NET の可能性を引き出します。画像内のテキストを簡単に認識し、結果をさまざまなドキュメント形式で保存できます。  
### [OCR 画像認識でスレッド数を設定](./set-threads-count/)  
.NET で OCR の効率を高めます。Aspose.OCR を使用してスレッド数を簡単に設定し、精度と速度を向上させます。  
### [OCR 画像認識で閾値を設定](./set-threshold-value/)  
堅牢な OCR ソリューションである Aspose.OCR for .NET を探求してください。カスタム閾値を簡単に設定し、アプリケーションのテキスト認識を強化します。  
### [OCR 画像認識で許可文字を指定](./specify-allowed-characters/)  
Aspose.OCR を使用した .NET で正確な OCR を実現します。画像からテキストを簡単に認識し、今すぐダウンロードして開発体験を変革しましょう。  
### [OCR 画像認識で無視文字を指定](./specify-ignored-characters/)  
Aspose.OCR for .NET の高度な OCR 機能を探求してください。効率的で正確、開発者に優しいです。  
### [OCR 画像認識で異なる言語を扱う](./working-with-different-languages/)  
Aspose.OCR for .NET で多言語 OCR の魔法を解き放ち、さまざまな言語でテキストを簡単に抽出します。  

## Aspose.OCR を使用した画像からテキスト抽出 – 共通設定概要  

OCR エンジンをロードし、目的の設定を構成して `Recognize` を呼び出す – これが **10 行未満のコード** で実現できる基本的なワークフローです。以下の共通設定を習得することで、プロジェクトの要件に応じて速度、精度、または多言語サポート向けにエンジンをカスタマイズできます。  

| 設定 | 目的 | 使用タイミング |
|---------|---------|-------------|
| **Save Result as Document** | OCR 出力を PDF/DOCX/TXT にエクスポート | 再利用可能で検索可能なドキュメントが必要なとき |
| **Threads Count** | 並列処理を制御 | 大量バッチやパフォーマンス重視のアプリ |
| **Threshold Value** | 画像の二値化を調整 | 低コントラストまたはノイズの多い画像 |
| **Allowed Characters** | 特定シンボルのホワイトリスト | ドメイン固有データ（例: シリアル番号） |
| **Ignored Characters** | 不要シンボルのブラックリスト | 句読点などのノイズ除去 |
| **Language Packs** | 多言語認識を有効化 | ラテン文字以外のスクリプトを含む文書 |

## よくある質問  

**Q: .NET Core プロジェクトで Aspose.OCR を使用できますか？**  
A: はい、Aspose.OCR for .NET は .NET Core、.NET 5+、および .NET 6+ を同一の API で完全にサポートしています。  

**Q: 低解像度画像で OCR の精度を向上させるには？**  
A: `Threshold` 値を上げ、適切な `Language` パックを有効にし、文字セットを制限するために `AllowedCharacters` を指定することを検討してください。  

**Q: PDF から直接テキストを抽出できますか？**  
A: Aspose.OCR は画像ファイルに特化していますが、まず Aspose.PDF を使用して PDF ページを画像に変換し、生成された画像に対して OCR を実行することが可能です。  

**Q: 本番環境で使用するにはどのライセンスが必要ですか？**  
A: デプロイには商用の Aspose.OCR ライセンスが必要です。評価用に 30 日間の無料トライアルが利用可能です。  

**Q: 処理できる画像のサイズに制限はありますか？**  
A: ライブラリは **500 MB** までの画像を問題なく処理できます。より大きなファイルの場合は、`ThreadsCount` を増やし、メモリ設定を調整してください。  

---  

**Last Updated:** 2026-05-19  
**Tested With:** Aspose.OCR 24.11 for .NET  
**Author:** Aspose  

{{< blocks/products/products-backtop-button >}}

## 関連チュートリアル

- [画像からテキスト抽出 – Aspose.OCR for .NET による OCR 最適化](/ocr/net/ocr-optimization/)
- [.NET で OCR 精度向上のためにスレッド数を設定](/ocr/net/ocr-settings/set-threads-count/)
- [複数言語で Aspose OCR を使用したテキスト画像認識](/ocr/net/ocr-settings/working-with-different-languages/)


{{< /blocks/products/pf/tutorial-page-section >}}  
{{< /blocks/products/pf/main-container >}}  
{{< /blocks/products/pf/main-wrap-class >}}