---
category: general
date: 2026-04-26
description: AsposeAI OCR 후처리를 사용하여 신용카드 번호를 빠르게 마스킹하세요. 단계별 튜토리얼에서 PCI 규정 준수, 정규식
  마스킹 및 데이터 정화 방법을 배웁니다.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: ko
og_description: AsposeAI를 사용하여 OCR 결과에서 신용카드 번호를 마스킹합니다. 이 튜토리얼에서는 PCI 규정 준수, 정규식
  마스킹 및 데이터 정화에 대해 다룹니다.
og_title: 신용카드 번호 마스킹 – 파이썬 OCR 후처리 완전 가이드
tags:
- OCR
- Python
- security
title: OCR 출력에서 신용카드 번호 마스킹 – 완전 파이썬 가이드
url: /ko/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# 마스크된 신용카드 번호 – 완전 Python 가이드

OCR 엔진에서 바로 추출한 텍스트에서 **신용카드 번호를 마스크**해야 할 때가 있나요? 당신만 그런 것이 아닙니다. 규제 산업에서는 전체 PAN(Primary Account Number)을 노출하면 PCI 컴플라이언스 감사에서 큰 문제가 될 수 있습니다. 좋은 소식은? 몇 줄의 Python 코드와 AsposeAI의 후처리 훅을 사용하면 중간 8자리 숫자를 자동으로 숨겨 안전하게 처리할 수 있다는 것입니다.

이 튜토리얼에서는 실제 시나리오를 따라가 보겠습니다: 영수증 이미지에 OCR을 실행하고, PCI 데이터를 정화하는 맞춤형 **OCR 후처리** 함수를 적용합니다. 최종적으로는 어떤 AsposeAI 워크플로에도 삽입할 수 있는 재사용 가능한 스니펫과, 엣지 케이스 처리 및 솔루션 확장에 대한 실용적인 팁을 제공하게 됩니다.

## 배울 내용

- **AsposeAI**에 맞춤형 후처리기를 등록하는 방법
- **정규식 마스킹** 접근법이 빠르고 신뢰할 수 있는 이유
- 데이터 정화와 관련된 **PCI 컴플라이언스** 기본
- 여러 카드 형식이나 국제 번호에 맞게 패턴을 확장하는 방법
- 예상 출력 및 마스킹이 정상 작동했는지 확인하는 방법

> **전제 조건** – Python 3 환경이 정상적으로 동작하고, Aspose.AI for OCR 패키지가 설치되어 있어야 합니다(`pip install aspose-ocr`). 또한 신용카드 번호가 포함된 샘플 이미지(예: `receipt.png`)가 필요합니다. 다른 외부 서비스는 필요하지 않습니다.

---

## 1단계: 신용카드 번호를 마스크하는 후처리기 정의

솔루션의 핵심은 OCR 결과를 받아 **정규식 마스킹**을 수행하고 정화된 텍스트를 반환하는 작은 함수에 있습니다.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**동작 원리:**  
- 정규식 `(\d{4})\d{8}(\d{4})`은 16자리 연속 숫자를 정확히 매치합니다. 이는 Visa, MasterCard 등 대부분의 카드 형식에 해당합니다.  
- 첫 번째와 마지막 네 자리(`\1`과 `\2`)를 캡처함으로써 디버깅에 필요한 최소 정보를 유지하면서 **PCI 컴플라이언스** 규정(전체 PAN 저장 금지)을 준수합니다.  
- 치환 문자열 `\1****\2`는 민감한 중간 8자리를 가려 `1234567812345678`을 `1234****5678`으로 변환합니다.

> **프로 팁:** 15자리 American Express 번호를 지원하려면 `r'(\d{4})\d{6}(\d{5})'`와 같은 두 번째 패턴을 추가하고 두 치환을 순차적으로 실행하세요.

---

## 2단계: AsposeAI 엔진 초기화

후처리기를 연결하기 전에 OCR 엔진 인스턴스를 생성해야 합니다. AsposeAI는 OCR 모델과 맞춤 처리용 간단한 API를 함께 제공합니다.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**왜 여기서 초기화하나요?**  
`AsposeAI` 객체를 한 번 생성하고 여러 이미지에 재사용하면 오버헤드가 감소합니다. 엔진은 언어 모델을 캐시해 이후 호출을 빠르게 처리하므로 영수증을 대량으로 스캔할 때 유용합니다.

---

## 3단계: 맞춤형 마스킹 함수 등록

AsposeAI는 `set_post_processor` 메서드를 제공해任意의 호출 가능한 객체를 연결할 수 있게 합니다. 여기서는 `mask_pci` 함수와 (현재는 비어 있는) 설정 딕셔너리를 전달합니다.

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**내부에서 무슨 일이 일어나나요?**  
나중에 `run_postprocessor`를 호출하면 AsposeAI가 원시 OCR 결과를 `mask_pci`에 전달합니다. 함수는 인식된 텍스트를 포함하는 가벼운 객체(`data`)를 받고, 새로운 문자열을 반환합니다. 이 설계는 핵심 OCR 로직을 건드리지 않으면서 **데이터 정화** 정책을 한 곳에서 적용할 수 있게 합니다.

---

## 4단계: 영수증 이미지에 OCR 실행

엔진이 출력 정화 방법을 알게 되었으니 이제 이미지를 전달합니다. 이 튜토리얼에서는 이미 언어 및 해상도 설정이 완료된 `engine` 객체가 있다고 가정합니다.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

**팁:** 사전 설정된 객체가 없다면 다음과 같이 만들 수 있습니다:

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

`recognize_image` 호출은 `text` 속성에 원시, 마스크되지 않은 문자열을 담은 객체를 반환합니다.

---

## 5단계: 등록된 후처리기 적용

원시 OCR 데이터를 확보했으니 AI 인스턴스에 전달합니다. 엔진은 자동으로 앞서 등록한 `mask_pci` 함수를 실행합니다.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**왜 `run_postprocessor`를 사용하고 직접 함수를 호출하지 않을까요?**  
이렇게 하면 워크플로가 일관성을 유지합니다. 특히 맞춤법 검사, 언어 감지 등 여러 후처리기가 있을 때 유용합니다. AsposeAI는 등록 순서대로 후처리기를 큐에 넣어 결정론적 출력을 보장합니다.

---

## 6단계: 정화된 출력 확인

마지막으로 정화된 텍스트를 출력하고 신용카드 번호가 올바르게 마스크됐는지 확인합니다.

```python
print(final_result.text)
```

**예상 출력** (발췌):

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

영수증에 카드 번호가 없었다면 텍스트는 그대로 유지됩니다—마스크할 것이 없으니 걱정할 필요가 없습니다.

---

## 엣지 케이스 및 일반적인 변형 처리

### 하나의 문서에 여러 카드 번호가 있는 경우
영수증에 PAN이 두 개 이상(예: 멤버십 카드와 결제 카드) 포함돼도 정규식이 전역으로 적용돼 모든 매치를 자동으로 마스크합니다. 추가 코드는 필요 없습니다.

### 비표준 포맷
OCR 결과에 공백이나 대시가 삽입될 수 있습니다(`1234 5678 1234 5678` 또는 `1234-5678-1234-5678`). 다음과 같이 패턴을 확장해 이러한 문자를 무시하도록 합니다:

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

추가된 `[ -]?`는 숫자 블록 사이에 선택적인 공백이나 하이픈을 허용합니다.

### 국제 카드
일부 지역에서는 19자리 PAN이 사용됩니다. 패턴을 다음과 같이 넓힐 수 있습니다:

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

길이에 관계없이 **PCI 컴플라이언스**는 중간 숫자를 마스크하도록 요구한다는 점을 기억하세요.

### 마스크된 값 로깅 (선택 사항)
감사 추적이 필요하면 `custom_settings`를 통해 플래그를 전달하고 함수를 다음과 같이 조정합니다:

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

그 후 다음과 같이 등록합니다:

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

---

## 전체 작업 예시 (복사‑붙여넣기 가능)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

이 스크립트를 `4111111111111111`이 포함된 영수증에 실행하면 다음과 같은 결과가 나옵니다:

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

원시 OCR부터 **데이터 정화**까지 전체 파이프라인이 몇 줄의 깔끔한 Python 코드로 구현되었습니다.

---

## 결론

우리는 AsposeAI의 후처리 훅, 간결한 정규식 루틴, 그리고 **PCI 컴플라이언스**를 위한 몇 가지 모범 사례를 활용해 OCR 결과에서 **신용카드 번호를 마스크**하는 방법을 보여드렸습니다. 이 솔루션은 완전 자립형이며 OCR 엔진이 읽을 수 있는 모든 이미지에 적용 가능하고, 더 복잡한 카드 형식이나 로깅 요구 사항을 다루도록 확장할 수 있습니다.

다음 단계는? 마스크된 번호 중 마지막 네 자리만 저장하는 **데이터베이스 삽입** 루틴과 결합하거나, 영수증 폴더 전체를 야간에 스캔하는 **배치 프로세서**와 통합해 보세요. 또한 주소 표준화나 언어 감지와 같은 다른 **OCR 후처리** 작업을 탐색해 볼 수 있습니다—모두 여기서 사용한 패턴을 그대로 적용하면 됩니다.

엣지 케이스, 성능, 혹은 다른 OCR 라이브러리로 코드를 옮기는 방법에 대한 질문이 있나요? 아래 댓글로 남겨 주세요. 함께 이야기를 이어가며 더 안전하고 효율적인 코딩을 즐기시길 바랍니다. Happy coding, and stay secure!  

![신용카드 번호 마스크가 OCR 파이프라인에서 작동하는 방식을 보여주는 다이어그램](https://example.com/images/ocr-mask-flow.png "OCR 후처리 마스크 흐름도")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}