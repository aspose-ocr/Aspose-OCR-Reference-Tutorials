---
category: general
date: 2026-02-17
description: Java에서 OCR을 사용해 이미지 파일의 텍스트를 인식하고, PNG 영수증에서 텍스트를 추출하며, Aspose OCR로 영수증을
  JSON으로 변환하는 방법을 배워보세요.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: ko
og_description: 이미지에서 텍스트를 인식하고, PNG 영수증에서 텍스트를 추출하며, 영수증을 JSON으로 변환하는 Java OCR 사용
  방법에 대한 단계별 가이드.
og_title: Java에서 OCR 사용 방법 – 이미지에서 텍스트 인식
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Java에서 OCR 사용 방법 – 이미지에서 텍스트를 빠르게 인식하기
url: /ko/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Java에서 OCR 사용 방법 – 이미지에서 텍스트를 빠르게 인식하기

영수증 사진에서 텍스트를 추출하는 **how to use OCR**가 궁금하셨나요? 몇몇 온라인 도구를 사용해 보았지만 문자 깨짐이나 파싱할 수 없는 형식이 나왔을 수도 있습니다. 좋은 소식은 몇 줄의 Java 코드만으로 이미지 파일에서 **recognize text from image**를 수행하고, PNG 영수증에서 **extract text from PNG**를 추출하며, 심지어 **convert receipt to JSON**까지 할 수 있다는 것입니다.  

이 튜토리얼에서는 Aspose OCR 라이브러리 라이선스 적용부터 데이터베이스나 머신러닝 모델에 전달할 수 있는 깔끔한 JSON 페이로드를 얻는 전체 워크플로우를 단계별로 살펴봅니다. 불필요한 내용은 없으며, IDE에 복사‑붙여넣기만 하면 바로 실행할 수 있는 실용적인 예제를 제공합니다. 마지막에는 `receipt.png` 를 입력받아 바로 사용할 수 있는 JSON 문자열을 출력하는 독립 실행형 프로그램을 완성하게 됩니다.

## 필요 사항

- **Java Development Kit (JDK) 8+** – 최신 버전이면 모두 동작합니다.
- **Aspose OCR for Java** 라이브러리 (Maven 아티팩트는 `com.aspose:aspose-ocr`).
- 유효한 **Aspose OCR 라이선스 파일** (`Aspose.OCR.lic`). 무료 체험판으로 테스트는 가능하지만 정식 라이선스를 사용하면 평가 제한이 해제됩니다.
- 읽고자 하는 텍스트가 포함된 이미지 파일(PNG, JPEG 등) – 여기서는 `receipt.png` 라고 부르고, 알려진 폴더에 배치합니다.
- 선호하는 IDE(IntelliJ IDEA, Eclipse, VS Code…) – 자유롭게 선택하세요.

> **Pro tip:** 라이선스 파일을 소스 폴더 밖에 두고 절대 경로나 상대 경로로 참조하면 버전 관리에 커밋되는 것을 방지할 수 있습니다.

이제 전제 조건이 명확해졌으니 실제 코드로 들어가 보겠습니다.

## OCR 사용 방법 – 핵심 단계

아래는 우리가 수행할 작업의 고수준 개요입니다:

1. **Aspose OCR 라이브러리를 로드하고 라이선스를 적용**합니다.  
2. **`OcrEngine` 인스턴스를 생성**합니다 – 무거운 작업을 담당하는 엔진입니다.  
3. **`OcrInput` 객체를 준비**하여 처리할 이미지를 지정합니다.  
4. **`ResultFormat.JSON` 으로 `recognize` 를 호출**하여 추출된 텍스트의 JSON 표현을 얻습니다.  
5. **JSON 출력 결과를 처리**합니다 – 콘솔에 출력하거나 파일에 저장하거나 추가 파싱을 수행합니다.

각 단계는 아래 섹션에서 자세히 설명합니다.

## Step 1 – Install Aspose OCR and Apply Your License

먼저 Maven을 사용한다면 `pom.xml` 에 Aspose OCR 의존성을 추가합니다:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

이제 Java 코드에서 라이선스를 로드합니다. 이 단계는 필수이며, 라이선스가 없으면 라이브러리가 평가 모드로 실행되어 출력에 워터마크가 삽입될 수 있습니다.

```java
import com.aspose.ocr.*;

public class OcrSetup {
    public static void applyLicense() throws Exception {
        // Replace the path with the actual location of your Aspose.OCR.lic file
        License ocrLicense = new License();
        ocrLicense.setLicense("C:/licenses/Aspose.OCR.lic");
    }
}
```

> **Why this matters:** `License` 객체는 OCR 엔진에 전체 기능 세트를 사용할 권한이 있음을 알려줍니다. 여기에는 고정밀 인식 및 JSON 내보내기가 포함됩니다. 이 단계를 건너뛰면 **recognize text from image**는 가능하지만 결과가 제한될 수 있습니다.

## Step 2 – Create the OCR Engine Instance

`OcrEngine` 클래스는 모든 OCR 작업의 진입점입니다. 픽셀을 읽고 어떤 문자를 나타내는지 판단하는 “두뇌”라고 생각하면 됩니다.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

엔진은 나중에 언어 설정, 디스키유(기울기 보정) 활성화 등으로 커스터마이징할 수 있습니다. 영수증이 라틴 문자 외의 스크립트를 사용하거나 각도가 기울어져 있을 경우에 유용합니다. 대부분 미국 기반 영수증은 기본 설정으로 충분합니다.

## Step 3 – Load the Image You Want to Process

이제 OCR 엔진이 영수증 파일을 가리키도록 설정합니다. `OcrInput` 클래스는 여러 이미지를 받을 수 있지만, 이번 튜토리얼에서는 단일 PNG 파일만 사용합니다.

```java
import com.aspose.ocr.*;

public class ImageLoader {
    public static OcrInput loadImage(String imagePath) {
        OcrInput input = new OcrInput();
        // Add the PNG receipt – this is where we **extract text from PNG**
        input.add(imagePath);
        return input;
    }
}
```

대량으로 **extract text from PNG** 파일을 처리해야 한다면 `input.add()` 를 반복 호출하거나 파일 경로 리스트를 전달하면 됩니다.

## Step 4 – Recognize Text and Convert Receipt to JSON

튜토리얼의 핵심 부분입니다. 엔진에 텍스트 인식을 요청하고 결과를 JSON 형식으로 반환하도록 합니다. `ResultFormat.JSON` 플래그가 모든 무거운 작업을 대신 수행합니다.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonRecognizer {
    public static String recognizeToJson(OcrEngine engine, OcrInput input) throws Exception {
        // Perform OCR and request JSON output
        OcrResult result = engine.recognize(input, ResultFormat.JSON);
        // Retrieve the JSON string
        return result.getJson();
    }
}
```

JSON 페이로드에는 인식된 각 라인, 경계 상자, 신뢰도 점수, 원시 텍스트가 포함됩니다. 이 구조 덕분에 **convert receipt to JSON** 후 어떤 다운스트림 API에도 손쉽게 전달할 수 있습니다.

## Step 5 – Put It All Together and Run the Program

아래는 모든 코드를 하나로 묶은 완전한 Java 클래스입니다. `JsonExportDemo.java`(또는 원하는 이름) 로 저장하고 IDE 혹은 커맨드 라인에서 실행하세요.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.output.*;

public class JsonExportDemo {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Apply your Aspose OCR license (replace with your actual license file)
        License ocrLicense = new License();
        ocrLicense.setLicense("Aspose.OCR.lic"); // <-- adjust path if needed

        // 2️⃣ Create an OCR engine instance
        OcrEngine ocrEngine = new OcrEngine();

        // 3️⃣ Prepare the input image that contains the text to be recognized
        OcrInput ocrInput = new OcrInput();
        // Replace with the absolute or relative path to your receipt PNG
        ocrInput.add("YOUR_DIRECTORY/receipt.png"); // <-- **extract text from PNG** here

        // 4️⃣ Perform recognition and request the result in JSON format
        OcrResult ocrResult = ocrEngine.recognize(ocrInput, ResultFormat.JSON);

        // 5️⃣ Retrieve the JSON string from the result
        String jsonResult = ocrResult.getJson();

        // 6️⃣ Output the JSON (or save it to a file for further processing)
        System.out.println(jsonResult);
    }
}
```

### Expected Output

프로그램을 실행하면 다음과 유사한 JSON 문자열이 출력됩니다(내용은 영수증에 따라 달라집니다).

```json
{
  "pages": [
    {
      "lines": [
        {
          "text": "Store Name",
          "confidence": 0.99,
          "boundingBox": [12, 34, 200, 45]
        },
        {
          "text": "Date: 2024-02-15",
          "confidence": 0.98,
          "boundingBox": [12, 60, 180, 45]
        },
        {
          "text": "Total: $23.45",
          "confidence": 0.97,
          "boundingBox": [12, 120, 150, 45]
        }
      ]
    }
  ]
}
```

이제 이 JSON을 데이터베이스, REST 엔드포인트, 혹은 데이터 분석 파이프라인에 바로 전달할 수 있습니다. **convert receipt to JSON** 단계는 이미 완료되었습니다.

## Common Questions and Edge Cases

### 이미지가 회전된 경우는 어떻게 하나요?

Aspose OCR은 가벼운 회전을 자동으로 감지하고 보정합니다. 심하게 기울어진 이미지의 경우 인식 전에 `engine.getImagePreprocessingOptions().setDeskew(true)` 를 호출하세요.

### 여러 언어를 처리하려면 어떻게 하나요?

`engine.getLanguage()` 를 사용해 원하는 언어를 설정합니다. 예: `engine.setLanguage(Language.FRENCH)`. 다국어 영수증에서 **recognize text from image** 를 수행할 때 유용합니다.

### JSON 대신 일반 텍스트를 출력하고 싶다면?

당연히 가능합니다. `ResultFormat.JSON` 을 `ResultFormat.TEXT` 로 바꾸고 `result.getText()` 를 호출하면 됩니다.

### OCR 범위를 특정 영역으로 제한할 수 있나요?

네. `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` 를 사용해 영수증 영역만 지정하면 속도와 정확도가 향상됩니다.

## Pro Tips for Production‑Ready OCR

- **라이선스 객체를 캐시**하세요. 파일을 반복 처리할 때 매번 생성하면 오버헤드가 발생합니다.
- **배치 처리**: 모든 영수증 경로를 하나의 `OcrInput` 에 로드하고 한 번에 `recognize` 를 호출합니다. JSON에는 페이지 배열이 포함되어 각 페이지마다 라인이 들어갑니다.
- **JSON 검증**: 문자열을 얻은 뒤 Jackson 같은 라이브러리로 파싱해 형식이 올바른지 확인한 뒤 저장하세요.
- **신뢰도 모니터링**: JSON에 라인별 `confidence` 필드가 있습니다. 0.85 이하의 라인은 필터링해 잡음 데이터를 방지하세요.
- **라이선스 보안**: 클라우드 배포 시 `Aspose.OCR.lic` 를 보안 금고나 환경 변수에 저장해 안전하게 관리하세요.

## Conclusion

우리는 **how to use OCR** 를 Java에서 활용해 **recognize text from image**, **extract text from PNG** 영수증을 수행하고 **convert receipt to JSON** 으로 변환하는 전체 과정을 간결하고 실행 가능한 예제로 다뤘습니다. 단계는 직관적이며 코드는 바로 실행 가능하고, JSON 출력은 어떤 다운스트림 시스템에도 바로 사용할 수 있는 구조화된 형태를 제공합니다.

다음 단계로는 JSON을 Apache Kafka 로 스트리밍하거나 정규식으로 라인 아이템 합계를 추출하거나, 클라우드 OCR 서비스와 연동해 확장성을 높이는 시나리오를 탐색해 볼 수 있습니다. 어떤 길을 선택하든 지금 배운 기본 원리는 변함없이 적용됩니다.

궁금한 점이나 진행 중 문제가 발생했다면 아래에 댓글을 남겨 주세요. 함께 해결해 봅시다. 즐거운 코딩 되시고, 지저분한 영수증 이미지를 깨끗하고 검색 가능한 데이터로 바꾸는 경험을 만끽하세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}