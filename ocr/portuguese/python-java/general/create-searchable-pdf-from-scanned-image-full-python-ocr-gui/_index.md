---
category: general
date: 2026-07-05
description: Crie PDF pesquisável com Python. Aprenda a fazer OCR em um PNG escaneado,
  converter PDF de imagem escaneada e obter um PDF pesquisável em minutos.
draft: false
keywords:
- create searchable pdf
- convert scanned image pdf
- how to ocr pdf
- ocr recognition example
- convert png searchable pdf
language: pt
og_description: Crie PDF pesquisável rapidamente. Este guia mostra como fazer OCR
  em um PNG, converter PDF de imagem escaneada e gerar um PDF pesquisável usando Python.
og_title: Criar PDF pesquisável a partir de imagem escaneada – Tutorial de OCR em
  Python
schemas:
- author: Aspose
  dateModified: '2026-07-05'
  description: Create searchable PDF with Python. Learn how to OCR a scanned PNG,
    convert scanned image PDF, and get a searchable PDF in minutes.
  headline: Create Searchable PDF from Scanned Image – Full Python OCR Guide
  type: TechArticle
tags:
- OCR
- Python
- PDF
- Automation
title: Criar PDF pesquisável a partir de imagem escaneada – Guia completo de OCR em
  Python
url: /pt/python-java/general/create-searchable-pdf-from-scanned-image-full-python-ocr-gui/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável a partir de imagem escaneada – Guia completo de OCR em Python

Já se perguntou como **criar PDF pesquisável** a partir de uma foto escaneada sem pagar por software caro? Você não está sozinho. Em muitos escritórios, os PDFs chegam como imagens planas — difíceis de pesquisar, impossíveis de copiar‑colar e um pesadelo para auditorias de conformidade. A boa notícia? Com algumas linhas de Python você pode transformar aquele PNG estático em um PDF totalmente pesquisável, e o processo é mais fácil do que você imagina.

Neste tutorial, vamos percorrer um **exemplo completo de reconhecimento OCR**, cobrindo tudo, desde a instalação da biblioteca correta até a gravação do arquivo PDF final. Ao final, você saberá exatamente como **converter PDFs de imagens escaneadas**, como **ocr pdf programaticamente**, e terá um script reutilizável que pode ser inserido em qualquer projeto.

## O que você aprenderá

- Instalar e configurar uma biblioteca Python de OCR (usaremos `pytesseract` e `pdf2image`).
- Inicializar o motor OCR e definir o idioma.
- Carregar um PNG escaneado (ou qualquer imagem) e executar OCR nele.
- Converter o resultado do OCR em um **PDF pesquisável** (array de bytes) e salvá‑lo.
- Dicas para lidar com documentos de múltiplas páginas, diferentes idiomas e armadilhas comuns.

Nenhuma experiência prévia com OCR é necessária — apenas um ambiente Python 3 funcionando e um pouco de curiosidade.

---

## Criar PDF pesquisável – Visão geral

Below is a high‑level flowchart of the steps we’ll implement.  

![Create searchable PDF workflow diagram](https://example.com/flowchart.png "Create searchable PDF workflow diagram")

*Texto alternativo: Diagrama de fluxo para criar PDF pesquisável mostrando inicialização do motor, carregamento da imagem, reconhecimento OCR, conversão para PDF e gravação do arquivo.*

---

## Etapa 1: Inicializar o motor OCR (how to ocr pdf)

Por que precisamos inicializar alguma coisa? O motor OCR é o cérebro que interpreta padrões de pixels como caracteres. Ao criar uma instância do motor e definir explicitamente o idioma, informamos à biblioteca qual alfabeto esperar, o que melhora drasticamente a precisão.

```python
import pytesseract
from pdf2image import convert_from_path
from PIL import Image
import io

# Ensure Tesseract is on your PATH or provide the executable location
pytesseract.pytesseract.tesseract_cmd = r"/usr/local/bin/tesseract"  # adjust as needed

# Define the language – ENGLISH is the default, but you can add more (e.g., 'fra' for French)
ocr_language = "eng"
```

**Dica profissional:** Se precisar fazer OCR em documentos com vários idiomas, instale os pacotes de idioma correspondentes para o Tesseract e passe uma lista como `"eng+spa"` para `ocr_language`.

---

## Etapa 2: Carregar a imagem escaneada (convert scanned image pdf)

A próxima peça do quebra‑cabeça é obter os dados da imagem no Python. Seja um PNG único ou um TIFF de múltiplas páginas, a classe `PIL.Image` pode abri‑lo. Se você estiver começando a partir de um PDF que já contém imagens escaneadas, `pdf2image` converterá cada página em uma imagem para nós.

```python
# Path to the scanned image (PNG, JPG, TIFF, etc.)
image_path = "YOUR_DIRECTORY/scanned_agreement.png"

# Open the image using Pillow
image = Image.open(image_path)

# If you were starting from a scanned PDF, you could do:
# pages = convert_from_path("scanned.pdf", dpi=300)
# image = pages[0]  # just take the first page for this example
```

**Por que isso importa:** Carregar a imagem como um objeto Pillow nos dá acesso aos seus dados de pixel brutos, que o motor OCR necessita. Pular esta etapa e alimentar bytes crus diretamente causaria erros.

---

## Etapa 3: Executar reconhecimento OCR na imagem (ocr recognition example)

Agora a parte divertida — deixar o motor ler o texto. `pytesseract.image_to_pdf_or_hocr` retorna um fluxo de bytes PDF que já contém uma camada de texto invisível, que é exatamente o que precisamos para um **PDF pesquisável**.

```python
# Run OCR and ask for a PDF output (includes the hidden text layer)
pdf_bytes = pytesseract.image_to_pdf_or_hocr(
    image,
    lang=ocr_language,
    extension='pdf'  # returns PDF bytes
)

# pdf_bytes is a binary blob that can be saved directly to disk
```

**Caso extremo:** Se sua imagem tem baixo contraste, considere aplicar um limiar simples antes do OCR:

```python
# Convert to grayscale and increase contrast
gray = image.convert('L')
threshold = gray.point(lambda x: 0 if x < 128 else 255, '1')
pdf_bytes = pytesseract.image_to_pdf_or_hocr(threshold, lang=ocr_language, extension='pdf')
```

Esta pequena etapa de pré‑processamento pode aumentar a precisão drasticamente.

---

## Etapa 4: Gravar os bytes do PDF em um arquivo (convert png searchable pdf)

A biblioteca OCR nos entrega um array de bytes — pense nele como o conteúdo bruto de um arquivo PDF. Tudo que precisamos fazer agora é gravar esses bytes no disco.

```python
output_path = "YOUR_DIRECTORY/agreement_searchable.pdf"

with open(output_path, "wb") as f:
    f.write(pdf_bytes)

print(f"✅ Searchable PDF created at: {output_path}")
```

**O que você verá:** Abra o arquivo resultante em qualquer visualizador de PDF e tente buscar uma palavra que você sabe que aparece na imagem original. O destaque deve pular diretamente para a localização, provando que a camada de texto invisível funciona.

---

## Etapa 5: Extender para documentos de múltiplas páginas (convert scanned image pdf)

Contratos do mundo real frequentemente abrangem várias páginas. Para **converter PDFs de imagens escaneadas** que contêm várias páginas, percorra cada página, faça OCR e concatene os PDFs resultantes.

```python
def ocr_image_to_pdf(image_obj, lang="eng"):
    """Helper that returns PDF bytes for a single image."""
    return pytesseract.image_to_pdf_or_hocr(image_obj, lang=lang, extension='pdf')

def merge_pdfs(pdf_bytes_list):
    """Combine multiple PDF byte streams into one."""
    from PyPDF2 import PdfMerger
    merger = PdfMerger()
    for i, pdf_bytes in enumerate(pdf_bytes_list):
        merger.append(io.BytesIO(pdf_bytes))
    output = io.BytesIO()
    merger.write(output)
    merger.close()
    return output.getvalue()

# Example: convert a multi‑page scanned PDF to searchable PDF
pages = convert_from_path("YOUR_DIRECTORY/scanned_contract.pdf", dpi=300)
pdf_parts = [ocr_image_to_pdf(p, lang=ocr_language) for p in pages]
final_pdf = merge_pdfs(pdf_parts)

with open("YOUR_DIRECTORY/contract_searchable.pdf", "wb") as f:
    f.write(final_pdf)

print("✅ Multi‑page searchable PDF created.")
```

**Por que mesclar?** Cada chamada a `image_to_pdf_or_hocr` produz um PDF independente. Mesclá‑los garante que o documento final preserve a ordem original das páginas.

---

## Armadilhas comuns e como corrigi‑las

| Sintoma | Causa provável | Correção |
|---------|----------------|----------|
| Nenhum texto pesquisável ao abrir o PDF | Tesseract não encontrou nenhum caractere (saída em branco) | Verifique a qualidade da imagem, aumente o DPI ou aplique pré‑processamento (contraste, binarização). |
| Caracteres corrompidos (ex.: �) | Pacote de idioma errado ou fontes ausentes | Instale os dados de idioma corretos (`tesseract‑lang‑eng`) e assegure que `ocr_language` corresponda. |
| Tamanho do arquivo PDF enorme (>10 MB para uma imagem de uma página) | Usando PNG sem perdas como fonte; OCR adiciona uma imagem em resolução total | Reduza a escala da imagem antes do OCR (`image.thumbnail((1240, 1754))` para A4). |
| Script falha no Windows com “tesseract.exe not found” | Binário do Tesseract não está no PATH | Adicione `pytesseract.pytesseract.tesseract_cmd = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"` (ajuste o caminho). |

---

## Script completo, pronto‑para‑executar

Juntando tudo, aqui está um único arquivo que você pode copiar‑colar e executar:

```python
#!/usr/bin/env python3
"""
create_searchable_pdf.py
A complete example that converts a scanned PNG (or PDF) into a searchable PDF using Tesseract OCR.
"""

import io
import sys
from pathlib import Path

import pytesseract
from pdf2image import convert_from_path
from PIL import Image
from PyPDF2 import PdfMerger

# -------------------- Configuration --------------------
# Adjust these paths for your environment
TESSERACT_CMD = r"/usr/local/bin/tesseract"   # macOS/Linux
# TESSERACT_CMD = r"C:\\Program Files\\Tesseract-OCR\\tesseract.exe"  # Windows
OCR_LANGUAGE = "eng"                         # Add '+spa' for Spanish, etc.
INPUT_PATH = Path("YOUR_DIRECTORY/scanned_agreement.png")
OUTPUT_PATH = Path("YOUR_DIRECTORY/agreement_searchable.pdf")
# -------------------------------------------------------

# Point pytesseract at the executable
pytesseract.pytesseract.tesseract_cmd = TESSERACT_CMD

def load_image(path: Path) -> Image.Image:
    """Load an image from disk; supports PNG, JPG, TIFF."""
    if not path.is_file():
        sys.exit(f"❌ File not found: {path}")
    return Image.open(path)

def ocr_to_pdf_bytes(img: Image.Image, lang: str = OCR_LANGUAGE) -> bytes:
    """Run OCR on a Pillow image and return PDF bytes with hidden text."""
    return pytesseract.image_to_pdf_or_hocr(img, lang=lang, extension='pdf')

def write_pdf(data: bytes, dest: Path):
    """Write PDF byte stream to a file."""
    dest.parent.mkdir(parents=True, exist_ok=True)
    with open(dest, "wb") as f:
        f.write(data)
    print(f"✅ Searchable PDF saved to {dest}")

def main():
    # Load the scanned image
    image = load_image(INPUT_PATH)

    # Optional: improve contrast for low‑quality scans
    # image = image.convert('L').point(lambda x: 0 if x < 128 else 255, '1')

    # OCR → PDF bytes
    pdf_bytes = ocr_to_pdf_bytes(image)

    # Save the result
    write_pdf(pdf_bytes, OUTPUT_PATH)

if __name__ == "__main__":
    main()
```

Salve isso como `create_searchable_pdf.py`, substitua os marcadores pelos caminhos reais e execute:

```bash
python create_searchable_pdf.py
```

Você deve ver um

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos estreitamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como fazer OCR de PDF em .NET com Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Converter imagens para PDF C# – Salvar resultado OCR de múltiplas páginas](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)
- [Reconhecimento OCR de documentos PDF no Aspose.OCR para Java](/ocr/hongkong/java/ocr-operations/recognize-pdf/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}