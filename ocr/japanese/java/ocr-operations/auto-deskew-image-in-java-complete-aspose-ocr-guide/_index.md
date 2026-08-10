---
category: general
date: 2026-06-19
description: JavaでAspose OCRを使用して画像を自動的にデスキューします。数ステップで傾きを補正し、OCRでテキストを抽出し、デスキュー角度を取得する方法を学びましょう。
draft: false
keywords:
- auto deskew image
- extract text ocr
- how to correct skew
- how to get deskew
language: ja
og_description: JavaでAspose OCRを使用した画像の自動デスケュー。傾きを補正し、テキストをOCRで抽出し、デスケュー角度を取得する方法をすべて一つのガイドで紹介します。
og_title: Javaで画像の自動傾き補正 – 完全なAspose OCRチュートリアル
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: Auto deskew image using Aspose OCR in Java. Learn how to correct skew,
    extract text OCR and get deskew angle in a few easy steps.
  headline: Auto Deskew Image in Java – Complete Aspose OCR Guide
  type: TechArticle
tags:
- Aspose OCR
- Java
- Image Processing
title: Javaで画像の自動傾き補正 – 完全なAspose OCRガイド
url: /ja/java/ocr-operations/auto-deskew-image-in-java-complete-aspose-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Javaで画像の自動デスケュー – 完全な Aspose OCR ガイド

OCR を実行する前に画像を **自動デスケュー** したいことはありませんか？たとえば、斜めのテーブルの上でレシートを撮影したり、スキャンしたフォームが微妙に傾いていてテキスト抽出が乱れてしまうことがあります。これは、下流処理で信頼できる **extract text OCR** 結果が必要なときに特に悩ましいポイントです。

このチュートリアルでは、Aspose OCR for Java を使用して **画像を自動デスケュー** する手順を詳しく解説し、**傾きの補正方法** とエンジンが完了した後に **デスケュー情報の取得方法** を示します。最後まで読めば、画像を自動で水平にし、きれいなテキストを抽出できる Java プログラムがすぐに実行可能になります。余計な説明は省き、実用的なコードと解説だけを提供します。

## 学べること

- Java プロジェクトで Aspose OCR をロードし、ライセンスを設定する方法  
- エンジンの自動デスケュー機能を有効にする方法  
- 過度な補正を防ぐための信頼度閾値の設定方法  
- 傾いた画像で OCR を実行し、適用されたデスケュー角度を取得する方法  
- 信頼度に基づく結果で認識テキストを抽出する方法  

**前提条件** – Java 8+ SDK、依存関係管理のための Maven または Gradle、そして Aspose OCR のライセンスファイル。Maven が初めてでも心配はいりません。必要最小限の `pom.xml` スニペットを後ほど紹介します。

---

## ## Aspose OCR で画像の自動デスケュー – 手順 1: プロジェクトのセットアップ

まずはライブラリをプロジェクトに追加します。`pom.xml`（または同等の Gradle エントリ）に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check for the latest version -->
</dependency>
```

> **プロのコツ:** バージョン番号に注意してください。Aspose はデスケューアルゴリズムのパフォーマンス向上を頻繁にリリースしています。

Maven がアーティファクトを解決したら、`SkewDemo` というシンプルな Java クラスを作成します。ここが **傾きの補正方法** と **デスケュー情報の取得方法** を実演するプレイグラウンドになります。

---

## ## 傾きの補正方法 – 手順 2: ライセンスとエンジンの初期化

OCR メソッドを呼び出す前に必ずライセンスをロードしてください。ライセンスがないと評価モードで動作し、処理できるページ数が制限されます。

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // Load the Aspose OCR license (replace with your actual path)
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

ライセンス設定がコードの先頭に分離されていることに注目してください。これは、ライセンス取得が画像ごとに繰り返すべきでない「一度だけ」の設定であるというベストプラクティスに沿っています。これを忘れると、エンジンはライセンス例外をスローし、初心者がよく遭遇する障壁となります。

---

## ## デスケュー情報の取得 – 手順 3: 自動デスケューの有効化と信頼度設定

次に OCR エンジンをインスタンス化し、**画像を自動デスケュー** するよう指示します。`setAutoDeskew(true)` 呼び出しにより、回転角度を検出してビットマップを水平基準に戻す内部アルゴリズムが有効になります。

```java
        // Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // Enable automatic deskewing
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        // Define how confident the engine must be before applying the correction
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // 85% confidence is a safe default
```

なぜ信頼度閾値が必要かというと、たとえば看板の写真を奇妙な角度で撮った場合、エンジンが大きな回転を推測してテキストを台無しにしてしまう可能性があるからです。`0.85` を設定することで「少なくとも 85 % の確信があるときだけデスケューを適用する」ことを指示しています。画像のノイズ具合に応じて、この値は上下に調整可能です。

---

## ## OCR でテキスト抽出 – 手順 4: 画像の認識

エンジンの準備ができたら、傾いた画像へのパスを渡します。`recognizeImage` メソッドは、デスケュー（有効な場合）と OCR を同時に実行します。

```java
        // Recognize text from a skewed image
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg");
```

ファイルが見つからない場合、Java は `FileNotFoundException` をスローします。簡単な確認として、パスが絶対パスか、プログラムを起動した作業ディレクトリからの相対パスであることを確認してください。

---

## ## 画像の自動デスケュー – 手順 5: デスケュー角度と抽出テキストの取得

認識が完了すると、`OcrResult` オブジェクトから 2 つの重要情報が得られます: エンジンが適用した角度とプレーンテキスト出力です。

```java
        // Print the applied deskew angle
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());

        // Print the extracted text
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

`getAppliedDeskewAngle()` メソッドは、度数で表された `double` を返します（時計回りは正）。画像がすでに水平であれば `0.0` が返ります。これが **デスケュー情報の取得方法** の核心で、監査ログに記録したり、UI に補正結果を表示したりする際に活用できます。

---

## ## 完全動作サンプル – すべての手順を 1 ファイルにまとめた例

以下は実行可能な完全版 Java クラスです。IDE に貼り付け、ライセンスと画像パスを自分の環境に合わせて置き換え、*Run* をクリックしてください。

```java
import com.aspose.ocr.*;

public class SkewDemo {
    public static void main(String[] args) throws Exception {
        // -------------------- Step 1: License --------------------
        License license = new License();
        license.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic"); // <-- update path

        // -------------------- Step 2: Engine --------------------
        OcrEngine ocrEngine = new OcrEngine();

        // -------------------- Step 3: Auto‑Deskew --------------------
        ocrEngine.setAutoDeskew(true);                     // auto deskew image
        ocrEngine.setDeskewConfidenceThreshold(0.85);     // high‑confidence only

        // -------------------- Step 4: Recognize --------------------
        OcrResult ocrResult = ocrEngine.recognizeImage("YOUR_DIRECTORY/angled-photo.jpg"); // <-- update path

        // -------------------- Step 5: Results --------------------
        System.out.println("Applied angle: " + ocrResult.getAppliedDeskewAngle());
        System.out.println("Extracted text:");
        System.out.println(ocrResult.getText());
    }
}
```

**期待される出力**（例）:

```
Applied angle: -2.7
Extracted text:
Invoice #12345
Date: 2024‑04‑01
Total: $89.99
Thank you for your business!
```

角度が小さな負の数になっていることに注目してください。これは元の写真が数度だけ左回りに傾いており、Aspose が OCR 前に補正したことを示しています。

---

## ## よくある落とし穴とエッジケース

| 問題 | 発生理由 | 対策 |
|-------|----------------|-----|
| **デスケューが適用されない（角度 = 0）** | 画像がすでに水平、または信頼度が閾値未満 | ノイズが多いスキャンの場合は `setDeskewConfidenceThreshold` を `0.6` に下げる |
| **出力にゴミ文字が混入** | 画像品質が低く、ノイズがデスケューと OCR の両方を妨げる | 平滑化フィルタで前処理するか、DPI を上げてから Aspose に渡す |
| **ライセンスが見つからない** | パスが間違っている、またはファイルが欠如 | 絶対パスを使用するか、`.lic` ファイルをクラスパスに配置し `license.setLicense("Aspose.OCR.lic");` を呼び出す |
| **大量バッチでメモリ不足** | 各呼び出しが画像全体をメモリに読み込むため | `OcrEngine` インスタンスを再利用し、各画像処理後に `ocrEngine.clear()` を呼ぶ |

---

## ## さらに踏み込む – 次のステップ

- **バッチ処理:** ディレクトリ内の画像をループし、各 `appliedDeskewAngle` を収集して CSV に保存し、分析に活用  
- **言語選択:** `ocrEngine.setLanguage(OcrLanguage.English);` で多言語ドキュメントの精度を向上  
- **領域限定 OCR:** 特定エリア（例: バーコード）のみが必要な場合は `ocrEngine.recognizeRegion(rect);` を使用  

これらの拡張も、**画像の自動デスケュー** を土台にすれば、正しく向けられたビットマップが高品質 OCR の最重要要素であることを活かせます。

---

## ## 結論

Java で Aspose OCR を使い **画像を自動デスケュー** するために必要なすべての手順を網羅し、**傾きの補正方法**、**デスケュー角度の取得方法**、そして **extract text OCR** によるクリーンテキスト抽出を実演しました。短く自己完結したプログラムは数秒で実行でき、別途画像処理ライブラリを導入する必要があるような面倒な問題を解決します。

自分の写真で試し、信頼度閾値を調整し、コンソールにデスケュー角度が表示されるのを確認してください。慣れたらバッチロジックを組み込んだり、ドキュメント管理パイプラインに統合したりしてみましょう。画像が正しく水平になることが、信頼できる OCR の秘訣です。

問題があればコメントを残すか、Aspose の公式 Java ドキュメントで最新 API の変更点をチェックしてください。コーディングを楽しみ、スキャンが常に水平であることを願っています！

![Diagram illustrating automatic deskew of a tilted image before OCR extraction – auto deskew image process](auto-deskew-diagram.png "auto deskew image workflow")


## 次に学ぶべきこと


以下のチュートリアルは、本ガイドで示したテクニックを応用した関連トピックを取り上げています。各リソースには、ステップバイステップの解説と完全なコード例が含まれており、API の追加機能を習得したり、独自の実装アプローチを探求したりするのに役立ちます。

- [How to calculate skew angle java using Aspose.OCR](/ocr/english/java/ocr-basics/calculate-skew-angle/)
- [recognize text image with Aspose OCR – Full Java OCR Tutorial](/ocr/english/java/ocr-operations/recognize-text-image-with-aspose-ocr-full-java-ocr-tutorial/)
- [Extract Text from Image Java with Aspose.OCR Detect Areas Mode](/ocr/english/java/ocr-operations/perform-ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}