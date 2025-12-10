---
date: 2025-12-10
description: Aprenda a reconhecer texto a partir de imagens e extrair parágrafos de
  imagens usando Aspose.OCR para Java. Guia passo a passo com exemplos de código.
linktitle: Recognize Text from Image and Retrieve Text Area Rectangles
second_title: Aspose.OCR Java API
title: Reconhecer texto a partir de imagem e recuperar retângulos das áreas de texto
url: /pt/java/ocr-basics/get-rectangles-with-text-areas/
weight: 12
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Reconhecer Texto de Imagem e Recuperar Retângulos de Áreas de Texto

## Introdução

Se você precisa **recognize text from image** arquivos em uma aplicação Java, o Aspose.OCR for Java oferece uma maneira rápida e precisa de fazer isso. Neste tutorial vamos percorrer passo a passo as etapas necessárias para extrair parágrafos de uma imagem, obter os retângulos delimitadores de cada área de texto e imprimir essas coordenadas no console. Ao final, você entenderá por que essa abordagem funciona, como integrar a biblioteca e onde pode estendê‑la para seus próprios casos de uso.

## Respostas Rápidas
- **O que significa “recognize text from image”?** Significa converter caracteres visuais de uma foto em dados de string editáveis.  
- **Qual biblioteca lida com isso em Java?** Aspose.OCR for Java.  
- **Preciso de licença para desenvolvimento?** Uma licença temporária está disponível para testes; uma licença completa é necessária para produção.  
- **Posso extrair parágrafos em vez de palavras individuais?** Sim – use `AreasType.PARAGRAPHS` para obter retângulos ao nível de parágrafo.  
- **O código é compatível com Java 11+?** Absolutamente, a API funciona com Java 11 e versões posteriores.

## O que é “recognize text from image” no Aspose.OCR?
O método `RecognizePage` do Aspose.OCR analisa o bitmap, aplica algoritmos de OCR e devolve a string reconhecida. Quando você solicita áreas de texto, a biblioteca também calcula as coordenadas exatas do `Rectangle` para cada bloco de texto, facilitando a realce ou o processamento de seções específicas posteriormente.

## Por que usar Aspose.OCR para Java?
- **Alta precisão** – suporta múltiplos idiomas e fontes complexas.  
- **Integração fácil** – um único JAR adiciona funcionalidades completas de OCR.  
- **Saída flexível** – você pode recuperar texto bruto, HTML formatado ou retângulos precisos de áreas de texto.  
- **Thread‑safe** – adequado para ambientes de servidor de alto volume.

## Pré‑requisitos

- **Java Development Kit** (JDK 11 ou mais recente) instalado na sua máquina.  
- **Aspose.OCR for Java** library – faça o download no site oficial [here](https://releases.aspose.com/ocr/java/).  
- Uma IDE ou ferramenta de build (Maven/Gradle) para gerenciar a dependência do JAR.

## Importar Pacotes

No seu projeto Java, importe as classes necessárias:

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AreasType;
import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.License.SetLicense;
import com.aspose.ocr.examples.Utils;

import java.awt.*;
import java.io.IOException;
import java.util.ArrayList;
```

## Guia Passo a Passo

### Etapa 1: Configurar Seu Projeto
Crie um novo projeto Java (ou adicione a um existente) e coloque o JAR do Aspose.OCR no classpath. Se usar Maven, adicione a dependência conforme descrito no pacote de download.

### Etapa 2: Definir Diretório do Documento e Caminho da Imagem
Especifique onde sua imagem de exemplo está localizada:

```java
// The path to the documents directory.
String dataDir = "Your Document Directory";

// The image path
String imagePath = dataDir + "p3.png";
```

### Etapa 3: Criar Instância do Aspose.OCR
Instancie o motor de OCR:

```java
// Create Aspose.OCR instance
AsposeOCR api = new AsposeOCR();
```

### Etapa 4: Reconhecer Texto na Imagem
Chame `RecognizePage` para converter a foto em texto simples. Esta etapa demonstra a capacidade central de **recognize text from image**:

```java
try {
    // Recognize page by full path to file
    String result = api.RecognizePage(imagePath);
    System.out.println("Result: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

### Etapa 5: Obter Retângulos com Áreas de Texto
Agora recupere os retângulos delimitadores para cada parágrafo (ou outros tipos de área). É aqui que você **extract paragraphs from image** e obtém suas coordenadas:

```java
// Get rectangles with text areas in the image.
ArrayList<Rectangle> rectResult = api.getTextAreas(imagePath, AreasType.PARAGRAPHS, true);

// Print each text area rectangle
for (Rectangle r : rectResult) {
    System.out.println("Text area:" + r);
}
```

## Problemas Comuns & Solução de Problemas

| Sintoma | Causa Provável | Correção |
|---------|----------------|----------|
| `IOException` on `RecognizePage` | Caminho de arquivo incorreto ou permissão de leitura ausente | Verifique se `imagePath` aponta para um PNG/JPG existente e se o aplicativo tem acesso ao sistema de arquivos. |
| String de resultado vazia | Imagem de baixa qualidade ou idioma não suportado | Pré‑procese a imagem (aumente o contraste, binarize) ou especifique o idioma correto usando `api.setLanguage("eng")`. |
| Nenhum retângulo retornado | Uso do `AreasType` errado (ex.: `WORDS` quando se esperam parágrafos) | Troque para `AreasType.PARAGRAPHS` ou `AreasType.LINES`, conforme necessário. |

## Perguntas Frequentes

**Q: É o Aspose.OCR compatível com Java 11?**  
A: Sim, o Aspose.OCR funciona com Java 11 e versões posteriores.

**Q: Posso usar o Aspose.OCR em projetos pessoais e comerciais?**  
A: Sim, você pode utilizá‑lo em qualquer tipo de projeto. Para detalhes de licenciamento, visite [here](https://purchase.aspose.com/buy).

**Q: Como obtenho uma licença temporária para avaliação?**  
A: Você pode obter uma licença temporária [here](https://purchase.aspose.com/temporary-license/).

**Q: Onde encontro suporte da comunidade ou assistência oficial?**  
A: Para suporte e discussões, visite o [Aspose.OCR forum](https://forum.aspose.com/c/ocr/16).

**Q: O Aspose.OCR suporta multithreading?**  
A: Sim, a biblioteca é thread‑safe e pode ser usada em ambientes concorrentes para melhor desempenho.

## Conclusão

Neste tutorial você aprendeu como **recognize text from image** arquivos usando Aspose.OCR for Java, extrair parágrafos e recuperar os retângulos exatos que circundam cada bloco de texto. Essas funcionalidades permitem criar PDFs pesquisáveis, destacar texto em sobreposições de UI ou alimentar dados estruturados em processos subsequentes. Explore a API mais a fundo para personalizar configurações de idioma, lidar com diferentes formatos de imagem ou integrar com armazenamento em nuvem.

---

**Last Updated:** 2025-12-10  
**Tested With:** Aspose.OCR 23.10 for Java  
**Author:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}