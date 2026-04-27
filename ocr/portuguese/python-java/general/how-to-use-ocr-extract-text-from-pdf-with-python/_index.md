---
category: general
date: 2026-04-26
description: como usar OCR em PDFs escaneados, extrair texto de PDF, executar OCR
  em PDF e converter PDF escaneado em arquivos pesquisáveis em poucos passos.
draft: false
keywords:
- how to use OCR
- extract text from pdf
- run OCR on pdf
- convert scanned pdf
- load pdf as image
language: pt
og_description: 'como usar OCR em Python: aprenda a extrair texto de PDF, executar
  OCR em PDF e converter PDF escaneado em documentos pesquisáveis.'
og_title: como usar OCR – Guia rápido para extrair texto de PDF
tags:
- OCR
- Python
- PDF
- Text Extraction
title: como usar OCR – Extrair texto de PDF com Python
url: /pt/python-java/general/how-to-use-ocr-extract-text-from-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como usar OCR – Extrair Texto de PDF com Python

Já se perguntou **como usar OCR** para extrair texto de um contrato, recibo ou ebook digitalizado? Você não está sozinho. Em muitos projetos do mundo real, o PDF que você recebe é apenas uma imagem, e sem OCR você não pode pesquisar, indexar ou analisar seu conteúdo.  

Neste tutorial vamos percorrer um exemplo completo e executável que mostra **como usar OCR**, como **extrair texto de PDF**, e por que você pode querer **converter PDF digitalizado** em documentos pesquisáveis. Também abordaremos a arte sutil de **carregar PDF como imagem** para que o motor de OCR veja cada página claramente.

> **Pré‑visualização rápida:** Ao final, você terá um script que carrega um PDF de várias páginas, executa OCR em cada página e imprime o texto reconhecido – sem necessidade de serviços externos.

## O que você precisará

- Python 3.9+ (qualquer versão recente funciona)
- Pacote `aocr` (ou qualquer biblioteca OCR compatível que forneça `OcrEngine` e `Image.load`)
- Um arquivo PDF digitalizado que você deseja processar (por exemplo, `contract.pdf`)
- Uma quantidade modesta de RAM (≈ 200 MB por PDF de 100 páginas costuma ser suficiente)

Se ainda não instalou a biblioteca OCR, execute:

```bash
pip install aocr
```

> **Dica profissional:** Use um ambiente virtual para manter suas dependências organizadas.

## Etapa 1: Carregar PDF como Imagem – A Primeira Peça do Quebra‑cabeça

Antes que qualquer OCR possa acontecer, o PDF deve ser representado como uma imagem. É aqui que a palavra‑chave secundária **load pdf as image** entra em ação.

```python
# Step 1: Create an OCR engine instance
ocr_engine = OcrEngine()

# Step 2: Load the PDF file as a multi‑page image
ocr_engine.image = aocr.Image.load("YOUR_DIRECTORY/contract.pdf")
```

*Por que isso importa:* `aocr.Image.load` rasteriza internamente cada página do PDF em um bitmap que o motor de OCR pode entender. Se você pular esta etapa e alimentar o PDF bruto, o motor lançará um erro porque espera dados de pixel, não dados vetoriais.

> **Nota:** O caminho pode ser absoluto ou relativo. Certifique‑se de que o arquivo seja legível; caso contrário, você encontrará um `FileNotFoundError`.

## Etapa 2: Executar OCR no PDF – Transformando Pixels em Caracteres

Agora que o PDF está como imagem, podemos finalmente **run OCR on PDF**. O trecho a seguir processa todas as páginas de uma vez:

```python
# Step 3: Run OCR on every page of the document
page_results = ocr_engine.process_all_pages()
```

*O que está acontecendo nos bastidores?* `process_all_pages` percorre as páginas rasterizadas, aplica o modelo OCR e devolve uma lista de objetos de resultado — um por página. Cada resultado contém o texto reconhecido, pontuações de confiança e caixas delimitadoras (se você precisar delas depois).

## Etapa 3: Extrair Texto de PDF – Tirando as Strings

Com os resultados de OCR em mãos, extrair o texto puro torna‑se trivial. Vamos iterar sobre as páginas e imprimir a saída, demonstrando a palavra‑chave secundária **extract text from pdf**.

```python
# Step 4: Iterate through the results and output the recognized text
for page_number, page_result in enumerate(page_results, start=1):
    print(f"--- Page {page_number} ---")
    print(page_result.text)
```

**Saída esperada** (truncada para brevidade):

```
--- Page 1 ---
This Agreement is made on the 1st day of January...
--- Page 2 ---
Section 2.1: Definitions...
```

Se precisar do texto em uma única string, basta concatenar:

```python
full_text = "\n".join(r.text for r in page_results)
```

Agora você extraiu com sucesso **texto de PDF** usando OCR.

## Etapa 4: Converter PDF Digitalizado – Tornando‑o Pesquisável

Muitas ferramentas downstream (como Elasticsearch ou SharePoint) esperam um PDF pesquisável em vez de um despejo de texto puro. Você pode incorporar a saída do OCR de volta ao PDF original, efetivamente **convert scanned PDF** em uma versão pesquisável.

```python
# Optional: Create a searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"
ocr_engine.save_searchable_pdf(searchable_pdf_path)
print(f"Searchable PDF saved to {searchable_pdf_path}")
```

*Por que se preocupar?* Um PDF pesquisável mantém o layout e as imagens originais enquanto permite seleção de texto e indexação — um ganho para humanos e máquinas.

## Armadilhas Comuns & Casos Limítrofes

### PDFs de Múltiplas Páginas Maiores que a Memória

Se seu PDF tem centenas de páginas, carregar tudo de uma vez pode esgotar a RAM. A biblioteca `aocr` suporta carregamento preguiçoso:

```python
ocr_engine.image = aocr.Image.load("bigfile.pdf", lazy=True)
```

Então processe as páginas uma a uma:

```python
for page in ocr_engine.image.iter_pages():
    result = ocr_engine.process_page(page)
    print(result.text)
```

### Digitalizações de Baixa Qualidade

A precisão do OCR cai drasticamente em digitalizações borradas ou de baixo contraste. Antes de alimentar a imagem ao motor, considere pré‑processamento:

```python
from aocr import preprocess

# Improve contrast and denoise
clean_image = preprocess.enhance(ocr_engine.image, contrast=1.5, denoise=True)
ocr_engine.image = clean_image
```

### Suporte a Idiomas

Por padrão, o motor assume inglês. Para **run OCR on PDF** em outro idioma, defina o código de idioma:

```python
ocr_engine.language = "spa"  # Spanish
```

Certifique‑se de que o modelo de idioma correspondente esteja instalado.

## Exemplo Completo Funcional

Juntando tudo, aqui está um script autocontido que você pode colocar em um arquivo chamado `ocr_pdf.py` e executar imediatamente:

```python
# ocr_pdf.py
from aocr import OcrEngine, Image, preprocess

def main(pdf_path: str, output_path: str = None):
    # Initialize OCR engine
    ocr_engine = OcrEngine()

    # Load PDF as image (lazy loading for large files)
    ocr_engine.image = Image.load(pdf_path, lazy=False)

    # Optional preprocessing – improves accuracy on noisy scans
    ocr_engine.image = preprocess.enhance(ocr_engine.image, contrast=1.4, denoise=True)

    # Run OCR on all pages
    page_results = ocr_engine.process_all_pages()

    # Print extracted text
    for i, result in enumerate(page_results, start=1):
        print(f"--- Page {i} ---")
        print(result.text)

    # If a searchable PDF is desired
    if output_path:
        ocr_engine.save_searchable_pdf(output_path)
        print(f"Searchable PDF saved to {output_path}")

if __name__ == "__main__":
    import argparse
    parser = argparse.ArgumentParser(description="Extract text from a scanned PDF using OCR.")
    parser.add_argument("pdf", help="Path to the input scanned PDF")
    parser.add_argument("-o", "--output", help="Path to save searchable PDF (optional)")
    args = parser.parse_args()
    main(args.pdf, args.output)
```

Execute assim:

```bash
python ocr_pdf.py YOUR_DIRECTORY/contract.pdf -o YOUR_DIRECTORY/contract_searchable.pdf
```

Você verá o texto impresso no console e, se forneceu `-o`, um PDF pesquisável aparecerá ao lado do arquivo original.

## Dicas Profissionais & Melhores Práticas

- **Processamento em lote:** Ao lidar com dezenas de PDFs, envolva a lógica acima em um loop e registre o sucesso/falha de cada arquivo.
- **Filtragem por confiança:** Cada `page_result` inclui uma métrica de confiança. Descarte ou sinalize páginas com baixa confiança para revisão manual.
- **Paralelismo:** Se sua CPU tem múltiplos núcleos, considere usar `concurrent.futures` para processar páginas em paralelo — apenas fique atento ao uso de memória.
- **Bloqueio de versão:** A API `aocr` pode evoluir. Fixe a versão em `requirements.txt` (ex.: `aocr==2.3.1`) para evitar quebras.

## Conclusão

Percorremos **como usar OCR** para **extrair texto de PDF**, **run OCR on PDF**, **load PDF as image**, e até **convert scanned PDF** em um formato pesquisável. O código está completo, as explicações cobrem tanto o *quê* quanto o *porquê*, e agora você tem um padrão reutilizável para qualquer projeto que lide com PDFs baseados em imagem.

O que vem a seguir? Experimente alimentar o texto extraído em um pipeline de linguagem natural, indexe os PDFs pesquisáveis com Elasticsearch, ou teste diferentes back‑ends de OCR como Tesseract ou Azure Computer Vision. O céu é o limite, e as ferramentas estão ao seu alcance.

Feliz codificação, e que seus PDFs estejam sempre pesquisáveis! 

![exemplo de como usar OCR](/images/ocr_workflow.png "como usar OCR")

---

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}