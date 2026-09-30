---
description: Aprenda como salvar resultados de OCR com Aspose.OCR para .NET – converta
  imagem em PDF, extraia texto de PNG e salve o texto reconhecido em DOCX, TXT, PDF
  ou XLSX.
linktitle: How to Save OCR Result as Document
second_title: Aspose.OCR .NET API
title: Como salvar o resultado de OCR como documento
url: /pt/net/ocr-settings/save-result-as-document/
weight: 10
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Salvar o Resultado do OCR como Documento

## Introdução

Neste tutorial você descobrirá **como salvar OCR** usando Aspose.OCR para .NET. Vamos percorrer o reconhecimento de texto em uma imagem e, em seguida, converter esse texto em formatos de documento populares como DOCX, TXT, PDF e XLSX. Ao final, você poderá automatizar a extração de dados de imagens e armazená‑los como arquivos pesquisáveis e editáveis — perfeito para arquivamento, relatórios ou processamento posterior.

## Respostas Rápidas
- **O que significa “how to save ocr”?** Refere‑se a persistir o texto reconhecido a partir de uma imagem em um formato de arquivo como DOCX, PDF, etc.  
- **Para quais formatos posso exportar?** DOCX, TXT, PDF e XLSX são suportados prontamente.  
- **Preciso de licença?** Um teste gratuito funciona para avaliação; uma licença comercial é necessária para uso em produção.  
- **Posso converter imagem para PDF diretamente?** Sim—salve o resultado do OCR como PDF para obter um documento PDF pesquisável.  
- **PNG é suportado?** Absolutamente; você pode **extrair texto de imagens PNG** com a mesma API.

## O que é OCR e Por Que Salvar Resultados como Documentos?

Optical Character Recognition (OCR) transforma texto impresso ou manuscrito dentro de imagens em cadeias legíveis por máquina. Salvar essas cadeias como documentos permite que você:

* Crie PDFs pesquisáveis para conformidade.  
* Popule planilhas (XLSX) para análise de dados.  
* Gere relatórios editáveis (DOCX).  
* Arquive logs em texto simples (TXT) para busca rápida.

## Pré‑requisitos

Antes de começar, certifique‑se de que você tem:

- Aspose.OCR for .NET instalado. Você pode baixá‑lo **[here](https://releases.aspose.com/ocr/net/)**.  
- Uma pasta na sua máquina que armazenará as imagens de origem e os documentos de saída. Atualize a variável `dataDir` no código para apontar para essa pasta.

## Importar Namespaces

Precisamos de alguns namespaces .NET para acessar I/O de arquivos e as classes Aspose OCR.

```csharp
using System;
using System.IO;
using Aspose.OCR;
```

### Etapa 1: Inicializar Aspose.OCR

Defina o caminho para o seu diretório de trabalho e crie uma instância do motor OCR.

```csharp
// The path to the documents directory.
string dataDir = "Your Document Directory";

// Initialize an instance of AsposeOcr
AsposeOcr api = new AsposeOcr();
```

### Etapa 2: Reconhecer Imagem

Passe o arquivo de imagem (por exemplo, um PNG) para o reconhecedor. É aqui que **reconhecemos imagens de texto** e as transformamos em um `RecognitionResult`.

```csharp
// Recognize image
RecognitionResult result = api.RecognizeImage(dataDir + "sample.png", new RecognitionSettings { });
```

### Etapa 3: Salvar Resultado em Diferentes Formatos

Agora exportamos o texto reconhecido. Escolha o formato que se adapta ao seu fluxo de trabalho — seja para **converter imagem para PDF**, **extrair texto de PNG**, ou gerar uma planilha.

```csharp
// Save the result in your preferred format
result.Save(RunExamples.GetDataDir_OCR() + "sample.docx", SaveFormat.Docx);
result.Save(RunExamples.GetDataDir_OCR() + "sample.txt", SaveFormat.Text);
result.Save(RunExamples.GetDataDir_OCR() + "sample.pdf", SaveFormat.Pdf);
result.Save(RunExamples.GetDataDir_OCR() + "sample.xlsx", SaveFormat.Xlsx);
```

### Etapa 4: Exibir Mensagem de Sucesso

Uma simples mensagem no console confirma que o processo foi concluído sem erros.

```csharp
Console.WriteLine("SaveResultAsDocument executed successfully");
```

## Armadilhas Comuns & Dicas

- **Caminhos de arquivo:** Sempre use caminhos absolutos ou garanta que `dataDir` termine com um separador de caminho (`\` ou `/`).  
- **Qualidade da imagem:** Imagens de alta resolução melhoram a precisão; considere pré‑processamento (corrigir inclinação, remover ruído) para melhores resultados.  
- **Modo de licença:** No modo de avaliação a saída pode conter marca d'água; aplique uma licença válida para removê‑la.

## Perguntas Frequentes

**Q1. O Aspose.OCR é compatível com diferentes formatos de imagem?**  
A1: Sim, o Aspose.OCR suporta uma ampla variedade de formatos de imagem, garantindo flexibilidade nas suas tarefas de OCR.

**Q2: Posso personalizar as configurações de reconhecimento para melhor precisão?**  
A2: Absolutamente! O Aspose.OCR fornece `RecognitionSettings` para ajustar finamente o processo de OCR de acordo com seus requisitos específicos.

**Q3: Existe um teste gratuito disponível?**  
A3: Sim, você pode começar com um teste gratuito **[here](https://releases.aspose.com/)**.

**Q4: Como posso obter uma licença temporária para Aspose.OCR?**  
A4: Licenças temporárias podem ser obtidas **[here](https://purchase.aspose.com/temporary-license/)**.

**Q5: Onde posso buscar ajuda ou conectar-me com a comunidade?**  
A5: Junte‑se à comunidade Aspose.OCR em **[Aspose Forum](https://forum.aspose.com/c/ocr/16)** para suporte e discussões.

---

**Última atualização:** 2026-02-12  
**Testado com:** Aspose.OCR 24.11 for .NET  
**Autor:** Aspose  

{{< /blocks/products/pf/tutorial-page-section >}}

{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}

{{< blocks/products/products-backtop-button >}}