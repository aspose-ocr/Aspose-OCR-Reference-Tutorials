---
category: general
date: 2026-02-14
description: JavaでAspose OCRを使用して画像からテキストを抽出します。正確な結果を得るために、関心領域を指定したフォームフィールドからテキストを抽出する方法を学びましょう。
draft: false
keywords:
- extract text from image
- extract text from form
language: ja
og_description: JavaでAspose OCRを使用して画像からテキストを抽出します。このチュートリアルでは、関心領域を利用してフォームフィールドからテキストを抽出する方法を示します。
og_title: Aspose OCRで画像からテキストを抽出 – Javaガイド
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Aspose OCRで画像からテキストを抽出する – Javaガイド
url: /ja/java/advanced-ocr-techniques/extract-text-from-image-with-aspose-ocr-java-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 画像からテキストを抽出する Aspose OCR – Java ガイド

画像からテキストを抽出する必要があったことはありませんか？しかし、**extract text from image** を行う代わりに画像全体を解析してしまい、CPUサイクルを無駄にし、ノイズの多い結果になってしまったことはありませんか？あなただけではありません。実際のアプリでは、たとえば請求書スキャナ、パスポートリーダー、データ入力フォームなど、全体のキャンバスではなく、ほんの数個のフィールドだけが重要です。

良いニュースは、Aspose OCR が **extract text from image** と、ポリゴンを定義することで特定のフォーム領域からも抽出できることです。このチュートリアルでは、Java を使って **extract text from form** フィールドを正確に抽出する方法、なぜこのアプローチが重要か、問題が発生したときに何を調整すべきかを説明します。

以下では、ライブラリの設定からトリッキーなエッジケースの処理までをすべてカバーします。最後まで読めば、必要なデータだけを取得する実行可能なスニペットが手に入ります。

## 必要なもの

- Java 17（または最近の JDK）– 新しいバージョンは Unicode のサポートが向上しています。  
- Aspose.OCR for Java 23.10（または執筆時点での最新バージョン）。  
- 明確に定義されたフィールドを含むサンプル画像 `form.png`。  
- IDE またはシンプルなテキストエディタ—IntelliJ IDEA、VS Code、または Notepad でも構いません。

コアデモでは Maven/Gradle の設定は不要です。Aspose OCR の JAR をクラスパスに追加するだけです。

---

## ステップ 1 – OCR エンジンの初期化と画像のロード

エンジンが最初に必要とするのは処理対象のビットマップです。ソースファイルと同じフォルダーにある `form.png` を指定します。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Create the OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // Load the source image – replace the path if your file lives elsewhere
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));
```

*Why this matters:*  
新しい `OcrEngine` を作成すると、クリーンな状態から開始でき、残存設定が実行に影響しないことが保証されます。画像を早めにロードすることで、ファイルの存在が検証され、後のステップで時間を無駄にする前に有用な例外が得られます。

> **Pro tip:** 画像が巨大（5 MB 超）な場合は、まずリサイズすることを検討してください。Aspose OCR は、いずれの方向でも 2000 px 未満の画像でより高速に動作します。

---

## ステップ 2 – 読み取りたいフィールドのポリゴンを定義する

*Region of Interest*（ROI）は、エンジンに検索領域を指示するポリゴンです。以下では、“First Name” 用と “Date of Birth” 用の 2 つの矩形を作成します。座標は自分のフォームに合わせて調整してください。

```java
        // Polygon for the first field (e.g., First Name)
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},   // X‑coordinates
                new int[]{100, 100, 150, 150}, // Y‑coordinates
                4);

        // Polygon for the second field (e.g., Date of Birth)
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);
```

*Why polygons instead of rectangles?*  
ポリゴンを使用すると、傾いたり非矩形のボックスにも柔軟に対応でき、印刷されたフォームをスキャンした際に完璧に揃っていないケースでよく使われます。

---

## ステップ 3 – Aspose OCR にこれらの領域だけに注目させる

ここでポリゴンをエンジンにバインドします。`setRegionsOfInterest` メソッドはリストを受け取るので、好きなだけフィールドを追加できます。

```java
        // Limit OCR to the defined regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));
```

*What happens under the hood?*  
Aspose OCR は各ポリゴンを個別のビットマップに切り取り、認識アルゴリズムを実行し、結果を結合します。これにより、周囲のグラフィックからの誤検出が大幅に減少します。

---

## ステップ 4 – OCR プロセスを実行する

すべて設定が完了したら OCR を起動します。`process()` 呼び出しは抽出されたテキストと信頼度スコアを保持する `OcrResult` オブジェクトを返します。

```java
        // Execute OCR on the selected ROIs
        OcrResult ocrResult = ocrEngine.process();
```

フィールドごとの信頼度が必要な場合は `ocrResult.getRegions()` を調べることができます—各領域は独自のスコアを持ちます。ほとんどのシンプルなフォームでは、全体のテキストで十分です。

---

## ステップ 5 – 抽出したテキストを表示（または保存）する

最後に、結果をコンソールに出力します。実際のアプリケーションでは、データベースや JSON ファイルに書き込んだり、API 経由で送信したりすることがあります。

```java
        // Output the extracted text
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

**期待される出力（例）:**

```
=== Extracted Text ===
John Doe
12/04/1990
```

2 行は定義した 2 つのポリゴンに対応しています。余分な空白がある場合は `String.trim()` でトリムしてください。

---

## 多数のフィールドがあるフォームからテキストを抽出する方法

フォームに数十個の入力項目がある場合、座標を手動で入力するのは面倒です。以下のような簡単なパターンを採用できます。

1. **Create a CSV** で各行に `fieldName, x1, y1, x2, y2, x3, y3, x4, y4` を保持します。  
2. **Load the CSV** を実行時に読み込み、各行をループして `Polygon` を作成し、ROI リストに追加します。  

```java
List<Polygon> rois = new ArrayList<>();
try (BufferedReader br = new BufferedReader(new FileReader("fields.csv"))) {
    String line;
    while ((line = br.readLine()) != null) {
        String[] parts = line.split(",");
        int[] xs = { Integer.parseInt(parts[1]), Integer.parseInt(parts[3]),
                    Integer.parseInt(parts[5]), Integer.parseInt(parts[7]) };
        int[] ys = { Integer.parseInt(parts[2]), Integer.parseInt(parts[4]),
                    Integer.parseInt(parts[6]), Integer.parseInt(parts[8]) };
        rois.add(new Polygon(xs, ys, 4));
    }
}
ocrEngine.getEngineOptions().setRegionsOfInterest(rois);
```

*Why bother?*  
ROI の自動生成により、複数のフォームレイアウトで同じ Java コードを再利用でき、プロジェクトを DRY（Don't Repeat Yourself）に保てます。

---

## エッジケースと考慮すべきヒント

- **Rotated scans:** 画像全体が回転している場合は `ocrEngine.getEngineOptions().setRotateAngle(degrees)` を呼び出します。  
- **Low contrast:** 読みやすさを向上させるために `ocrEngine.getEngineOptions().setContrast(1.5f)` を設定します。  
- **Non‑Latin scripts:** `ocrEngine.getEngineOptions().setLanguage(OcrLanguage.Spanish)`（またはサポートされている任意の言語）で言語を切り替えます。  
- **Partial OCR failures:** 常に `ocrResult.getConfidence()` を確認し、80 % 未満の場合はユーザーに手動確認を促すことを検討してください。  

---

## 完全動作例（コピー＆ペースト可能）

以下に、コンパイルして実行できる完全なプログラムを示します。`YOUR_DIRECTORY` を `form.png` が格納されているフォルダーに置き換えてください。

```java
import com.aspose.ocr.*;
import java.awt.Polygon;
import java.util.*;

public class MultiRoiDemo {
    public static void main(String[] args) throws Exception {

        // Step 1 – Initialize engine and load image
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/form.png"));

        // Step 2 – Define polygons for each form field
        Polygon firstField = new Polygon(
                new int[]{50, 200, 200, 50},
                new int[]{100, 100, 150, 150},
                4);
        Polygon secondField = new Polygon(
                new int[]{300, 500, 500, 300},
                new int[]{200, 200, 250, 250},
                4);

        // Step 3 – Limit OCR to those regions
        ocrEngine.getEngineOptions()
                 .setRegionsOfInterest(Arrays.asList(firstField, secondField));

        // Step 4 – Run OCR
        OcrResult ocrResult = ocrEngine.process();

        // Step 5 – Show the result
        System.out.println("=== Extracted Text ===");
        System.out.println(ocrResult.getText());
    }
}
```

コンパイル方法:

```bash
javac -cp "aspose-ocr-23.10.jar" MultiRoiDemo.java
java -cp ".:aspose-ocr-23.10.jar" MultiRoiDemo
```

定義した ROI に対応する 2 行のテキストが表示されるはずです。

---

## よくある質問

**Q: Does this work with PDFs?**  
A: 直接は対応していません。各 PDF ページを画像に変換（例: Aspose PDF を使用）してから、OCR エンジンに渡してください。

**Q: What if my form has checkboxes?**  
A: OCR はブール状態を読み取れませんが、チェックボックス領域を ROI として扱い、ピクセル密度を調べてチェックの有無を推測できます。

**Q: Can I extract text from a multi‑page form in one go?**  
A: 各ページ画像をループし、同じ ROI リストを再利用して結果を連結すれば可能です。

---

## 結論

Aspose OCR を使用した **extract text from image** の完全なエンドツーエンドソリューションを解説し、同じ手法で **extract text from form** フィールドを正確に抽出できることを示しました。ポリゴンを定義し、エンジンの注目領域を限定し、一般的な落とし穴に対処することで、画像全体を処理するオーバーヘッドなしに高速でクリーンなデータが得られます。

次のステップに進む準備はできましたか？この OCR 出力を JSON ペイロードに連結したり、機械学習モデルに渡して検証したりしてみてください。可能性は無限大です。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}