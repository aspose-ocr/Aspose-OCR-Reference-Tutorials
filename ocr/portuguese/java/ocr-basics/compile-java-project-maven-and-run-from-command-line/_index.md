---
category: general
date: 2026-10-18
description: Compile o projeto Java Maven e execute a partir da linha de comando usando
  os comandos Maven clean, compile e exec. Aprenda como construir e executar o aplicativo
  Java de forma eficiente.
draft: false
images:
- PLACEHOLDER_URL/og-image.png
keywords:
- compile java project maven
- execute java class command line
- maven clean compile run
- build and run java app
- maven compile source code
language: pt
lastmod: 2026-10-18
og_description: Compile um projeto Java com Maven e execute-o a partir da linha de
  comando com um guia passo a passo. Domine maven clean compile run para construir
  e rodar o aplicativo Java.
og_image_alt: Terminal screenshot showing mvn clean compile exec commands
og_title: Compilar projeto Java Maven – executar a partir da linha de comando
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
title: Compilar projeto Java Maven e executar a partir da linha de comando
url: /pt/java/ocr-basics/compile-java-project-maven-and-run-from-command-line/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Compilar projeto Java Maven e executar a partir da linha de comando

Se você precisa **compilar projeto Java Maven** e lançar a classe resultante diretamente a partir de um terminal, este guia mostra exatamente como fazer. Ao final do tutorial você será capaz de limpar artefatos antigos, compilar o código-fonte e **executar classe Java na linha de comando** usando uma única cadeia de comandos Maven.

O tutorial cobre tudo o que você precisa saber para **construir e executar aplicativo Java** com Maven, incluindo plugins necessários, armadilhas comuns e dicas para shells baseados em Windows e Unix. Nenhuma documentação externa é necessária — basta seguir os passos abaixo.

## Pré-requisitos

* Java Development Kit (JDK) 8 ou mais recente instalado e `JAVA_HOME` configurado.
* Apache Maven 3.6+ disponível no seu `PATH`.
* Um projeto Maven que contém um `pom.xml` e uma classe Java com o método `public static void main(String[] args)` (para este exemplo a classe é `com.aspose.ocr.examples.SimpleOcrDemo`).

## Compilar projeto Java Maven

O primeiro passo é remover quaisquer classes compiladas anteriormente e outros artefatos de construção. Executar `mvn clean` garante um início limpo e impede que bytecode obsoleto cause erros em tempo de execução.

```bash
# Step 1: Clean previous build artifacts
mvn clean
```

*Por que limpar?* O Maven armazena as classes compiladas em `target/`. Se você pular a fase de limpeza, arquivos `.class` antigos podem permanecer e ocultar problemas de compilação, especialmente após refatorar nomes de pacotes.

## Executar classe Java na linha de comando

Após a limpeza, compile os arquivos-fonte. A fase `compile` do Maven traduz todas as fontes em `src/main/java` para bytecode e coloca os resultados em `target/classes`.

```bash
# Step 2: Compile the source code
mvn compile
```

Agora você tem uma saída de **compilação de código-fonte Maven** pronta para execução. O próximo comando executa a classe compilada sem precisar de um JAR separado.

```bash
# Step 3: Run the Simple OCR demo
mvn exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

O objetivo `exec:java` do plugin **maven clean compile run** lança a classe especificada diretamente do diretório de saída compilado. Esta é a maneira mais rápida de **executar classe Java na linha de comando** durante o desenvolvimento.

### Saída esperada

Quando a demonstração for executada com sucesso, você deverá ver algo semelhante a:

```
[INFO] Scanning for projects...
[INFO] ------------------------------------------------------------------------
[INFO] Building SimpleOCR Demo 1.0
[INFO] ------------------------------------------------------------------------
Hello, OCR world!
Processing completed in 1.23 seconds.
```

Se você receber uma `ClassNotFoundException`, verifique novamente o nome totalmente qualificado da classe e assegure que ela esteja sob `src/main/java`.

## Fluxo de trabalho Maven clean compile run

Juntando os três comandos, obtém-se um fluxo de trabalho compacto e repetível:

```bash
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

*Por que encadeá‑los?* Combinar as fases elimina a necessidade de pressionar **Enter** três vezes e reduz a chance de esquecer um passo. O Maven executará as fases na ordem em que aparecem, garantindo uma construção limpa antes da execução.

### Dicas para um fluxo de trabalho mais suave

| Dica | Descrição |
|-----|-------------|
| **Use um perfil** | Defina um profile Maven que agrupe `clean`, `compile` e `exec:java` para que você possa executar `mvn demo` em vez de digitar a cadeia completa. |
| **Adicionar opções JVM** | Passe `-Dexec.args="-Xmx512m"` para aumentar o tamanho do heap para aplicativos que consomem muita memória. |
| **Multiplataforma** | No Windows use `mvn.cmd` enquanto shells Unix usam `mvn`. O mesmo comando funciona em ambos os ambientes. |

## Construir e executar aplicativo Java com Maven

Se você prefere um artefato distribuível, pode deixar o Maven empacotar suas classes compiladas em um JAR executável e então executá‑lo com o comando padrão `java -jar`:

```bash
# Package the app into a JAR (includes dependencies if you use the shade plugin)
mvn clean package

# Run the packaged JAR
java -jar target/simple-ocr-demo-1.0.jar
```

Esta abordagem é útil quando você precisa **construir e executar aplicativo Java** em um servidor onde o Maven não está instalado. Contudo, para desenvolvimento rápido a sequência **maven clean compile run** é mais rápida porque pula a etapa de empacotamento.

## Compilação de código-fonte Maven – armadilhas comuns

Embora os comandos sejam simples, os desenvolvedores frequentemente encontram os seguintes problemas:

1. **Plugin `exec-maven-plugin` ausente**  
   Se o Maven não conseguir encontrar o objetivo `exec:java`, adicione o plugin ao seu `pom.xml`:

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

2. **Classpath incorreto**  
   O Maven compila para `target/classes`. Se você mover arquivos manualmente ou alterar o diretório de saída padrão, o objetivo `exec:java` pode não localizar sua classe. Mantenha o layout padrão a menos que tenha um motivo específico para alterá‑lo.

3. **Usando a versão errada do JDK**  
   O Maven herda o JDK de `JAVA_HOME`. Compilar código-fonte com JDK 11 e executar com JDK 8 causará `UnsupportedClassVersionError`. Verifique a versão do JDK com `java -version` e `mvn -v`.

4. **Problemas de aspas no shell**  
   No Unix, envolva o valor de `-Dexec.mainClass` em aspas simples se ele contiver caracteres especiais:  
   `mvn exec:java -Dexec.mainClass='com.example.Main'`.  
   No Windows, aspas duplas funcionam bem.

Ao abordar esses pontos, você pode **executar classe Java na linha de comando** de forma confiável em qualquer ambiente.

## Dica profissional: automatizar com um script

Para equipes que recompilam a demonstração com frequência, crie um pequeno script shell ou batch:

```bash
#!/usr/bin/env bash
# run-demo.sh – clean, compile, and execute the OCR demo
mvn clean compile exec:java -Dexec.mainClass="com.aspose.ocr.examples.SimpleOcrDemo"
```

Torne‑o executável (`chmod +x run-demo.sh`) e execute `./run-demo.sh`. Isso elimina erros de digitação e garante que cada desenvolvedor siga a sequência exata **maven clean compile run**.

## Conclusão

Agora você sabe como **compilar projeto Java Maven** e instantaneamente **executar classe Java na linha de comando** usando os objetivos clean, compile e exec do Maven. O fluxo de trabalho passo a passo garante uma construção limpa, elimina artefatos obsoletos e permite **construir e executar aplicativo Java** com uma única linha de comando.  

Em seguida, você pode explorar:

* Adicionar o **shade plugin** para produzir um uber‑JAR para implantação.  
* Configurar perfis Maven para diferentes ambientes (dev, test, prod).  
* Integrar testes unitários com `mvn test` antes da etapa de compilação.

Experimente essas variações para adaptar o fluxo de trabalho aos seus próprios projetos, e você terá um pipeline de construção robusto e repetível que funciona em Windows, macOS e Linux. Feliz codificação!

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como usar OCR em Java – Guia completo passo a passo](/ocr/english/java/ocr-operations/how-to-use-ocr-in-java-complete-step-by-step-guide/)
- [Executar OCR em imagem com Java – Guia completo da Aspose OCR](/ocr/english/java/ocr-operations/run-ocr-on-image-with-java-complete-aspose-ocr-guide/)
- [Como realizar OCR com Aspose OCR em Java – Guia passo a passo](/ocr/english/java/ocr-operations/how-to-perform-ocr-with-aspose-ocr-in-java-step-by-step-guid/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}