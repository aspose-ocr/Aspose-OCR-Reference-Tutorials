---
category: general
date: 2026-05-31
description: C#에서 Aspose OCR을 사용하여 이미지에서 표를 추출합니다. 이미지를 표로 변환하고, 표 감지를 활성화하며, 결과를
  효율적으로 출력하는 방법을 배워보세요.
draft: false
keywords:
- extract tables from image
- convert image to table
- OCR table extraction
- Aspose OCR C#
- image to spreadsheet conversion
- table detection in OCR
language: ko
og_description: Aspose OCR을 사용하여 이미지에서 표를 추출합니다. 이 가이드는 이미지를 표로 변환하고, 표 감지를 활성화하며,
  C#에서 결과를 처리하는 방법을 보여줍니다.
og_title: 이미지에서 표 추출 – 단계별 C# 튜토리얼
schemas:
- author: Aspose
  dateModified: '2026-05-31'
  description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  headline: Extract Tables from Image with Aspose OCR – Complete C# Guide
  type: TechArticle
- description: Extract tables from image using Aspose OCR in C#. Learn how to convert
    image to table, enable table detection, and output results efficiently.
  name: Extract Tables from Image with Aspose OCR – Complete C# Guide
  steps:
  - name: Expected Output
    text: 'Assuming the source image contains a 3 × 4 table of invoice line items,
      you might see something like:'
  - name: Low‑Resolution Images
    text: 'When your source picture is under 150 dpi, the table detection algorithm
      may miss cell boundaries. A quick fix is to upscale the image using `System.Drawing`
      before feeding it to Aspose:'
  - name: Skewed Tables
    text: 'If the table is rotated even a few degrees, enable auto‑deskew:'
  - name: Multiple Tables on One Page
    text: Aspose OCR returns each table as a separate object in `result.Tables`. You
      can treat them individually, or merge them into a single DataTable if you need
      a unified view.
  - name: Exporting to Excel
    text: 'Once you have a `DataTable`, exporting to an `.xlsx` file is a breeze with
      `ClosedXML`:'
  type: HowTo
- questions:
  - answer: Yes. Convert each PDF page to an image first (`PdfRenderer` or `Ghostscript`),
      then feed the bitmap to Aspose OCR.
    question: Does this work with PDFs?
  - answer: Absolutely. The `ImageStream.FromFile` method accepts JPEG, PNG, BMP,
      and TIFF out of the box.
    question: Can I extract tables from a JPG?
  - answer: Aspose OCR treats merged cells as separate logical cells; you may need
      to post‑process the output to combine them based on confidence or content patterns.
    question: What if my table has merged cells?
  - answer: Practically, the engine handles tables up to several hundred rows. Performance
      degrades linearly, so consider chunking very large scans.
    question: Is there a limit on table size?
  type: FAQPage
tags:
- OCR
- C#
- Aspose
- Data Extraction
title: Aspose OCR을 사용하여 이미지에서 표 추출 – 완전한 C# 가이드
url: /ko/net/image-and-drawing-recognition/extract-tables-from-image-with-aspose-ocr-complete-c-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 표 추출 – 완전한 C# 가이드

이미지에서 **표를 추출**해야 할 때가 있었지만 어디서 시작해야 할지 몰랐나요? 혼자가 아닙니다; 많은 개발자들이 스캔한 청구서나 영수증을 사용 가능한 데이터로 변환하려 할 때 이 장벽에 부딪힙니다. 좋은 소식은? Aspose OCR을 사용하면 몇 줄의 C# 코드만으로 **이미지를 표로 변환**할 수 있습니다.

이 튜토리얼에서는 실제 예제를 통해 진행합니다: 표가 포함된 PNG를 로드하고, 시각적 레이아웃을 구조화된 그리드로 변환한 뒤, 각 셀의 내용과 신뢰도 점수를 출력합니다. 끝까지 따라오시면 .NET 프로젝트에 바로 삽입할 수 있는 완전한 코드 스니펫과, 엣지 케이스 처리 및 확장성을 위한 팁을 얻을 수 있습니다.

## 필요 사항

- **.NET 6.0** 이상 (코드는 .NET Framework 4.6+에서도 동작합니다)
- **Aspose.OCR** NuGet 패키지 (`Install-Package Aspose.OCR`)
- 실제로 표가 들어 있는 이미지 파일 (예: `invoice_with_table.png`)
- 기본 C# IDE (Visual Studio, Rider, 또는 C# 확장 기능이 설치된 VS Code)

그것만 있으면 됩니다—추가 OCR 엔진도 없고, 무거운 종속성도 없습니다. 준비되셨나요? 바로 시작해봅시다.

## 1단계: OCR 엔진 초기화하여 **이미지에서 표 추출**

먼저 `OcrEngine` 인스턴스를 생성하고 소스 이미지에 지정합니다. 엔진은 모든 픽셀을 읽고 레이아웃을 이해하려는 두뇌와 같습니다.

```csharp
using Aspose.OCR;
using Aspose.OCR.Models;

// Initialize the OCR engine with the input image
OcrEngine engine = new OcrEngine
{
    // ImageStream.FromFile loads the image from disk
    Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
};
```

> **왜 중요한가:** 엔진을 올바르게 초기화하지 않으면 OCR 엔진이 분석할 대상이 없으며, 이미지에서 표를 전혀 얻을 수 없습니다. `ImageStream.FromFile` 호출은 일반적인 포맷 문제(PNG, JPEG, BMP)를 자동으로 처리하므로 별도의 변환 단계가 필요하지 않습니다.

## 2단계: 표 감지 활성화 – **이미지를 표로 변환**의 핵심

Aspose OCR은 이미지에서 일반 텍스트를 읽을 수 있지만, 표를 인식하려면 `DetectTables` 플래그를 켜야 합니다. 이 플래그가 바로 표 감지를 담당합니다.

```csharp
// Turn on table detection in the OCR options
engine.Options = new OcrOptions
{
    DetectTables = true   // This activates the table extraction algorithm
};
```

> **프로 팁:** 순수 텍스트만 필요하면 `DetectTables`를 `false`로 두세요. 활성화하면 약간의 오버헤드가 발생하지만, 스프레드시트나 데이터베이스에 바로 넣을 수 있는 깔끔하고 구조화된 결과를 얻을 수 있습니다.

## 3단계: OCR 인식 수행 – 진실의 순간

이제 엔진에게 실제로 이미지를 읽도록 요청합니다. `Recognize` 메서드는 일반 텍스트와 감지된 표를 모두 포함하는 `OcrResult` 객체를 반환합니다.

```csharp
// Execute the OCR process
OcrResult result = engine.Recognize();
```

> **내부에서 무슨 일이 일어나나요?** Aspose는 이미지 전처리 단계(디스키유, 이진화)를 수행한 뒤 신경망 기반 텍스트 인식기를 적용합니다. `DetectTables`가 `true`이면 레이아웃 분석을 추가로 수행해 문자들을 행과 열로 그룹화합니다.

## 4단계: 감지된 표 순회 – **이미지에서 표 추출** 실전

엔진이 표를 찾았다면 `result.Tables`에 나타납니다. 각 표, 행, 열을 순회하면서 셀 텍스트와 신뢰도 비율을 출력합니다.

```csharp
// Loop over every detected table
foreach (var table in result.Tables)
{
    Console.WriteLine("Table found:");
    for (int r = 0; r < table.Rows; r++)
    {
        for (int c = 0; c < table.Columns; c++)
        {
            var cell = table[r, c];
            // Show cell text and its confidence level
            Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
        }
        Console.WriteLine(); // New line after each row
    }
}
```

> **왜 신뢰도를 확인하나요?** OCR은 특히 저해상도 스캔에서 완벽하지 않습니다. `Confidence` 값(0‑100)은 셀을 그대로 받아들일지, 수동 검토를 위해 표시할지를 결정하는 기준이 됩니다. 일반적인 임계값은 중요한 데이터의 경우 80 % 정도입니다.

### 예상 출력

소스 이미지에 3 × 4 청구서 라인 아이템 표가 포함되어 있다고 가정하면 다음과 같은 결과가 나타날 수 있습니다:

```
Table found:
Item (conf:96%)   Qty (conf:94%)   Price (conf:97%)   Total (conf:95%)
Pen (conf:99%)    10 (conf:98%)    1.20 (conf:97%)    12.00 (conf:96%)
Notebook (conf:95%) 5 (conf:93%)  3.50 (conf:94%)    17.50 (conf:92%)
...
```

표가 전혀 감지되지 않으면 `result.Tables`는 비어 있게 되며, 출력할 내용이 없지만 프로그램은 정상적으로 종료됩니다.

## 5단계: 엣지 케이스 및 일반적인 함정 처리

### 저해상도 이미지

소스 이미지 해상도가 150 dpi 이하이면 표 감지 알고리즘이 셀 경계를 놓칠 수 있습니다. 간단한 해결책은 `System.Drawing`을 사용해 이미지를 확대한 뒤 Aspose에 전달하는 것입니다.

```csharp
using System.Drawing;
using System.Drawing.Imaging;

// Load and upscale
Bitmap bmp = new Bitmap(@"YOUR_DIRECTORY/invoice_with_table.png");
Bitmap resized = new Bitmap(bmp, new Size(bmp.Width * 2, bmp.Height * 2));
engine.Image = ImageStream.FromBitmap(resized);
```

### 기울어진 표

표가 몇 도 정도 회전되어 있다면 자동 디스키유를 활성화하세요:

```csharp
engine.Options.Deskew = true; // Turns on automatic deskewing
```

### 한 페이지에 여러 표

Aspose OCR은 각 표를 `result.Tables`의 별도 객체로 반환합니다. 개별적으로 처리하거나, 통합된 뷰가 필요할 경우 하나의 `DataTable`로 병합할 수 있습니다.

```csharp
// Example: Merge all tables into one DataTable
var merged = new System.Data.DataTable();
foreach (var tbl in result.Tables)
{
    // Simple merge logic – assumes same column count
    // Add rows from each table
    for (int r = 0; r < tbl.Rows; r++)
    {
        var row = merged.NewRow();
        for (int c = 0; c < tbl.Columns; c++)
        {
            row[c] = tbl[r, c].Text;
        }
        merged.Rows.Add(row);
    }
}
```

### Excel로 내보내기

`DataTable`을 확보하면 `ClosedXML`을 이용해 `.xlsx` 파일로 내보내는 작업이 매우 간단합니다:

```csharp
using ClosedXML.Excel;

var workbook = new XLWorkbook();
var worksheet = workbook.Worksheets.Add(merged, "ExtractedTable");
workbook.SaveAs("ExtractedTable.xlsx");
```

이제 진정으로 **이미지를 표로 변환**했으며, 스프레드시트를 다운스트림 프로세스로 전달할 수 있습니다.

## 전체 작업 예제 – 시작부터 마무리까지

아래는 모든 과정을 하나로 모은 완전한 실행 가능한 프로그램입니다. 새 콘솔 프로젝트에 붙여넣고 파일 경로만 교체한 뒤 **F5**를 눌러 실행하세요.

```csharp
using System;
using Aspose.OCR;
using Aspose.OCR.Models;
using System.Drawing;
using System.Data;
using ClosedXML.Excel;

class Program
{
    static void Main()
    {
        // 1️⃣ Initialize OCR engine with the image
        OcrEngine engine = new OcrEngine
        {
            Image = ImageStream.FromFile(@"YOUR_DIRECTORY/invoice_with_table.png")
        };

        // 2️⃣ Enable table detection (key to convert image to table)
        engine.Options = new OcrOptions
        {
            DetectTables = true,
            Deskew = true // Helps with slightly rotated scans
        };

        // 3️⃣ Perform recognition
        OcrResult result = engine.Recognize();

        // 4️⃣ Process each detected table
        DataTable merged = new DataTable();
        bool firstTable = true;

        foreach (var table in result.Tables)
        {
            Console.WriteLine("Table found:");
            for (int r = 0; r < table.Rows; r++)
            {
                // Ensure DataTable has enough columns
                if (firstTable && merged.Columns.Count < table.Columns)
                {
                    for (int i = merged.Columns.Count; i < table.Columns; i++)
                        merged.Columns.Add($"Col{i + 1}");
                }

                DataRow dr = merged.NewRow();
                for (int c = 0; c < table.Columns; c++)
                {
                    var cell = table[r, c];
                    Console.Write($"{cell.Text} (conf:{cell.Confidence}%)\t");
                    dr[c] = cell.Text; // Populate DataTable for Excel export
                }
                Console.WriteLine();
                merged.Rows.Add(dr);
            }
            firstTable = false;
            Console.WriteLine(); // Blank line between tables
        }

        // 5️⃣ Optional: Export merged result to Excel
        if (merged.Rows.Count > 0)
        {
            using var wb = new XLWorkbook();
            wb.Worksheets.Add(merged, "ExtractedTables");
            wb.SaveAs("ExtractedTables.xlsx");
            Console.WriteLine("\nExcel file 'ExtractedTables.xlsx' created successfully.");
        }
        else
        {
            Console.WriteLine("\nNo tables were detected in the image.");
        }
    }
}
```

**흐름 설명**

1. **엔진 설정** – 이미지를 로드하고 Aspose에 표 감지를 지시합니다.
2. **옵션 튜닝** – `DetectTables`가 핵심 작업을 수행하고, `Deskew`는 각도된 스캔의 정확도를 높입니다.
3. **인식** – 일반 텍스트와 `Table` 객체 컬렉션을 모두 반환합니다.
4. **순회** – 각 셀을 신뢰도와 함께 출력하고, 이후 내보내기를 위해 `DataTable`을 구축합니다.
5. **내보내기** – `ClosedXML`(경량, 인터옵 불필요)로 `.xlsx` 파일을 작성합니다—다운스트림 분석이나 보고에 최적입니다.

## 자주 묻는 질문

- **이 방법이 PDF에서도 작동하나요?**  
  네. 각 PDF 페이지를 먼저 이미지로 변환(`PdfRenderer` 또는 `Ghostscript` 사용)한 뒤 Aspose OCR에 전달하면 됩니다.

- **JPG에서 표를 추출할 수 있나요?**  
  물론 가능합니다. `ImageStream.FromFile` 메서드는 JPEG, PNG, BMP, TIFF를 기본적으로 지원합니다.

- **표에 병합 셀이 있으면 어떻게 되나요?**  
  Aspose OCR은 병합 셀을 별개의 논리 셀로 처리합니다; 신뢰도나 내용 패턴을 기반으로 후처리하여 셀을 결합해야 할 수도 있습니다.

- **표 크기에 제한이 있나요?**  
  실질적으로 엔진은 수백 행까지의 표를 처리할 수 있습니다. 성능은 선형적으로 감소하므로 매우 큰 스캔은 청크 단위로 나누어 처리하는 것이 좋습니다.

## 마무리

우리는 방금 여러분에게 어떻게

## 다음에 배워야 할 내용은?

- [How to extract table from image using Aspose.OCR for .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Extract Text from Image – OCR Optimization with Aspose.OCR for .NET](/ocr/english/net/ocr-optimization/)
- [How to Extract Text from Image by Preparing Rectangles in OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}