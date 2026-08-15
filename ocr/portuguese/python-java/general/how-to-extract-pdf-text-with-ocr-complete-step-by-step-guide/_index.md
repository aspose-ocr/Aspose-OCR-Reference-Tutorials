---
category: general
date: 2026-03-26
description: Como extrair texto de PDF usando OCR. Aprenda a carregar PDF como imagem,
  reconhecer o texto do PDF e extrair texto do PDF com um exemplo simples em Python.
draft: false
keywords:
- how to extract pdf
- extract text from pdf
- recognize pdf text
- load pdf as image
- how to use OCR
language: pt
og_description: Como extrair texto de PDF usando OCR. Este guia mostra como carregar
  o PDF como imagem, reconhecer o texto do PDF e extrair texto do PDF em Python.
og_title: Como Extrair Texto de PDF com OCR – Tutorial Completo
tags:
- OCR
- Python
- PDF processing
title: Como Extrair Texto de PDF com OCR – Guia Completo Passo a Passo
url: /pt/python-java/general/how-to-extract-pdf-text-with-ocr-complete-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Extrair Texto de PDF com OCR – Guia Completo Passo a Passo

Já se perguntou **como extrair PDF** que na verdade são apenas imagens escaneadas? Você não está sozinho—muitos desenvolvedores esbarram nessa barreira quando precisam de conteúdo pesquisável, mas só têm PDFs de imagem. A boa notícia? Algumas linhas de código e uma biblioteca OCR robusta podem transformar esses PDFs‑imagem em texto simples num instante.  

Neste tutorial, vamos percorrer **como usar OCR** para carregar um PDF como imagem, reconhecer texto em PDF e, finalmente, **extrair texto de PDF** de documentos de qualquer tamanho. Ao final, você terá um script executável, uma explicação clara de cada etapa e algumas dicas para evitar os problemas habituais.

## O que Você Precisa

- Python 3.9 ou mais recente (o código também funciona em 3.10+)
- O pacote Python `ocr` (ou qualquer biblioteca OCR compatível que exponha `OcrEngine`, `OcrEngineMode` e `Imaging.Image`)
- Um PDF multipágina que você deseja processar (para a demonstração, chamaremos de `multi_page.pdf`)
- Familiaridade básica com ambientes virtuais (opcional, mas recomendado)

> **Dica profissional:** Se você está no Windows, considere usar o Anaconda Prompt; no macOS/Linux, um simples `python -m venv venv && source venv/bin/activate` resolve.

## Etapa 1: Instalar a Biblioteca OCR

Primeiro, obtenha o pacote OCR do PyPI. O exemplo abaixo usa um pacote fictício `ocr` que espelha a API mostrada no trecho de código, mas a maioria das bibliotecas reais (como `pytesseract` + `pdf2image`) segue o mesmo padrão.

```bash
pip install ocr
```

Se você estiver usando um motor diferente, substitua `ocr` pelo nome apropriado (por exemplo, `pip install pytesseract pdf2image`).

## Etapa 2: Inicializar o Motor OCR

Criar uma instância do motor é a base de **como extrair PDF** texto. Pense no motor como o cérebro que interpretará os pixels dentro de cada página do PDF.

```python
import ocr

# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Set the engine to the default mode (fast enough for most PDFs)
ocr_engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)
```

> **Por que isso importa:** `set_engine_mode` permite trocar velocidade por precisão. `DEFAULT` é uma escolha equilibrada; se precisar de maior precisão, altere para `HIGH_ACCURACY` (se a biblioteca suportar).

## Etapa 3: Carregar o PDF como um Objeto de Imagem

OCR funciona em imagens, não em contêineres PDF, portanto devemos converter o PDF em uma representação de imagem primeiro. O método `Imaging.Image.load` lida com PDFs multipágina automaticamente.

```python
# Step 3: Load the multi‑page PDF as an image object
pdf_path = "YOUR_DIRECTORY/multi_page.pdf"
pdf_image = ocr.Imaging.Image.load(pdf_path)
```

> **Caso extremo:** Algumas bibliotecas aceitam apenas uma imagem de página única. Nesse cenário, você percorreria cada página usando `pdf2image.convert_from_path`. Nossa chamada `load` abstrai isso, tornando **load pdf as image** uma única linha.

## Etapa 4: Reconhecer Texto em Todas as Páginas

Agora vem o núcleo de **recognize PDF text**. O motor escaneia cada página, retornando uma lista de objetos de resultado—um por página.

```python
# Step 4: Recognize text on all pages of the PDF
page_results = ocr_engine.recognize_multi_page(pdf_image)
```

Cada `page_result` contém métodos como `get_text()` (texto simples) e `get_confidence()` (métrica de qualidade opcional).  

> **Dica:** Se você precisar apenas da primeira página, chame `recognize(pdf_image[0])` em vez do auxiliar multipágina.

## Etapa 5: Iterar pelos Resultados e Exibir o Texto Extraído

Finalmente, iteramos sobre os resultados, imprimindo o texto de cada página. Isso completa o fluxo de trabalho de **extract text from PDF**.

```python
# Step 5: Print extracted text page by page
for index, page_result in enumerate(page_results):
    print(f"--- Page {index + 1} ---")
    print(page_result.get_text())
    # Optional: show confidence score
    # print(f"Confidence: {page_result.get_confidence():.2f}%")
```

### Saída Esperada

Se `multi_page.pdf` contiver três páginas com as palavras “Hello”, “World” e “Python”, você verá:

```
--- Page 1 ---
Hello
--- Page 2 ---
World
--- Page 3 ---
Python
```

É isso—seu PDF agora está totalmente pesquisável e o texto está pronto para processamento posterior (indexação, análise de sentimento, o que precisar).

## Etapa 6: Lidando com Problemas Comuns

| Problema | Por que Acontece | Solução Rápida |
|----------|------------------|----------------|
| **Saída em branco** | As páginas do PDF são escaneadas em DPI baixo, tornando os caracteres indistinguíveis. | Aumente a resolução da imagem antes do OCR: `pdf_image = pdf_image.resize(300)` (300 DPI é um ponto ideal). |
| **Caracteres estranhos** | Alfabetos não latinos precisam de pacotes de idioma. | Carregue o modelo de idioma apropriado: `ocr_engine.load_language('spa')` para espanhol, etc. |
| **Estouro de memória em PDFs enormes** | Carregar todas as páginas de uma vez consome RAM. | Processar páginas em lotes: `for img in pdf_image.split(batch=10): …` (pseudo‑código). |
| **Desempenho lento** | Usar `DEFAULT` em um documento massivo pode ser lento. | Troque para o modo `FAST` ou execute OCR em paralelo usando `concurrent.futures`. |

## Bônus: Salvando o Texto Extraído em um Arquivo

A maioria dos pipelines reais precisa que o texto seja persistido. Aqui está um pequeno helper que grava tudo em `output.txt`.

```python
output_path = "YOUR_DIRECTORY/output.txt"

with open(output_path, "w", encoding="utf-8") as f:
    for idx, result in enumerate(page_results):
        f.write(f"--- Page {idx + 1} ---\n")
        f.write(result.get_text() + "\n\n")
print(f"All text saved to {output_path}")
```

Agora você pode alimentar `output.txt` em um motor de busca, um banco de dados ou qualquer modelo de PLN.

## Juntando Tudo – Script Completo

Abaixo está o programa completo, pronto para ser executado. Copie e cole, ajuste os caminhos dos arquivos e está pronto para usar.

```python
# -*- coding: utf-8 -*-
"""
How to extract PDF text with OCR – end‑to‑end example.

Prerequisites:
    pip install ocr
"""

import ocr

def extract_text_from_pdf(pdf_path: str):
    """
    Load a PDF, run OCR on every page, and return a list of strings.
    """
    # Initialize engine
    engine = ocr.OcrEngine()
    engine.set_engine_mode(ocr.OcrEngineMode.DEFAULT)

    # Load PDF as image (multi‑page support)
    pdf_image = ocr.Imaging.Image.load(pdf_path)

    # Recognize text on all pages
    results = engine.recognize_multi_page(pdf_image)

    # Collect plain text
    texts = [res.get_text() for res in results]
    return texts

def main():
    pdf_file = "YOUR_DIRECTORY/multi_page.pdf"
    texts = extract_text_from_pdf(pdf_file)

    # Print and optionally save
    for i, txt in enumerate(texts, start=1):
        print(f"--- Page {i} ---")
        print(txt)
        print()

    # Save to file
    out_path = "YOUR_DIRECTORY/extracted_text.txt"
    with open(out_path, "w", encoding="utf-8") as out_f:
        for i, txt in enumerate(texts, start=1):
            out_f.write(f"--- Page {i} ---\n{txt}\n\n")
    print(f"Extracted text stored in {out_path}")

if __name__ == "__main__":
    main()
```

Execute:

```bash
python extract_pdf_ocr.py
```

Você deverá ver o conteúdo de cada página impresso no console, seguido de uma confirmação de que o arquivo `extracted_text.txt` foi criado.

## Conclusão

Cobremos **como extrair PDF** texto de documentos apenas de imagem usando um motor OCR, desde a instalação da biblioteca até o tratamento de resultados multipágina e a gravação da saída. Agora você sabe **como usar OCR**, como **carregar PDF como imagem**, e como **reconhecer texto em PDF** de forma confiável.  

Próximos passos? Experimente trocar o modo padrão do motor por uma configuração de alta precisão, experimente pacotes de idioma para PDFs multilíngues, ou canalize o texto extraído para um índice de busca full‑text como o Elasticsearch. O céu é o limite depois que você dominar o básico de extração de texto de arquivos PDF.

---

![exemplo de como extrair pdf](images/ocr_flowchart.png){alt="diagrama de fluxo de como extrair pdf"}

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}