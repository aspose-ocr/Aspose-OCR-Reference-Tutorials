---
category: general
date: 2026-02-17
description: Aprenda a usar OCR em Java para reconhecer texto de arquivos de imagem,
  extrair texto de recibos PNG e converter o recibo para JSON com o Aspose OCR.
draft: false
keywords:
- how to use OCR
- recognize text from image
- extract text from png
- convert receipt to json
language: pt
og_description: Guia passo a passo sobre como usar OCR em Java para reconhecer texto
  de imagens, extrair texto de recibos em PNG e converter o recibo em JSON.
og_title: Como usar OCR em Java – Reconhecer texto de uma imagem
tags:
- OCR
- Java
- Aspose
- Image Processing
title: Como usar OCR em Java – Reconheça texto de uma imagem rapidamente
url: /pt/java/ocr-operations/how-to-use-ocr-in-java-recognize-text-from-image-quickly/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Usar OCR em Java – Reconheça Texto de Imagem Rapidamente

Já se perguntou **como usar OCR** para extrair texto de uma foto de um recibo? Talvez você já tenha experimentado algumas ferramentas online, apenas para acabar com caracteres embaralhados ou um formato que não consegue analisar. A boa notícia é que, com algumas linhas de código Java, você pode **reconhecer texto de imagem**, **extrair texto de PNG** de recibos e até **converter recibo para JSON** para processamento posterior.  

Neste tutorial vamos percorrer todo o fluxo – desde licenciar a biblioteca Aspose OCR até obter um payload JSON limpo que você pode inserir em um banco de dados ou em um modelo de machine‑learning. Sem enrolação, apenas um exemplo prático e executável que você pode copiar‑colar no seu IDE. Ao final, você terá um programa autônomo que recebe `receipt.png` e gera uma string JSON pronta para uso.

## O que Você Precisa

- **Java Development Kit (JDK) 8+** – qualquer versão recente funciona.  
- Biblioteca **Aspose OCR for Java** (o artefato Maven é `com.aspose:aspose-ocr`).  
- Um **arquivo de licença Aspose OCR válido** (`Aspose.OCR.lic`). O trial gratuito serve para testes, mas uma licença adequada remove as limitações de avaliação.  
- Um arquivo de imagem (PNG, JPEG, etc.) que contenha o texto que você deseja ler – vamos chamá‑lo de `receipt.png` e colocá‑lo em uma pasta conhecida.  
- Seu IDE favorito (IntelliJ IDEA, Eclipse, VS Code…) – escolha livremente.

> **Dica de especialista:** Mantenha seu arquivo de licença fora da pasta de código‑fonte e faça referência a ele via caminho absoluto ou relativo para evitar comitar o arquivo ao controle de versão.

Agora que os pré‑requisitos estão claros, vamos mergulhar no código propriamente dito.

## Como Usar OCR – Etapas Principais

A seguir, uma visão geral de alto nível das ações que vamos executar:

1. **Carregar a biblioteca Aspose OCR** e aplicar sua licença.  
2. **Criar uma instância `OcrEngine`** – este é o motor que faz o trabalho pesado.  
3. **Preparar um objeto `OcrInput`** apontando para a imagem que você quer processar.  
4. **Chamar `recognize` com `ResultFormat.JSON`** para obter uma representação JSON do texto extraído.  
5. **Tratar a saída JSON** – imprimir, gravar em arquivo ou analisar mais a fundo.

Cada etapa é explicada em detalhes nas seções a seguir.

## Etapa 1 – Instalar Aspose OCR e Aplicar Sua Licença

Primeiro, adicione a dependência Aspose OCR ao seu `pom.xml` se estiver usando Maven:

```xml
<dependency>
    <groupId>com.aspose</groupId>
    <artifactId>aspose-ocr</artifactId>
    <version>23.12</version> <!-- Check Maven Central for the latest version -->
</dependency>
```

Agora, no seu código Java, carregue a licença. Esta etapa é essencial; sem ela a biblioteca roda em modo de avaliação e pode inserir marcas d’água na saída.

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

> **Por que isso importa:** O objeto `License` informa ao motor OCR que você está autorizado a usar o conjunto completo de recursos, que inclui reconhecimento de alta precisão e exportação JSON. Pular esta etapa ainda permitirá **reconhecer texto de imagem**, mas os resultados podem ser limitados.

## Etapa 2 – Criar a Instância do Motor OCR

A classe `OcrEngine` é o ponto de entrada para todas as operações de OCR. Pense nela como o “cérebro” que lê os pixels e decide quais caracteres eles representam.

```java
import com.aspose.ocr.*;

public class OcrEngineFactory {
    public static OcrEngine createEngine() {
        // No special configuration needed for basic usage
        return new OcrEngine();
    }
}
```

Você pode personalizar o motor (por exemplo, definir idioma, habilitar deskew) mais tarde se seus recibos contiverem scripts não latinos ou estiverem escaneados em ângulo. Para a maioria dos recibos dos EUA, as configurações padrão funcionam muito bem.

## Etapa 3 – Carregar a Imagem que Você Quer Processar

Agora vamos apontar o motor OCR para o arquivo que contém o recibo. A classe `OcrInput` pode aceitar múltiplas imagens, mas para este tutorial vamos mantê‑la simples com um único PNG.

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

Se precisar **extrair texto de PNG** em lote, basta chamar `input.add()` repetidamente ou passar uma lista de caminhos de arquivos.

## Etapa 4 – Reconhecer Texto e Converter Recibo para JSON

Aqui está o coração do tutorial. Pedimos ao motor que reconheça o texto e solicitamos o resultado no formato JSON. A flag `ResultFormat.JSON` faz todo o trabalho pesado para nós.

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

O payload JSON inclui cada linha reconhecida, sua caixa delimitadora, pontuação de confiança e o texto bruto. Essa estrutura torna trivial **converter recibo para JSON** e então enviá‑lo a qualquer API downstream.

## Etapa 5 – Juntar Tudo e Executar o Programa

A seguir está a classe Java completa, pronta para ser executada, que une todas as partes. Salve‑a como `JsonExportDemo.java` (ou outro nome de sua preferência) e execute‑a pelo seu IDE ou linha de comando.

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

### Saída Esperada

Executar o programa imprime uma string JSON semelhante ao exemplo abaixo (o conteúdo exato depende do seu recibo):

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

Agora você pode enviar esse JSON para um banco de dados, um endpoint REST ou um pipeline de análise de dados. A etapa **converter recibo para JSON** já está feita para você.

## Perguntas Frequentes e Casos de Borda

### E se a imagem estiver rotacionada?

Aspose OCR detecta e corrige rotações leves automaticamente. Para imagens muito inclinadas, chame `engine.getImagePreprocessingOptions().setDeskew(true)` antes do reconhecimento.

### Como lidar com múltiplos idiomas?

Use `engine.getLanguage()` para definir o idioma desejado, por exemplo `engine.setLanguage(Language.FRENCH)`. Isso é útil quando você precisa **reconhecer texto de imagem** que contém recibos multilíngues.

### Posso gerar texto simples em vez de JSON?

Claro. Substitua `ResultFormat.JSON` por `ResultFormat.TEXT` e chame `result.getText()`.

### Existe como limitar o OCR a uma região específica?

Sim—use `ocrInput.add(imagePath, new Rectangle(x, y, width, height))` para focar na área do recibo, o que pode melhorar velocidade e precisão.

## Dicas Profissionais para OCR Pronto para Produção

- **Cache o objeto de licença** se você estiver processando muitos arquivos em um loop; criá‑lo repetidamente adiciona overhead.  
- **Processamento em lote**: carregue todos os caminhos de recibos em um único `OcrInput` e chame `recognize` uma única vez. O JSON conterá um array de páginas, cada uma com suas linhas.  
- **Valide o JSON**: depois de obter a string, parseie‑a com uma biblioteca como Jackson para garantir que está bem‑formada antes de armazená‑la.  
- **Monitore a confiança**: o JSON inclui um campo `confidence` por linha. Filtre linhas abaixo de um limiar (ex.: 0.85) para evitar dados lixo.  
- **Proteja sua licença**: armazene `Aspose.OCR.lic` em um cofre seguro ou variável de ambiente, especialmente em implantações na nuvem.

## Conclusão

Cobrimos **como usar OCR** em Java para **reconhecer texto de imagem**, **extrair texto de PNG** de recibos e **converter recibo para JSON** — tudo com um exemplo conciso, de ponta a ponta. As etapas são diretas, o código é totalmente executável e a saída JSON fornece uma representação estruturada pronta para qualquer sistema downstream.

A seguir, você pode explorar cenários mais avançados: enviar o JSON para Apache Kafka para processamento em tempo real, aplicar expressões regulares para extrair totais de itens, ou integrar com um serviço OCR na nuvem para escalabilidade. Seja qual for o caminho, os fundamentos que você acabou de aprender permanecerão os mesmos.

Tem dúvidas ou encontrou algum problema ao tentar isso? Deixe um comentário abaixo e vamos solucionar juntos. Boa codificação e aproveite para transformar aquelas imagens bagunçadas de recibos em dados limpos e pesquisáveis!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}