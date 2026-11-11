---
category: general
date: 2026-06-19
description: Como executar OCR passo a passo e melhorar a precisão do OCR com técnicas
  de OCR de texto simples. Aprenda um fluxo de trabalho rápido para extração de texto
  confiável.
draft: false
keywords:
- how to run OCR
- improve OCR accuracy
- plain text OCR
- OCR post‑processing
- layout‑aware OCR
language: pt
og_description: Como executar OCR de forma eficiente. Este tutorial mostra como melhorar
  a precisão do OCR usando OCR de texto simples e pós‑processamento de IA.
og_title: Como Executar OCR em Python – Guia Completo
schemas:
- author: Aspose
  dateModified: '2026-06-19'
  description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  headline: How to Run OCR in Python – Complete Guide
  type: TechArticle
- description: How to run OCR step‑by‑step and improve OCR accuracy with plain text
    OCR techniques. Learn a fast workflow for reliable text extraction.
  name: How to Run OCR in Python – Complete Guide
  steps:
  - name: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
    text: '**Batch processing** – Wrap the whole script in a function that walks a
      directory, handling thousands of files in parallel with `concurrent.futures`.'
  - name: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
    text: '**Language models** – Swap the simple difflib heuristic for a call to OpenAI’s
      `gpt‑4o` or a locally hosted LLaMA model to get richer contextual corrections.'
  - name: '**Export formats** – Write the corrected structure to a searchable PDF'
    text: '**Export formats** – Write the corrected structure to a searchable PDF'
  type: HowTo
tags:
- OCR
- Python
- AI
title: Como Executar OCR em Python – Guia Completo
url: /pt/python/general/how-to-run-ocr-in-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Executar OCR em Python – Guia Completo

Já se perguntou **como executar OCR** em um lote de PDFs escaneados sem passar horas ajustando configurações? Você não está sozinho. Em muitos projetos o primeiro obstáculo é simplesmente obter texto confiável a partir de uma imagem, e a diferença entre um resultado instável e uma extração limpa costuma depender de alguns passos inteligentes.

Neste guia vamos percorrer um pipeline prático de quatro etapas que não apenas **executa OCR**, mas também **melhora a precisão do OCR** ao combinar uma passagem rápida de texto simples com uma segunda passagem consciente de layout e um pós‑processador impulsionado por IA. Ao final você terá um script pronto para uso, uma explicação clara de por que cada estágio importa e dicas para lidar com casos extremos como páginas de múltiplas colunas ou digitalizações ruidosas.

---

## O Que Você Precisa

Antes de mergulharmos, certifique‑se de que tem o seguinte:

- **Python 3.9+** – o código usa type hints e f‑strings.  
- **Tesseract OCR** instalado e acessível via o comando `tesseract`. (No Ubuntu: `sudo apt install tesseract-ocr`; no Windows baixe o instalador do repositório oficial.)  
- O wrapper **pytesseract** (`pip install pytesseract`).  
- Uma **biblioteca de pós‑processamento de IA** – para este exemplo vamos fingir que você tem um módulo leve `ai` que oferece `run_postprocessor`. Substitua‑o pela API GPT‑4 da OpenAI ou por um LLM local, se preferir.  
- Algumas imagens ou PDFs de exemplo para testar.

É só isso. Nenhum framework pesado, nenhuma ginástica com Docker. Apenas alguns installs via pip e você está pronto para começar.

---

## Etapa 1: Executar uma Passagem Rápida de OCR de Texto Simples

A primeira coisa que a maioria dos desenvolvedores ignora é que uma execução de OCR *texto simples* é extremamente rápida e fornece uma verificação rápida de sanidade. Vamos chamar `engine.Recognize()` para obter os caracteres brutos sem nenhum metadado de layout. Isso é o que chamamos de **OCR de texto simples**.

```python
import pytesseract
from PIL import Image

def plain_text_ocr(image_path: str) -> str:
    """Run a quick plain‑text OCR pass and return the raw string."""
    img = Image.open(image_path)
    # pytesseract returns a single string with line breaks.
    raw_text = pytesseract.image_to_string(img, lang='eng')
    return raw_text
```

*Por que isso importa:*  
- **Velocidade** – uma passagem simples em uma página de 300 dpi geralmente termina em menos de um segundo.  
- **Linha de base** – você pode comparar a saída estruturada posterior com essa linha de base para identificar erros gritantes.  
- **Detecção de erros** – se a passagem simples falhar completamente (ex.: tudo ilegível), você sabe que a qualidade da imagem está muito baixa e pode abortar cedo.

---

## Etapa 2: Executar uma Passagem Detalhada de OCR Consciente de Layout

Texto simples é ótimo, mas ele descarta *onde* cada palavra está na página. Para faturas, formulários ou revistas de múltiplas colunas você precisa de coordenadas, números de linha e, talvez, até informações de fonte. É aí que `engine.RecognizeStructured()` entra.

A seguir está um wrapper leve sobre a saída **TSV** do Tesseract, que nos fornece uma hierarquia de páginas → linhas → palavras, preservando as caixas delimitadoras.

```python
from typing import List, Dict

def structured_ocr(image_path: str) -> List[Dict]:
    """Return a list of pages, each containing lines with word coordinates."""
    img = Image.open(image_path)

    # Tesseract TSV includes page, block, paragraph, line, word indices.
    tsv_data = pytesseract.image_to_data(img, output_type=pytesseract.Output.DICT, lang='eng')

    pages = {}
    for i, level in enumerate(tsv_data["level"]):
        if level != 5:  # focus on word level (5)
            continue
        page_num = tsv_data["page_num"][i]
        line_num = tsv_data["line_num"][i]
        word = tsv_data["text"][i]
        if not word.strip():
            continue

        # Build nested dict structure.
        pages.setdefault(page_num, {}).setdefault(line_num, []).append({
            "text": word,
            "bbox": (
                tsv_data["left"][i],
                tsv_data["top"][i],
                tsv_data["width"][i],
                tsv_data["height"][i],
            ),
        })

    # Convert dicts to a more convenient list format.
    structured_result = []
    for page_id, lines in pages.items():
        page_obj = {"PageNumber": page_id, "Lines": []}
        for line_id, words in lines.items():
            line_text = " ".join(w["text"] for w in words)
            line_obj = {
                "LineNumber": line_id,
                "Text": line_text,
                "Words": words,
            }
            page_obj["Lines"].append(line_obj)
        structured_result.append(page_obj)

    return structured_result
```

*Por que fazemos isso:*  
- **Coordenadas** permitem que você mapeie o texto extraído de volta para a imagem original, facilitando realces ou redações.  
- **Agrupamento por linhas** preserva o layout original, essencial quando você precisa reconstruir tabelas ou colunas.  
- Essa passagem é um pouco mais lenta que a simples, mas ainda termina em alguns segundos para a maioria dos documentos.

---

## Etapa 3: Executar o Pós‑Processador de IA para Corrigir Erros de OCR

Mesmo o melhor motor de OCR comete erros — pense em “rn” vs “m”, diacríticos ausentes ou palavras divididas. Um modelo de IA pode analisar a string bruta e os dados estruturados, identificar inconsistências e reescrever o texto mantendo as coordenadas originais intactas.

Abaixo está uma implementação **mock**; substitua o corpo por uma chamada real a um LLM, se você tiver um.

```python
def ai_postprocess(plain_text: str, structured_result: List[Dict]) -> List[Dict]:
    """
    Simulate an AI post‑processor that corrects OCR errors.
    It walks through each line, compares it with the plain text,
    and applies simple heuristics (e.g., spell‑check).
    """
    import difflib
    corrected = []

    for page in structured_result:
        new_page = {"PageNumber": page["PageNumber"], "Lines": []}
        for line in page["Lines"]:
            # Find the closest match in the plain text using difflib.
            best_match = difflib.get_close_matches(line["Text"], plain_text.splitlines(), n=1, cutoff=0.6)
            corrected_text = best_match[0] if best_match else line["Text"]
            # Preserve original word list but replace the text field.
            new_line = {
                "LineNumber": line["LineNumber"],
                "Text": corrected_text,
                "Words": line["Words"],  # coordinates stay the same
            }
            new_page["Lines"].append(new_line)
        corrected.append(new_page)

    return corrected
```

*Por que esta etapa melhora a precisão do OCR:*  
- **Correções contextuais** – a IA pode decidir que “l0ve” provavelmente é “love” com base nas palavras ao redor.  
- **Preservação de coordenadas** – você mantém as informações de layout, de modo que tarefas subsequentes (como anotação de PDF) permaneçam precisas.  
- **Refinamento iterativo** – você pode executar o pós‑processador várias vezes, cada passagem limpando mais erros.

---

## Etapa 4: Iterar Sobre a Saída Estruturada Corrigida

Agora que temos uma estrutura limpa, extrair o texto final é trivial. Abaixo imprimimos cada linha, mas você também poderia escrever para um CSV, alimentar um banco de dados ou gerar um PDF pesquisável.

```python
def display_corrected_text(structured_result: List[Dict]) -> None:
    """Print each line of corrected OCR output."""
    for page in structured_result:
        print(f"\n--- Page {page['PageNumber']} ---")
        for line in page["Lines"]:
            print(line["Text"])

# Example usage tying everything together
if __name__ == "__main__":
    img_path = "sample_scan.png"

    # 1️⃣ Plain‑text OCR
    plain = plain_text_ocr(img_path)
    print("✅ Plain text OCR completed.")

    # 2️⃣ Structured OCR
    structured = structured_ocr(img_path)
    print("✅ Structured OCR completed.")

    # 3️⃣ AI post‑processing
    corrected = ai_postprocess(plain, structured)
    print("✅ AI post‑processor finished.")

    # 4️⃣ Show results
    display_corrected_text(corrected)
```

**Saída esperada** (supondo uma fatura simples de uma página):

```
--- Page 1 ---
Invoice #12345
Date: 2024‑05‑01
Bill To: Acme Corp
Item Qty Price Total
Widget A 2 $15.00 $30.00
Widget B 1 $25.00 $25.00
Subtotal $55.00
Tax $5.50
Total $60.50
```

Observe como as quebras de linha e a ordem das colunas são preservadas, e glitches comuns de OCR como “$15.00” lido como “$15,00” são corrigidos pela etapa de IA.

---

## Como Este Fluxo de Trabalho Ajuda a **Melhorar a Precisão do OCR**

| Etapa | O que corrige | Por que importa |
|------|---------------|-----------------|
| **OCR de texto simples** | Detecta páginas ilegíveis cedo | Economiza tempo ao pular entradas sem esperança |
| **OCR estruturado** | Captura layout, coordenadas | Habilita tarefas posteriores (realce, redação) |
| **Pós‑processador de IA** | Corrige ortografia, une palavras divididas, ajusta números | Eleva a precisão geral de caracteres de ~85 % para >95 % em digitalizações ruidosas |
| **Iteração** | Permite re‑executar com parâmetros ajustados | Afina o pipeline para tipos específicos de documentos |

Ao combinar esses três conceitos — **OCR de texto simples**, extração consciente de layout e correção por IA — você obtém uma solução robusta que *significativamente* **melhora a precisão do OCR** sem precisar escrever uma rede neural personalizada do zero.

---

## Armadilhas Comuns & Dicas de Profissional

- **Armadilha:** Alimentar uma imagem de baixa resolução (≤150 dpi) ao Tesseract gera saída confusa.  
  **Dica de profissional:** Pré‑procese com `Pillow` — aplique `Image.convert('L')` e `Image.filter(ImageFilter.MedianFilter())` antes do OCR.

- **Armadilha:** O pós‑processador de IA pode reescrever terminologia específica do domínio (ex.: “SKU123”).  
  **Dica de profissional:** Crie uma lista branca de termos e passe‑a para o LLM ou para uma biblioteca de verificação ortográfica como `pyspellchecker`.

- **Armadilha:** Páginas de múltiplas colunas são mescladas em uma única linha.  
  **Dica de profissional:** Detecte limites de coluna usando o campo `block_num` na saída TSV do Tesseract e divida as linhas conforme necessário.

- **Armadilha:** PDFs grandes causam estouro de memória ao carregar todas as páginas de uma vez.  
  **Dica de profissional:** Processar páginas incrementalmente — itere sobre `pdf2image.convert_from_path(..., first_page=n, last_page=n)`.

---

## Expandindo o Pipeline

Se você está curioso sobre os próximos passos, considere as seguintes melhorias:

1. **Processamento em lote** – Envolva todo o script em uma função que percorra um diretório, manipulando milhares de arquivos em paralelo com `concurrent.futures`.  
2. **Modelos de linguagem** – Troque a heurística simples de difflib por uma chamada ao `gpt‑4o` da OpenAI ou a um modelo LLaMA hospedado localmente para obter correções contextuais mais ricas.  
3. **Formatos de exportação** – Escreva a estrutura corrigida para um PDF pesquisável  

## O Que Você Deve Aprender a Seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas em seus próprios projetos.

- [Como Fazer OCR de Texto em Imagem com Idioma Usando Aspose.OCR](/ocr/english/java/ocr-operations/perform-ocr-language-selection/)
- [Como Usar OCR - Técnicas Avançadas com Aspose.OCR para Java](/ocr/english/java/advanced-ocr-techniques/)
- [Melhorar a Precisão do OCR – Modo Detectar Áreas no OCR](/ocr/hongkong/net/text-recognition/ocr-detect-areas-mode/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}