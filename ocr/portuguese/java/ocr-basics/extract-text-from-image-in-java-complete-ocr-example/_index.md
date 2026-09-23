---
category: general
date: 2026-01-12
description: Extrair texto de imagem usando Aspose OCR em Java. Aprenda como extrair
  texto de uma imagem de fatura com um exemplo de OCR em Java e obtenha o texto OCR
  resultante.
draft: false
keywords:
- extract text from image
- how to extract text
- java ocr example
- process invoice image
- output ocr text
language: pt
og_description: Extrair texto de imagem usando Aspose OCR em Java. Este guia mostra
  como extrair texto de uma imagem de fatura, inclui um exemplo de OCR em Java e gera
  o texto OCR.
og_title: Extrair Texto de Imagem em Java – Exemplo Completo de OCR
tags:
- OCR
- Java
- Aspose
title: Extrair Texto de Imagem em Java – Exemplo Completo de OCR
url: /pt/java/ocr-basics/extract-text-from-image-in-java-complete-ocr-example/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagem em Java – Exemplo Completo de OCR

Já se perguntou como **extrair texto de imagem** sem perder a cabeça? Talvez você tenha uma pilha de faturas escaneadas e precise dos números rapidamente. Na minha experiência, a maneira mais fácil é deixar que uma biblioteca OCR dedicada faça o trabalho pesado. Este tutorial mostra *como extrair texto* de uma imagem de fatura típica usando Aspose OCR para Java, e ainda demonstra um **java ocr example** que gera o texto OCR que você pode encaminhar para seu sistema downstream.

Vamos percorrer tudo o que você precisa saber: desde a configuração do projeto, definição da região de interesse (ROI) que foca no cabeçalho e no valor total, até a impressão do texto extraído. Ao final, você será capaz de **process invoice image** arquivos automaticamente e recuperar texto limpo e pesquisável.

> **O que você receberá:** um programa Java pronto‑para‑executar, explicações claras de cada passo e dicas práticas para lidar com faturas do mundo real.

## Pré-requisitos

- Java Development Kit (JDK) 8 ou mais recente instalado.
- Maven ou Gradle para gerenciamento de dependências (exemplo Maven mostrado).
- Uma licença Aspose OCR para Java (a versão de avaliação gratuita funciona para testes).
- Uma imagem de fatura (`invoice.png`) colocada em um diretório conhecido.

Se algum desses itens lhe for desconhecido, não se preocupe — a maioria está a apenas um download de distância, e o código ainda compilará com a edição comunitária.

## Etapa 1: Configurar Seu Projeto Maven

Primeiro, crie um novo projeto Maven (ou adicione a um existente). No seu `pom.xml`, adicione a dependência Aspose OCR:

```xml
<!-- pom.xml -->
<dependencies>
    <dependency>
        <groupId>com.aspose</groupId>
        <artifactId>aspose-ocr</artifactId>
        <version>23.9</version> <!-- Use the latest version available -->
    </dependency>
</dependencies>
```

> **Dica profissional:** Mantenha o número da versão atualizado; lançamentos mais recentes costumam melhorar a precisão para fontes difíceis encontradas em faturas.

Depois de salvar o arquivo, execute `mvn clean install` para baixar a biblioteca para seu repositório local.

## Etapa 2: Carregar a Imagem da Fatura

Agora que a biblioteca está pronta, vamos escrever uma pequena classe Java. A primeira coisa que fazemos é criar uma instância `OcrEngine` e apontá‑la para a imagem que você deseja ler.

```java
import com.aspose.ocr.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {
        // Step 2: Load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png"); // <-- replace with your path
```

Por que criamos o engine **antes** de carregar a imagem? O engine contém configurações como idioma, DPI e ROI. Definir a imagem antecipadamente garante que essas configurações se apliquem ao arquivo exato que você está prestes a processar.

## Etapa 3: Definir Regiões de Interesse (ROI)

Faturas frequentemente contêm muito ruído — tabelas, logotipos e texto pequeno. Ao limitar o OCR apenas ao cabeçalho e ao valor total, você aumenta drasticamente tanto a velocidade quanto a precisão. Aspose permite descrever essas zonas com retângulos.

```java
        // Step 3: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Apply ROI to the engine
        engine.setRegion(region);
```

As coordenadas estão em pixels (`x`, `y`, `width`, `height`). Se suas faturas variam em tamanho, você pode calcular esses valores dinamicamente — talvez verificando as dimensões da imagem primeiro. Essa é uma boa extensão se você precisar de uma solução **process invoice image** que funcione em lotes.

## Etapa 4: Executar OCR nas Regiões Especificadas

Com a ROI configurada, o motor OCR pode focar sua atenção onde mais importa. O método `recognize()` retorna um `OcrResult` contendo o texto extraído.

```java
        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();
```

Nos bastidores, Aspose realiza várias etapas de pré‑processamento: binarização, remoção de ruído e segmentação de caracteres. Você não precisa chamar essas etapas manualmente — basta deixar `recognize()` fazer seu trabalho.

## Etapa 5: Exibir o Texto Extraído

Finalmente, imprimimos o texto no console. Em uma aplicação real, você pode armazená‑lo em um banco de dados, enviá‑lo para um pipeline de análise downstream ou até gerar um PDF pesquisável.

```java
        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

Ao executar o programa, você deverá ver algo como:

```
ROI text:
Acme Corp.
Invoice #12345
Date: 2025-12-31
Total Amount: $1,250.00
```

Se a saída parecer confusa, verifique novamente as coordenadas do retângulo ou aumente a resolução da imagem. Motores OCR adoram digitalizações nítidas e de alta DPI.

## Exemplo Completo Funcional

Abaixo está o arquivo Java completo e autocontido que você pode copiar‑colar em `src/main/java/RoiExample.java`. Nenhum trecho externo é necessário — tudo o que você precisa está aqui.

```java
import com.aspose.ocr.*;
import com.aspose.ocr.region.*;

public class RoiExample {
    public static void main(String[] args) throws Exception {

        // Step 1: Create the OCR engine and load the source image
        OcrEngine engine = new OcrEngine();
        engine.setImage("YOUR_DIRECTORY/invoice.png");

        // Step 2: Define the regions of interest (header and total amount)
        OcrRegion region = OcrRegion.builder()
                .addRectangle(0, 0, 800, 150)      // header area
                .addRectangle(0, 1200, 800, 200)   // total amount area
                .build();

        // Step 3: Apply the ROI configuration to the engine
        engine.setRegion(region);

        // Step 4: Run OCR on the specified regions
        OcrResult result = engine.recognize();

        // Step 5: Output the extracted text
        System.out.println("ROI text:");
        System.out.println(result.getText());
    }
}
```

> **Nota:** Substitua `YOUR_DIRECTORY` pelo caminho absoluto da sua imagem de fatura. Se estiver usando um caminho relativo, certifique‑se de que o diretório de trabalho corresponde ao local onde você executa o comando `java`.

## Perguntas Frequentes & Casos Limite

### E se o tamanho da fatura mudar?

Você pode calcular a ROI dinamicamente:

```java
int imgWidth = engine.getImage().getWidth();
int imgHeight = engine.getImage().getHeight();

int headerHeight = imgHeight / 10;
int totalHeight = imgHeight / 8;

OcrRegion region = OcrRegion.builder()
        .addRectangle(0, 0, imgWidth, headerHeight)
        .addRectangle(0, imgHeight - totalHeight, imgWidth, totalHeight)
        .build();
```

### Como lidar com múltiplos idiomas?

Aspose OCR suporta pacotes de idiomas. Basta definir o idioma antes de chamar `recognize()`:

```java
engine.setLanguage(OcrLanguage.Spanish); // or OcrLanguage.English, etc.
```

### E se o OCR retornar strings vazias?

Culposos típicos são:

- Baixa resolução da imagem (< 300 DPI). Aumente ou solicite digitalizações de qualidade superior.
- Fundos excessivamente escuros ou claros. Aplique um filtro simples de aumento de contraste antes do OCR.
- Coordenadas de ROI incorretas que perdem o texto completamente.

## Dicas para OCR Pronto para Produção

1. **Processamento em Lote:** Envolva a lógica em um loop que itere sobre um diretório de arquivos de fatura. Registre cada resultado para auditoria.
2. **Tratamento de Erros:** Capture `OcrException` para pular graciosamente imagens corrompidas sem interromper todo o trabalho.
3. **Desempenho:** Reutilize uma única instância `OcrEngine` em várias imagens; criar um novo engine por arquivo adiciona sobrecarga desnecessária.
4. **Validação:** Após a extração, execute uma verificação regex no valor total (`\$\d{1,3}(,\d{3})*(\.\d{2})?`) para garantir que o número pareça realista.

Implementar essas sugestões transforma um simples **java ocr example** em uma solução robusta e escalável para qualquer empresa que precise **process invoice image** arquivos de fatura todas as noites.

## Conclusão

Acabamos de cobrir como **extrair texto de imagem** em arquivos Java usando Aspose OCR, focando em um cenário prático de processamento de faturas. Ao definir uma região de interesse, executar o motor OCR e imprimir o **output OCR text**, você agora tem uma base sólida para construir pipelines automatizados de captura de dados.

Próximos passos? Tente expandir a ROI para incluir tabelas de itens, experimente diferentes configurações de idioma ou alimente as strings extraídas em uma biblioteca de geração de PDF para documentos pesquisáveis. O céu é o limite quando você combina OCR com ferramentas Java modernas.

Tem mais perguntas sobre **como extrair texto** de outros tipos de documentos, ou precisa de ajuda para ajustar a ROI em layouts incomuns? Deixe um comentário abaixo — feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}