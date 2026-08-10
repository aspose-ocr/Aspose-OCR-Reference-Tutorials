---
category: general
date: 2026-06-19
description: Como extrair PDF usando OCR em Python – tutorial passo a passo cobrindo
  extração de texto de PDF, reconhecimento de texto de imagem e um exemplo de OCR
  em Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize text from image
- ocr python example
- read pdf with ocr
language: pt
og_description: Como extrair PDF usando OCR em Python. Aprenda a extrair texto de
  PDF, reconhecer texto de imagem e veja um exemplo completo de OCR em Python.
og_title: Como extrair texto de PDF com OCR em Python – Tutorial completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  headline: How to Extract PDF Text with OCR in Python – Complete Guide
  type: TechArticle
- description: How to extract PDF using OCR in Python – step‑by‑step tutorial covering
    extract text from PDF, recognize text from image, and an OCR Python example.
  name: How to Extract PDF Text with OCR in Python – Complete Guide
  steps:
  - name: – Install the Required Packages
    text: First, we need an OCR engine. The example below uses the popular **ocr**
      package (a thin wrapper around Tesseract). If you prefer a different backend,
      the concepts stay the same.
  - name: – Initialize the OCR Engine and Set Language
    text: Now we spin up the engine and tell it to look for English characters. You
      can swap `ocr.Language.English` for any supported language code.
  - name: – Load a PDF Page as an Image
    text: OCR works on raster images, not PDF objects. The `ocr.Image.from_pdf` helper
      renders the chosen page to a bitmap. Adjust `page_number` for other pages (0‑based
      indexing).
  - name: – Recognize Text from the Rendered Image
    text: Here’s the heart of the **ocr python example**. The engine processes the
      bitmap and returns an object containing the extracted string.
  - name: – Print or Store the Extracted Text
    text: Finally, we output the result. In a real application you’d probably write
      to a file or a database.
  type: HowTo
tags:
- OCR
- Python
- PDF
- Text Extraction
title: Como Extrair Texto de PDF com OCR em Python – Guia Completo
url: /pt/python-java/general/how-to-extract-pdf-text-with-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Extrair Texto de PDF com OCR em Python – Guia Completo

Já se perguntou **como extrair PDF** quando o arquivo é apenas uma imagem escaneada? Você não está sozinho. Em muitos projetos do mundo real — pense em contratos, faturas ou arquivos históricos — o PDF que você recebe não tem texto selecionável. A boa notícia? Algumas linhas de Python podem transformar essas páginas apenas de imagem em texto pesquisável e editável.

Neste tutorial, percorreremos um **exemplo de OCR Python** prático que lê um PDF, renderiza sua primeira página como imagem e então **extrai texto de PDF** usando um motor OCR. Ao final, você saberá exatamente como **ler PDF com OCR**, por que cada etapa é importante e como adaptar o código para documentos multipáginas ou diferentes idiomas.

## O que você aprenderá

- Instalar e configurar uma biblioteca OCR confiável para Python.  
- Converter páginas de PDF em imagens adequadas para OCR.  
- **Reconhecer texto a partir de imagem** e obter strings Unicode limpas.  
- Armadilhas comuns (PDFs de baixa resolução, páginas giradas) e como evitá‑las.  
- Estender o script para lidar com múltiplas páginas ou processamento em lote.

**Pré‑requisitos**: Python 3.8+, pip e um entendimento básico de ambientes virtuais. Não é necessária experiência prévia com OCR — basta acompanhar.

---

## ## Como Extrair Texto de PDF com OCR em Python

Este cabeçalho H2 contém nossa palavra‑chave principal exatamente onde os motores de busca adoram vê‑la. Vamos mergulhar direto no código.

### Etapa 1 – Instalar os Pacotes Necessários

Primeiro, precisamos de um motor OCR. O exemplo abaixo usa o popular pacote **ocr** (um wrapper leve ao redor do Tesseract). Se você preferir um backend diferente, os conceitos permanecem os mesmos.

```bash
# Create a fresh virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR wrapper and Pillow for image handling
pip install ocr pillow
```

> **Dica profissional:** No Linux, você também precisará do binário do Tesseract: `sudo apt-get install tesseract-ocr`. Usuários macOS podem obtê‑lo via Homebrew: `brew install tesseract`.

### Etapa 2 – Inicializar o Motor OCR e Definir o Idioma

Agora iniciamos o motor e instruímos a procurar por caracteres em inglês. Você pode trocar `ocr.Language.English` por qualquer código de idioma suportado.

```python
import ocr

# Step 1: Create an OCR engine and set the language to English
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.English
```

**Por que isso importa:** Especificar o idioma melhora drasticamente a precisão, pois o motor pode aplicar dicionários e modelos de caracteres específicos do idioma.

### Etapa 3 – Carregar uma Página de PDF como Imagem

OCR funciona em imagens raster, não em objetos PDF. O helper `ocr.Image.from_pdf` renderiza a página escolhida para um bitmap. Ajuste `page_number` para outras páginas (indexação baseada em 0).

```python
# Step 2: Load the first page of the PDF as an image
pdf_file_path = "YOUR_DIRECTORY/contract.pdf"
page_image = ocr.Image.from_pdf(pdf_file_path, page_number=1)
```

> **Caso extremo:** Se o PDF contiver gráficos vetoriais em vez de imagens escaneadas, você pode obter uma renderização nítida. Para digitalizações de baixa resolução, considere aumentar o DPI: `ocr.Image.from_pdf(..., dpi=300)`.

### Etapa 4 – Reconhecer Texto a partir da Imagem Renderizada

Aqui está o coração do **exemplo de ocr python**. O motor processa o bitmap e retorna um objeto contendo a string extraída.

```python
# Step 3: Recognize text from the rendered page image
ocr_result = ocr_engine.recognize(page_image)
```

O atributo `ocr_result.text` contém a saída em texto simples, preservando quebras de linha quando possível.

### Etapa 5 – Imprimir ou Armazenar o Texto Extraído

Finalmente, exibimos o resultado. Em uma aplicação real, você provavelmente gravaria em um arquivo ou em um banco de dados.

```python
# Step 4: Print the extracted text
print(ocr_result.text)
```

Executar o script deve exibir algo como:

```
THIS AGREEMENT is made on the 1st day of January 2024...
```

Esse é um fluxo completo de **extrair texto de pdf** usando OCR.

---

## ## Reconhecer Texto a partir de Imagem – Ajustando a Precisão

Se você está interessado apenas em **reconhecer texto a partir de imagem** (por exemplo, um JPEG de um recibo), pode pular a etapa de conversão de PDF:

```python
image_path = "receipt.jpg"
page_image = ocr.Image.from_file(image_path)   # Directly load an image
ocr_result = ocr_engine.recognize(page_image)
print(ocr_result.text)
```

**Dicas para melhores resultados:**

- **Pré‑processar** a imagem: converter para escala de cinza, aplicar limiarização ou corrigir inclinação. Pillow facilita isso.
- **Aumentar o DPI** durante a renderização do PDF: resolução maior fornece mais detalhes ao motor OCR.
- **Habilitar a configuração do motor OCR** para segmentação de página (`ocr_engine.config = "--psm 6"` para blocos uniformes).

## ## Ler PDF com OCR – Manipulando Múltiplas Páginas

A maioria dos contratos abrange várias páginas. Iterar sobre cada página é simples:

```python
def extract_all_pages(pdf_path):
    all_text = []
    for i in range(ocr.Image.pdf_page_count(pdf_path)):
        img = ocr.Image.from_pdf(pdf_path, page_number=i)
        result = ocr_engine.recognize(img)
        all_text.append(result.text)
    return "\n--- PAGE BREAK ---\n".join(all_text)

full_text = extract_all_pages("YOUR_DIRECTORY/contract.pdf")
print(full_text)
```

Esta função **lê PDF com OCR**, concatena a saída e insere um marcador de quebra de página claro. Você pode então enviar `full_text` para um índice de busca ou armazená‑lo como um arquivo `.txt`.

## ## Armadilhas Comuns e Como Corrigi‑las

| Sintoma | Causa Provável | Correção |
|---------|----------------|----------|
| Caracteres embaralhados, muitos `?` | Idioma errado ou arquivos de dados de idioma ausentes | Instale o pacote de idioma Tesseract correto (`tesseract-ocr-<lang>`) e defina `ocr_engine.language`. |
| Linhas ausentes ou palavras truncadas | DPI baixo (abaixo de 150) | Renderize o PDF em 300 DPI ou mais (`dpi=300`). |
| Texto está rotacionado ou invertido | Página escaneada não está na posição correta | Use `ocr.Image.deskew(page_image)` antes do reconhecimento. |
| Processamento lento em PDFs grandes | Processamento das páginas sequencialmente em uma única thread | Paralelize com `concurrent.futures.ThreadPoolExecutor`. |

## ## Estendendo o Exemplo OCR Python

- **Exportar para PDF/A**: Após a extração, você pode incorporar o texto de volta a um PDF pesquisável usando `reportlab` ou `pypdf2`.
- **Detecção de idioma**: Use `langdetect` na saída OCR para mudar `ocr_engine.language` dinamicamente.
- **Processamento em lote**: Percorra um diretório com `os.listdir` e aplique `extract_all_pages` a cada arquivo.

## ## Saída Esperada e Verificação

Ao executar o script em uma digitalização clara, em idioma inglês, você deverá ver um bloco de texto limpo com pontuação correta. Verifique por:

1. Comparar algumas linhas com a imagem escaneada original.  
2. Executar uma contagem simples de palavras (`len(ocr_result.text.split())`) para garantir que a saída não esteja vazia.  
3. Opcionalmente, alimentar o resultado em um corretor ortográfico como `pyspellchecker` para identificar erros de OCR.

## Conclusão

Cobremos **como extrair PDF** quando a análise tradicional falha, demonstramos um **exemplo completo de ocr python**, e explicamos como **reconhecer texto a partir de imagem** e **ler PDF com OCR** para cenários de página única e multipáginas. Com os trechos de código acima, você pode transformar qualquer PDF escaneado em texto pesquisável e editável — sem necessidade de digitação manual.

Próximos passos? Experimente trocar o idioma para espanhol (`ocr.Language.Spanish`) ou experimente técnicas de pré‑processamento de imagem para melhorar a precisão. Se você está construindo um sistema de gerenciamento de documentos, considere indexar o texto extraído com Elasticsearch para buscas ultrarrápidas.

Tem perguntas ou encontrou um PDF estranho? Deixe um comentário, e feliz codificação!  

![Como extrair PDF usando OCR em Python](image.png "Como extrair PDF usando OCR em Python")

## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Reconhecer Texto de PDF – Operações OCR com Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [Extrair texto de imagem C# com seleção de idioma usando Aspose.OCR](/ocr/english/net/ocr-configuration/ocr-operation-with-language-selection/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}