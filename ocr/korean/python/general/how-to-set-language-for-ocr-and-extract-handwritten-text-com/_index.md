---
category: general
date: 2026-03-26
description: OCR 엔진에서 언어를 설정하고 이미지에서 손글씨 텍스트를 추출하는 방법 – 이미지에서 텍스트로 변환하는 단계별 튜토리얼.
draft: false
keywords:
- how to set language
- extract handwritten text
- convert image to text
- how to extract handwritten
- recognize handwritten notes
language: ko
og_description: OCR 엔진에서 언어를 설정하고 이미지에서 손글씨 메모를 추출하는 방법. 몇 분 안에 이미지를 텍스트로 변환하는 방법을
  배워보세요.
og_title: OCR 언어 설정 방법 – 손글씨 텍스트를 쉽게 추출하기
tags:
- OCR
- Python
- Image Processing
title: OCR 언어 설정 및 손글씨 텍스트 추출 방법 – 완전 가이드
url: /ko/python/general/how-to-set-language-for-ocr-and-extract-handwritten-text-com/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# OCR 언어 설정 및 손글씨 텍스트 추출 방법 – 완전 가이드

OCR 엔진에 **언어를 설정하는 방법**을 궁금해 본 적 있나요? 실제로 필요한 문자를 인식하도록 말이죠. 식료품 목록 사진, 회의 메모, 혹은 흐릿한 다이어그램 사진이 있어도 텍스트를 추출하지 못할 때가 있죠. 좋은 소식은? 컴퓨터 비전 박사 학위가 필요 없습니다—몇 줄의 Python 코드와 올바른 플래그만 있으면 됩니다.

이 튜토리얼에서는 PNG에서 **손글씨 텍스트를 추출**하고 이미지를 일반 텍스트로 변환하는 정확한 단계들을 살펴보며, 각 설정 뒤에 숨은 “왜”를 설명합니다. 끝까지 따라오면 노트‑테이킹 앱이든 배치‑처리 파이프라인이든 어떤 프로젝트에서도 손글씨 메모를 인식할 수 있게 됩니다.

> **필요한 준비물**  
> • Python 3.8+ (코드는 3.10에서도 동작)  
> • `ocr` 라이브러리 (또는 `OcrEngine`을 제공하는 호환 래퍼)  
> • `note_handwritten.png` 같은 샘플 이미지 – 확장 라틴 문자가 포함된 이미지면 무엇이든 OK.

시작해봅시다.

---

## How to Set Language and Enable Handwritten Recognition

먼저 OCR 엔진에 어떤 알파벳을 기대해야 하는지 알려줘야 합니다. 이 단계를 건너뛰면 엔진은 일반적인 문자 집합을 기본값으로 사용해, 종종 억양이 있는 문자나 특수 기호를 잘못 인식합니다.

```python
import ocr  # Assuming the library is named `ocr`

# Step 1: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Step 2: Choose the language that includes extended Latin characters
ocr_engine.language = ocr.Language.ExtendedLatin

# Step 3: Turn on the handwritten‑text flag
ocr_engine.recognize_handwritten = True
```

**왜 중요한가:**  
- **ExtendedLatin** 은 “ñ”, “ø”, “ç”와 같이 많은 유럽 메모에 흔히 쓰이는 문자를 포함합니다.  
- `recognize_handwritten` 플래그는 기본 인쇄 텍스트 OCR 모델을 손글씨 스트로크에 훈련된 신경망 모델로 전환합니다. 이 플래그가 없으면 엔진은 낙서를 잡음으로 취급합니다.

> **프로 팁:** 여러 언어의 문서를 처리해야 한다면 언어당 별도의 엔진을 인스턴스화하거나 각 호출 전에 `ocr_engine.language` 를 동적으로 전환하세요. 이렇게 하면 사용하지 않는 문자 집합을 로드하는 오버헤드를 피할 수 있습니다.

![OCR 엔진 구성 화면에서 언어 설정 방법을 보여주는 스크린샷](/images/ocr-set-language.png "OCR 엔진에서 언어를 설정하는 방법")

*이미지 대체 텍스트: “OCR 엔진 구성 화면에서 언어를 설정하는 방법.”*

---

## Extract Handwritten Text from a PNG Image

엔진이 무엇을 찾아야 할지 알게 되었으니 이제 이미지를 전달할 차례입니다. `recognize_image` 메서드는 풍부한 결과 객체를 반환하고, `text` 속성에 우리가 원하는 일반 문자열이 들어 있습니다.

```python
# Step 4: Perform OCR on the input image
handwritten_result = ocr_engine.recognize_image("YOUR_DIRECTORY/note_handwritten.png")

# Step 5: Print the extracted text
print(handwritten_result.text)
```

스크립트를 실행하면 다음과 같은 출력이 나타납니다:

```
Buy milk
Call Dr. García at 5 pm
Pick up résumé
```

이 출력은 이미지 → 텍스트 변환에 성공했으며, 엔진이 제공한 언어 설정을 올바르게 적용했음을 증명합니다.

**흔히 겪는 실수**  
- **잘못된 경로** – 파일 위치를 다시 확인하세요; 파일이 없으면 `FileNotFoundError` 가 발생합니다.  
- **저해상도 이미지** – 손글씨 OCR은 300 dpi 이하에서는 제대로 동작하지 않습니다. 해상도를 높이거나 다시 스캔하세요.  
- **색상 반전** – 배경이 어둡고 잉크가 밝은 경우 색상을 먼저 반전시켜야 합니다 (`Pillow` 로 가능).

---

## Convert Image to Text Using a Helper Function

수십 개의 파일에 OCR을 적용하려면 로직을 재사용 가능한 함수로 감싸는 것이 좋습니다. 이렇게 하면 코드를 테스트하기도 쉽고, 다른 파이프라인에 통합하기도 편해집니다.

```python
def extract_handwritten_text(image_path: str) -> str:
    """
    Loads an image, sets the OCR engine to ExtendedLatin,
    enables handwritten recognition, and returns the plain text.
    """
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()   # Remove leading/trailing whitespace


# Example usage
if __name__ == "__main__":
    txt = extract_handwritten_text("YOUR_DIRECTORY/note_handwritten.png")
    print("📝 Handwritten notes:\n", txt)
```

헬퍼 함수는 **손글씨 추출 방법**을 분리해 두어 Flask 엔드포인트, CLI 도구, 배치 작업 등 어디서든 설정을 다시 작성하지 않고 호출할 수 있습니다.

---

## Recognize Handwritten Notes in Real‑World Scenarios

다음은 **손글씨 메모를 인식**해야 할 가능성이 높은 몇 가지 상황과 이 설정이 어떻게 적용되는지에 대한 예시입니다:

| 시나리오 | 언어가 중요한 이유 | 권장 조정 |
|----------|---------------------|-----------------|
| **다국어 식료품 목록** | 항목에 억양이 포함될 수 있음 (예: “crème”) | 목록별로 `ocr_engine.language` 를 전환하거나 지원되는 경우 `ocr.Language.AutoDetect` 사용 |
| **교실 화이트보드 사진** | 분필 자국이 옅게 보일 수 있음 | 엔진에 전달하기 전에 이미지 대비를 높이기 |
| **의료 처방전** | 손글씨가 매우 난잡함 | 약물 이름 사전과 결합한 맞춤법 교정 사전을 사용 |

각 경우에 핵심 단계—**언어 설정 방법**, 손글씨 모드 활성화, `recognize_image` 호출—는 동일합니다. 이 일관성이 접근 방식을 견고하고 유지 보수하기 쉽게 만들어 줍니다.

---

## Edge Cases & Advanced Tweaks

1. **배치 처리** – 엔진을 한 번만 로드하고 파일을 순회하면서 필요할 때만 `language` 속성을 변경합니다. 이렇게 하면 초기화 오버헤드가 크게 감소합니다.  
2. **비라틴 스크립트** – Cyrillic이나 Arabic을 처리해야 한다면 `ExtendedLatin` 대신 해당 열거형(`ocr.Language.Cyrillic` 등)으로 교체하면 됩니다. 동일한 패턴이 적용됩니다.  
3. **부분 인식** – 매우 짧은 스트로크에 대해 엔진이 빈 문자열을 반환할 때가 있습니다. 간단한 검증(`if not result.text.strip(): …`)을 통해 보조 모델로 전환하거나 사용자가 다시 스캔하도록 요청할 수 있습니다.  
4. **성능 프로파일링** – 대규모 데이터셋에서는 `recognize_image` 호출 시간을 측정하세요. 병목이 된다면 `concurrent.futures.ThreadPoolExecutor` 로 병렬 처리하는 것을 고려해 보세요.

---

## Full Working Example

아래는 `handwritten_ocr.py` 라는 파일에 복사‑붙여넣기 할 수 있는 전체 스크립트입니다. 명령줄 인수 파싱을 포함해 어떤 이미지든 지정해서 실행할 수 있습니다.

```python
#!/usr/bin/env python3
"""
handwritten_ocr.py – Convert an image containing handwritten notes
to plain text using the OCR library.

Usage:
    python handwritten_ocr.py path/to/image.png
"""

import sys
import argparse
import ocr  # Replace with the actual import if the library name differs


def extract_handwritten_text(image_path: str) -> str:
    """Extracts handwritten text from the given image."""
    engine = ocr.OcrEngine()
    engine.language = ocr.Language.ExtendedLatin
    engine.recognize_handwritten = True

    result = engine.recognize_image(image_path)
    return result.text.strip()


def main():
    parser = argparse.ArgumentParser(
        description="Convert handwritten image to text (how to set language, extract handwritten text)."
    )
    parser.add_argument("image", help="Path to the PNG/JPG image containing handwritten notes")
    args = parser.parse_args()

    try:
        text = extract_handwritten_text(args.image)
        if text:
            print("✅ Extracted text:\n", text)
        else:
            print("⚠️ No text detected – try a higher‑resolution image.")
    except Exception as e:
        print(f"❌ Error processing {args.image}: {e}", file=sys.stderr)
        sys.exit(1)


if __name__ == "__main__":
    main()
```

다음과 같이 실행합니다:

```bash
python handwritten_ocr.py YOUR_DIRECTORY/note_handwritten.png
```

앞서 보여드린 출력과 동일한 결과가 나타나면 **이미지를 텍스트로 변환**하고 **손글씨 메모를 인식**하는 데 성공한 것입니다.

---

## Conclusion

우리는 OCR 엔진에 **언어를 설정**하는 방법, 손글씨 텍스트 플래그를 켜는 방법, 그리고 **손글씨 텍스트를 추출**하는 재사용 가능한 함수를 만드는 과정을 다뤘습니다. 위 단계들을 따르면 단일 메모든, 방대한 스캔 문서 아카이브든 **이미지를 텍스트로 변환**할 수 있습니다.

다음 단계로는 다양한 언어 팩을 실험해 보거나, 폴더 전체를 배치 처리하거나, JSON 결과를 반환하는 웹 서비스에 이 로직을 통합해 보세요. 기본 원리는 동일하며, `ocr` 라이브러리의 유연성 덕분에 거의 모든 사용 사례에 맞게 조정할 수 있습니다.

에지 케이스, 성능 최적화, 다른 언어 확장 등에 대한 질문이 있으면 댓글을 남기거나 GitHub 에서 저에게 ping 주세요 – 즐거운 코딩 되세요!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}