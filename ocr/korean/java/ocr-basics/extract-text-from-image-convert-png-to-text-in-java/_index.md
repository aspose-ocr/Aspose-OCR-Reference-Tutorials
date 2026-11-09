---
category: general
date: 2026-10-30
description: Aspose OCR Java를 사용하여 이미지에서 텍스트를 추출 – PNG를 텍스트로 변환하는 방법, OCR을 위한 이미지
  로드, 그리고 Java OCR 튜토리얼을 따라보세요.
draft: false
keywords:
- convert png to text
- ocr image to text
- extract text from png
- aspose ocr java
- extract text image java
lastmod: 2026-10-30
og_description: Aspose OCR Java로 이미지에서 텍스트를 추출합니다. 단계별 Java OCR 튜토리얼을 따라 PNG를 텍스트로
  변환하고, OCR을 위해 이미지를 로드하며, 다국어 콘텐츠를 효율적으로 처리하세요.
og_image_alt: Screenshot of Java OCR code converting PNG to text using Aspose OCR
og_title: Java OCR로 PNG를 텍스트로 변환 – Aspose 가이드
schemas:
- author: Aspose
  dateModified: '2026-10-30'
  description: extract text from image using Aspose OCR Java – learn how to convert
    PNG to text, load image for OCR, and follow a java ocr tutorial.
  headline: Extract text from image – convert PNG to text in Java
  type: TechArticle
- questions:
  - answer: Yes, a commercial license is required for production use; a free trial
      is available for evaluation.
    question: Can I use Aspose OCR in a commercial application without extra licensing
      fees?
  - answer: Absolutely. The library includes language packs for Arabic, Hebrew, Persian,
      and other RTL scripts.
    question: Does Aspose OCR support right‑to‑left scripts such as Arabic or Hebrew?
  - answer: Aspose OCR can process images up to 10 000 × 10 000 pixels using streaming
      mode, which keeps memory usage under 200 MB.
    question: How large of an image can the engine handle?
  - answer: Yes, `OcrResult.getWords()` returns a collection where each word has a
      `getConfidence()` method.
    question: Is there a way to get confidence scores for each recognized word?
  - answer: The library supports JDK 8, 11, 17, and later LTS releases.
    question: What Java versions are officially supported?
  type: FAQPage
tags:
- OCR
- Java
- Aspose
- Image Processing
title: 이미지에서 텍스트 추출 – Java에서 PNG를 텍스트로 변환
url: /ko/java/ocr-basics/extract-text-from-image-convert-png-to-text-in-java/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 이미지에서 텍스트 추출 – Java에서 PNG를 텍스트로 변환

이미지에서 **텍스트를 추출**해야 했지만, 번거로운 과정을 거치지 않고 이를 가능하게 해줄 라이브러리를 몰라 고민한 적이 있나요? 당신만 그런 것이 아닙니다—개발자들은 지속적으로 “Java에서 PNG를 텍스트로 변환하려면 어떻게 해야 하나요?”라고 묻습니다. 좋은 소식은 Aspose OCR 덕분에 전체 과정이 아주 쉬워진다는 것입니다. 이 가이드에서는 완전한 **java ocr tutorial**을 단계별로 살펴보고, **load image for OCR** 방법을 보여드리며, 깨끗하고 검색 가능한 텍스트를 얻을 수 있습니다.

엔진 설정부터 다국어 콘텐츠 처리까지 모든 내용을 다룰 것이므로, 끝까지 읽으면 **convert PNG to text** 파일을 크기, 형식, 언어에 관계없이 만들 수 있습니다. 외부 서비스나 API 키 없이—단일 JAR와 몇 줄의 코드만 있으면 됩니다.

## 빠른 답변
- **Java에서 PNG를 텍스트로 변환할 수 있는 라이브러리는 무엇인가요?** Aspose OCR for Java.  
- **기본 변환에 필요한 코드 라인은 몇 줄인가요?** 라이브러리를 추가한 후 약 5줄 정도.  
- **Aspose OCR이 영어 외의 언어를 지원하나요?** 예—크메르어, 중국어, 아랍어 등을 포함한 70개 이상의 언어 팩을 지원합니다.  
- **OCR 엔진을 오프라인으로 실행할 수 있나요?** 물론입니다; 엔진은 완전히 온프레미스에서 동작하며 인터넷 연결이 필요 없습니다.  
- **필요한 Java 버전은 무엇인가요?** JDK 8 이상; JDK 11+도 완전히 지원됩니다.

## PNG를 텍스트로 변환한다는 의미는
**Convert PNG to text**는 PNG 이미지 안에 나타나는 텍스트 문자를 추출하여 편집·검색·저장이 가능한 일반 텍스트 문자열로 변환하는 것을 의미합니다. 이 과정은 일반적으로 광학 문자 인식(OCR)이라고 불립니다. 픽셀 패턴을 분석하고 언어별 사전과 매칭함으로써 스캔한 문서, 스크린샷 또는 읽을 수 있는 텍스트가 포함된 비트맵을 편집 가능한 데이터로 변환합니다.

## Java용 Aspose OCR을 사용하는 이유
Aspose OCR은 **50개 이상의 입력 형식**(PNG, JPEG, BMP, TIFF 포함)을 지원하며 스트리밍 아키텍처 덕분에 전체 파일을 메모리에 로드하지 않고도 **수백 페이지 문서**를 처리할 수 있습니다. 이 라이브러리는 **70개 이상의 언어 팩**을 제공하며 고해상도 스캔에서 **최대 95 % 정확도**를 제공합니다. 또한 매월 새로운 스크립트와 성능 향상을 추가하는 업데이트를 받습니다.

## 준비물
- JDK 8 이상이 설치되어 있어야 합니다(코드는 JDK 11+에서도 동작합니다).  
- Maven 또는 Gradle을 사용해 Aspose OCR 라이브러리를 가져오거나, Aspose 웹사이트에서 JAR를 수동으로 다운로드할 수 있습니다.  
- 읽을 수 있는 텍스트가 포함된 PNG 이미지가 필요합니다(예제로 `khmer-sign.png`를 사용합니다).  
- 편하게 사용할 수 있는 IDE 또는 텍스트 편집기—IntelliJ IDEA, Eclipse, VS Code 등 어느 것이든 괜찮습니다.

이것으로 모두 준비되었습니다. 무거운 프레임워크도, 클라우드 자격 증명도 필요 없습니다. 준비되셨나요? 이미지 파일에서 텍스트 추출을 시작해봅시다.

## 프로젝트에 Aspose OCR을 추가하는 방법
OCR 엔진을 빌드 설정에 추가하여 컴파일 시 클래스가 사용 가능하도록 합니다. 이 단계는 Aspose OCR JAR와 그 종속성이 올바르게 참조되도록 하여 Java 소스 파일에서 필요한 패키지를 import할 수 있게 합니다. 의존성을 선언하면 Maven이나 Gradle이 중앙 저장소에서 라이브러리를 다운로드하고 컴파일 및 런타임 실행을 위한 클래스패스에 배치합니다.

**Maven** – add this dependency to `pom.xml`:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.10</version> <!-- check the latest version on Maven Central -->
</dependency>
```

**Gradle** – add the following line to your `build.gradle`:

```groovy
implementation 'com.aspose:aspose-ocr:23.10'
```

수동으로 진행하고 싶다면 Aspose 다운로드 페이지에서 JAR를 받아 프로젝트의 `libs` 폴더에 넣은 뒤 빌드 경로에 추가하면 됩니다.

> **Pro tip:** 항상 최신 안정 버전을 선택하세요; 오래된 릴리스는 언어 팩이나 버그 수정이 누락될 수 있습니다.

## OCR 엔진 인스턴스를 생성하는 방법
OcrEngine은 OCR 인식을 수행하는 핵심 클래스입니다. 이미지 픽셀을 텍스트로 변환하는 데 필요한 모든 내부 버퍼, 언어 데이터 및 처리 설정을 캡슐화합니다. 각 작업마다 새로운 인스턴스를 생성하면 특히 언어 또는 처리 모드를 바꿔 실행할 때 결정론적인 결과를 보장합니다.

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // Initialize the OCR engine
        OcrEngine ocrEngine = new OcrEngine();
        // ... further steps will follow
    }
}
```

왜 매번 새로운 엔진을 생성할까요? 엔진이 언어 사전을 캐시하기 때문에, 엔진을 재설정하면 서로 다른 언어 스캔 간에 교차 오염을 방지할 수 있습니다.

## 원하는 언어 활성화 방법 (선택 사항이지만 권장됨)
OcrLanguage는 엔진이 인식 중에 사용하는 특정 언어 사전을 나타냅니다. 적절한 언어를 선택하면 검색 범위가 줄어들고 처리 속도가 빨라지며 이미지에 기대하는 문자 집합에 집중함으로써 정확도가 향상됩니다.

`OcrLanguage`는 특정 언어 사전을 나타냅니다. 예제에서는 크메르어(`khm`)를 활성화하지만, 영어는 `ENG`, 중국어는 `CHN` 등으로 교체할 수 있습니다.

```java
// Enable Khmer language support (ISO 639‑2 code "khm")
ocrEngine.getLanguages().add(OcrLanguage.KHM);
```

> **Why this matters:** **load image for OCR**을 수행하면 엔진은 활성화된 언어 사전만 검색합니다. 모든 언어를 켜두면 속도가 느려지고 오탐이 증가할 수 있습니다.

## OCR을 위한 이미지 로드 방법 – PNG를 텍스트로 변환
ImageStream은 이미지 파일을 OCR 엔진과 호환되는 스트림으로 읽어들이는 래퍼이며, 형식 감지를 자동으로 처리합니다. 저수준 I/O를 추상화하여 파일 처리 세부 사항에 신경 쓰지 않고 간단한 객체를 엔진에 전달할 수 있게 합니다.

`ImageStream`은 이미지 파일을 OCR 엔진과 호환되는 스트림으로 읽어들이는 래퍼이며, 형식 감지를 자동으로 처리합니다.

```java
// Load the PNG that contains the text you want to extract
ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));
```

이미지가 다른 형식(JPEG, BMP, TIFF)이라면 동일한 메서드가 작동합니다—Aspose가 자동으로 형식을 감지합니다. 파일 경로가 올바른지 확인하세요; 그렇지 않으면 `FileNotFoundException`이 발생합니다.

## OCR 프로세스를 실행하고 PNG를 텍스트로 변환하는 방법
OcrResult는 인식 작업의 결과를 보관하며, 추출된 텍스트와 각 문자·단어에 대한 신뢰도 메트릭을 포함합니다. 엔진에서 `recognize()` 메서드를 호출하면 원시 문자열 및 추가 세부 정보를 조회할 수 있는 OcrResult 객체를 반환받습니다.

`ocrEngine.recognize()`는 추출된 문자열을 반환하는 `getText()`와 문자별 신뢰도 메트릭을 제공하는 `getConfidence()`를 포함한 `OcrResult`를 반환합니다.

```java
// Run OCR and fetch the recognized text
String recognizedText = ocrEngine.recognize().getText();
```

이것으로 **convert PNG to text**를 완료했습니다. 반환된 문자열은 엔진이 본 그대로 줄 바꿈 및 공백을 포함할 수 있습니다. 필요에 따라 `trim()`, `replaceAll("\\s+", " ")` 등으로 후처리할 수 있습니다.

## 결과를 출력하거나 저장하는 방법
Result는 `getText()`를 통해 인식된 텍스트를 제공하는 OcrResult 인스턴스입니다. 콘솔에 결과를 출력하면 OCR이 성공했는지 빠르게 확인할 수 있으며, 실제 운영에서는 텍스트를 파일, 데이터베이스 또는 다른 서비스에 기록할 수 있습니다.

`System.out.println(result.getText());`는 추출된 텍스트를 출력합니다.

```java
System.out.println("Recognized text:");
System.out.println(recognizedText);
```

**예상 출력** (제공된 크메르 사인에 대해) 다음과 같이 나타날 수 있습니다:

```
សួស្តី
Welcome
```

출력이 깨진 경우, 3단계에서 올바른 언어를 활성화했는지와 이미지가 너무 흐릿하지 않은지 다시 확인하세요. 이미지 해상도를 높이면(예: 300 dpi 스캔) 도움이 되는 경우가 많습니다.

## 전체 작업 예제는 어떻게 보이나요?
아래는 의존성 추가부터 OCR 결과 출력까지 모든 단계를 보여주는 독립 실행형 Java 프로그램입니다. `ExtractTextExample` 클래스에는 엔진을 생성하고, 언어를 설정하고, 이미지를 로드하고, 인식을 실행하고, 텍스트를 출력하는 `main` 메서드가 포함되어 있습니다. 이 코드를 `ExtractTextExample.java` 파일에 복사·붙여넣기하고 바로 실행할 수 있습니다.

```java
import com.aspose.ocr.*;

public class ExtractTextExample {
    public static void main(String[] args) throws Exception {
        // 1️⃣ Create OCR engine
        OcrEngine ocrEngine = new OcrEngine();

        // 2️⃣ Enable the language you need (Khmer in this case)
        ocrEngine.getLanguages().add(OcrLanguage.KHM);

        // 3️⃣ Load the PNG image you want to extract text from
        ocrEngine.setImage(ImageStream.fromFile("YOUR_DIRECTORY/khmer-sign.png"));

        // 4️⃣ Run OCR – this step actually converts PNG to text
        String recognizedText = ocrEngine.recognize().getText();

        // 5️⃣ Show the result
        System.out.println("=== OCR Result ===");
        System.out.println(recognizedText);
    }
}
```

프로그램을 다음과 같이 실행합니다:

```bash
mvn compile exec:java -Dexec.mainClass=ExtractTextExample
```

또는 Gradle을 사용하는 경우:

```bash
./gradlew run --args='ExtractTextExample'
```

콘솔에 추출된 텍스트가 출력되어 Aspose OCR을 사용해 **extract text from image**에 성공했음을 확인할 수 있습니다.

## 흔히 발생하는 문제와 해결 방법
| 증상 | 가능한 원인 | 해결 방법 |
|------|--------------|-----------|
| 빈 문자열 반환 | 언어가 활성화되지 않았거나 잘못된 언어 코드 | 적절한 `OcrLanguage`를 추가하세요(예: 영어는 `ENG`). |
| 깨진 문자 | 이미지 해상도가 낮거나 배경이 노이즈가 많음 | 고해상도 소스를 사용하거나 샤프닝 필터로 전처리하세요. |
| `OutOfMemoryError` | 전체 크기의 매우 큰 이미지를 로드함 | 엔진에 전달하기 전에 이미지를 축소하세요(`ImageStream.fromFile(...).scale(0.5)`). |
| `FileNotFoundException` | 잘못된 경로 | 절대 경로나 상대 경로를 확인하고 `Paths.get(...).toAbsolutePath()`를 사용하세요. |

> **Remember:** OCR은 확률적 프로세스입니다. 설정이 완벽하더라도 특히 필기체 스크립트의 경우 몇몇 문자를 수동으로 교정해야 할 수도 있습니다.

## 이 튜토리얼 이후에 할 수 있는 다음 단계
- **Batch processing:** PNG 파일이 들어 있는 디렉터리를 순회하면서 각 이미지에 동일한 로직을 적용합니다.  
- **PDF output:** Aspose PDF를 사용해 추출된 텍스트를 검색 가능한 PDF에 삽입합니다.  
- **Language detection:** 언어를 설정하기 전에 `ocrEngine.detectLanguage()`를 호출해 엔진이 자동으로 언어를 추정하도록 합니다.  
- **Cloud integration:** 코드를 REST 엔드포인트로 감싸 마이크로서비스가 호출하도록 하여 확장 가능한 OCR 서비스를 제공합니다.

이 모든 주제는 방금 완료한 **java ocr tutorial**을 기반으로 하며, Aspose OCR API가 얼마나 다재다능한지 보여줍니다.

## 자주 묻는 질문

**Q: Aspose OCR을 상용 애플리케이션에서 추가 라이선스 비용 없이 사용할 수 있나요?**  
A: 예, 상용 사용을 위해서는 상업용 라이선스가 필요합니다; 평가용 무료 체험판을 제공하고 있습니다.

**Q: Aspose OCR이 아랍어, 히브리어와 같은 오른쪽에서 왼쪽으로 쓰는 스크립트를 지원하나요?**  
A: 물론입니다. 라이브러리는 아랍어, 히브리어, 페르시아어 및 기타 RTL 스크립트용 언어 팩을 포함합니다.

**Q: 엔진이 처리할 수 있는 이미지 크기는 얼마나 큰가요?**  
A: Aspose OCR은 스트리밍 모드를 사용해 최대 10 000 × 10 000 픽셀까지 처리할 수 있으며, 메모리 사용량을 200 MB 이하로 유지합니다.

**Q: 인식된 각 단어에 대한 신뢰도 점수를 얻을 수 있나요?**  
A: 예, `OcrResult.getWords()`는 각 단어가 `getConfidence()` 메서드를 가진 컬렉션을 반환합니다.

**Q: 공식적으로 지원되는 Java 버전은 무엇인가요?**  
A: 이 라이브러리는 JDK 8, 11, 17 및 이후 LTS 릴리스를 지원합니다.

## 결론
우리는 **java ocr tutorial**을 완전하게 따라가며 Aspose OCR을 사용해 **이미지에서 텍스트를 추출**하고, **PNG를 텍스트로 변환**하며, **OCR을 위한 이미지 로드**를 올바르게 수행하는 방법을 배웠습니다. 단계는 간단합니다: 라이브러리를 추가하고, 엔진을 생성하고, 적절한 언어를 활성화하고, PNG를 로드하고, `recognize()`를 실행하고, 출력을 처리합니다. 이 기반을 통해 데이터 입력 자동화, 검색 가능한 아카이브 구축, 혹은 사진에서 기계가 읽을 수 있는 텍스트가 필요한 모든 애플리케이션을 구현할 수 있습니다.

자신의 이미지로 직접 시도해 보세요—예를 들어 영수증 스크린샷이나 스캔한 계약서 등. 언어 설정을 조정하고 해상도를 실험하면 솔루션이 얼마나 유연한지 곧 알 수 있을 것입니다. 문제가 발생하면 문제점 표를 다시 확인하거나 Aspose 공식 문서를 참고하세요; 문서는 상세하고 최신 상태로 유지됩니다.

코딩을 즐기세요, 그리고 다음 프로젝트가 깨끗하고 검색 가능한 텍스트로 가득하길 바랍니다!

**마지막 업데이트:** 2026-10-30  
**테스트 환경:** Aspose OCR for Java 24.10  
**작성자:** Aspose

## 관련 튜토리얼

- [Java 이미지 로드로 텍스트 추출](/ocr/java/ocr-operations/extract-text-from-image-java-load-image-for-ocr/)
- [Aspose OCR Java 예제 – 이미지 빠르게 텍스트로 변환](/ocr/java/ocr-operations/aspose-ocr-java-example-convert-image-to-text-fast/)
- [Java 배치 이미지 OCR – PNG 파일 빠르게 텍스트 추출](/ocr/java/ocr-operations/batch-image-ocr-in-java-extract-text-from-png-files-fast/)

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}