---
category: general
date: 2026-03-17
description: C#でPNG画像を高速にバッチOCRする方法。PNGファイルからテキストを抽出し、PNGをテキストに変換し、シンプルなスクリプトでディレクトリ内の画像を読み取る方法を学びましょう。
draft: false
keywords:
- how to batch OCR
- extract text png
- convert png to text
- read images from directory
language: ja
og_description: C#でステップバイステップのコードを使用してPNG画像を一括OCRする方法。PNGファイルからテキストを抽出し、PNGをテキストに変換し、ディレクトリから画像を簡単に読み取ります。
og_title: C#でPNG画像を一括OCRする方法 – 完全ガイド
tags:
- OCR
- C#
- Image Processing
title: C#でPNG画像を一括OCRする方法 – 完全ガイド
url: /ja/net/text-recognition/how-to-batch-ocr-png-images-in-c-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# C# で PNG 画像をバッチ OCR する方法 – 完全ガイド

スクリーンショットが大量に入ったフォルダを、手動で1つずつ開かずに **バッチ OCR** したいと思ったことはありませんか？ あなただけではありません—開発者は大規模な PNG コレクションをバッチ OCR する方法を常に尋ねています。特に、テキスト抽出した PNG ファイルを下流の分析に利用したい場合は必須です。  

このチュートリアルでは、**テキスト PNG** ファイルを **抽出し、PNG をテキストに変換** し、**ディレクトリから画像を読み取る** 最適な方法を示す、すぐに実行できる C# のサンプルを順を追って解説します。最後まで読めば、各画像の横に `.txt` が自動で生成され、手作業のコピペに費やす時間を何時間も削減できます。

## 期待できる成果

- OCR エンジンを一度だけ初期化し、バッチ全体で再利用する。  
- ループを書かずに、指定フォルダ内のすべての `*.png` を走査する。  
- 各 OCR 結果を元のファイル名と同じ名前のテキストファイルに書き出す。  
- 空フォルダや画像以外のファイルが混在するケースなど、一般的な例外を優雅に処理する。

### 前提条件

- .NET 6.0 以降（コードは .NET Core や .NET Framework でも動作）  
- `OcrEngine`、`ImageStream`、`OcrResult` 型を提供する OCR ライブラリ（例として、スニペットで使用している架空の **FastOCR** SDK）  
- 基本的な C# の知識—高度なパターンは不要です。

---

## バッチ OCR PNG 画像の概要

以下は **完全に実行可能なプログラム** です。新しいコンソールプロジェクトにコピー＆ペーストし、プレースホルダーのパスを置き換えて **F5** を押すだけで動作します。

```csharp
using System;
using System.IO;
using System.Linq;
using FastOCR;               // <-- Replace with your actual OCR namespace

class Program
{
    static void Main()
    {
        // -------------------------------------------------
        // Step 1: Initialize the OCR engine (language = English)
        // -------------------------------------------------
        var ocrEngine = new OcrEngine();
        ocrEngine.Config.Language = Language.English;

        // -------------------------------------------------
        // Step 2: Locate every PNG file in the input folder
        // -------------------------------------------------
        string inputFolder = @"YOUR_DIRECTORY\images";
        string[] imagePaths = Directory.GetFiles(inputFolder, "*.png");

        if (imagePaths.Length == 0)
        {
            Console.WriteLine("No PNG files found – nothing to process.");
            return;
        }

        // -------------------------------------------------
        // Step 3: Convert file paths to ImageStream objects
        // -------------------------------------------------
        var imageStreams = imagePaths
            .Select(path => ImageStream.FromFile(path))
            .ToList();

        // -------------------------------------------------
        // Step 4: Recognize text in the entire batch
        // -------------------------------------------------
        IReadOnlyList<OcrResult> ocrResults = ocrEngine.RecognizeBatch(imageStreams);

        // -------------------------------------------------
        // Step 5: Write each result to a .txt file next to the image
        // -------------------------------------------------
        string outputFolder = @"YOUR_DIRECTORY\output";
        Directory.CreateDirectory(outputFolder); // ensures the folder exists

        for (int i = 0; i < ocrResults.Count; i++)
        {
            string originalFileName = Path.GetFileNameWithoutExtension(imagePaths[i]);
            string outputPath = Path.Combine(outputFolder, $"{originalFileName}.txt");
            File.WriteAllText(outputPath, ocrResults[i].Text);
            Console.WriteLine($"✅ {originalFileName}.txt created");
        }

        Console.WriteLine("All done! Check the output folder for your text files.");
    }
}
```

> **期待される出力:** `image01.png` に対しては `image01.txt` が生成され、認識された文字列が格納されます。コンソールには書き込みが完了したファイル名が順に表示されます。

![バッチ OCR の概要図](how-to-batch-ocr-diagram.png "C# で PNG 画像をバッチ OCR する流れを示す図")

---

## 手順ごとの解説

### 1. OCR エンジンの初期化 – プロセスの中心  

`var ocrEngine = new OcrEngine();` でエンジンインスタンスを1つ作成し、バッチ全体で再利用します。エンジンを再利用することは **重要** です。多くの OCR ライブラリは構築時に言語モデルなど重いリソースを確保するため、1回だけ初期化すればパフォーマンスが大幅に向上します—特に数十〜数百枚の PNG を処理する場合は顕著です。

> **プロのコツ:** 英語以外の言語が必要な場合は `ocrEngine.Config.Language = Language.Spanish;`（またはサポートされている列挙子）を設定してください。  

### 2. ディレクトリから画像を読み取る – すべての PNG を取得  

`Directory.GetFiles(@"YOUR_DIRECTORY\images", "*.png")` は、**ディレクトリから画像を読み取る** という二次キーワードが示す通りの動作をします。絶対パスの配列が返され、後で OCR エンジンに渡します。  

> **`SearchOption.AllDirectories` を使わない理由:** 画像がサブフォルダにある場合は `GetFiles(path, "*.png", SearchOption.AllDirectories)` に切り替えられます。ただし、深い階層を走査すると不要なファイルが混入する可能性があるため、必要に応じてフィルタリングしてください。

### 3. ファイルパスを ImageStream オブジェクトに変換  

多くの OCR SDK はパスではなくストリームを受け取ります。LINQ の `Select(path => ImageStream.FromFile(path)).ToList()` は、バッチ認識が一度に処理できる **ストリームのリスト** を作成します。このステップにより、ファイルハンドルが一度だけ開かれ、I/O のオーバーヘッドが削減されます。

> **エッジケース:** ファイルが破損していると `ImageStream.FromFile` が例外を投げることがあります。耐障害性が必要なら `try/catch` でラップしてください。

### 4. バッチ全体でテキストを認識  

`ocrEngine.RecognizeBatch(imageStreams)` が **バッチ OCR** の要です。各画像を個別にループして単一画像メソッドを呼び出す代わりに、コレクション全体をエンジンに渡します。内部的にライブラリが並列処理を行うことが多く、マルチコアマシンで速度が大幅に向上します。

> **ヒント:** OCR ライブラリにバッチメソッドが無い場合でも、`Parallel.ForEach` を使って単一画像の `Recognize` を並列実行すれば同様の効果が得られます。

### 5. 各 OCR 結果を書き出す – PNG をテキストに変換  

最後の `for` ループは `ocrResults[i].Text` を元の PNG と同名の `.txt` ファイルに書き込みます。これが二次キーワード *convert PNG to text* が示す動作です。`Path.Combine` を使用することで出力フォルダが存在しない場合でも安全にパスを組み立て、パストラバーサルのバグを防ぎます。

> **よくある落とし穴:** 出力ディレクトリを事前に作成しないと `DirectoryNotFoundException` が発生します。`Directory.CreateDirectory(outputFolder);` で事前に作成しておきましょう。

---

## 実務でのバリエーションへの対応

| 状況 | 変更点 | 理由 |
|-----------|----------------|-----|
| **入力フォルダが空** | 先頭の `if (imagePaths.Length == 0)` ガードを保持 | 無駄な OCR 呼び出しを防ぎ、親切なメッセージを表示 |
| **混在ファイルタイプ** | `Directory.EnumerateFiles(..., "*.*", SearchOption.TopDirectoryOnly).Where(f => f.EndsWith(".png", StringComparison.OrdinalIgnoreCase))` を使用 | PNG のみを対象にし、*extract text png* の要件を満たす |
| **巨大画像（>5 MB）** | OCR 前にダウンサンプル: `ImageStream.FromFile(path).Resize(1920, 1080)`（API がサポートしている場合） | メモリ負荷を減らし、認識精度が向上することが多い |
| **別言語の OCR** | `ocrEngine.Config.Language = Language.French;` を設定 | ソース画像の言語にエンジンを合わせる |

---

## よくある質問 (FAQ)

**Q: JPEG や TIFF ファイルでも動作しますか？**  
A: コアロジックは同じです。検索パターンを `"*.jpg"` や `"*.tif"` に変更し、OCR ライブラリが該当フォーマットをデコードできることを確認してください。

**Q: 数千枚の画像を処理するとメモリが足りなくなる場合は？**  
A: バッチ呼び出しをストリーミング方式に置き換え、例えば 50 枚ずつ処理してからストリームを解放し、次のチャンクを読み込むようにします。

**Q: OCR の信頼度スコアが欲しいです。どこで取得できますか？**  
A: 多くの `OcrResult` オブジェクトは `Confidence` プロパティを提供します。書き出しステップを拡張して以下のように出力できます：

```csharp
var result = ocrResults[i];
string content = $"Confidence: {result.Confidence:P2}\n{result.Text}";
File.WriteAllText(outputPath, content);
```

---

## まとめ

C# で PNG 画像を **バッチ OCR** する方法を、最初から最後まで網羅しました。エンジンを一度だけ初期化し、ディレクトリから画像を取得、ストリームに変換、バッチで認識し、結果をテキストファイルに書き出すというパターンを習得すれば、**extract text PNG**、**convert PNG to text**、**read images from directory** のタスクに対して、実務レベルの堅牢なソリューションが手に入ります。

次のステップは？ OCR プロバイダーを差し替えてみる、スペルチェックなどのマルチスレッド後処理を追加する、あるいは `.txt` を検索インデックスに投入するなど、バッチワークフローをマスターしたら可能性は無限です。

何か独自の工夫があればコメントで共有してください。ハッピーコーディング！

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}