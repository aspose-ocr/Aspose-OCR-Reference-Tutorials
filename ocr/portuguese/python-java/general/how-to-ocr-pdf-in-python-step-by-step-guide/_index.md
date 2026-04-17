---
category: general
date: 2026-03-28
description: Aprenda a fazer OCR de PDF com Python rapidamente. Este guia mostra como
  extrair texto de PDF, reconhecer texto de PDF e converter PDF escaneado em texto
  usando o Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- ocr pdf with python
- extract text from pdf
- recognize text from pdf
- convert scanned pdf to text
language: pt
og_description: Domine como fazer OCR de PDF com Python. Extraia texto de PDF, reconheça
  texto de PDF e converta PDFs escaneados em texto em minutos.
og_title: Como fazer OCR de PDF em Python – Guia Completo
tags:
- PDF
- OCR
- Python
- Aspose
title: Como fazer OCR de PDF em Python – Guia passo a passo
url: /pt/python-java/general/how-to-ocr-pdf-in-python-step-by-step-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em PDF com Python – Guia Passo a Passo

Já se perguntou **como fazer OCR em PDF** quando o arquivo é apenas uma foto de uma página? Você não está sozinho. Neste tutorial vamos percorrer os passos exatos para fazer OCR em arquivos PDF, extrair texto de PDF e transformar um PDF escaneado em texto pesquisável — tudo com código Python puro.

Cobriremos tudo, desde a instalação da biblioteca Aspose OCR até a extração do texto reconhecido de cada página. Ao final, você será capaz de **OCR PDF com Python**, **extrair texto de PDF** e **converter PDF escaneado em texto** sem precisar vasculhar documentação espalhada. Sem enrolação, apenas um exemplo prático e executável que você pode copiar e colar.

## O que Você Precisa

Antes de mergulharmos, certifique‑se de que você tem:

* Python 3.8+ (a versão estável mais recente funciona melhor)  
* Uma licença do Aspose OCR for Python ou uma chave de avaliação gratuita – você pode obtê‑la no site da Aspose.  
* Um PDF escaneado que você deseja processar (vamos chamá‑lo de `input.pdf`).  

Se já tem tudo isso, ótimo — vamos começar. Caso contrário, a instalação do pacote é simples e vamos mostrar como fazer.

## Como Fazer OCR em PDF – Configurando o Ambiente

A primeira coisa que você precisa fazer é obter o módulo Aspose OCR na sua máquina. O pacote se chama `aspose-ocr` e pode ser instalado via pip:

```bash
pip install aspose-ocr
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv venv`) para que suas dependências fiquem organizadas.

Depois que o pacote estiver instalado, você está pronto para importá‑lo e iniciar o motor de OCR. Essa é a base para todo fluxo de **ocr pdf with python** que você criará depois.

## OCR PDF com Python – Importando Aspose OCR

Agora que a biblioteca está disponível, vamos trazê‑la para o nosso script. Também configuraremos o motor para trabalhar em *modo PDF direto*, que indica ao Aspose para ler os bytes do PDF diretamente do arquivo, em vez de converter cada página em imagem primeiro.

```python
# Step 1: Import the Aspose OCR module
import aspose.ocr as aocr

# Step 2: Create an OCR engine instance and enable direct PDF processing
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
```

Por que usar `PdfMode.DIRECT`? Porque ele pula uma etapa extra de rasterização, tornando o processo mais rápido e preservando o layout original — especialmente útil quando você precisa **recognize text from PDF** com precisão.

## Reconhecer Texto de PDF – Executando o Motor

Com o motor pronto, aponte‑o para o seu arquivo escaneado. O método `recognize_from_pdf` faz todo o trabalho pesado: ele analisa cada página, executa o algoritmo de OCR e devolve um objeto `OcrResult` que contém uma coleção de objetos `Page`.

```python
# Step 3: Define the path to the PDF you want to process
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# Step 4: Perform OCR on the PDF and obtain the result object
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)
```

Se você está se perguntando se isso funciona com PDFs criptografados — sim, basta fornecer a senha via `ocr_engine.password = "secret"` antes de chamar `recognize_from_pdf`. Esse é um caso de borda que muitos tutoriais ignoram, mas é útil em pipelines reais.

## Extrair Texto de PDF – Acessando os Resultados das Páginas

A lista `ocr_result.pages` contém uma entrada por página. Cada objeto `Page` tem um atributo `.text` que contém a representação em texto puro da página escaneada. Vamos percorrer a lista e imprimir os resultados para que você veja exatamente o que foi extraído.

```python
# Step 5: Iterate through each page and display the recognized text
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)
```

Executar o script exibirá algo como:

```
PDF OCR complete. Text per page:
--- Page 1 ---
Lorem ipsum dolor sit amet, consectetur adipiscing elit.
--- Page 2 ---
Sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
```

Essa saída prova que você conseguiu **extract text from PDF** e **recognize text from PDF** usando Aspose OCR. Agora você pode encaminhar as strings para um banco de dados, um índice de busca ou qualquer pipeline de NLP subsequente.

![exemplo de como OCR PDF](placeholder-image.png "exemplo de como OCR PDF")

*Texto alternativo da imagem:* **exemplo de como OCR PDF** – mostra a saída no console do texto reconhecido por página.

## Converter PDF Escaneado em Texto – Salvando a Saída

A maioria dos desenvolvedores não quer apenas ver o texto no console; eles precisam de um arquivo persistente. Abaixo está um pequeno helper que grava o texto de cada página em um arquivo `.txt` separado, efetivamente **convert scanned PDF to text** em uma pasta chamada `output`.

```python
import os

output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Depois que o script terminar, você terá um diretório organizado:

```
output_text/
│─ page_1.txt
│─ page_2.txt
└─ …
```

Agora você completou **convert scanned PDF to text** e pode alimentar esses arquivos a qualquer processo posterior — busca, análise ou até mesmo um simples `grep`.

## Perguntas Frequentes & Casos de Borda

**E se meu PDF contiver imagens misturadas com texto real?**  
Aspose OCR tentará reconhecer tudo, mas você pode acelerar o processo desativando OCR para páginas que já contêm texto selecionável. Defina `ocr_engine.auto_detect_page_orientation = True` e então chame `ocr_engine.recognize_from_pdf(..., detect_text=False)` para as páginas que já estão boas.

**Posso controlar o modelo de idioma?**  
Com certeza. Defina `ocr_engine.language = aocr.Language.English` (ou qualquer idioma suportado) antes de chamar `recognize_from_pdf`. Isso melhora a precisão para documentos que não estejam em inglês.

**Como lidar com PDFs muito grandes (100+ páginas)?**  
Processá‑los em blocos. O método `recognize_from_pdf` aceita um argumento `page_range`, por exemplo, `ocr_engine.recognize_from_pdf(path, page_range=(1, 20))`. Percorra intervalos para manter o uso de memória baixo.

## Exemplo Completo Funcional

Juntando tudo, aqui está um script único que você pode salvar como `ocr_pdf.py` e executar:

```python
import os
import aspose.ocr as aocr

# -------------------------------------------------
# 1️⃣  Initialize the OCR engine (direct PDF mode)
# -------------------------------------------------
ocr_engine = aocr.OcrEngine()
ocr_engine.pdf_mode = aocr.PdfMode.DIRECT
# Optional: set language for better accuracy
ocr_engine.language = aocr.Language.English

# -------------------------------------------------
# 2️⃣  Path to the scanned PDF you want to process
# -------------------------------------------------
input_pdf_path = "YOUR_DIRECTORY/input.pdf"

# -------------------------------------------------
# 3️⃣  Run OCR – this is where we actually recognize text from PDF
# -------------------------------------------------
ocr_result = ocr_engine.recognize_from_pdf(input_pdf_path)

# -------------------------------------------------
# 4️⃣  Print the extracted text (shows how to extract text from PDF)
# -------------------------------------------------
print("PDF OCR complete. Text per page:")
for page_index, page in enumerate(ocr_result.pages):
    print(f"--- Page {page_index + 1} ---")
    print(page.text)

# -------------------------------------------------
# 5️⃣  Save each page as a .txt file (convert scanned PDF to text)
# -------------------------------------------------
output_dir = "output_text"
os.makedirs(output_dir, exist_ok=True)

for i, page in enumerate(ocr_result.pages, start=1):
    txt_path = os.path.join(output_dir, f"page_{i}.txt")
    with open(txt_path, "w", encoding="utf-8") as f:
        f.write(page.text)
    print(f"Saved page {i} text to {txt_path}")
```

Execute-o com:

```bash
python ocr_pdf.py
```

Você deverá ver a saída no console confirmando o texto de cada página e a localização dos arquivos `.txt` salvos.

## Conclusão

Cobremos **como fazer OCR em PDF** usando Python, demonstramos uma forma limpa de **ocr pdf with python**, mostramos como **extract text from PDF**, explicamos a mecânica por trás de **recognize text from PDF** e, por fim, fornecemos um snippet pronto para uso que **convert scanned PDF to text**. Todo o processo está encapsulado

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}