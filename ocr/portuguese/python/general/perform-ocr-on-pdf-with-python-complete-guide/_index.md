---
category: general
date: 2026-06-25
description: Faça OCR em PDF usando Python — aprenda como carregar PDF para OCR, extrair
  texto das páginas do PDF e visualizar o texto reconhecido de forma eficiente.
draft: false
keywords:
- perform OCR on PDF
- extract text from PDF pages
- load PDF for OCR
- how to OCR large PDF
- preview recognized text
language: pt
og_description: Execute OCR em PDF com Python. Este guia mostra como carregar PDF
  para OCR, extrair texto das páginas do PDF e visualizar rapidamente o texto reconhecido.
og_title: Realize OCR em PDF com Python – Tutorial passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  headline: Perform OCR on PDF with Python – Complete Guide
  type: TechArticle
- description: Perform OCR on PDF using Python—learn how to load PDF for OCR, extract
    text from PDF pages, and preview recognized text efficiently.
  name: Perform OCR on PDF with Python – Complete Guide
  steps:
  - name: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
    text: '**Parallelize per page** – Use `concurrent.futures.ThreadPoolExecutor`
      if the OCR engine is thread‑safe.'
  - name: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
    text: '**Cache intermediate images** – Some engines let you store rasterized pages
      on SSD, dramatically cutting CPU load on re‑runs.'
  - name: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
    text: '**Batch write output** – Instead of appending to a Python list, open the
      output file once and write each page’s text as soon as it’s ready.'
  - name: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
    text: '**Adjust DPI** – Lowering the DPI during rasterization reduces memory but
      may affect accuracy; find a sweet spot (usually 200‑300 DPI).'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Realize OCR em PDF com Python – Guia Completo
url: /pt/python/general/perform-ocr-on-pdf-with-python-complete-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Realizar OCR em PDF com Python – Guia Completo

Já precisou **realizar OCR em arquivos PDF** mas não sabia por onde começar? Talvez você tenha uma montanha de contratos escaneados, ou um único manual volumoso que se recusa a cooperar com seu extrator de texto habitual. Em resumo, você quer **carregar PDF para OCR**, extrair o texto e obter uma pré‑visualização rápida — tudo sem estourar a memória da sua máquina.

Bem, você está no lugar certo. Neste tutorial vamos percorrer um script Python totalmente funcional que **extrai texto de páginas PDF**, mostra como **visualizar o texto reconhecido** e ainda resolve o clássico problema de **como fazer OCR em PDF grande** de forma eficiente.

Ao final, você terá um programa pronto‑para‑executar, uma compreensão clara de cada parâmetro de configuração e várias dicas para evitar armadilhas comuns que atrapalham iniciantes.

---

## O que você vai aprender

- Como **carregar PDF para OCR** usando a biblioteca `aocr`.
- Os passos exatos para **realizar OCR em PDF** página por página.
- Formas de **extrair texto de páginas PDF** mantendo o uso de memória sob controle.
- Como **visualizar o texto reconhecido** para validar os resultados.
- Estratégias para lidar com **PDFs grandes** sem esgotar a RAM.

> **Dica:** Este guia assume que você tem Python 3.9+ instalado e familiaridade básica com ambientes virtuais. Se você é novo no Python, configure um virtualenv primeiro — confie em mim, isso evita dores de cabeça depois.

---

## Pré‑requisitos

| Requisito | Por que é importante |
|-----------|----------------------|
| Pacote Python `aocr` (ou qualquer motor OCR compatível) | Fornece a classe `OcrEngine` usada ao longo do script. |
| `pip` e um ambiente virtual | Mantém as dependências isoladas do Python do sistema. |
| Espaço em disco suficiente para extrações temporárias de imagens | Alguns motores OCR gravam imagens das páginas em disco antes de processá‑las. |
| Opcional: `tqdm` para barras de progresso | Melhora a experiência ao lidar com trabalhos de **como fazer OCR em PDF grande**. |

Instale o essencial com:

```bash
python -m venv ocr-env
source ocr-env/bin/activate   # Windows: ocr-env\Scripts\activate
pip install aocr tqdm
```

Se o seu PDF estiver protegido por senha, você precisará fornecê‑la posteriormente — veja a seção “Casos de Borda”.

---

## Etapa 1: Realizar OCR em PDF – Configurando o Motor

Primeiro de tudo, precisamos de uma instância do motor OCR. Pense nele como o cérebro que lerá a imagem de cada página e gerará texto puro.

```python
import aocr                     # The OCR library
from tqdm import tqdm           # Optional, for a nice progress bar

def create_engine():
    """
    Initialise the OcrEngine with sensible defaults.
    Returns the configured engine ready for processing.
    """
    engine = aocr.OcrEngine()
    # Limit memory usage – crucial when tackling how to OCR large PDF files
    engine.max_memory_mb = 200               # 200 MB cap, adjust if needed
    # Choose a recognition mode that matches your source material
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine
```

> **Por que definir `max_memory_mb`?**  
> Motores OCR costumam armazenar imagens das páginas em RAM. Ao limitar a memória, você impede que o script trave em um contrato de 500 páginas.

---

## Etapa 2: Carregar PDF para OCR e Configurar as Definições

Agora realmente **carregamos PDF para OCR**. O caminho pode ser absoluto ou relativo; apenas certifique‑se de que o arquivo exista.

```python
def load_pdf(engine, pdf_path):
    """
    Loads the PDF into the OCR engine.
    Raises FileNotFoundError if the file does not exist.
    """
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages ready.")
    except Exception as e:
        raise RuntimeError(f"Failed to load PDF: {e}")
```

Se o PDF estiver criptografado, `engine.load_pdf` normalmente lançará uma exceção. Nesse caso, você pode chamar `engine.load_pdf(pdf_path, password="secret")` — falaremos mais sobre isso adiante.

---

## Etapa 3: Extrair Texto de Páginas PDF – O Loop Principal

É aqui que **realizamos OCR em PDF** página por página. Também **visualizaremos o texto reconhecido** nos primeiros poucos centenas de caracteres para que você possa confirmar que tudo está funcionando.

```python
def ocr_pages(engine, preview_len=200):
    """
    Iterates over each page, runs OCR, and yields the recognized text.
    Also prints a short preview for each page.
    """
    for page_index in tqdm(range(engine.page_count), desc="Processing pages"):
        # Select the current page – essential for multi‑page PDFs
        engine.select_page(page_index)

        # Perform the actual OCR
        page_text = engine.recognize()

        # Preview the first `preview_len` characters (helps with debugging)
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))

        yield page_text
```

> **Dica de especialista:** A barra de progresso `tqdm` fornece um indicativo visual, especialmente útil ao lidar com documentos de **como fazer OCR em PDF grande** que levam minutos para processar.

---

## Etapa 4: Juntando Tudo – Um Script Pronto‑para‑Executar

A seguir está o exemplo completo e executável. Salve como `pdf_ocr.py` e execute com `python pdf_ocr.py caminho/para/seu/arquivo.pdf`.

```python
#!/usr/bin/env python3
"""
Complete script to perform OCR on PDF, extract text from PDF pages,
and preview recognized text. Works for both small and large PDFs.
"""

import sys
import aocr
from tqdm import tqdm

def create_engine():
    engine = aocr.OcrEngine()
    engine.max_memory_mb = 200
    engine.recognition_mode = aocr.RecognitionMode.PRINTED
    return engine

def load_pdf(engine, pdf_path):
    try:
        engine.load_pdf(pdf_path)
        print(f"✅ Loaded '{pdf_path}' – {engine.page_count} pages.")
    except Exception as exc:
        raise RuntimeError(f"Unable to load PDF: {exc}")

def ocr_pages(engine, preview_len=200):
    for page_index in tqdm(range(engine.page_count), desc="OCR progress"):
        engine.select_page(page_index)
        page_text = engine.recognize()
        print(f"\n--- Page {page_index + 1} Preview ---")
        print(page_text[:preview_len] + ("…" if len(page_text) > preview_len else ""))
        yield page_text

def main(pdf_path):
    engine = create_engine()
    load_pdf(engine, pdf_path)

    all_text = []
    for txt in ocr_pages(engine):
        all_text.append(txt)

    # Optional: write the combined output to a .txt file
    out_path = pdf_path.rsplit(".", 1)[0] + "_ocr.txt"
    with open(out_path, "w", encoding="utf-8") as f:
        f.write("\n\n".join(all_text))
    print(f"\n✅ OCR complete. Full text saved to: {out_path}")

if __name__ == "__main__":
    if len(sys.argv) != 2:
        print("Usage: python pdf_ocr.py <path_to_pdf>")
        sys.exit(1)
    pdf_file = sys.argv[1]
    main(pdf_file)
```

### Saída Esperada (trecho)

```
✅ Loaded 'large_contract.pdf' – 342 pages.

--- Page 1 Preview ---
Contract Agreement between Party A and Party B ... 

--- Page 2 Preview ---
Recitals: Whereas, the parties desire to ...

...
✅ OCR complete. Full text saved to: large_contract_ocr.txt
```

Você verá uma pré‑visualização curta para cada página, seguida de uma confirmação final de que o arquivo de texto concatenado foi gravado.

---

## Casos de Borda & Dicas Práticas

| Situação | O que fazer |
|----------|-------------|
| **PDF criptografado** | Passe a senha: `engine.load_pdf(pdf_path, password="mySecret")`. |
| **PDF muito grande (> 1000 páginas)** | Aumente `max_memory_mb` com cautela, ou processe em blocos (ex.: 200 páginas de cada vez). |
| **Conteúdo misto (impresso + manuscrito)** | Troque `engine.recognition_mode` para `aocr.RecognitionMode.MIXED` se a biblioteca suportar. |
| **Fontes ausentes ou baixa qualidade de escaneamento** | Pré‑procese as páginas com uma biblioteca de aprimoramento de imagem (ex.: Pillow) antes de chamar `recognize()`. |
| **Travamentos por falta de memória** | Reduza `preview_len` ou grave o texto de cada página diretamente no disco ao invés de mantê‑lo tudo em uma lista. |

---

## Como Fazer OCR em PDF Grande de Forma Eficiente – Estratégias Avançadas

Ao enfrentar **como fazer OCR em PDF grande**, velocidade e estabilidade se tornam críticas. Aqui vão alguns truques que você pode inserir no script:

1. **Paralelizar por página** – Use `concurrent.futures.ThreadPoolExecutor` se o motor OCR for thread‑safe.
2. **Cache de imagens intermediárias** – Alguns motores permitem armazenar páginas rasterizadas em SSD, reduzindo drasticamente a carga de CPU em execuções subsequentes.
3. **Gravar saída em lotes** – Em vez de acumular tudo em uma lista Python, abra o arquivo de saída uma única vez e escreva o texto de cada página assim que estiver pronto.
4. **Ajustar DPI** – Reduzir o DPI durante a rasterização diminui o uso de memória, mas pode afetar a precisão; encontre um ponto ideal (geralmente 200‑300 DPI).

Abaixo um trecho rápido mostrando como você poderia paralelizar a etapa de OCR (opcional, descomente para usar):

```python
# from concurrent.futures import ThreadPoolExecutor

# def ocr_page(engine, idx):
#     engine.select_page(idx)
#     return engine.recognize()

# with ThreadPoolExecutor(max_workers=4) as executor:
#     results = list(tqdm(executor.map(lambda i: ocr_page(engine, i),
#                                    range(engine.page_count)),
#                     total=engine.page_count,
#                     desc="Parallel OCR"))
```

Lembre‑se: paralelismo pode aumentar o uso de CPU, então monitore a temperatura do seu sistema em execuções longas.

---

## Perguntas Frequentes

**Q: Posso usar este script com outras bibliotecas OCR como o Tesseract?**  
A: Absolutamente. Substitua as chamadas `aocr` por `pytesseract.image_to

## O que você deve aprender a seguir?

Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Perform Image Text Extraction from Stream Using Aspose OCR](/ocr/english/net/image-and-drawing-recognition/recognize-image-from-stream/)
- [How to extract text from image from URL using Aspose.OCR for Java](/ocr/english/java/advanced-ocr-techniques/perform-ocr-image-from-url/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}