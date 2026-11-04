---
category: general
date: 2026-03-07
description: Java를 사용해 이미지에서 OCR을 실행합니다. PNG에서 텍스트를 인식하고, 영수증에서 텍스트를 추출하며, 전체 Java
  OCR 예제로 OCR을 위한 이미지를 로드하는 방법을 배워보세요.
draft: false
keywords:
- run OCR on image
- recognize text from png
- extract text from receipt
- java OCR example
- load image for OCR
language: ko
og_description: Java로 이미지에 OCR을 실행합니다. 이 가이드는 PNG에서 텍스트를 인식하고, 영수증에서 텍스트를 추출하며, 전체
  Java OCR 예제를 사용하여 OCR을 위한 이미지를 로드하는 방법을 보여줍니다.
og_title: Java로 이미지 OCR 실행 – GPU 기반 텍스트 추출
tags:
- OCR
- Java
- GPU
- Image Processing
title: Java로 이미지 OCR 실행 – GPU 기반 텍스트 추출
url: /ko/java/advanced-ocr-techniques/run-ocr-on-image-with-java-gpu-powered-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java로 이미지 OCR 실행 – GPU 가속 텍스트 추출

이미지 파일에 **OCR을 실행**해야 하는데 Java에서 어디서 시작해야 할지 몰라 고민한 적 있나요? 혼자가 아닙니다—많은 개발자들이 스캔한 영수증이나 PNG 스크린샷에서 텍스트를 추출하려고 할 때 같은 장벽에 부딪히곤 합니다.  

이 튜토리얼에서는 **완전한 Java OCR 예제**를 단계별로 안내합니다. 이 예제는 **PNG 파일에서 텍스트를 인식**할 뿐만 아니라 **영수증 이미지에서 텍스트를 추출**하는 방법을 보여주며, 속도 향상을 위해 GPU 가속을 활용합니다. 최종적으로 이미지 로드 → OCR 처리 → 평문 출력까지 바로 실행 가능한 프로그램을 얻을 수 있습니다.

## 배울 내용

- 간단한 `ImageInputStream`을 사용해 **OCR용 이미지 로드**하는 방법
- GPU 지원을 활성화해 최신 하드웨어에서 엔진을 더 빠르게 실행하는 방법
- **PNG에서 텍스트 인식**하고 영수증에서 유용한 문자열을 추출하는 정확한 단계
- 흔히 발생하는 함정(예: 잘못된 GPU 디바이스 ID)과 베스트 프랙티스 팁
- IDE에 복사‑붙여넣기만 하면 바로 실행 가능한 전체 코드 스니펫

**전제 조건**

- Java 17 이상 (코드에서 간결함을 위해 `var` 키워드를 사용하지만, Java 8을 사용한다면 명시적 타입으로 교체 가능)
- `OcrEngine`, `ImageInputStream`, `OcrResult` 클래스를 제공하는 OCR 라이브러리(예: 가상의 *FastOCR* SDK; 실제 사용하는 라이브러리로 교체)
- 성능 향상이 필요하다면 GPU가 활성화된 머신(선택 사항이지만 권장)

---

## Step 1: Run OCR on Image – Enable GPU Acceleration

첫 번째 작업은 OCR 엔진을 생성하고 GPU 사용을 지정하는 것입니다. 이 단계는 GPU 지원이 없으면 엔진이 CPU로 전환되어 고해상도 영수증을 처리할 때 눈에 띄게 느려지기 때문에 매우 중요합니다.

```java
// Step 1: Create the OCR engine and enable GPU acceleration
OcrEngine ocrEngine = new OcrEngine();

// Turn on GPU usage – this makes the recognition much faster
ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage

// Optional: select which GPU device to use (0 = first GPU)
ocrEngine.getConfig().setGpuDeviceId(0);
```

**왜 중요한가:**  
GPU 가속은 OCR 엔진이 수행하는 무거운 행렬 연산을 그래픽 카드에 넘겨줍니다. GPU가 여러 대 있는 경우 `setGpuDeviceId` 값을 변경해 메모리가 가장 많은 디바이스를 선택할 수 있습니다. GPU를 활성화하지 않으면 “왜 내 OCR이 이렇게 느린가?”라는 불만이 자주 발생합니다.

> **Pro tip:** 머신에 호환 가능한 GPU가 없으면 `setUseGpu(true)` 호출은 단순히 무시됩니다—크래시가 발생하지는 않지만 처리 속도는 느려집니다.

---

## Step 2: Load Image for OCR

엔진이 준비되었으니 이제 이미지를 전달해야 합니다. 아래 예제는 디스크에 저장된 PNG 영수증을 로드하는 방법을 보여줍니다. 경로는 OCR 라이브러리가 지원하는 다른 이미지 포맷으로 자유롭게 교체할 수 있습니다.

```java
// Step 2: Load the image you want to recognize
ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
```

**예외 상황:**  
파일이 존재하지 않거나 경로가 잘못되면 `ImageInputStream`이 `IOException`을 발생시킵니다. 호출을 try‑catch 블록으로 감싸고 유용한 메시지를 로그에 남기세요:

```java
try {
    ImageInputStream imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
} catch (IOException e) {
    System.err.println("Failed to load image: " + e.getMessage());
    return;
}
```

---

## Step 3: Recognize Text from PNG

이미지를 로드했으니 이제 OCR 엔진이 마법을 부릴 차례입니다. 이 단계는 실제로 **PNG에서 텍스트를 인식**(또는 지원되는 다른 포맷)하고 `OcrResult` 객체를 반환합니다.

```java
// Step 3: Run the OCR process on the image
OcrResult ocrResult = ocrEngine.recognize(imageStream);
```

**내부 동작:**  
엔진은 전처리(기울기 보정, 이진화)를 수행하고, 문자 검출을 위해 신경망을 실행한 뒤, 결과를 텍스트 라인으로 조합합니다. 앞서 GPU를 활성화했기 때문에 신경망 연산이 그래픽 카드에서 수행되어 전체 실행 시간이 몇 초 단축됩니다.

---

## Step 4: Extract Text from Receipt

인식이 끝나면 보통 원시 텍스트만 필요합니다. `OcrResult` 클래스는 일반적으로 `getText()` 메서드를 제공해 단일 `String`을 반환합니다. 이후 정규식 등을 이용해 총액, 날짜 등을 추출하는 후처리를 수행하면 됩니다.

```java
// Step 4: Print the recognized plain‑text result
System.out.println("Recognized text:");
System.out.println(ocrResult.getText());
```

**Typical receipt output:**  

```
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

이 문자열을 자체 파서에 전달해 총액, 항목, 세금 정보를 추출할 수 있습니다.

---

## Step 5: Full Java OCR Example – Ready to Run

모든 내용을 하나로 합치면 **완전한 Java OCR 예제**가 됩니다. `Main.java` 파일에 그대로 붙여넣고, OCR 라이브러리를 클래스패스에 포함시키면 바로 실행할 수 있습니다.

```java
import com.fastocr.OcrEngine;
import com.fastocr.ImageInputStream;
import com.fastocr.OcrResult;

public class Main {
    public static void main(String[] args) {
        // 1️⃣ Create OCR engine and enable GPU
        OcrEngine ocrEngine = new OcrEngine();
        ocrEngine.getConfig().setUseGpu(true);          // enable GPU usage
        ocrEngine.getConfig().setGpuDeviceId(0);        // optional: select GPU #0

        // 2️⃣ Load the image you want to recognize
        ImageInputStream imageStream;
        try {
            imageStream = new ImageInputStream("YOUR_DIRECTORY/receipt.png");
        } catch (Exception e) {
            System.err.println("Error loading image: " + e.getMessage());
            return;
        }

        // 3️⃣ Run OCR on the image
        OcrResult ocrResult = ocrEngine.recognize(imageStream);

        // 4️⃣ Output the plain‑text result
        System.out.println("Recognized text:");
        System.out.println(ocrResult.getText());
    }
}
```

**예상 콘솔 출력**(위의 샘플 영수증 기준):

```
Recognized text:
Store: Coffee Corner
Date: 2026-03-07
Item      Qty   Price
Latte      2    $5.80
Muffin     1    $2.50
TOTAL           $8.30
```

출력이 깨져 보이면 이미지가 선명한지(고 DPI)와 OCR 언어 팩이 영수증 언어와 일치하는지 다시 확인하세요.

---

## Common Questions & Gotchas

| Question | Answer |
|----------|--------|
| *What if my GPU isn’t detected?* | 엔진이 자동으로 CPU로 전환됩니다. 드라이버와 `setGpuDeviceId`가 실제 디바이스와 일치하는지 확인하세요(`nvidia-smi` 명령이 도움이 됩니다). |
| *Can I process JPEG or TIFF files?* | 가능합니다—`ImageInputStream`에 파일 확장자를 JPEG 또는 TIFF 등으로 바꾸면 됩니다. 대부분의 OCR 라이브러리는 포맷을 자동 감지합니다. |
| *Is there a way to batch‑process many receipts?* | 인식 코드를 루프 안에 넣고 동일한 `OcrEngine` 인스턴스를 재사용하세요. 이미지마다 엔진을 재초기화하면 GPU 메모리가 낭비됩니다. |
| *How do I improve accuracy on low‑contrast receipts?* | 이미지 전처리(대비 증가, 그레이스케일 변환)를 수행한 뒤 OCR 엔진에 전달하세요. 일부 라이브러리는 `preprocess` API를 제공합니다. |

---

## Conclusion

이제 **Java에서 이미지에 OCR을 실행**하는 전체 흐름을 알게 되었습니다. 이미지 로드 → PNG 텍스트 인식 → 영수증 텍스트 추출까지의 과정을 다루었으며, **java OCR example**를 통해 어떤 프로젝트에도 쉽게 적용할 수 있습니다.  

다음 단계는 GPU 플래그를 끄고 성능 차이를 확인해 보거나, 다양한 이미지 해상도를 실험해 보는 것입니다. 또한 정규식 기반 파서를 통합해 자동으로 총액을 추출하도록 할 수 있습니다. 더 깊이 있는 주제가 궁금하다면 **OCR 후처리**, **언어 모델 교정**, **배치 처리 파이프라인**을 살펴보세요.

행복한 코딩 되시고, 영수증이 언제나 읽히길 바랍니다!  

![run OCR on image example](/images/run-ocr-on-image.png "run OCR on image – Java example")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}