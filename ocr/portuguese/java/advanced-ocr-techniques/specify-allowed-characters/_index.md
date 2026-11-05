---
date: 2026-05-24
description: Descubra como usar OCR com Aspose.OCR para Java, extrair texto de imagens,
  definir caracteres permitidos e aplicar uma licença temporária em minutos.
keywords:
- how to use OCR
- extract text from images
- how to apply license
- how to set characters
linktitle: Especificando caracteres permitidos no Aspose.OCR
schemas:
- author: Aspose
  dateModified: '2026-05-24'
  description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  headline: How to Use OCR – Extract Text from Images with Aspose.OCR
  type: TechArticle
- description: Discover how to use OCR with Aspose.OCR for Java, extract text from
    images, set allowed characters, and apply a temporary license in minutes.
  name: How to Use OCR – Extract Text from Images with Aspose.OCR
  steps:
  - name: Set Your Document Directory
    text: Choose a folder where OCR results and temporary files will be stored. This
      path is later used to locate the image you want to process.
  - name: Specify the Image Path
    text: Provide the full file system path or a class‑path resource location that
      points to the image you wish to analyse.
  - name: Create an Aspose.OCR Instance
    text: '`AsposeOCR` is the core engine that performs optical character recognition.
      Instantiate it with either a temporary or permanent license string.'
  - name: Perform OCR Recognition
    text: '`RecognizeLine` extracts a single line of text from the supplied image
      and returns it as a plain Java `String`. You can call this method repeatedly
      for multi‑line documents. > **Pro tip:** If you need to restrict the output
      to digits only (e.g., for invoice numbers), call `setAllowedCharacters("0123'
  type: HowTo
- questions:
  - answer: Visit the [temporary license page](https://purchase.aspose.com/temporary-license/)
      to request a trial key that removes evaluation watermarks.
    question: How can I obtain a temporary license for Aspose.OCR?
  - answer: Join the community at the [Aspose.OCR Forum](https://forum.aspose.com/c/ocr/16)
      for help and discussions.
    question: Where can I find support for Aspose.OCR?
  - answer: Yes, use the `setAllowedCharacters` API to define a custom whitelist of
      characters. This is ideal for numeric‑only fields.
    question: Can I specify allowed characters in Aspose.OCR?
  - answer: Absolutely—Aspose.OCR is regularly updated to stay compatible with the
      newest Java releases.
    question: Is Aspose.OCR compatible with the latest JDK versions?
  - answer: The library also supports block, paragraph, and full‑page recognition,
      language packs, and advanced image preprocessing.
    question: Are there additional OCR features beyond line recognition?
  type: FAQPage
second_title: Aspose.OCR Java API
title: Como usar OCR – Extrair texto de imagens com Aspose.OCR
url: /pt/java/advanced-ocr-techniques/specify-allowed-characters/
weight: 15
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como usar OCR – Extrair texto de imagens com Aspose.OCR

Em aplicações Java modernas, **como usar OCR** é uma pergunta frequente, especialmente quando você precisa transformar faturas digitalizadas, recibos ou formulários impressos em texto pesquisável. Este tutorial guia você por um exemplo completo de **Aspose.OCR for Java**: extraindo texto de imagens, restringindo a saída a um conjunto de caracteres personalizado e aplicando uma licença temporária para avaliação rápida.

## Respostas rápidas
- **What does Aspose.OCR do?** Ele extrai texto de imagens com alta precisão e permite limitar os caracteres reconhecidos.  
- **Do I need a license?** Uma licença temporária ou permanente é necessária para uso em produção; a chave temporária remove marcas d'água.  
- **Which JDK version is supported?** A biblioteca funciona com as versões mais recentes do JDK (JDK 17, 19, 21).  
- **Can I limit recognized characters?** Sim—use o método `setAllowedCharacters` para restringir a saída.  
- **How long does the setup take?** Aproximadamente 10‑15 minutos para uma implementação básica de ponta a ponta.

## O que é “extrair texto de imagens”?
Extrair texto de imagens, também conhecido como reconhecimento óptico de caracteres (OCR), converte caracteres visuais—sejam impressos, manuscritos ou digitados—em cadeias legíveis por máquina. Essa transformação permite que aplicações pesquisem, indexem, editem e analisem o conteúdo programaticamente, suportando fluxos de trabalho como processamento de faturas, arquivamento de documentos e automação de entrada de dados.

## Por que usar Aspose.OCR para Java?
Aspose.OCR suporta **mais de 60 idiomas**, pode processar imagens de até **10 MB** sem carregar o arquivo inteiro na memória e oferece **>95 % de precisão** em digitalizações limpas. A biblioteca é autônoma, não requer motores OCR externos, o que simplifica a implantação e reduz a sobrecarga de licenciamento.

## Pré-requisitos

### Kit de Desenvolvimento Java (JDK)

Certifique-se de que você tem o Kit de Desenvolvimento Java mais recente instalado. Você pode baixá-lo [aqui](https://www.oracle.com/java/technologies/javase-downloads.html).

### Biblioteca Aspose.OCR para Java

Faça o download e instale a biblioteca Aspose.OCR para Java a partir do [link de download](https://releases.aspose.com/ocr/java/).

### Licença Aspose.OCR

Para desbloquear a funcionalidade completa, obtenha uma licença. Você pode comprar uma [aqui](https://purchase.aspose.com/buy) ou solicitar uma [licença temporária](https://purchase.aspose.com/temporary-license/) para fins de avaliação.

## Como usar OCR com Aspose.OCR para Java?

Carregue sua imagem, configure o motor OCR e chame o método de reconhecimento—tudo em algumas linhas simples. Este parágrafo de resposta direta indica exatamente o que fazer: criar uma instância `AsposeOCR` com sua string de licença, definir os caracteres permitidos e invocar `RecognizeLine` na imagem alvo para receber o texto extraído. A API lida com o pré-processamento da imagem internamente, assim você obtém resultados limpos sem código adicional.

### Importar Pacotes

A classe `AsposeOCR` está no pacote `com.aspose.ocr`. Importe as classes necessárias antes de começar a codificar.

```java
package com.aspose.ocr.examples.OcrFeatures;

import com.aspose.ocr.AsposeOCR;
import com.aspose.ocr.examples.Utils;

import java.io.IOException;
```

## Guia passo a passo

### Etapa 1: Defina seu diretório de documentos

Escolha uma pasta onde os resultados do OCR e arquivos temporários serão armazenados. Esse caminho será usado posteriormente para localizar a imagem que você deseja processar.

```java
String dataDir = "Your Document Directory";
```

### Etapa 2: Especifique o caminho da imagem

Forneça o caminho completo no sistema de arquivos ou a localização de recurso no class‑path que aponta para a imagem que você deseja analisar.

```java
String imagePath = dataDir + "0001460985.Jpeg";
```

### Etapa 3: Crie uma instância Aspose.OCR

`AsposeOCR` é o motor central que realiza o reconhecimento óptico de caracteres. Instancie‑o com uma string de licença temporária ou permanente.

```java
AsposeOCR api = new AsposeOCR("YourLicenseKey");
```

### Etapa 4: Execute o reconhecimento OCR

`RecognizeLine` extrai uma única linha de texto da imagem fornecida e a retorna como uma `String` Java simples. Você pode chamar este método repetidamente para documentos com várias linhas.

```java
try {
    String result = api.RecognizeLine(imagePath);
    System.out.println("File: " + imagePath);
    System.out.println("Result line: " + result);
} catch (IOException e) {
    e.printStackTrace();
}
```

> **Dica profissional:** Se precisar restringir a saída apenas a dígitos (por exemplo, para números de fatura), chame `setAllowedCharacters("0123456789")` na instância `AsposeOCR` antes de invocar `RecognizeLine`. Isso força o motor a ignorar quaisquer símbolos não numéricos.  
> `setAllowedCharacters` é um método de `AsposeOCR` que restringe a saída do OCR a uma lista branca de caracteres especificada.

## Problemas comuns e soluções

| Problema | Motivo | Correção |
|----------|--------|----------|
| **Nenhuma saída ou string vazia** | Caminho da imagem incorreto ou formato não suportado | Verifique `imagePath` e use um formato suportado (JPEG, PNG, BMP) |
| **Erros de reconhecimento** | Imagem de baixa resolução ou fundo ruidoso | Pré‑procese a imagem (aumente o contraste, binarize) antes do OCR |
| **Licença não aplicada** | Chave de licença ausente ou inválida | Certifique‑se de que a string de licença está correta e passada ao construtor `AsposeOCR` |

## Perguntas frequentes

**Q: Como posso obter uma licença temporária para Aspose.OCR?**  
A: Visite a [página de licença temporária](https://purchase.aspose.com/temporary-license/) para solicitar uma chave de avaliação que remove marcas d'água de avaliação.

**Q: Onde posso encontrar suporte para Aspose.OCR?**  
A: Junte‑se à comunidade no [Fórum Aspose.OCR](https://forum.aspose.com/c/ocr/16) para ajuda e discussões.

**Q: Posso especificar caracteres permitidos no Aspose.OCR?**  
A: Sim, use a API `setAllowedCharacters` para definir uma lista branca personalizada de caracteres. Isso é ideal para campos apenas numéricos.

**Q: O Aspose.OCR é compatível com as versões mais recentes do JDK?**  
A: Absolutamente—Aspose.OCR é atualizado regularmente para permanecer compatível com as versões mais recentes do Java.

**Q: Existem recursos OCR adicionais além do reconhecimento de linhas?**  
A: A biblioteca também suporta reconhecimento de blocos, parágrafos e páginas completas, pacotes de idiomas e pré‑processamento avançado de imagens.

## Conclusão

Seguindo este **tutorial Aspose OCR Java**, você agora sabe **como usar OCR** para extrair texto de imagens, limitar o conjunto de caracteres e aplicar uma licença temporária para testes rápidos. Aprofunde‑se na [documentação](https://reference.aspose.com/ocr/java/) completa para explorar suporte multilíngue, processamento em lote e pipelines de pré‑processamento personalizados.

---

**Última atualização:** 2026-05-24  
**Testado com:** Aspose.OCR for Java 24.11  
**Autor:** Aspose  

{{< blocks/products/products-backtop-button >}}

## Tutoriais relacionados

- [Como definir licença e verificar licença Aspose.OCR em Java](/ocr/java/ocr-basics/set-license/)
- [Converter imagem em texto em Java usando Aspose.OCR BufferedImage](/ocr/java/advanced-ocr-techniques/perform-ocr-buffered-image/)
- [Exemplo Aspose OCR Java – Reconhecendo linhas em imagens](/ocr/java/advanced-ocr-techniques/recognize-lines/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}