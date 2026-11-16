---
category: general
date: 2026-02-27
description: Aspose OCR を使用してスキャンした PDF から検索可能な PDF を作成します。スキャン PDF の変換方法、PDF からテキストを抽出する方法、検索可能にする方法を学びましょう。
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- how to convert pdf
- extract text from pdf
- convert pdf to searchable
language: ja
og_description: スキャンしたファイルから検索可能なPDFを作成します。このガイドでは、スキャンしたPDFを変換し、PDFからテキストを抽出し、Aspose
  OCRを使用して検索可能なPDFを生成する方法を示します。
og_title: Javaで検索可能なPDFを作成する – 完全チュートリアル
tags:
- Java
- OCR
- PDF processing
title: Javaで検索可能なPDFを作成する – ステップバイステップガイド
url: /ja/java/ocr-operations/create-searchable-pdf-with-java-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java で検索可能な PDF を作成する – 完全チュートリアル

紙のスキャンから **検索可能な PDF** を作成したいけど、どこから始めればいいか分からないことはありませんか？同じ壁にぶつかる開発者は多数います。ワークフローでテキスト検索できるドキュメントが必要なのに、静止画像のままになってしまう… そんなときは、数行の Java と Aspose OCR さえあれば、スキャンした PDF を完全に検索可能なものに変換できます。手作業の OCR ツールは不要です。

このチュートリアルでは、スキャンした PDF の読み込み、OCR の実行、検索可能な PDF の書き出しまでの一連の流れを解説します。途中で **convert scanned PDF** の方法や、**how to convert PDF** をプログラムで行う手順、**extract text from PDF** の実装例も紹介します。最後まで読めば、任意の Java プロジェクトに組み込める再利用可能なコードスニペットが手に入ります。

## 必要なもの

- **Java 17**（または最近の JDK；Aspose OCR は Java 8 以降で動作）
- **Aspose OCR for Java** ライブラリ（Aspose の公式サイトから JAR をダウンロードするか、Maven 依存として追加）
- 検索可能にしたい **scanned PDF** ファイル
- お好みの IDE またはテキストエディタ（IntelliJ、VS Code、Eclipse など）

> **Pro tip:** Maven を使用している場合、以下の依存関係を `pom.xml` に追加すれば自動的にライブラリが取得できます：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.9</version> <!-- check for the latest version -->
</dependency>
```

Gradle を使う場合は、同等の記述は次の通りです：

```gradle
implementation 'com.aspose:aspose-ocr:23.9'
```

前提条件が整ったので、いよいよコードに入りましょう。

![スキャンした文書が検索可能なテキストに変換される様子を示すイラスト](/images/create-searchable-pdf.png)

*Image alt text: create searchable pdf illustration*

## Step 1: OCR エンジンの初期化

まず最初に必要なのは `OcrEngine` のインスタンスです。このオブジェクトが OCR プロセス全体を管理し、変換メソッドへアクセスできるようにします。

```java
import com.aspose.ocr.*;

public class PdfSearchableDemo {
    public static void main(String[] args) throws Exception {

        // Step 1: Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();
```

**重要ポイント:** エンジンには言語、解像度、出力形式といった設定が保持されます。1 回だけインスタンス化して複数ファイルで再利用すれば、毎回新しいエンジンを作成するよりも効率的です。

## Step 2: 入力と出力のパスを定義

エンジンに対して **scanned PDF** の所在と、生成した **searchable PDF** の保存先を教える必要があります。

```java
        // Step 2: Specify input (scanned PDF) and output (searchable PDF) file paths
        String inputPdfPath = "YOUR_DIRECTORY/scanned-document.pdf";
        String outputPdfPath = "YOUR_DIRECTORY/searchable-document.pdf";
```

`YOUR_DIRECTORY` は実際に使用しているフォルダーに置き換えてください。Web サービスを構築する場合は、これらのパスをメソッド引数や HTTP の multipart アップロードとして受け取ることも可能です。

## Step 3: スキャン PDF を検索可能 PDF に変換

ここが本番です——`convertPdfToSearchablePdf` を呼び出します。このメソッドは各ページに対して OCR を実行し、見えないテキスト層を埋め込んだ新しい PDF を生成します。

```java
        // Step 3: Convert the scanned PDF into a searchable PDF
        ocrEngine.convertPdfToSearchablePdf(inputPdfPath, outputPdfPath);
```

**内部処理の流れ:**  
1. ラスタ画像ページごとに OCR エンジンへ送信。  
2. 認識された文字列を隠しテキストストリームに配置。  
3. 元の画像はそのまま保持されるため、レイアウトは元と同一。

変換後に **extract text from PDF** が必要な場合は、同じ `ocrEngine` を再利用できます：

```java
        // Optional: Extract text from the newly created searchable PDF
        String extractedText = ocrEngine.getTextFromPdf(outputPdfPath);
        System.out.println("Extracted text preview (first 200 chars):");
        System.out.println(extractedText.substring(0, Math.min(200, extractedText.length())));
```

## Step 4: 出力結果の確認

簡単な `println` で生成ファイルの場所を表示します。実際のアプリでは、呼び出し元にパスを返したり、HTTP でストリームとして返したりすることが多いでしょう。

```java
        // Step 4: Notify that the searchable PDF has been created
        System.out.println("Searchable PDF created at: " + outputPdfPath);
    }
}
```

### 期待される結果

プログラム実行時に次のような出力が得られます：

```
Searchable PDF created at: /home/user/documents/searchable-document.pdf
Extracted text preview (first 200 chars):
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

生成された `searchable-document.pdf` を任意の PDF ビューア（Adobe Reader、Foxit、Chrome など）で開き、テキスト選択や検索ボックスで検索してみてください。画像だけだったページが検索可能になっているはずです。

## よくあるバリエーションとエッジケース

### ループで複数 PDF を変換

バッチ処理で **convert scanned pdf** を行う場合は、変換呼び出しをループで囲みます：

```java
File folder = new File("YOUR_DIRECTORY/batch/");
for (File file : folder.listFiles((dir, name) -> name.toLowerCase().endsWith(".pdf"))) {
    String output = "YOUR_DIRECTORY/searchable/" + file.getName();
    ocrEngine.convertPdfToSearchablePdf(file.getAbsolutePath(), output);
    System.out.println("Converted: " + file.getName());
}
```

### 言語別の処理

Aspose OCR は多数の言語に対応しています。変換前に言語を設定してください：

```java
ocrEngine.getLanguage().setLanguage(Language.French);
```

### OCR 精度の調整

DPI を上げると認識精度は向上しますが、処理時間も長くなります。解像度は次のように調整可能です：

```java
ocrEngine.getImageProcessingOptions().setResolution(300); // 300 DPI is a good balance
```

### すでに検索可能な PDF の場合

既にテキスト層が存在する PDF に対して変換を実行しても安全です。エンジンは既存のテキスト層を検出し、OCR をスキップして時間を節約します。

## 本番環境でのプロティップ

- **`OcrEngine` をリクエスト間で再利用** する；インスタンス生成は比較的コストが高いです。  
- **リソースの解放**：長時間稼働するサービスでは `ocrEngine.dispose()` を必ず呼び出す。  
- **パフォーマンスのロギング**：変換に要した時間を測定。大容量 PDF は 10 ページごとに数秒かかることがあります。  
- **ファイルパスの安全性**：ユーザー提供のパスはディレクトリトラバーサル攻撃を防ぐために検証する。  
- **並列処理**：大量バッチの場合はスレッドプールの活用を検討。ただしライブラリのスレッドセーフ性に関するドキュメントを確認してください。

## FAQ

**Q: パスワード保護された PDF でも動作しますか？**  
A: はい。変換前に `ocrEngine.setPassword("yourPassword")` でパスワードを設定すれば対応可能です。

**Q: 変換後の検索可能 PDF を直接 Web 応答に埋め込めますか？**  
A: 可能です。変換後にファイルを `byte[]` に読み込み、`HttpServletResponse` の出力ストリームへ `Content-Type: application/pdf` と共に書き出します。

**Q: OCR の品質が低い場合はどうすれば？**  
A: DPI を上げる、言語設定を変更する、あるいは Aspose.Imaging で事前に画像のデスクューやデスペックル処理を行うと改善できることがあります。

## 結論

これで Java と Aspose OCR を使って **searchable PDF** を作成する方法が分かりました。サンプル全体は **convert scanned PDF**、隠しテキストの抽出、出力確認までを数行のコードで実現しています。ここからはバッチジョブへの拡張、Web サービスへの統合、他のドキュメント処理パイプラインとの組み合わせなど、さまざまなシナリオに応用できます。

次のステップに進みませんか？Aspose PDF を使って **how to convert pdf** を DOCX や HTML など他フォーマットに変換したり、**extract text from pdf** を活用した自然言語処理タスクに挑戦したりしましょう。今日作成した検索可能 PDF が、将来の高度な検索エンジン、データマイニングスクリプト、アクセシブルな文書アーカイブの基盤となります。

Happy coding, and may your PDFs always be searchable!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}