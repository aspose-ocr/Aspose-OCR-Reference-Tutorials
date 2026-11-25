---
category: general
date: 2026-06-22
description: 'OCR를 위한 이미지 기울기 보정 방법: 이미지 전처리 OCR 단계 학습, 소금·후추 노이즈 제거 및 정확도 향상.'
draft: false
keywords:
- how to deskew image
- image preprocessing ocr
- remove salt pepper
- preprocess images OCR
language: ko
og_description: OCR을 위한 이미지 기울기 보정, 소금·후추 잡음 제거 및 전처리 이미지 OCR 기술 적용을 포함한 완전한 Java
  예제.
og_title: 이미지 기울기 보정 방법 – 이미지 전처리 OCR 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: 'How to deskew image for OCR: learn image preprocessing OCR steps,
    remove salt pepper noise, and boost accuracy.'
  headline: How to Deskew Image – Image Preprocessing OCR Guide
  type: TechArticle
tags:
- OCR
- image-processing
- Java
title: 이미지 기울기 보정 방법 – 이미지 전처리 OCR 가이드
url: /ko/java/ocr-operations/how-to-deskew-image-image-preprocessing-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지 기울기 보정 방법 – 이미지 전처리 OCR 가이드

OCR 엔진이 실제로 텍스트를 읽을 수 있도록 **이미지 기울기 보정 방법**을 궁금해 본 적 있나요? 당신만 그런 것이 아닙니다. 기울어진 스캔은 완벽한 문서를 뒤죽박죽으로 만들 수 있으며, 대부분의 개발자들이 최소 한 번은 이 문제를 겪습니다.

이 튜토리얼에서는 회전을 교정할 뿐만 아니라 **소금‑후추** 잡음도 제거하고 대비를 높이는 전체 **이미지 전처리 OCR** 파이프라인을 단계별로 살펴보겠습니다—즉 엔진에 전달하기 전에 **이미지 OCR 전처리**에 필요한 모든 것을 포함합니다. 마지막까지 하면 바로 실행 가능한 Java 코드와 각 단계가 왜 중요한지에 대한 명확한 개념을 얻을 수 있습니다.

## 이미지 기울기 보정 방법 – 전처리 파이프라인 구축

OCR 친화적인 워크플로우의 핵심은 일련의 필터를 연결하는 **preprocess options** 객체입니다. 이를 컨베이어 벨트에 비유하면, 각 필터가 하나의 작업을 수행하고 이미지를 다음 단계로 전달합니다. 아래는 `DeskewFilter`, `DenoiseFilter`, `ContrastBoostFilter`를 제공하는 가상의 OCR 라이브러리를 사용한 최소하지만 완전한 예시입니다.

```java
import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.DeskewFilter;
import com.example.ocr.filters.DenoiseFilter;
import com.example.ocr.filters.ContrastBoostFilter;

/**
 * Demonstrates how to deskew image and apply common OCR preprocessing steps.
 */
public class OcrPreprocessDemo {

    public static void main(String[] args) {
        // 1️⃣ Create the OCR engine (replace with your actual implementation)
        Engine engine = new Engine();

        // 2️⃣ Build the preprocessing pipeline
        ImagePreprocessOptions preprocessOptions = new ImagePreprocessOptions();

        // 2a️⃣ Deskew – correct rotation up to ±15°
        preprocessOptions.addFilter(new DeskewFilter(15));

        // 2b️⃣ Denoise – remove salt‑and‑pepper noise
        preprocessOptions.addFilter(new DenoiseFilter());

        // 2c️⃣ Contrast boost – make low‑contrast scans more readable
        preprocessOptions.addFilter(new ContrastBoostFilter(1.5f));

        // 3️⃣ Attach the pipeline to the engine
        engine.setPreprocessOptions(preprocessOptions);

        // 4️⃣ Run OCR on a sample image
        String result = engine.recognizeText("sample-scanned-page.png");

        // 5️⃣ Output the recognized text
        System.out.println("=== OCR RESULT ===");
        System.out.println(result);
    }
}
```

### 왜 이렇게 동작하나요

* **DeskewFilter**는 이미지의 주요 텍스트 라인을 분석하고 각도를 추정하여 비트맵을 수평으로 회전시킵니다. 대부분의 라이브러리는 보정 범위를 ±15°로 제한하는데, 이는 더 큰 각도가 보통 수동 개입이 필요한 심하게 스캔된 페이지를 의미하기 때문입니다.
* **DenoiseFilter**는 고전적인 *소금‑후추* 패턴을 대상으로 합니다—TV의 잡음처럼 보이는 고립된 검은색 또는 흰색 픽셀입니다. 이를 제거하면 OCR 엔진이 잡음을 문자로 오인하는 것을 방지합니다.
* **ContrastBoostFilter**는 히스토그램을 확장하여 옅은 획을 돋보이게 합니다. `1.5f`의 곱셈값은 안전한 기본값이며, 스캔이 특히 흐릿한 경우 이를 높일 수 있습니다.

> **팁:** 문서가 10°를 초과하는 기울기가 없다는 것을 알고 있다면, 그 작은 범위를 `DeskewFilter`에 전달하세요—알고리즘이 더 빠르게 실행되고 과도하게 보정될 가능성이 줄어듭니다.

## 이미지 전처리 OCR: 올바른 순서로 필터 추가하기

순서는 중요합니다. 기울기 보정 전에 *노이즈 제거*를 하면 잡음이 각도 감지를 방해해 정렬이 잘못될 수 있습니다. 반대로, 기울기 보정 후에 대비를 높이면 회전으로 인해 새로운 잡음이 생기는 것을 방지합니다.

아래는 어떤 프로젝트에도 복사‑붙여넣기 할 수 있는 간단한 체크리스트입니다:

| 단계 | 필터 | 이유 |
|------|--------|--------|
| 1 | `DeskewFilter` | 텍스트 기준선을 정렬합니다 |
| 2 | `DenoiseFilter` | 고립된 픽셀 노이즈를 제거합니다 |
| 3 | `ContrastBoostFilter` | OCR 가독성을 향상시킵니다 |

추가 단계가 필요하다면—예를 들어 이진 OCR을 위한 **binarization** 필터—대비를 높인 **후에** 삽입하면 됩니다. 깨끗하고 고대비인 이미지가 더 정확하게 이진화되기 때문입니다.

## DenoiseFilter로 소금‑후추 잡음 제거

소금‑후추 잡음은 저품질 스캔, 특히 저가 휴대폰 카메라에서 촬영한 경우에 흔히 발생합니다. 우리 라이브러리의 `DenoiseFilter`는 주변 이웃의 중간값으로 각 픽셀을 교체하는 median‑filter 커널을 구현합니다. 효과는? 실제 문자에 흐림을 주지 않으면서 작은 점들이 사라집니다.

```java
// Example: customizing the median kernel size (default is 3x3)
preprocessOptions.addFilter(new DenoiseFilter(5)); // 5x5 kernel for heavy noise
```

*커널 크기를 언제 늘려야 할까요?* 원본 이미지에 큰 점들이 많이 보인다면, 더 큰 커널이 이를 정리해 주지만 주의하세요: 너무 크게 하면 작은 글꼴의 섬세한 획까지 지워버릴 수 있습니다.

## 이미지 전처리 OCR – 파이프라인 적용하기

필터 체인을 구성한 후엔 엔진에 연결하는 한 줄 코드(`engine.setPreprocessOptions`)만 있으면 됩니다. 그 순간부터 `recognizeText` 호출마다 자동으로 파이프라인이 실행됩니다. 각 필터를 수동으로 호출할 필요가 없으며, 코드가 깔끔해지고 향후 변경(새 필터 추가, 매개변수 조정)도 중앙에서 관리됩니다.

다음은 원래 12° 기울기와 눈에 띄는 소금‑후추 잡음이 있던 샘플 스캔을 처리한 성공적인 실행 결과입니다:

```
=== OCR RESULT ===
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
Thank you for your business!
```

텍스트가 깨끗하고 올바르게 정렬되었으며, 이전에 “I n v o i c e” 혹은 “$‑‑‑”와 같이 나타났을 불필요한 문자들이 사라진 것을 확인하세요.

## 엣지 케이스 및 일반적인 함정

| 상황 | 주의할 점 | 추천 해결책 |
|-----------|-------------------|---------------|
| Rotation > 15° | DeskewFilter가 포기할 수 있음 | 수동으로 미리 회전하거나 더 넓은 범위 필터 사용 |
| Extremely low resolution ( < 100 dpi ) | ContrastBoostFilter가 세부 정보를 복구하지 못함 | 이미지를 먼저 리샘플링 (예: `ResampleFilter`) |
| Mixed noise (Gaussian + salt‑pepper) | `DenoiseFilter`만으로는 부족함 | `DenoiseFilter` 전에 `GaussianBlurFilter`를 연결 |
| Color scans with colored text | 그레이스케일 변환 필요 | 대비 강화 전에 `GrayscaleFilter` 삽입 |

이러한 상황을 미리 예상하면 나중에 디버깅에 소요되는 시간을 크게 절약할 수 있습니다.

## 전체 작동 예제 (All‑in‑One)

아래는 `com.example.ocr` 의존성을 포함하는 Maven 또는 Gradle 프로젝트에 바로 넣을 수 있는 독립형 Java 클래스입니다. 이 예제는 **이미지 기울기 보정 방법**, **소금‑후추 잡음 제거**, 그리고 **이미지 OCR 전처리** 방식을 보여줍니다.

```java
package com.myapp.demo;

import com.example.ocr.Engine;
import com.example.ocr.ImagePreprocessOptions;
import com.example.ocr.filters.*;

public class CompleteOcrPipeline {

    public static void main(String[] args) {
        // -------------------------------------------------
        // 1️⃣ Initialise OCR engine (replace with your own)
        // -------------------------------------------------
        Engine engine = new Engine();

        // -------------------------------------------------
        // 2️⃣ Configure preprocessing pipeline
        // -------------------------------------------------
        ImagePreprocessOptions options = new ImagePreprocessOptions();

        // Deskew up to ±15° – the core of "how to deskew image"
        options.addFilter(new DeskewFilter(15));

        // Remove salt‑and‑pepper artifacts
        options.addFilter(new DenoiseFilter());

        // Boost contrast by 1.5× to aid OCR recognition
        options.addFilter(new ContrastBoostFilter(1.5f));

        // (Optional) Convert to grayscale – often improves OCR accuracy
        options.addFilter(new GrayscaleFilter());

        // Attach the pipeline
        engine.setPreprocessOptions(options);

        // -------------------------------------------------
        // 3️⃣ Perform OCR on a test file
        // -------------------------------------------------
        String imagePath = "src/main/resources/scanned-document.png";
        String text = engine.recognizeText(imagePath);

        // -------------------------------------------------
        // 4️⃣ Show the result
        // -------------------------------------------------
        System.out.println("=== OCR RESULT ===");
        System.out.println(text);
    }
}
```

**예상 출력** (`scanned-document.png`에 명확한 청구서가 포함되어 있다고 가정) :

```
=== OCR RESULT ===
Invoice #98765
Date: 2024‑02‑28
Amount Due: $2,340.75
Please remit payment within 30 days.
```

이미지를 이미 완벽하게 정렬된 것으로 교체하면, 파이프라인이 여전히 실행됨을 확인할 수 있습니다—문제가 발생하지 않으며 OCR 정확도도 높게 유지됩니다.

## 결론

이제 **이미지 기울기 보정 방법**과 각 전처리 단계—**이미지 전처리 OCR**, **소금‑후추 제거**, 그리고 **이미지 OCR 전처리**—가 깨끗하고 검색 가능한 텍스트를 제공하는 데 핵심적인 역할을 한다는 것을 확실히 이해했습니다. 위 예제는 완전한,

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 주제를 다룹니다. 각 자료는 단계별 설명과 함께 완전한 코드 예제를 제공하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색할 수 있도록 돕습니다.

- [AspOCR 사용 방법: .NET용 이미지 OCR 필터 전처리](/ocr/english/net/ocr-optimization/preprocessing-filters-for-image/)
- [OCR 이미지 전처리를 위한 기울기 각도 계산](/ocr/english/net/skew-angle-calculation/calculate-skew-angle/)
- [OCR 이미지 인식에서 임계값 설정 방법](/ocr/english/net/ocr-settings/set-threshold-value/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}