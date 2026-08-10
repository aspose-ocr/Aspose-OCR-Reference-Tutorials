---
category: general
date: 2026-04-29
description: Aspose OCR のストリーミングモードを使用して TIFF ファイルを OCR する方法を学びましょう。このガイドでは、タイル化された
  TIFF 画像からテキストタイルを効率的に抽出する方法を示します。
draft: false
keywords:
- how to ocr tiff
- extract text tiles
language: ja
og_description: Aspose OCR ストリーミングを使用して TIFF を OCR する方法。大きな TIFF 画像からテキストタイルを抽出するステップバイステップのコード。
og_title: TIFFをOCRする方法 – 完全ストリーミングガイド
tags:
- OCR
- Java
- Aspose
- TIFF
title: TIFFのOCR方法 – 大きなTIFFをストリーミングし、Javaでテキストタイルを抽出する
url: /ja/java/advanced-ocr-techniques/how-to-ocr-tiff-stream-large-tiffs-and-extract-text-tiles-in/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# how to ocr tiff – 大きな TIFF をストリーミングしテキストタイルを抽出する Java

一度にメモリに読み込めないほど大きな **how to ocr tiff** ファイルについて考えたことはありますか？ あなただけではありません。多くの開発者が TIFF 画像が何十ものタイルに分割され、通常の `ocrEngine.recognize()` 呼び出しが失敗して壁にぶつかります。  

良いニュースです。Aspose OCR のストリーミングモードを使えば、各タイルを別々のストリームとして供給できるため、ヒープを圧迫することなく **extract text tiles** が可能になります。このチュートリアルでは、完全に実行可能な Java のサンプルを順に解説し、各行が重要な理由を説明し、回避すべき落とし穴を指摘します。

> **What you’ll get:** タイル化された TIFF をリアルタイムで結合し、結合されたテキストを出力し、他の言語や画像フォーマット向けにコードを適応させる方法を示す実行可能なプログラムです。

---

## Prerequisites

- **Java 17** 以上（コードは try‑with‑resources を使用しているため JDK 8+ でも動作しますが、現在の LTS は JDK 17 です）。
- **Aspose.OCR for Java** ライブラリ（v23.10 以降）。Maven で追加します：

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version>
</dependency>
```

- 個々の TIFF タイルが格納されたフォルダー（例: `tile_0.tif`, `tile_1.tif`, …）。  
- 任意: IntelliJ IDEA や VS Code といった IDE、しかしシンプルなテキストエディタでも問題ありません。

---

## Step 1 – Prepare the Tile Paths (Why It Matters)

OCR エンジンが何かを行う前に、各画像ピースの場所を把握している必要があります。デモ目的でパスをハードコーディングするのは問題ありませんが、実運用ではディレクトリを走査したりマニフェストファイルを読み込んだりするのが一般的です。

```java
// Define the absolute or relative paths to each TIFF tile
String[] tilePaths = {
    "YOUR_DIRECTORY/tile_0.tif",
    "YOUR_DIRECTORY/tile_1.tif",
    "YOUR_DIRECTORY/tile_2.tif"
};
```

> **Pro tip:** タイルは辞書順（0, 1, 2…）に保ってください。エンジンはストリームを供給した順序で認識テキストを連結します。

---

## Step 2 – Enable Streaming Mode on the OCR Engine (Primary Keyword)

ここで `OcrEngine` インスタンスを作成し、ストリーミングを有効にします。これが **how to ocr tiff** を RAM に全体をロードせずに実行する核心です。

```java
// Initialize the OCR engine
OcrEngine ocrEngine = new OcrEngine();

// Activate streaming – essential for large or tiled TIFFs
ocrEngine.getProcessingSettings().setEnableStreaming(true);

// Set the language to English; change as needed (e.g., "fr", "de")
ocrEngine.getLanguageSettings().setLanguage("en");
```

**Why streaming?**  
`setEnableStreaming(true)` を呼び出すと、エンジンは受信した各 `ImageStream` を前のストリームの続きとして扱います。内部で仮想キャンバスを構築し、タイルを仮想的に結合した上で最終的に一度だけ OCR を実行します。これにより、マルチギガバイトの TIFF を一括で読み込もうとした際に発生する “OutOfMemoryError” を回避できます。

---

## Step 3 – Append Each Tile as an Input Stream (Secondary Keyword)

以下のループが各タイルをエンジンに供給します。`try‑with‑resources` ブロックによりファイルハンドルが速やかにクローズされるため、数十個のファイルを扱う際に重要です。

```java
for (String tilePath : tilePaths) {
    try (InputStream stream = new FileInputStream(tilePath)) {
        // Wrap the raw InputStream in Aspose's ImageStream wrapper
        ocrEngine.appendImage(ImageStream.fromStream(stream));
    } catch (IOException e) {
        // If a single tile fails, we log and continue – you might want to abort instead
        System.err.println("Failed to load tile: " + tilePath);
        e.printStackTrace();
    }
}
```

**extract text tiles** というフレーズが自然に組み込まれていることに注目してください。各イテレーションでタイルからテキストが *抽出* され、結果セットに追加されます。

---

## Step 4 – Run Recognition and Output the Combined Text (Primary Keyword)

すべてのタイルがキューに入った後、単一の呼び出しで仮想画像に対して OCR が実行されます。結果は単一の巨大な TIFF を処理したかのように全文テキストを含みます。

```java
// Perform OCR on the combined virtual image
OcrResult ocrResult = ocrEngine.recognize();

// Print the extracted text to the console
System.out.println("=== OCR Output ===");
System.out.println(ocrResult.getText());
```

**Expected output**（タイルに “Hello World” が分割して含まれていると仮定）:

```
=== OCR Output ===
Hello World
```

タイルに複数行がある場合は、供給した順序通りに表示されます。`ocrResult.getText()` をファイルに書き出して、後続処理に回すことも可能です。

---

## Step 5 – Full, Runnable Example (All Steps in One Place)

以下は `StreamingExample.java` にコピペできる完全版プログラムです。インポート文、コメント、エラーハンドリングをすべて含んでいます。

```java
import com.aspose.ocr.*;
import java.io.*;

public class StreamingExample {
    public static void main(String[] args) throws Exception {
        // ------------------------------------------------------------
        // Step 1: List the TIFF tile files
        // ------------------------------------------------------------
        String[] tilePaths = {
            "YOUR_DIRECTORY/tile_0.tif",
            "YOUR_DIRECTORY/tile_1.tif",
            "YOUR_DIRECTORY/tile_2.tif"
        };

        // ------------------------------------------------------------
        // Step 2: Set up the OCR engine in streaming mode
        // ------------------------------------------------------------
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getProcessingSettings().setEnableStreaming(true);
        ocrEngine.getLanguageSettings().setLanguage("en");

        // ------------------------------------------------------------
        // Step 3: Feed each tile as a separate stream
        // ------------------------------------------------------------
        for (String tilePath : tilePaths) {
            try (InputStream stream = new FileInputStream(tilePath)) {
                ocrEngine.appendImage(ImageStream.fromStream(stream));
            } catch (IOException e) {
                System.err.println("Unable to read tile: " + tilePath);
                e.printStackTrace();
                // Optionally: return; // abort on missing tile
            }
        }

        // ------------------------------------------------------------
        // Step 4: Recognize the combined image and display the text
        // ------------------------------------------------------------
        OcrResult ocrResult = ocrEngine.recognize();
        System.out.println("=== OCR Output ===");
        System.out.println(ocrResult.getText());
    }
}
```

保存、コンパイル、実行：

```bash
javac -cp "path/to/aspose-ocr.jar" StreamingExample.java
java -cp ".:path/to/aspose-ocr.jar" StreamingExample
```

コンソールに結合された OCR テキストが表示されるはずです。

---

## Advanced Tips & Common Pitfalls (Why This Works)

| Issue | Why It Happens | How to Fix / Optimize |
|-------|----------------|-----------------------|
| **Out‑of‑memory errors** | `BufferedImage` にフルサイズの TIFF を読み込むとヒープ全体を消費します。 | ストリーミングモード (`setEnableStreaming(true)`) を使用 – エンジンは画像全体を実体化しません。 |
| **Tile order mismatch** | アルファベット順でソートされ、数値順とずれる（例: `tile_10.tif` が `tile_2.tif` の前に来る）。 | 数字をゼロ埋め (`tile_00.tif`, `tile_01.tif`) するか、`Comparator` でプログラム的にソート。 |
| **Wrong language** | OCR のデフォルトは英語で、非英語テキストは文字化けします。 | `ocrEngine.getLanguageSettings().setLanguage("fr")` など、対応する ISO コードを指定。 |
| **Partial failures** | 1 つの破損タイルが全体の処理を止めてしまう。 | タイルごとに `IOException` を捕捉し、ログに記録して続行するか中止するか判断。 |
| **Performance bottleneck** | 多数の小ファイル読み取りでディスク I/O が支配的になる。 | タイルを ZIP にまとめてメモリ上でストリームする、または高速 SSD を使用。 |

---

## When to Use Streaming vs. Single‑Image OCR

- **Streaming** が適しているケース:
  - マルチページ TIFF やギガピクセルスキャン。
  - メモリが制限されている環境（例: Docker コンテナ、モバイルデバイス）。
  - 画像チャンクをすでに受け取っているパイプライン（例: カメラフィード）。

- **Single‑image OCR** が問題なく使えるケース:
  - 小さな PNG/JPEG ファイル（< 5 MB）。
  - シンプルさがパフォーマンスを上回るワンオフのスキャン。

---

## Conclusion

これで **how to ocr tiff** ファイルを Aspose OCR のストリーミング機能で処理し、**extract text tiles** を効率的に行う方法をしっかりと理解できました。エンジンの初期化、ストリーミングの有効化、各タイルの追加、仮想キャンバスの認識という一連の手順が「何を」「なぜ」「どうやって」行うかを網羅しています。

次のステップは？ `"en"` を別の言語コードに置き換えてみる、あるいは異なる画像フォーマット（`.png`, `.jpg`）で実験してみる。OCR 結果を検索インデックスや PDF ジェネレータに直接流し込むことも可能です。パターンは変わりません：ストリーム → 結合 → 認識。

タイルが数百に増えるケースやエラーハンドリングで困ったことがあれば、下のコメント欄で質問してください。Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}