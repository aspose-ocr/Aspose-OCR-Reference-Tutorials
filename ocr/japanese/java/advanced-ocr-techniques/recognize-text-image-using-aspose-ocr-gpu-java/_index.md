---
category: general
date: 2026-02-17
description: JavaでAspose OCRのGPUサポートを利用し、テキスト画像を高速に認識します。画像からテキストを抽出し、最適なパフォーマンスを得るためにGPUデバイスIDを設定する方法を学びましょう。
draft: false
keywords:
- recognize text image
- extract text from image
- set gpu device id
- Aspose OCR Java
- GPU acceleration OCR
language: ja
og_description: JavaでAspose OCRのGPUサポートを利用し、テキスト画像を高速に認識します。このガイドでは、画像からテキストを抽出し、GPUデバイスIDを設定する方法を示します。
og_title: Aspose OCR GPU を使用したテキスト画像の認識 – Java
tags:
- Java
- OCR
- Aspose
- GPU
title: Aspose OCR GPU を使用したテキスト画像の認識 – Java
url: /ja/java/advanced-ocr-techniques/recognize-text-image-using-aspose-ocr-gpu-java/
---

the next step? Try processing a folder of scanned PDFs, experiment with different `setLanguage` options, or combine OCR with a machine‑learning model for post‑processing. The possibilities are endless, and the performance gains from GPU acceleration make even large‑scale projects feasible."

Translate.

Final: "Happy coding, and feel free to drop a comment if you hit any snags!" translate.

Then closing shortcodes.

Make sure to keep markdown formatting.

Now produce final content.{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Aspose OCR GPU を使用したテキスト画像の認識 – Java

Java アプリケーションで **テキスト画像を認識** したいが、大きなファイルで CPU がボトルネックになっていることはありませんか？ あなただけではありません—高解像度のスキャンを処理する際に多くの開発者が同じ壁にぶつかります。 良いニュースは、Aspose OCR を使えば **画像からテキストを抽出** でき、GPU 上で処理時間を劇的に短縮できます。  

このチュートリアルでは、ライセンスの設定方法、GPU 加速の有効化方法、複数のグラフィックカードがある場合の **set gpu device id** の指定方法を示す、完全に実行可能なサンプルを順を追って解説します。最後まで実行すれば、コンソールに認識結果が出力される自己完結型プログラムが手に入ります—追加の手順は不要です。

## 必要なもの

- **Java 17** 以上（API は Java 8+ と互換性がありますが、最新の LTS の方がパフォーマンスが向上します）。  
- **Aspose OCR for Java** ライブラリ（Aspose のウェブサイトから JAR をダウンロード）。  
- 有効な **Aspose OCR ライセンスファイル** (`Aspose.OCR.lic`)。無料トライアルでも動作しますが、GPU 機能はライセンス版でのみ利用可能です。  
- 明瞭で機械可読なテキストを含む画像ファイル（`sample-image.png`）。  
- GPU が有効な環境（NVIDIA CUDA 対応カードが最適）。  

これらの項目に心当たりがなくても心配はいりません—各項目は後ほど順に説明します。

## 手順 1: Aspose OCR をプロジェクトに追加

まず、Aspose OCR の JAR をクラスパスに含めます。Maven を使用している場合は、`pom.xml` に以下の依存関係を追加してください。

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- replace with the latest version -->
</dependency>
```

Gradle を使用する場合は次のように記述します。

```gradle
implementation 'com.aspose:aspose-ocr:23.12'
```

手動で設定したい場合は、JAR を `libs/` フォルダーに配置し、IDE のモジュールパスに追加してください。

> **Pro tip:** バージョン番号はライブラリのリリースノートと同期させておきましょう。新しいバージョンは GPU 処理向けのパフォーマンス改善が含まれていることが多いです。

## 手順 2: Aspose OCR ライセンスをロードする（GPU 使用には必須）

ライセンスがないと `setEnableGpu(true)` 呼び出しは静かに CPU モードにフォールバックします。`main` の冒頭でライセンスをロードしてください。

```java
import com.aspose.ocr.License;

// ...

License ocrLicense = new License();
ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

`YOUR_DIRECTORY` を `.lic` ファイルを保存した絶対パスまたは相対パスに置き換えます。パスが間違っていると Aspose は `FileNotFoundException` をスローするので、スペルを必ず確認してください。

## 手順 3: OCR エンジンを作成し GPU 加速を有効化

ここで `OcrEngine` をインスタンス化し、GPU の使用を指示します。複数のカードがある環境では `setGpuDeviceId` メソッドで特定のカードを選択できます。

```java
import com.aspose.ocr.OcrEngine;

// ...

OcrEngine ocrEngine = new OcrEngine();
ocrEngine.getDevice().setEnableGpu(true);       // activate GPU support
ocrEngine.getDevice().setGpuDeviceId(0);        // optional: choose GPU index (0 = first card)
```

デバイス ID を指定する意味は何ですか？ マルチ GPU サーバーでは、画像前処理用に 1 枚、OCR 用に別の 1 枚を割り当てることがあります。ID を設定することで、重い処理を正しいハードウェアに委任できます。

## 手順 4: 入力画像を準備

Aspose OCR は PNG、JPG、BMP、TIFF など多様なフォーマットに対応しています。画像ファイルを `OcrInput` オブジェクトでラップします。

```java
import com.aspose.ocr.OcrInput;

// ...

OcrInput ocrInput = new OcrInput();
ocrInput.add("YOUR_DIRECTORY/sample-image.png"); // path to the image you want to process
```

ストリーム（例: アップロードされたファイル）を処理したい場合は、代わりに `ocrInput.add(InputStream)` を使用してください。

## 手順 5: 認識処理を実行し結果を取得

`recognize` メソッドは `OcrResult` を返し、プレーンテキスト、信頼度スコア、必要に応じてレイアウト情報も含まれます。

```java
import com.aspose.ocr.OcrResult;

// ...

OcrResult ocrResult = ocrEngine.recognize(ocrInput);
System.out.println("Recognized text:\n" + ocrResult.getText());
```

コンソールには次のような出力が表示されます。

```
Recognized text:
Hello, world!
This is a sample image.
```

画像がぼやけている、または言語が未対応の場合、結果が空になることがあります。その際は `ocrResult.getConfidence()`（0‑100）の値を確認し、前処理を行って再試行するか判断してください。

## 完全な実行可能サンプル

すべてを組み合わせると、IDE にコピペできる単一の Java クラスが完成します。

```java
import com.aspose.ocr.*;

public class GpuOcrDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Load license – required for GPU usage
        License ocrLicense = new License();
        ocrLicense.setLicense("YOUR_DIRECTORY/Aspose.OCR.lic");

        // 2️⃣ Create OCR engine and turn on GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getDevice().setEnableGpu(true);      // enable GPU acceleration
        ocrEngine.getDevice().setGpuDeviceId(0);       // optional: select GPU index

        // 3️⃣ Load the image you want to process
        OcrInput ocrInput = new OcrInput();
        ocrInput.add("YOUR_DIRECTORY/sample-image.png");

        // 4️⃣ Perform recognition
        OcrResult ocrResult = ocrEngine.recognize(ocrInput);

        // 5️⃣ Output the recognized text
        System.out.println("Recognized text:\n" + ocrResult.getText());
    }
}
```

> **Expected output:** コンソールに `sample-image.png` に表示されているテキストがそのまま出力されます。GPU が有効な場合、典型的な 300 dpi スキャンで CPU の数秒から 1 秒未満へと処理時間が大幅に短縮されます。

## よくある質問とエッジケース

### ヘッドレスサーバーでも動作しますか？

はい。GPU ドライバーがインストールされていればディスプレイは不要です。`CUDA` ツールキット（または使用している GPU に相当するもの）がシステム `PATH` に含まれていることを確認してください。

### 複数の GPU があり、GPU 1 を使用したい場合は？

デバイス ID を変更します。

```java
ocrEngine.getDevice().setGpuDeviceId(1); // selects the second GPU (zero‑based index)
```

### 別の言語で画像からテキストを抽出するには？

`recognize` を呼び出す前に言語を設定します。

```java
ocrEngine.setLanguage(OcrLanguage.FRENCH);
```

Aspose は 30 以上の言語をサポートしています。全一覧は API ドキュメントをご参照ください。

### 画像が複数ページを含む場合（例: PDF を画像に変換した場合）は？

各ページごとに別々の `OcrInput` エントリを作成するか、ファイルをループ処理してください。

```java
for (String path : imagePaths) {
    ocrInput.add(path);
}
```

エンジンは順番に結果を連結します。

### 低信頼度の結果をどう処理するか？

信頼度スコアを確認します。

```java
if (ocrResult.getConfidence() < 70) {
    System.out.println("Low confidence – consider preprocessing the image.");
}
```

一般的な前処理手順としては、二値化、ノイズ除去、または 300 dpi へのリサイズがあります。

## パフォーマンス向上のヒント

- **バッチ処理:** 複数の画像を 1 つの `OcrInput` にまとめて追加すると、GPU コンテキストの初期化オーバーヘッドが削減されます。  
- **ウォームアップ:** JVM 起動後にダミー認識を 1 回実行しておくと、最初の呼び出しで発生するドライバー初期化遅延を回避できます。  
- **メモリ管理:** 大きな `OcrInput` オブジェクトは使用後に `ocrInput.clear()` で破棄し、GPU メモリを解放してください。  

## 結論

これで、Java における Aspose OCR の GPU エンジンを使った **テキスト画像の認識** 方法、任意のサポート言語で **画像からテキストを抽出** する方法、そして複数のグラフィックカードを使用する際の **set gpu device id** の指定方法が分かりました。上記の完全なサンプルコードはそのまま動作するはずです—ライセンスと画像パスを差し替えるだけで OK です。

次のステップに進む準備はできましたか？ スキャンした PDF フォルダーを一括処理したり、`setLanguage` オプションをいろいろ試したり、OCR 結果を機械学習モデルで後処理したりしてみてください。可能性は無限大で、GPU 加速によるパフォーマンス向上により大規模プロジェクトでも実現可能です。

楽しいコーディングを！問題が発生したら遠慮なくコメントで教えてくださいね。

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}