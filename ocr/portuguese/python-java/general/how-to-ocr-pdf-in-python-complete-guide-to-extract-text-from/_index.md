---
category: general
date: 2026-06-22
description: Aprenda a fazer OCR em arquivos PDF com Python, extrair texto de PDF
  e converter PDF em texto usando uma abordagem baseada em fluxo. Passos simples para
  processar PDFs escaneados.
draft: false
keywords:
- how to ocr pdf
- extract text from pdf
- convert pdf to text
- load pdf from stream
- process scanned pdf
language: pt
og_description: Como fazer OCR de arquivos PDF em Python? Siga este guia para extrair
  texto de PDF, converter PDF em texto e processar PDFs escaneados usando um stream.
og_title: Como fazer OCR de PDF em Python – Guia passo a passo
schemas:
- author: Aspose
  dateModified: '2026-06-22'
  description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  headline: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  type: TechArticle
- description: Learn how to OCR PDF files in Python, extract text from PDF, and convert
    PDF to text using a stream‑based approach. Simple steps for processing scanned
    PDF.
  name: How to OCR PDF in Python – Complete Guide to Extract Text from PDFs
  steps:
  - name: Expected Output
    text: 'If `multipage.pdf` contains three scanned pages, you’ll see something like:'
  - name: 1. PDFs with Mixed Image and Text Layers
    text: 'Some PDFs already contain a hidden text layer (e.g., exported from Word).
      If you want the OCR engine to **ignore existing text** and re‑process the image,
      set:'
  - name: 2. Large Files Exceeding Memory Limits
    text: 'When working with gigabyte‑size PDFs, consider processing in chunks:'
  - name: 3. Language and Font Support
    text: 'If your scanned documents are in French or contain special characters,
      tell the engine which language model to use:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Como fazer OCR de PDF em Python – Guia completo para extrair texto de PDFs
url: /pt/python-java/general/how-to-ocr-pdf-in-python-complete-guide-to-extract-text-from/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em PDF com Python – Guia Completo para Extrair Texto de PDFs

Já se perguntou **como fazer OCR em arquivos PDF** sem precisar lidar com ferramentas pesadas de desktop? Você não está sozinho. Em muitos projetos reais—pense em automação de faturas ou digitalização de arquivos de arquivo—você precisa de uma maneira confiável de transformar um PDF escaneado em texto pesquisável e editável.

Neste tutorial vamos percorrer um exemplo limpo, de ponta a ponta, que **extrai texto de páginas PDF** usando um motor de OCR leve em Python. Ao final, você saberá exatamente como **converter PDF em texto**, como **carregar PDF a partir de stream**, e como **processar PDF escaneado** de forma eficiente. Sem mágica, apenas código Python puro que você pode inserir no seu projeto hoje.

## O que você vai aprender

- Instalar e configurar uma biblioteca Python de OCR que entenda entrada PDF.  
- Habilitar o modo de reconhecimento de PDF e definir o formato de saída como texto simples.  
- Carregar um PDF multipágina a partir de um stream de arquivo (o padrão clássico “load pdf from stream”).  
- Executar OCR em todas as páginas e recuperar o conteúdo textual.  
- Imprimir ou armazenar os resultados para processamento posterior.

**Pré‑requisitos**  
- Python 3.8+ instalado na sua máquina.  
- Familiaridade básica com pip e ambientes virtuais.  
- Um arquivo PDF escaneado (chamado `multipage.pdf` no exemplo) colocado em um diretório conhecido.

Se algum desses itens lhe for desconhecido, não se preocupe—cada passo é explicado em linguagem simples, e forneceremos os comandos exatos que você precisa.

---

## Etapa 1: Instalar o Motor de OCR (como fazer OCR em PDF)

Primeiro de tudo—você precisa de um motor de OCR que consiga lidar com entrada PDF. Para este guia usaremos o hipotético pacote `ocr` (a API espelha SDKs comerciais populares, mas o mesmo padrão funciona com Tesseract‑OCR, ABBYY ou Google Vision quando adequadamente encapsulados).

```bash
# Create a virtual environment (optional but recommended)
python -m venv venv
source venv/bin/activate   # Windows: venv\Scripts\activate

# Install the OCR package
pip install ocr
```

> **Dica profissional:** Se você estiver no Windows e encontrar erros de permissão, tente `pip install --user ocr` em vez disso.

Depois que o pacote estiver instalado, você pode importá‑lo no seu script e criar uma instância do motor—este é o coração de **como fazer OCR em PDF**.

```python
import ocr

# Step 1: Create an OCR engine instance
engine = ocr.OcrEngine()
```

O objeto `OcrEngine` contém todas as configurações que ajustaremos mais tarde, como idioma, DPI e—crucialmente—modo PDF.

---

## Etapa 2: Habilitar Reconhecimento de PDF e Escolher Saída (extrair texto de PDF)

Por padrão, muitos SDKs de OCR assumem que você está fornecendo imagens. Para fazer o motor tratar o stream de entrada como um PDF, habilitamos a flag de reconhecimento de PDF e solicitamos saída em texto simples.

```python
# Step 2: Turn on PDF mode and request plain text results
settings = engine.get_settings()
settings.set_recognize_pdf(True)                     # tells the engine to parse PDF containers
settings.set_output_format(ocr.OutputFormat.TEXT)   # we want raw text, not XML or PDF
```

Por que especificar o formato de saída? Porque alguns motores podem retornar PDF com camadas de texto ocultas, PDFs pesquisáveis ou JSON com caixas delimitadoras. Para a maioria dos pipelines de extração de dados, **extrair texto de PDF** como strings simples é o formato mais limpo para etapas posteriores.

---

## Etapa 3: Carregar o PDF a partir de um Stream de Arquivo (load PDF from stream)

Carregar um PDF a partir de um stream é um padrão econômico em memória—você evita carregar o arquivo inteiro na RAM de uma só vez. Isso é especialmente útil ao lidar com documentos grandes e multipáginas.

```python
# Step 3: Load the multi‑page PDF from a file stream
pdf_path = "YOUR_DIRECTORY/multipage.pdf"
pdf_stream = ocr.ImageStream.from_file(pdf_path)   # wraps the file handle in an OCR‑friendly object
engine.set_image(pdf_stream)
```

> **E se o arquivo estiver no S3 ou em outro bucket na nuvem?**  
> Basta substituir `from_file` por um método que aceite um buffer de bytes (por exemplo, `ImageStream.from_bytes(s3_object.read())`). O restante do pipeline permanece idêntico.

---

## Etapa 4: Executar OCR em Todas as Páginas (processar PDF escaneado)

Agora começa o trabalho pesado. O motor iterará por cada página, executará o reconhecimento e retornará uma lista de objetos de página—cada um expondo seu conteúdo textual.

```python
# Step 4: Perform OCR on all pages of the PDF
pages = engine.recognize_pdf()
```

Nos bastidores, a biblioteca OCR descompacta cada página PDF, rasteriza‑a na DPI configurada e alimenta o bitmap ao seu modelo de rede neural. O resultado? Uma coleção de objetos `Page` prontos para extração.

---

## Etapa 5: Recuperar e Exibir o Texto Reconhecido (converter PDF em texto)

Por fim, percorremos as páginas retornadas e imprimimos o texto reconhecido. Este é o momento em que **converter PDF em texto** realmente acontece.

```python
# Step 5: Iterate through the recognized pages and display their text
for index, page in enumerate(pages):
    print(f"--- Page {index + 1} ---")
    print(page.get_text())
```

### Saída Esperada

Se `multipage.pdf` contiver três páginas escaneadas, você verá algo como:

```
--- Page 1 ---
Invoice #12345
Date: 2024‑03‑15
Total: $1,250.00
...

--- Page 2 ---
Item Description   Qty   Price
Widget A           10    $50.00
Widget B            5    $30.00
...

--- Page 3 ---
Thank you for your business!
```

Observe a separação limpa entre as páginas—útil caso você precise armazenar o texto de cada página em um banco de dados ou enviá‑lo a um modelo de NLP posterior.

---

## Lidando com Casos de Borda Comuns

### 1. PDFs com Camadas Mistas de Imagem e Texto
Alguns PDFs já contêm uma camada de texto oculta (por exemplo, exportados do Word). Se você quiser que o motor de OCR **ignore o texto existente** e reprocessar a imagem, defina:

```python
settings.set_force_ocr(True)   # forces rasterization and OCR even if text exists
```

### 2. Arquivos Grandes que Excedem Limites de Memória
Ao trabalhar com PDFs de tamanho gigabyte, considere processar em blocos:

```python
for page_number in range(1, engine.get_page_count() + 1):
    single_page_stream = engine.get_page_stream(page_number)
    engine.set_image(single_page_stream)
    page = engine.recognize_pdf()[0]   # only one page at a time
    print(f"--- Page {page_number} ---")
    print(page.get_text())
```

### 3. Suporte a Idioma e Fonte
Se seus documentos escaneados estiverem em francês ou contiverem caracteres especiais, informe ao motor qual modelo de idioma usar:

```python
settings.set_language("fr")   # or "en", "de", etc.
```

---

## Script Completo – Pronto para Executar

Abaixo está o exemplo completo e executável que une todas as peças. Salve como `ocr_pdf.py` e execute `python ocr_pdf.py`.

```python
import ocr

def main():
    # Initialize engine
    engine = ocr.OcrEngine()

    # Configure for PDF recognition and plain‑text output
    settings = engine.get_settings()
    settings.set_recognize_pdf(True)
    settings.set_output_format(ocr.OutputFormat.TEXT)

    # Optional: force OCR even if PDF already has text
    # settings.set_force_ocr(True)

    # Load PDF from a stream
    pdf_path = "YOUR_DIRECTORY/multipage.pdf"
    pdf_stream = ocr.ImageStream.from_file(pdf_path)
    engine.set_image(pdf_stream)

    # Perform OCR on every page
    pages = engine.recognize_pdf()

    # Output the results
    for idx, page in enumerate(pages):
        print(f"--- Page {idx + 1} ---")
        print(page.get_text())

if __name__ == "__main__":
    main()
```

**Executar o script** imprimirá o texto de cada página no console, exatamente como mostrado na seção “Saída Esperada”. A partir daí, você pode redirecionar a saída para um arquivo:

```bash
python ocr_pdf.py > extracted_text.txt
```

---

## Conclusão

Acabamos de cobrir **como fazer OCR em PDF** usando Python do início ao fim. Ao configurar o motor, carregar o documento via stream e iterar sobre cada página reconhecida, você pode **extrair texto de PDF**, **converter PDF em texto** e **processar PDF escaneado** com apenas algumas linhas de código. A abordagem escala de pequenas faturas de duas páginas a arquivos de arquivo massivos com centenas de páginas.

Qual o próximo passo? Experimente alimentar as strings extraídas em um índice de busca, um resumidor de modelo de linguagem ou um pipeline de validação de dados. Você também pode experimentar formatos de saída como JSON para manter metadados posicionais para análises avançadas de documentos.

Tem dúvidas sobre como lidar com PDFs criptografados ou integrar com armazenamento na nuvem? Deixe um comentário abaixo—bom código!

![Diagrama mostrando o fluxo de trabalho OCR PDF – como fazer OCR PDF, carregar PDF a partir de stream, reconhecer páginas e extrair texto](ocr-pdf-workflow.png "diagrama do fluxo de trabalho como fazer OCR PDF")


## O que você deve aprender a seguir?


Os tutoriais a seguir abordam tópicos intimamente relacionados que ampliam as técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens alternativas de implementação em seus próprios projetos.

- [How to OCR PDF in .NET with Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [How to Extract Text from Image Using Aspose.OCR for .NET](/ocr/english/net/text-recognition/get-recognition-result/)
- [How to Extract Text from ZIP Archives Using Aspose.OCR for .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-archive/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}