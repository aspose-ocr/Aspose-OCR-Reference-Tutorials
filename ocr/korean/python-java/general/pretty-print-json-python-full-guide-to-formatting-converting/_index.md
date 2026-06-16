---
category: general
date: 2026-06-16
description: Python에서 JSON을 빠르게 예쁘게 출력하고, JSON을 dict로 변환하거나 JSON 문자열을 로드하여 데이터 조작하는
  방법을 배워보세요. 단계별 튜토리얼.
draft: false
keywords:
- pretty print json python
- convert json to dict
- load json string python
language: ko
og_description: Python에서 JSON을 예쁘게 출력하고, JSON을 dict로 변환하거나 JSON 문자열을 로드하는 방법을 즉시 확인하세요.
  몇 분 만에 JSON 처리 마스터하기.
og_title: Python에서 JSON 예쁘게 출력하기 – 완전한 포맷팅 및 변환 가이드
schemas:
- author: Aspose
  dateModified: '2026-06-16'
  description: Pretty print JSON Python quickly and learn how to convert JSON to dict
    or load JSON string Python for data manipulation. Step‑by‑step tutorial.
  headline: Pretty Print JSON Python – Full Guide to Formatting & Converting
  type: TechArticle
tags:
- python
- json
- data‑processing
title: 파이썬으로 JSON 예쁘게 출력하기 – 포맷팅 및 변환 완전 가이드
url: /ko/python-java/general/pretty-print-json-python-full-guide-to-formatting-converting/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# JSON Python 예쁘게 출력 – 포맷팅 및 변환 전체 가이드

JSON Python을 **예쁘게 출력**해야 할 때가 있었고, 출력이 항상 한 줄의 읽기 어려운 형태로 보이는 이유가 궁금했나요? 당신만 그런 것이 아닙니다. 많은 프로젝트에서 원시 JSON 문자열은 뒤얽힌 혼란스러운 형태여서 디버깅이 마치 건초 더미에서 바늘을 찾는 것처럼 느껴집니다.  

좋은 소식은? 몇 가지 내장 함수만으로 그 혼란스러운 데이터를 깔끔하게 들여쓰기된 형태로 변환하고, **convert JSON to dict**를 통해 원활한 후속 처리를 할 수 있다는 것입니다. 이 튜토리얼에서는 JSON 문자열을 Python에서 로드하고 데이터를 반복하는 단계까지 모든 과정을 차근차근 살펴볼 것이므로, 포맷팅에 신경 쓰지 않고 로직에 집중할 수 있습니다.

## 이 튜토리얼에서 다루는 내용

- `json.dumps`와 `indent` 인자를 사용하여 **pretty print JSON Python**하는 방법.  
- `JSON string Python`을 네이티브 딕셔너리로 **load**하는 정확한 방법.  
- 결과 딕셔너리를 유용한 Python 객체로 변환하는 방법, 각 단어와 신뢰도 점수를 출력하는 실용적인 예제 포함.  
- 일반적인 함정(예: 비ASCII 문자 처리) 및 빠른 해결책.  
- 즉시 복사·붙여넣기하고 바로 적용할 수 있는 완전한 실행 스크립트.

이 가이드를 끝까지 읽으면 어떤 JSON 페이로드든 인간이 읽기 쉬운 형식으로 변환하고 순수 Python만으로 조작할 수 있게 됩니다—외부 라이브러리는 필요 없습니다.

---

## 사전 요구 사항

- Python 3.8 이상 (`json` 모듈은 표준 라이브러리의 일부입니다).  
- 딕셔너리와 반복문에 대한 기본 이해.  
- 선택 사항으로, JSON을 반환하는 OCR 엔진이나 서비스—예제는 모의 `engine.recognize()` 호출을 사용하지만, 이를 자신의 데이터 소스로 교체할 수 있습니다.

---

## 단계 1: OCR 수행 (또는 JSON 생성 인식)

우선, JSON 호환 결과가 필요합니다. 많은 컴퓨터 비전 워크플로우에서 OCR 엔진은 JSON으로 직렬화할 수 있는 구조화된 객체를 출력합니다. 아래는 최소한의 플레이스홀더입니다:

```python
# Step 1: Simulate an OCR engine that returns a result object
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    # The real engine would have a .to_json() method; we mimic it
    def to_json(self, indent=None):
        import json
        return json.dumps({"words": self.words}, indent=indent)

# Imagine `engine` is your pre‑configured OCR engine
engine = MockResult()
result = engine  # In real code: result = engine.recognize()
```

> **이 단계가 중요한 이유:**  
> OCR을 수행하지 않더라도 API, 파일, 메시지 큐 등에서 데이터를 받는 경우가 많습니다. 객체는 **pretty print**하기 전에 JSON으로 직렬화 가능해야 합니다.

---

## 단계 2: JSON Python 예쁘게 출력

이제 원시 데이터를 깔끔하게 들여쓰기된 문자열로 변환합니다. `indent` 매개변수가 핵심 역할을 합니다.

```python
# Step 2: Serialize the result with pretty printing
json_str = result.to_json(indent=2)  # <-- pretty print JSON Python
print("🔍 Pretty‑printed JSON output:")
print(json_str)   # optional: view the raw JSON output
```

출력은 다음과 같습니다:

```json
{
  "words": [
    {
      "text": "Hello",
      "confidence": 0.98
    },
    {
      "text": "World",
      "confidence": 0.95
    }
  ]
}
```

> **팁:** 더 넓은 간격을 원한다면 `indent=4`를 사용하고, 키를 알파벳 순으로 정렬하려면 `sort_keys=True`를 추가하세요.

---

## 단계 3: JSON 문자열 Python → 네이티브 딕셔너리 로드

예쁘게 출력된 문자열은 사람에게는 좋지만, 실제 작업에서는 Python이 딕셔너리를 선호합니다. 여기서 **load JSON string Python**을 네이티브 구조로 변환합니다.

```python
# Step 3: Convert the JSON string to a Python dict
import json

result_dict = json.loads(json_str)   # <-- load json string python
print("\n✅ Loaded dict type:", type(result_dict))
```

다음과 같이 표시됩니다:

```
✅ Loaded dict type: <class 'dict'>
```

> **왜 이렇게 하는가:**  
> 딕셔너리는 O(1) 조회, 가변 데이터, 그리고 Python 생태계와의 원활한 통합을 제공합니다. JSON 문자열을 직접 다루려 하면 번거로운 문자열 파싱을 강요받게 됩니다.

---

## 단계 4: 인식된 단어 반복 – 실제 사용 사례

각 단어와 신뢰도 점수를 추출해 봅시다. 이는 **convert json to dict**(이미 가진 딕셔너리)와 실용적인 반복을 모두 보여줍니다.

```python
# Step 4: Display each word with its confidence score
print("\n🗣️ Recognized words and confidence values:")
for word in result_dict["words"]:
    # f‑string gives us a clean, readable line
    print(f'{word["text"]} (conf: {word["confidence"]})')
```

예상 출력:

```
🗣️ Recognized words and confidence values:
Hello (conf: 0.98)
World (conf: 0.95)
```

> **예외 상황 팁:** JSON에 `"words"` 키가 없을 수 있다면 `KeyError`를 방지하세요:

```python
for word in result_dict.get("words", []):
    # safe iteration even when "words" is absent
    print(f'{word.get("text", "<unknown>")} (conf: {word.get("confidence", 0)})')
```

---

## 단계 5: 비ASCII 문자 처리 (Unicode 지원)

OCR 엔진은 종종 “é” 또는 “ü”와 같은 문자를 반환합니다. 기본 `json.dumps`는 이를 `\u00e9`와 같이 이스케이프합니다. 읽기 쉽게 유지하려면 `ensure_ascii=False`를 전달하세요.

```python
# Example with non‑ASCII text
result.words.append({"text": "café", "confidence": 0.92})
json_str_utf8 = result.to_json(indent=2)
json_str_utf8 = json.dumps(json.loads(json_str_utf8), indent=2, ensure_ascii=False)

print("\n🌍 Pretty‑printed JSON with Unicode:")
print(json_str_utf8)
```

이제 출력은 이스케이프된 형태 대신 **café**를 보여줍니다. 이는 나중에 **convert json to dict**할 때 필수적이며, 딕셔너리는 올바른 Unicode 문자열을 포함하게 됩니다.

---

## 단계 6: 예쁘게 출력된 JSON 저장 및 재로드 (선택 사항)

때때로 포맷된 JSON을 파일에 저장해 두고 나중에 확인하고 싶을 수 있습니다.

```python
# Step 6: Write pretty JSON to a file
with open("ocr_result_pretty.json", "w", encoding="utf-8") as f:
    f.write(json_str_utf8)

# Later you can read it back and still have a dict
with open("ocr_result_pretty.json", "r", encoding="utf-8") as f:
    loaded_dict = json.load(f)   # <-- load json string python from file
print("\n📂 Loaded back from file, type:", type(loaded_dict))
```

파일에는 깔끔하게 들여쓰기된 JSON이 들어가며, `json.load`가 자동으로 이를 딕셔너리로 파싱합니다.

---

## 단계 7: 전체 합치기 – 단일 파일 솔루션

아래는 논의된 모든 단계를 포함한 독립 실행형 스크립트입니다. `pretty_json_demo.py`라는 파일에 넣고 실행해 보세요.

```python
#!/usr/bin/env python3
"""
Complete example: pretty print JSON Python, convert JSON to dict,
and load JSON string Python for further processing.
"""

import json

# ----------------------------------------------------------------------
# Mock OCR engine – replace with your real engine when ready
# ----------------------------------------------------------------------
class MockResult:
    def __init__(self):
        self.words = [
            {"text": "Hello", "confidence": 0.98},
            {"text": "World", "confidence": 0.95},
        ]

    def to_json(self, indent=None, ensure_ascii=True):
        # Produce a JSON string; indent triggers pretty printing
        return json.dumps({"words": self.words}, indent=indent, ensure_ascii=ensure_ascii)

# ----------------------------------------------------------------------
# Main workflow
# ----------------------------------------------------------------------
def main():
    # Step 1: Get the result object (real code would call engine.recognize())
    result = MockResult()

    # Step 2: Pretty print JSON Python
    json_str = result.to_json(indent=2)          # pretty print JSON Python
    print("🔍 Pretty‑printed JSON:")
    print(json_str)

    # Step 3: Load JSON string Python → dict
    result_dict = json.loads(json_str)          # load json string python
    print("\n✅ Dictionary type:", type(result_dict))

    # Step 4: Iterate over words
    print("\n🗣️ Words with confidence:")
    for word in result_dict.get("words", []):
        print(f'{word.get("text", "<missing>")} (conf: {word.get("confidence", 0)})')

    # Step 5: Demonstrate Unicode handling
    result.words.append({"text": "café", "confidence": 0.92})
    json_utf8 = result.to_json(indent=2, ensure_ascii=False)
    print("\n🌍 Unicode‑friendly pretty JSON:")
    print(json_utf8)

    # Step 6: Save to file and reload
    with open("pretty_output.json", "w", encoding="utf-8") as f:
        f.write(json_utf8)

    with open("pretty_output.json", "r", encoding="utf-8") as f:
        reloaded = json.load(f)                 # load json string python from file
    print("\n📂 Reloaded dict, size:", len(reloaded.get("words", [])))

if __name__ == "__main__":
    main()
```

실행:

```bash
python pretty_json_demo.py
```

예쁘게 출력된 JSON, 딕셔너리 타입, 각 단어와 신뢰도, 그리고 `pretty_output.json`에 저장된 Unicode 친화적 버전을 확인할 수 있습니다.  

**이것이 전체 흐름**입니다—원시 OCR 출력부터 깔끔하고 조작 가능한 Python 딕셔너리까지.

---

## 자주 묻는 질문 (FAQs)

| Question | Answer |
|----------|--------|
| **외부 라이브러리가 필요합니까?** | 아니요. 내장 `json` 모듈이 예쁘게 출력과 로딩을 모두 처리합니다. |
| **JSON이 너무 크면 어떻게 해야 하나요?** | `json.dump`를 파일 핸들과 함께 사용하여 전체를 메모리에 로드하지 않도록 하세요; 여전히 `indent`를 설정해 예쁜 파일을 만들 수 있습니다. |
| **키를 정렬할 수 있나요?** | 예—`json.dumps`에 `sort_keys=True`를 추가하면 결정적인 순서가 되며, diff 기반 테스트에 도움이 됩니다. |
| **잘못된 JSON을 어떻게 처리하나요?** | `json.loads`를 `try/except json.JSONDecodeError` 블록으로 감싸고 문제 문자열을 로그에 기록하세요. |
| **더 빠른 대안이 있나요?** | 대용량 페이로드의 경우 `orjson`이나 `ujson` 같은 라이브러리가 더 빠르지만, `indent`를 지원하지는 **out‑of‑** |

## 다음에 배워야 할 내용은?

다음 튜토리얼들은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 리소스는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하는 데 도움을 줍니다.

- [이미지 인식에서 JSON 결과를 얻기 위한 Aspose OCR 사용 방법](/ocr/english/net/text-recognition/get-result-as-json/)
- [이미지 인식에서 JSON 결과를 얻기 위한 Aspose OCR 사용 방법 (스페인어)](/ocr/spanish/net/text-recognition/get-result-as-json/)
- [이미지 인식에서 JSON 결과를 얻기 위한 Aspose OCR 사용 방법 (독일어)](/ocr/german/net/text-recognition/get-result-as-json/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}