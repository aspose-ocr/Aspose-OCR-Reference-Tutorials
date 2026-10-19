---
category: general
date: 2026-07-05
description: Extrair tabela de imagem usando OCR em Python. Aprenda como extrair a
  tabela, converter a imagem para TSV e dominar técnicas de OCR de tabela em imagem
  com Python.
draft: false
keywords:
- extract table from image
- how to extract table
- convert image to tsv
- ocr table image python
language: pt
og_description: Extrair tabela de imagem com OCR em Python. Este guia mostra como
  extrair a tabela, converter a imagem em TSV e usar ferramentas Python de OCR para
  tabelas em imagens.
og_title: Extrair Tabela de Imagem – Converter Imagem para TSV em Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  headline: Extract Table from Image – Convert Image to TSV in Python
  type: TechArticle
- description: Extract table from image using Python OCR. Learn how to extract table,
    convert image to TSV, and master ocr table image python techniques.
  name: Extract Table from Image – Convert Image to TSV in Python
  steps:
  - name: Initialise the aocr OCR engine.
    text: Initialise the aocr OCR engine.
  - name: Attach the AI post‑processor.
    text: Attach the AI post‑processor.
  - name: Load a table image.
    text: Load a table image.
  - name: Perform structured OCR.
    text: Perform structured OCR.
  - name: Clean the results.
    text: Clean the results.
  - name: Export the table as a TSV file.
    text: Export the table as a TSV file.
  type: HowTo
tags:
- OCR
- Python
- Table Extraction
title: Extrair Tabela de Imagem – Converter Imagem para TSV em Python
url: /pt/python/general/extract-table-from-image-convert-image-to-tsv-in-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair tabela de imagem – Converter imagem para TSV em Python

Já se perguntou como extrair uma tabela de uma imagem sem perder a cabeça? Neste tutorial vamos percorrer **como extrair dados de tabela** de uma foto usando a biblioteca `aocr`, e então transformar esses dados em um arquivo TSV organizado. Sem mágica, apenas algumas linhas de Python e um pouco de pós‑processamento impulsionado por IA.

Se você já tentou copiar‑colar uma tabela de uma fatura escaneada ou de uma captura de tela e acabou com uma bagunça, vai entender por que vale a pena dominar uma abordagem baseada em OCR. Ao final, você poderá alimentar qualquer imagem de tabela no Python e obter valores separados por tabulação limpos, prontos para planilhas ou bancos de dados.

---

## O que você vai precisar

| Requisito | Por que é importante |
|-----------|----------------------|
| Python 3.9+ | O pacote `aocr` tem como alvo runtimes modernos do Python. |
| Biblioteca `aocr` (`pip install aocr`) | Fornece o motor OCR e o pós‑processador de IA que usaremos. |
| Um arquivo de imagem contendo uma tabela (PNG, JPG, etc.) | Os dados de origem que vamos extrair. |
| Opcional: um ambiente virtual | Mantém as dependências isoladas — altamente recomendado. |

Ter isso pronto evita interrupções no meio do tutorial.

---

## Instale as dependências

Primeiro, vamos instalar as ferramentas de OCR. Abra um terminal e execute:

```bash
# Create and activate a virtual environment (optional but clean)
python -m venv ocr-env
source ocr-env/bin/activate   # On Windows: ocr-env\Scripts\activate

# Install the aocr package
pip install aocr
```

> **Dica profissional:** Se encontrar erros de permissão, adicione `--user` ao comando `pip install` ou use `pipx` para uma instalação global.

---

## Etapa 1 – Inicializar o motor OCR

O motor é o coração do processo. Pense nele como o “cérebro” que analisa cada pixel e decide a que caractere cada um pertence.

```python
import aocr

# Create an OCR engine instance – this sets up the model and default settings
engine = aocr.OcrEngine()
```

Por que instanciamos um motor em vez de chamar uma única função? O objeto motor nos permite anexar pós‑processadores personalizados posteriormente, oferecendo controle granular sobre a saída — essencial quando você precisa de precisão **ocr table image python**.

---

## Etapa 2 – Anexar o pós‑processador de IA

`aocr` vem com um pós‑processador de IA leve que limpa os resultados brutos do OCR enquanto preserva as bordas das células. Nenhum argumento extra é necessário, o que mantém o código organizado.

```python
# Hook the AI post‑processor into the engine
engine.set_post_processor(ai.run_postprocessor, None)
```

Se você pular esta etapa, ainda obterá texto bruto, mas a estrutura da tabela ficará ruidosa — imagine uma planilha onde cada célula é um mistério. O pós‑processador faz o trabalho pesado de alinhar o texto à sua grade original.

---

## Etapa 3 – Carregar a imagem da sua tabela

Você pode carregar uma imagem de qualquer caminho, mas para clareza usaremos um diretório placeholder. Substitua `"YOUR_DIRECTORY/invoice_table.png"` pelo caminho real do seu arquivo.

```python
# Load the image that contains the table
image_path = "YOUR_DIRECTORY/invoice_table.png"
image = aocr.Image.from_file(image_path)
```

> **Observação:** `aocr.Image` detecta automaticamente o formato da imagem e normaliza os canais de cor, portanto você não precisa pré‑processar o arquivo a menos que esteja gravemente degradado.

---

## Etapa 4 – Executar OCR estruturado

Agora o motor escaneia a imagem e devolve um objeto de tabela bruto. Esse objeto contém linhas, colunas e o texto bruto de cada célula.

```python
# Recognise the table structure and extract raw cell data
raw_table = engine.recognize_structured(image)
```

Por que usar `recognize_structured` em vez de uma chamada genérica `recognize`? A variante estruturada tenta inferir os limites de linhas/colunas, fornecendo um resultado tipo matriz que é muito mais fácil de converter para TSV depois.

---

## Etapa 5 – Limpar os dados com o pós‑processador de IA

Executar o pós‑processador refina a saída bruta: remove caracteres estranhos, mescla fragmentos divididos e garante que o texto de cada célula esteja corretamente alinhado.

```python
# Apply the AI post‑processor to tidy up the table
processed_table = engine.run_postprocessor(raw_table)
```

Se você inspecionar `processed_table.table`, verá uma lista de linhas, cada linha sendo uma lista de objetos `Cell`. Cada `Cell` possui um atributo `.text` que contém a string limpa.

---

## Etapa 6 – Exportar a tabela como TSV

A etapa final é transformar os dados processados em um arquivo de valores separados por tabulação (TSV) — exatamente o que você precisa quando quiser **converter imagem para TSV** para Excel ou Google Sheets.

```python
import csv

# Define the output TSV path
tsv_path = "extracted_table.tsv"

# Open the file and write rows as tab‑separated values
with open(tsv_path, "w", newline="", encoding="utf-8") as tsv_file:
    writer = csv.writer(tsv_file, delimiter="\t")
    for row in processed_table.table:
        # Extract text from each cell and write the row
        writer.writerow([cell.text for cell in row])

print(f"✅ Table successfully saved to {tsv_path}")
```

Executar o script imprime cada linha no console (se preferir) e grava um arquivo TSV limpo que pode ser aberto em qualquer programa de planilha.

### Verificação rápida

```python
# Print the TSV to the console for a sanity check
for row in processed_table.table:
    print("\t".join(cell.text for cell in row))
```

Você deve ver colunas alinhadas corretamente, como:

```
Item	Qty	Price	Total
Apple	10	0.50	5.00
Banana	5	0.30	1.50
```

Se a saída parecer embaralhada, verifique novamente a qualidade da imagem (nitidez, contraste) e considere ajustar as configurações do motor OCR — `engine.set_config(...)` permite ajustar modelos de idioma e limites de confiança.

---

## Lidando com casos de borda comuns

| Situação | Correção sugerida |
|----------|-------------------|
| **Imagem inclinada** | Pré‑rotacione usando `Pillow` (`Image.rotate`) antes de enviá‑la ao `aocr`. |
| **Baixo contraste** | Aplique equalização de histograma (`cv2.equalizeHist`) para melhorar a legibilidade. |
| **Células mescladas** | Pós‑processar o TSV para dividir células com base em delimitadores conhecidos ou usar a flag `merge_cells=False` se disponível. |
| **PDFs de múltiplas páginas** | Converta cada página em uma imagem primeiro (`pdf2image`) e execute o pipeline em um loop. |

Esses ajustes mantêm seu fluxo de trabalho **ocr table image python** robusto em diferentes materiais de origem.

---

## Script completo – solução tudo‑em‑um

Abaixo está o script completo, pronto‑para‑executar, que reúne todas as etapas discutidas. Salve‑o como `extract_table.py` e execute `python extract_table.py`.

```python
#!/usr/bin/env python3
"""
Extract Table from Image – Convert Image to TSV (Python)

This script demonstrates how to:
1. Initialise the aocr OCR engine.
2. Attach the AI post‑processor.
3. Load a table image.
4. Perform structured OCR.
5. Clean the results.
6. Export the table as a TSV file.

Author: Your Name
Date: 2026-07-05
"""

import aocr
import csv
import sys
from pathlib import Path

def main(image_path: str, output_tsv: str = "extracted_table.tsv"):
    # Step 1 – Initialise engine
    engine = aocr.OcrEngine()

    # Step 2 – Attach AI post‑processor
    engine.set_post_processor(ai.run_postprocessor, None)

    # Step 3 – Load image
    if not Path(image_path).is_file():
        sys.exit(f"❌ Image not found: {image_path}")
    image = aocr.Image.from_file(image_path)

    # Step 4 – Structured OCR
    raw_table = engine.recognize_structured(image)

    # Step 5 – Clean with post‑processor
    processed_table = engine.run_postprocessor(raw_table)

    # Step 6 – Write TSV
    with open(output_tsv, "w", newline="", encoding="utf-8") as tsv_file:
        writer = csv.writer(tsv_file, delimiter="\


## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair texto de imagem com Aspose OCR – Guia passo a passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Como extrair tabela de imagem usando Aspose.OCR para .NET](/ocr/english/net/text-recognition/recognize-table/)
- [Como extrair texto de imagem preparando retângulos no OCR](/ocr/english/net/ocr-optimization/prepare-rectangles/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}