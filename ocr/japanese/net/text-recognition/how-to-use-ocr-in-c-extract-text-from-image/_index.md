---
category: general
date: 2026-03-05
description: C#でOCRを使用して画像からテキストを抽出する方法。画像をテキストに変換し、韓国語文字を読み取り、OCR用に画像をすばやくロードする方法を学びましょう。
draft: false
keywords:
- how to use OCR
- extract text from image
- convert image to text
- read korean characters
- load image for OCR
language: ja
og_description: C#でOCRを使用し、画像からテキストを即座に抽出する方法。このガイドでは、画像をテキストに変換し、韓国語文字を読み取り、OCR用に画像をロードする方法を示します。
og_title: C#でOCRを使用する方法 – 画像からテキストを抽出
tags:
- OCR
- C#
- Aspose
title: C#でOCRを使用する方法 – 画像からテキストを抽出する
url: /ja/net/text-recognition/how-to-use-ocr-in-c-extract-text-from-image/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で OCR を使用する方法 – 画像からテキストを抽出する

スクリーンショットに韓国語テキストがたくさんあって、プレーンな文字列が欲しいとき、**OCR の使い方**に悩んだことはありませんか？ 同じように頭を抱えている方は多いです。このチュートリアルでは、**画像からテキストを抽出**し、**画像をテキストに変換**し、さらに Aspose.OCR を使って **韓国語文字を読み取る** 完全な実行可能サンプルを順を追って解説します。

また、**OCR 用画像の読み込み**という見落としがちなステップもカバーするので、後で「ファイルが見つかりません」というエラーに悩まされることはありません。最後には、任意の .NET プロジェクトに組み込める自己完結型プログラムが手に入ります。

## 必要なもの

- .NET 6+（または .NET Framework 4.7.2 以降） – 両方で動作します。  
- Aspose.OCR for .NET – Aspose のウェブサイトから無料トライアルを入手できます。  
- 韓国語テキストが含まれるサンプル画像（`korean_doc.png`）  
- お好きな IDE（Visual Studio、Rider、VS Code など）

他のサードパーティライブラリは不要です。

## 手順 1: プロジェクトのセットアップと Aspose.OCR の追加

まず、新しいコンソールアプリを作成します：

```bash
dotnet new console -n OcrDemo
cd OcrDemo
```

次に、Aspose.OCR の NuGet パッケージを追加します：

```bash
dotnet add package Aspose.OCR
```

> **プロのコツ:** ライセンスファイルがある場合はプロジェクトのルートに配置してください。ライセンスがない場合は無料トライアルが動作しますが、出力に透かしが入ります。

## 手順 2: OCR の使用方法 – エンジンの初期化

ここから C# のコードを書きます。**OCR の使い方**の最初のステップは `OcrEngine` をインスタンス化することです。このオブジェクトがライブラリの中心で、後で必要になるすべての設定を保持します。

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.ImageProcessing;

namespace OcrDemo
{
    class Program
    {
        static void Main(string[] args)
        {
            // Step 2: Initialize the OCR engine
            var ocrEngine = new OcrEngine();

            // Optional: apply your license to remove trial limitations
            // Replace the path with the actual location of your .lic file
            ocrEngine.SetLicense("YOUR_DIRECTORY/Aspose.OCR.lic");
```

**重要ポイント:** エンジンインスタンスがないと、言語設定や画像の読み込み、結果の取得ができません。エンジンは内部リソースも管理するため、1 回作成して再利用する方が新しいオブジェクトを毎回生成するより効率的です。

## 手順 3: 言語の選択 – 韓国語文字の読み取り

次の行でエンジンに対象言語を指示します。目的は **韓国語文字を読み取る** ことなので、`OcrLanguage.Korean` を設定します。必要に応じて Arabic、Thai、Gujarati などに差し替えることも可能です。

```csharp
            // Step 3: Tell the engine which language to recognize
            ocrEngine.Language = OcrLanguage.Korean; // alternatives: Arabic, Thai, Gujarati, etc.
```

**重要性:** 言語を正しく選択すると精度が大幅に向上します。OCR エンジンは言語固有の辞書と文字モデルを使用するため、誤った言語を設定すると文字化けした出力になることがあります。

## 手順 4: OCR 用画像の読み込み – 画像をテキストに変換

エンジンが作業を始める前に、**OCR 用画像の読み込み**が必要です。`ImageStream.FromFile` メソッドはファイルをエンジンが理解できる形式に読み込みます。

```csharp
            // Step 4: Load the image that contains the text
            ocrEngine.Image = ImageStream.FromFile("YOUR_DIRECTORY/korean_doc.png");
```

画像が別フォルダーにある場合はパスを調整してください。実行時にファイルが見つかるよう、ファイルの *Build Action* を “Copy if newer” に設定することを忘れずに。

> **よくある落とし穴:** 文字列リテラル内でバックスラッシュ（`\`）をエスケープせずに使用するとコンパイルエラーになります。`\\` のように二重に書くか、逐語的文字列（`@"C:\path\file.png"`）を使ってください。

## 手順 5: OCR の実行 – 画像からテキストを抽出

ここで本格的な処理が行われます。`Recognize()` を呼び出すと OCR アルゴリズムが実行され、`Text` プロパティで生の文字列が取得できます。

```csharp
            // Step 5: Run OCR and get the recognized text
            string recognizedText = ocrEngine.Recognize().Text;
```

この時点で **画像からテキストを抽出** し、実質的に **画像をテキストに変換** したことになります。元のレイアウトに改行があった場合は、結果文字列にも改行コードが含まれます。

## 手順 6: 結果の表示 – 出力の確認

最後に、コンソールへ結果を出力して正しく動作したか確認します。

```csharp
            // Step 6: Output the result to the console
            Console.WriteLine("=== Recognized Text ===");
            Console.WriteLine(recognizedText);
        }
    }
}
```

プログラムを実行：

```bash
dotnet run
```

### 期待される出力

```
=== Recognized Text ===
안녕하세요. 이것은 OCR 테스트 문서입니다.
```

画像と同様の韓国語文字が表示されていれば、**OCR の使い方**を Aspose.OCR でマスターしたことになります！

![OCR の使用例図](image.png)

*画像の代替テキスト: OCR の使用例図 – 画像の読み込みから認識テキストの出力までのフローを示す。*

## エッジケースとバリエーション

### 1. 複数ページの処理

複数ページ（例: マルチページ TIFF）を含む **画像からテキストを抽出** したい場合は、各ページごとに `ImageStream` インスタンスを作成し、`Recognize()` を呼び出すループを実装します。

### 2. 低品質スキャンへの対処

低解像度の画像は精度を下げます。`Recognize()` を呼び出す前に、Aspose の前処理ツールで画像を改善できます：

```csharp
ocrEngine.Image = ImageProcessing.Preprocess(ocrEngine.Image, ImageProcessingOptions.Deskew);
```

### 3. 言語の動的切替

混在言語の文書がある場合は、認識ごとに `ocrEngine.Language` を変更できます：

```csharp
ocrEngine.Language = OcrLanguage.English;
string english = ocrEngine.Recognize().Text;

ocrEngine.Language = OcrLanguage.Korean;
string korean = ocrEngine.Recognize().Text;
```

### 4. 結果をファイルに保存

**画像をテキストに変換**した結果を保存したい場合は、文字列を `.txt` ファイルに書き出すだけです：

```csharp
System.IO.File.WriteAllText("output.txt", recognizedText);
```

## よくある質問

- **このコードを実行するのにライセンスは必要ですか？**  
  いいえ。無料トライアルで実験は可能ですが、出力に透かしが入ります。購入ライセンスを取得すれば透かしが除去され、パフォーマンスも最大化されます。

- **Linux で使用できますか？**  
  もちろんです。Aspose.OCR はクロスプラットフォーム対応です。Linux 上の .NET Core では `libgdiplus` などのネイティブ依存関係をインストールしてください。

- **画像がファイルではなくストリームの場合はどうすればよいですか？**  
  `ImageStream.FromStream(yourStream)` を使用します。API は任意の `System.IO.Stream` を受け付けます。

## 結論

C# で **OCR の使い方**をステップバイステップで解説し、**画像からテキストを抽出**、**画像をテキストに変換**、そして **韓国語文字を読み取る** 方法と **OCR 用画像の読み込み** の重要ポイントを網羅しました。上記の完全な実行例はそのまま動作し、追加のヒントはより高度なシナリオへの道しるべとなります。

次のチャレンジはどうですか？別の言語に差し替えたり、PDF をページ単位で処理したり、OCR 呼び出しを Web API に組み込んでユーザーが画像をアップロードして即座にテキストを取得できるようにしたり。可能性は無限大です。これでしっかりとした土台ができました。

Happy coding!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}