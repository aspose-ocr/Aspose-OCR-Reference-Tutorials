---
date: 2026-02-12
description: Aprenda a fazer OCR de texto em imagens com seleção de idioma usando
  Aspose.OCR para Java. Este guia passo a passo cobre extração de texto em Java, correção
  de inclinação de OCR e muito mais.
linktitle: How to OCR Image Text with Language Using Aspose.OCR
second_title: Aspose.OCR Java API
title: Como fazer OCR de texto em imagem com idioma usando Aspose.OCR
url: /pt/java/ocr-operations/perform-ocr-language-selection/
weight: 11
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR de texto em imagem com idioma usando Aspose.OCR

## Introdução

Extrair texto de arquivos de imagem é uma necessidade comum, seja ao digitalizar documentos escaneados, processar recibos ou criar arquivos pesquisáveis. Neste tutorial, percorreremos um exemplo completo e prático que demonstra **como fazer OCR de texto em imagem** com uma configuração de idioma específica, para que você possa integrar OCR confiável em suas aplicações Java hoje. Você também verá como lidar com correção de inclinação (skew) e reconhecimento baseado em regiões para obter a máxima precisão.

## Respostas Rápidas
- **Qual biblioteca realiza OCR em Java?** Aspose.OCR for Java  
- **Qual configuração seleciona o idioma?** `settings.setLanguage(Language.Eng)` (ou qualquer idioma suportado)  
- **Preciso de licença para desenvolvimento?** Uma licença de avaliação gratuita funciona para testes; uma licença comercial é necessária para produção.  
- **Posso limitar o OCR a uma região da imagem?** Sim, use `RecognitionSettings.setRecognitionAreas()` com retângulos.  
- **Qual é o tempo de execução típico?** Alguns segundos por página em um laptop padrão, dependendo do tamanho da imagem e da complexidade do idioma.

## Como fazer OCR de texto em imagem com seleção de idioma
Nesta seção respondemos à pergunta central **como fazer OCR** de uma imagem quando você conhece o idioma do texto. Selecionar o idioma correto melhora drasticamente a precisão do reconhecimento, pois o motor OCR pode aplicar dicionários e modelos de caracteres específicos do idioma.

### Por que isso importa
- **Maior precisão** – modelos específicos de idioma reduzem erros de reconhecimento.  
- **Aumento de desempenho** – o motor ignora verificações de idiomas desnecessárias.  
- **Melhor tratamento de diacríticos** – francês, espanhol, alemão etc. são reconhecidos corretamente quando o enum `Language` correspondente é usado.

## O que é “extrair texto de imagem”?
Extrair texto de imagem (OCR) converte a representação visual de caracteres em cadeias de texto legíveis por máquina. Isso permite buscas, análises e fluxos de extração de dados que, de outra forma, exigiriam transcrição manual.

## Por que usar Aspose.OCR com seleção de idioma?
- **Suporte multilíngue** – escolha o(s) idioma(s) exato(s) presente(s) na sua imagem para melhorar a precisão.  
- **Controle refinado** – ajuste a inclinação, defina áreas de reconhecimento e configure o comportamento de auto‑skew.  
- **API pura em Java** – sem dependências nativas, fácil de integrar em qualquer projeto Java.  
- **Dados de resultado ricos** – obtenha texto puro, JSON, retângulos delimitadores e avisos em uma única chamada.

## Pré-requisitos

Antes de começar, certifique‑se de que você tem:

- **Java Development Kit (JDK)** instalado (JDK 8 ou superior).  
- Biblioteca **Aspose.OCR for Java** – faça o download no site oficial [here](https://reference.aspose.com/ocr/java/).  
- Um arquivo de imagem que contenha o texto que você deseja extrair, por exemplo, `p3.png`.

## Importar Pacotes

No seu arquivo fonte Java, inclua as classes necessárias do Aspose.OCR e as utilidades padrão do Java:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.Language;
import com.aspose.ocr.License;
import com.aspose.ocr.RecognitionResult;
import com.aspose.ocr.RecognitionSettings;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Guia passo a passo

### Etapa 1: Configurar seu diretório de documentos

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";
```

Substitua `"Your Document Directory"` pelo caminho absoluto onde `p3.png` está localizado.

### Etapa 2: Definir o caminho da imagem

```java
// The image path
String file = dataDir + "p3.png";
```

Certifique‑se de que a variável `file` aponta para a imagem exata que você pretende processar.

### Etapa 3: Criar instância da API Aspose.OCR

```java
// Create API instance
AsposeOCR api = new AsposeOCR();
```

O objeto `AsposeOCR` fornece acesso a todas as operações de OCR.

### Etapa 4: Definir opções de reconhecimento (seleção de idioma)

```java
// Set recognition options
RecognitionSettings settings = new RecognitionSettings();
settings.setAutoSkew(false);
ArrayList<Rectangle> rectangles = new ArrayList<Rectangle>();
rectangles.add(new Rectangle(90, 186, 775, 95));
settings.setRecognitionAreas(rectangles);
settings.setSkew(0.5);
settings.setLanguage(Language.Eng);
```

Aqui nós:

1. Desativamos o auto‑skew porque fornecemos um valor de inclinação manual.  
2. Definimos uma região retangular (`RecognitionAreas`) para limitar o OCR à parte da imagem que realmente contém texto.  
3. Definimos o **idioma** para Inglês (`Language.Eng`). Altere para `Language.Fra`, `Language.Spa`, etc., conforme a imagem de origem.

### Etapa 5: Executar OCR e recuperar resultados

```java
// Get result object
RecognitionResult result = null;
try {
    result = api.RecognizePage(file, settings);
} catch (IOException e) {
    e.printStackTrace();
}
```

A chamada `RecognizePage` executa o motor OCR usando a imagem e as configurações definidas. O resultado é armazenado em um objeto `RecognitionResult`.

### Etapa 6: Imprimir e utilizar resultados

```java
// Print result
System.out.println("Result: \n" + result.recognitionText + "\n\n");
for (String n : result.recognitionAreasText) {
    System.out.println(n);
}
for (Rectangle n : result.recognitionAreasRectangles) {
    System.out.println(n.height + ":" + n.width + ":" + n.x + ":" + n.y);
}
System.out.println("\nJSON:" + result.GetJson());
System.out.println("Angle:" + result.skew);
for (String n : result.warnings) {
    System.out.println(n);
}

System.out.println("OCROperationWithLanguageSelection: execution complete");
```

A saída no console mostra:

- O texto completo extraído (`recognitionText`).  
- Texto para cada retângulo definido (`recognitionAreasText`).  
- Coordenadas dos retângulos delimitadores.  
- Uma representação JSON para fácil processamento posterior.  
- Ângulo de inclinação detectado e quaisquer avisos.

Agora você pode alimentar `result.recognitionText` na sua lógica de negócios — armazená‑lo, indexá‑lo ou enviá‑lo para outro serviço.

## Problemas comuns e soluções

| Problema | Causa | Correção |
|----------|-------|----------|
| **Caracteres estranhos** | Idioma errado selecionado | Defina o enum `Language` correto (ex.: `Language.Fra` para francês). |
| **Nenhum texto retornado** | Área de reconhecimento não cobre o texto | Ajuste as coordenadas do `Rectangle` ou remova `RecognitionAreas` para processar a imagem inteira. |
| **Desempenho lento** | Imagem muito grande ou alta resolução | Reduza a escala da imagem antes do OCR ou aumente a alocação de memória para a JVM. |
| **Avisos sobre formato não suportado** | Formato da imagem não reconhecido | Converta a imagem para PNG, JPEG ou TIFF antes do processamento. |

## Perguntas Frequentes

**P: Posso reconhecer múltiplos idiomas em uma única chamada de OCR?**  
R: Sim. Use `settings.setLanguage(Language.Eng | Language.Fra)` para habilitar o reconhecimento multilíngue.

**P: Quais formatos de imagem o Aspose.OCR suporta?**  
R: PNG, JPEG, BMP, TIFF, GIF e vários outros. Basta fornecer o caminho correto do arquivo.

**P: Existe um limite de tamanho para a imagem?**  
R: Não há um limite rígido, mas imagens muito grandes aumentam o uso de memória e o tempo de processamento. Considere redimensionar arquivos grandes.

**P: Como obtenho uma licença de produção?**  
R: Compre uma licença no site da Aspose e aplique‑a via a classe `License`, conforme mostrado na documentação da Aspose.

**P: Posso extrair texto de uma página PDF diretamente?**  
R: Não diretamente com Aspose.OCR. Converta a página PDF em uma imagem primeiro (por exemplo, usando Aspose.PDF) e então execute o OCR.

## Conclusão

Agora você viu como **extrair texto de imagem** usando Aspose.OCR para Java, selecionando o idioma adequado e limitando o reconhecimento a regiões específicas. Essa abordagem oferece OCR preciso e de alto desempenho, que pode ser incorporado a qualquer fluxo de trabalho baseado em Java — de sistemas de gerenciamento de documentos a pipelines de captura de dados. Pronto para avançar? Experimente trocar o enum de idioma, teste diferentes áreas de reconhecimento e integre os resultados na lógica da sua própria aplicação.

---

**Last Updated:** 2026-02-12  
**Tested With:** Aspose.OCR 24.11 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}