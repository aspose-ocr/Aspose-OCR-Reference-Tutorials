---
category: general
date: 2026-02-14
description: JavaでAspose OCRを使用して画像の傾き補正と前処理を行う方法を学びましょう。精度を向上させ、フォームからテキストを抽出し、OCR結果を改善します。
draft: false
keywords:
- how to deskew image
- preprocess image for ocr
- extract text from form
- how to improve ocr
- process image with ocr
language: ja
og_description: Javaで画像の傾き補正とOCR用前処理をマスターしよう。このガイドでは、フォームからテキストを抽出し、OCR精度を向上させる方法を示します。
og_title: OCR用画像の傾き補正方法 – Java 前処理チュートリアル
tags:
- OCR
- Java
- Image Processing
title: OCR用画像の傾き補正方法 – 完全なJava前処理ガイド
url: /ja/java/advanced-ocr-techniques/how-to-deskew-image-for-ocr-complete-java-pre-processing-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 用画像のデスキュー方法 – 完全 Java 前処理ガイド

**画像をデスキュー（傾き補正）**して OCR エンジンに渡す方法を考えたことはありますか？ あなただけではありません。実務で扱うスキャンした請求書、手書きフォーム、古い新聞アーカイブなど、多くのプロジェクトで斜めにスキャンされた画像は認識精度を大きく低下させます。 良いニュースは、数行の Java コードと Aspose OCR ライブラリさえあれば、画像をまっすぐにし、ノイズを除去し、二値化して、OCR エンジンがプロのように読み取れるようにできることです。

このチュートリアルでは、スキャンしたフォームの読み込み、デスキューフィルタの適用、ノイズ除去、クリーンな白黒画像への変換、そして最終的なテキスト抽出という一連のパイプラインを順に解説します。最後まで読むと、**OCR の精度を向上させる方法**、**画像を OCR で処理する方法**を確実に理解でき、**フォームからテキストを抽出する**コードサンプルを数秒で実行できるようになります。

## 必要なもの

- **Java Development Kit (JDK) 8 以上** – 任意の最新 JDK でコンパイル可能です。
- **Aspose.OCR for Java** ライブラリ（執筆時点の最新バージョン 23.12）。Maven Central から取得するか、Aspose のサイトから JAR をダウンロードしてください。
- テスト用画像ファイル（例: `scanned_form.jpg`）。できれば少し傾いたスキャン文書が望ましいです。
- お好きな IDE（IntelliJ IDEA、Eclipse、VS Code など） – `main` メソッドを実行できる環境。

> **プロのコツ:** Maven を使用している場合は、以下の依存関係を `pom.xml` に追加してください。必要なすべてのトランジティブライブラリが自動的に取得されます。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version>
</dependency>
```

---

## Step 1 – OCR エンジンインスタンスの作成  

最初に行うのは `OcrEngine` のインスタンス化です。これは、後で画像上の文字を読み取る「脳」の役割を果たします。

```java
import com.aspose.ocr.*;

public class DeskewDemo {
    public static void main(String[] args) throws Exception {

        // Initialize the OCR engine – this object holds all settings.
        OcrEngine ocrEngine = new OcrEngine();
```

なぜこのステップが重要かというと、エンジンがなければ後で追加する前処理フィルタを適用する場所がありません。エンジンは言語パック、認識モデル、出力形式も管理します。

---

## Step 2 – クリーンしたい画像の読み込み  

次に、エンジンに対して補正したいファイルを指定します。`ImageStream.fromFile` はファイルをストリームに読み込み、Aspose が扱える形に変換します。

```java
        // Load the image (replace the path with your own file location)
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/scanned_form.jpg"));
```

画像が JAR 内のリソースフォルダにある場合は、代わりに `ImageStream.fromResource` を使用できます。重要なのは、エンジンが **ビットマップ** を受け取り操作できることです。

---

## Step 3 – 前処理フィルタを正しい順序で追加  

ここが本番です。3 つのフィルタをチェーンします。

1. **DeskewFilter** – 傾き角度を自動検出し、画像を水平に回転させます。
2. **NoiseRemovalFilter** – 低品質スキャンにしばしば見られる斑点や粒子を除去します。
3. **BinarizationFilter** – 画像を純粋な白黒に変換し、ほとんどの OCR エンジンが好む高コントラスト状態にします。

```java
        // Attach preprocessing filters: deskew → denoise → binarize
        ocrEngine.getEngineOptions()
                 .addPreprocessingFilter(new DeskewFilter())
                 .addPreprocessingFilter(new NoiseRemovalFilter())
                 .addPreprocessingFilter(new BinarizationFilter());
```

> **なぜこの順序か？** まずデスキューを行うことで、元のピクセルに対して回転が適用されます。回転後にクリーンアップすることで、新たなノイズの生成を防げます。最後に二値化することで、OCR に対して鮮明で高コントラストな画像を提供でき、**画像を OCR で処理する**際に最適です。

---

## Step 4 – 前処理済み画像で OCR を実行  

エンジンにテキストの読み取りを指示します。`process()` 呼び出しは、認識された文字列とオプションの信頼度スコアを含む `OcrResult` を返します。

```java
        // Perform OCR on the cleaned image
        OcrResult ocrResult = ocrEngine.process();

        // Print the extracted text to the console
        System.out.println("=== Recognized Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

すべてが正常に動作すれば、元のフォームにあった生の文字列が出力されます。これは **フォームからテキストを抽出する** ワークフローの核心であり、文字列を取得したらフィールドの解析、データベースへの投入、PDF 生成などが可能になります。

---

## Step 5 – 出力を確認しパラメータを調整  

軽度に傾いた請求書でデモを実行すれば、可読な出力が得られるはずです。ただし、以下のようなエッジケースもあります。

- **極端な角度 (>15°)** – `DeskewFilter` の許容範囲を `setAngleThreshold` で拡大する必要があります。
- **背景パターンが濃い** – 二値化前に `ContrastEnhancementFilter` を追加すると効果的です。
- **マルチページ PDF** – 各ページを画像に変換してからループ処理し、同じエンジンインスタンスを再利用します。

以下は 10 度回転したレシートのサンプルコンソール出力です。

```
=== Recognized Text ===
Date: 02/13/2026
Item          Qty   Price
Coffee        2     $4.00
Bagel         1     $2.50
Total                $6.50
```

元の傾きにも関わらず、テキスト行がきれいに揃っていることが確認できます。これが **画像をデスキューする** 正しい手順の威力です。

---

## よくある落とし穴と回避策  

| 問題 | 発生理由 | 対策 |
|------|----------|------|
| **デスキュー後にゴミが出る** | 画像が暗すぎてエッジ検出ができない | デスキュー前に `BrightnessContrastFilter` で明るさを上げる |
| **文字が抜ける** | 二値化閾値が強すぎる | 適応的閾値の `OtsuBinarizationFilter` を使用 |
| **大容量ファイルで処理が遅い** | フィルタがフル解像度ビットマップで動作している | 他のステップの前に `ResizeFilter`（例: 最大 1500 px）で縮小 |

---

## ボーナス: 前処理結果の可視化  

OCR 前にクリーンアップされた画像を確認したい場合は、以下のようにエクスポートできます。

```java
        // Save the pre‑processed image for inspection
        ocrEngine.getEngineOptions()
                 .getPreprocessedImage()
                 .save("cleaned_form.png");
```

![how to deskew image の例](https://example.com/cleaned_form.png "Aspose OCR を使用した画像デスキューの結果")

**alt テキスト** には主要キーワードが含まれており、SEO 要件とスクリーンリーダーへの配慮を満たしています。

---

## まとめ – 本チュートリアルで学んだこと  

- `DeskewFilter` を使った **画像のデスキュー** 方法
- 完全な **OCR 前処理チェーン**（デスキュー → デノイズ → 二値化）
- Aspose OCR で **フォームからテキストを抽出する** 正確なコード例
- **OCR の精度を向上させる** コツと、難しいケースへの対処法
- 本番環境でも使える **画像を OCR で処理する** 簡易メソッド

---

## 次のステップ  

単一ページの補正と読み取りができたら、スケールアップを検討してください。

1. **バッチ処理** – フォルダ内のスキャン画像をすべて同じパイプラインで処理する。
2. **フィールド抽出** – 正規表現や Apache PDFBox などのライブラリを使い、生テキストを構造化データにマッピングする。
3. **クラウドサービスとの連携** – クリーン画像を Azure Form Recognizer や Google Document AI に送信し、高度なレイアウト解析を実行する。

これらのトピックはすべて、しっかりとした **OCR 前処理** が土台となります。

---

### 最後に  

完璧な OCR 結果は単一のテクニックだけで得られるものではなく、体系的なワークフローが鍵です。**画像をデスキューする** 方法をマスターしたことで、最大の障壁を取り除きました。ここからは他のフィルタを試したり、閾値を微調整したりして、認識率の向上を実感できるでしょう。

実装中に問題が発生したり、さらなる改善アイデアがあればコメントで教えてください。コーディングを楽しみながら、スキャン画像が常に真っすぐになることを願っています！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}