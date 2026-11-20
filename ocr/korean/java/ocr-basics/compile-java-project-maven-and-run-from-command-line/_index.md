---
category: general
date: 2026-10-18
description: Maven clean, compile, exec 명령을 사용하여 명령줄에서 Java 프로젝트를 컴파일하고 실행합니다. Java
  애플리케이션을 효율적으로 빌드하고 실행하는 방법을 배워보세요.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: ko
lastmod: 2026-10-18
og_description: 단계별 가이드를 통해 Maven으로 Java 프로젝트를 컴파일하고 명령줄에서 실행하세요. Maven clean, compile,
  run을 마스터하여 Java 애플리케이션을 빌드하고 실행합니다.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Java 프로젝트 Maven 컴파일 – 명령줄에서 실행
schemas:
- author: Aspose
  dateModified: '2026-10-18'
  description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  headline: Compile java project maven and run from command line
  type: TechArticle
- description: Compile java project maven and run from command line using Maven clean,
    compile, and exec commands. Learn how to build and run java app efficiently.
  name: Compile java project maven and run from command line
  steps:
  - name: '**Missing `exec-maven-plugin`**'
    text: '**Missing `exec-maven-plugin`**'
  - name: '**Incorrect classpath**'
    text: '**Incorrect classpath**'
  - name: '**Using the wrong JDK version**'
    text: '**Using the wrong JDK version**'
  - name: '**Shell quoting problems**'
    text: '**Shell quoting problems**'
  type: HowTo
tags:
- Maven
- Java
- Command line
title: Maven으로 Java 프로젝트를 컴파일하고 명령줄에서 실행하기
url: /ko/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Maven으로 Java 프로젝트 컴파일 및 명령줄에서 실행하기

터미널에서 **compile java project maven**을 수행하고 결과 클래스를 직접 실행해야 한다면, 이 가이드가 정확히 어떻게 하는지 보여줍니다. 튜토리얼이 끝날 때쯤에는 오래된 아티팩트를 정리하고, 소스 코드를 컴파일하며, 단일 Maven 명령 체인을 사용해 **execute java class command line**을 수행할 수 있게 됩니다.

이 튜토리얼은 Maven으로 **build and run java app**을 수행하는 데 필요한 모든 것을 다루며, 필수 플러그인, 일반적인 함정, Windows 및 Unix 기반 셸에 대한 팁을 포함합니다. 외부 문서는 필요하지 않으며, 아래 단계만 따라 하면 됩니다.

## 사전 요구 사항

* Java Development Kit (JDK) 8 이상이 설치되어 있고 `JAVA_HOME`이 설정되어 있음.
* Apache Maven 3.6 이상이 `PATH`에 포함되어 있음.
* `pom.xml` 파일과 `public static void main(String[] args)` 메서드를 가진 Java 클래스를 포함하는 Maven 프로젝트 (예시 클래스는 `com.aspose.ocr.examples.SimpleOcrDemo`).

## Maven으로 Java 프로젝트 컴파일

첫 번째 단계는 이전에 컴파일된 클래스와 기타 빌드 아티팩트를 제거하는 것입니다. `mvn clean`을 실행하면 새로 시작할 수 있으며, 오래된 바이트코드가 런타임 오류를 일으키는 것을 방지합니다.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*왜 clean?* Maven은 컴파일된 클래스를 `target/`에 저장합니다. clean 단계을 건너뛰면 오래된 `.class` 파일이 남아 컴파일 문제를 숨길 수 있으며, 특히 패키지 이름을 리팩터링한 후에 그렇습니다.

## 명령줄에서 Java 클래스 실행

clean을 수행한 후, 소스 파일을 컴파일합니다. Maven의 `compile` 단계는 모든 `src/main/java` 소스를 바이트코드로 변환하고 결과를 `target/classes`에 배치합니다.

```bash
# Step 2: Compile the source code
mvn compile
```

이제 **maven compile source code** 출력이 실행 준비가 되었습니다. 다음 명령은 별도의 JAR 없이 컴파일된 클래스를 실행합니다.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

`exec:java` 목표는 **maven clean compile run** 플러그인의 일부로, 지정된 클래스를 컴파일된 출력 디렉터리에서 직접 실행합니다. 이는 개발 중에 **execute java class command line**을 수행하는 가장 빠른 방법입니다.

### 예상 출력

데모가 성공적으로 실행되면 다음과 유사한 출력이 표시됩니다.

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

`ClassNotFoundException`이 발생하면, 완전한 클래스 이름을 다시 확인하고 `src/main/java` 아래에 존재하는지 확인하십시오.

## Maven clean compile run 워크플로우

세 개의 명령을 함께 사용하면 간결하고 반복 가능한 워크플로우가 생성됩니다.

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*왜 체인으로 연결하나요?* 단계들을 결합하면 **Enter** 키를 세 번 누를 필요가 없으며, 단계 누락 가능성을 줄입니다. Maven은 나타나는 순서대로 단계를 실행하여 실행 전에 깨끗한 빌드를 보장합니다.

### 원활한 워크플로우를 위한 팁

| Tip | Description |
|-----|-------------|
| **프로파일 사용** | `clean`, `compile`, `exec:java`을 하나로 묶는 Maven 프로파일을 정의하여 전체 체인을 입력하는 대신 `mvn demo`만 실행할 수 있습니다. |
| **JVM 옵션 추가** | 메모리 집약적인 애플리케이션을 위해 힙 크기를 늘리려면 `-Dexec.args="-Xmx512m"`을 전달합니다. |
| **크로스‑플랫폼** | Windows에서는 `mvn.cmd`를, Unix 셸에서는 `mvn`을 사용합니다. 동일한 명령이 두 환경 모두에서 동작합니다. |

## Maven으로 Java 앱 빌드 및 실행

배포 가능한 아티팩트를 원한다면, Maven이 컴파일된 클래스를 실행 가능한 JAR로 패키징하도록 하고, 표준 `java -jar` 명령으로 실행할 수 있습니다:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

이 방법은 Maven이 설치되지 않은 서버에서 **build and run java app**을 해야 할 때 유용합니다. 하지만 빠른 개발을 위해서는 **maven clean compile run** 순서가 패키징 단계를 건너뛰기 때문에 더 빠릅니다.

## Maven compile source code – 일반적인 함정

명령은 간단하지만, 개발자들은 종종 다음과 같은 문제에 직면합니다:

1. **Missing `exec-maven-plugin`**  
   Maven이 `exec:java` 목표를 찾지 못하면 `pom.xml`에 플러그인을 추가하십시오:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.codehaus.mojo</groupId>
         <artifactId>exec-maven-plugin</artifactId>
         <version>3.1.0</version>
         <configuration>
           <mainClass>com.aspose.ocr.examples.SimpleOcrDemo</mainClass>
         </configuration>
       </plugin>
     </plugins>
   </build>
   ```

2. **Incorrect classpath**  
   Maven은 `target/classes`에 컴파일합니다. 파일을 수동으로 이동하거나 기본 출력 디렉터리를 변경하면 `exec:java` 목표가 클래스를 찾지 못할 수 있습니다. 특별한 이유가 없는 한 기본 레이아웃을 유지하십시오.

3. **Using the wrong JDK version**  
   Maven은 `JAVA_HOME`에서 JDK를 상속합니다. JDK 11 소스 코드를 컴파일하고 JDK 8에서 실행하면 `UnsupportedClassVersionError`가 발생합니다. `java -version` 및 `mvn -v`로 JDK 버전을 확인하십시오.

4. **Shell quoting problems**  
   Unix에서는 특수 문자가 포함된 경우 `-Dexec.mainClass` 값을 작은 따옴표로 감싸세요:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   Windows에서는 큰 따옴표를 사용하면 정상적으로 동작합니다.

이러한 사항들을 해결하면 어떤 환경에서도 **execute java class command line**을 안정적으로 수행할 수 있습니다.

## 전문가 팁: 스크립트로 자동화

데모를 자주 재빌드하는 팀을 위해 작은 셸 스크립트 또는 배치 스크립트를 만들 수 있습니다:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

스크립트를 실행 가능하게(`chmod +x run-demo.sh`) 만든 뒤 `./run-demo.sh`를 실행하십시오. 이렇게 하면 입력 오류를 방지하고 모든 개발자가 정확히 **maven clean compile run** 순서를 따르게 됩니다.

## 결론

이제 **compile java project maven**을 수행하고 Maven의 clean, compile, exec 목표를 사용해 즉시 **execute java class command line**을 수행하는 방법을 알게 되었습니다. 단계별 워크플로우는 새 빌드를 보장하고 오래된 아티팩트를 제거하며, 단일 명령줄로 **build and run java app**을 할 수 있게 합니다.  

다음과 같은 내용을 탐색해 볼 수 있습니다:

* 배포용 uber‑JAR를 생성하기 위해 **shade plugin** 추가
* 다양한 환경(dev, test, prod)을 위한 Maven 프로파일 구성
* 컴파일 단계 전에 `mvn test`로 단위 테스트 통합

이러한 변형을 실험해 보면서 워크플로우를 프로젝트에 맞게 적용하면 Windows, macOS, Linux에서 동작하는 견고하고 반복 가능한 빌드 파이프라인을 구축할 수 있습니다. 즐거운 코딩 되세요!

## 다음에 배워야 할 내용은?

다음 튜토리얼은 이 가이드에서 시연한 기술을 기반으로 하는 밀접한 관련 주제를 다룹니다. 각 자료는 완전한 코드 예제와 단계별 설명을 포함하여 추가 API 기능을 마스터하고 프로젝트에서 대체 구현 방식을 탐색하도록 돕습니다.

- [Java에서 OCR 사용 방법 – 완전한 단계별 가이드](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Java로 이미지에서 OCR 실행 – 완전한 Aspose OCR 가이드](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Java에서 Aspose OCR로 OCR 수행 방법 – 단계별 가이드](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}