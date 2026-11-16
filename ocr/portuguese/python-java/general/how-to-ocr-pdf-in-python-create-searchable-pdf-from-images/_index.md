---
category: general
date: 2026-06-06
description: Como fazer OCR de PDF e criar arquivos PDF pesquisáveis a partir de imagens
  usando Python. Aprenda a adicionar texto pesquisável e converter imagem para PDF/A
  em minutos.
draft: false
keywords:
- how to ocr pdf
- create searchable pdf
- add searchable text
- ocr image to pdf
- convert image to pdf/a
language: pt
og_description: Como fazer OCR em PDF passo a passo. Aprenda a adicionar texto pesquisável
  e converter imagem para PDF/A usando um script Python simples.
og_title: Como fazer OCR em PDF – Guia rápido para criar PDFs pesquisáveis
schemas:
- author: Aspose
  dateModified: '2026-06-06'
  description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  headline: How to OCR PDF in Python – Create Searchable PDF from Images
  type: TechArticle
- description: How to OCR PDF and create searchable PDF files from images using Python.
    Learn to add searchable text and convert image to PDF/A in minutes.
  name: How to OCR PDF in Python – Create Searchable PDF from Images
  steps:
  - name: Why this matters
    text: '- **Preserving graphics** means the visual layout (tables, logos, stamps)
      stays exactly as the scanner captured it. - The `result` object typically contains
      a hidden text layer that we’ll later embed into the PDF. - Using `recognize_image`
      instead of `recognize_pdf` avoids an extra conversion step, '
  - name: Why this matters
    text: '- **Searchable PDF**: The output file contains a hidden, selectable text
      layer. You can now Ctrl + F through the document. - **PDF/A compliance**: Some
      organizations (legal, finance) require PDF/A for audit trails; this step satisfies
      that rule automatically. - The method also **adds searchable text'
  - name: Expected output
    text: 'When you run the script, the console prints:'
  type: HowTo
tags:
- OCR
- PDF
- Python
- Automation
title: Como fazer OCR de PDF em Python – Criar PDF pesquisável a partir de imagens
url: /pt/python-java/general/how-to-ocr-pdf-in-python-create-searchable-pdf-from-images/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em PDF – Transforme Imagens Escaneadas em PDFs Pesquisáveis

Já se perguntou **como fazer OCR em PDF** quando tudo o que você tem é uma imagem escaneada de uma nota fiscal ou recibo? Você não está sozinho. Em muitos escritórios a documentação recebida chega como PNGs ou JPEGs simples, e o próximo passo — tornar esse conteúdo pesquisável — parece uma caixa‑preta.  

A boa notícia? Com apenas algumas linhas de Python você pode **criar PDFs pesquisáveis**, **adicionar texto pesquisável**, e até **converter imagem para PDF/A** para arquivamento de longo prazo. Neste tutorial vamos percorrer cada etapa, explicar por que elas são importantes e fornecer um script pronto‑para‑executar que você pode inserir em qualquer projeto.

> **Dica profissional:** A mesma abordagem funciona para digitalizações de várias páginas; basta percorrer os arquivos em um loop e o motor faz o trabalho pesado.

---

## O que você precisará

Antes de mergulharmos, certifique‑se de que você tem o seguinte em sua máquina:

| Requisito | Por que é importante |
|-------------|-----------------|
| Python 3.9 ou mais recente | Sintaxe moderna e melhor suporte a bibliotecas |
| `pdfium`‑based OCR engine (e.g., `pdfocr` or a commercial SDK) | Lida tanto com reconhecimento de imagem quanto com geração de PDF/A |
| Um arquivo de imagem (PNG, JPEG, TIFF) que você deseja transformar em um PDF pesquisável | A fonte do texto |
| Permissão de escrita na pasta de saída | Para que o script possa salvar o novo PDF |

Se você ainda não instalou o SDK de OCR, execute:

```bash
pip install pdfocr   # replace with your vendor's package name
```

É isso — sem dependências de sistema complexas, apenas um pip install.

---

## Visão geral de como fazer OCR em PDF

Em alto nível, o processo consiste em três ações simples:

1. **Reconhecer** o texto dentro da imagem enquanto preserva os gráficos originais.  
2. **Exportar** o resultado do OCR junto com a imagem original como um **PDF/A pesquisável** (o formato de PDF amigável para arquivamento).  
3. **Validar** que o arquivo resultante contém texto selecionável e pesquisável sobreposto à imagem original.

A seguir, você verá cada etapa em código, com explicações do *porquê* por trás dos comandos.

---

## Etapa 1: Reconhecer Texto da Imagem

Primeiro, pedimos ao motor de OCR que leia os pixels e retorne um objeto de resultado que contém tanto a imagem bruta quanto o texto extraído. Pense nele como o motor “lendo” a nota fiscal para você.

```python
# Step 1: Recognize text from the image and keep the original graphics
result = engine.recognize_image("YOUR_DIRECTORY/invoice.png")
```

### Por que isso importa

- **Preservar gráficos** significa que o layout visual (tabelas, logotipos, carimbos) permanece exatamente como o scanner capturou.  
- O objeto `result` normalmente contém uma camada de texto oculto que inseriremos no PDF mais tarde.  
- Usar `recognize_image` em vez de `recognize_pdf` evita uma etapa extra de conversão, o que acelera o processamento para imagens de página única.

#### Variações comuns

- Se você tem um **TIFF de várias páginas**, passe o caminho do arquivo diretamente; a maioria dos motores tratará cada página como uma imagem separada.  
- Para PDFs que já contêm imagens, você pode chamar `engine.recognize_pdf("file.pdf")` e pular esta etapa completamente.

---

## Etapa 2: Exportar Resultado do OCR como PDF/A pesquisável

Agora pegamos o `result` da etapa 1 e instruímos o motor a gravar um novo arquivo. A bandeira chave aqui é *PDF/A* — a versão padrão ISO do PDF projetada para preservação de longo prazo.

```python
# Step 2: Export the OCR result together with the original image as a searchable PDF/A
result.save_as_pdfa("YOUR_DIRECTORY/invoice_searchable.pdf")
```

### Por que isso importa

- **PDF pesquisável**: O arquivo de saída contém uma camada de texto oculta e selecionável. Você pode agora usar Ctrl + F no documento.  
- **Conformidade PDF/A**: Algumas organizações (jurídicas, financeiras) exigem PDF/A para trilhas de auditoria; esta etapa satisfaz essa regra automaticamente.  
- O método também **adiciona texto pesquisável** sem achatar a imagem, mantendo a fidelidade visual perfeita.

#### Caso especial: Precisa de um PDF comum em vez disso?

Se você não se importa com PDF/A, substitua `save_as_pdfa` por `save_as_pdf`. O restante do fluxo de trabalho permanece o mesmo.

---

## Etapa 3: Verificar o PDF pesquisável

Uma verificação rápida de sanidade salva você de bugs misteriosos mais tarde. Abra o arquivo gerado em qualquer visualizador de PDF, tente selecionar uma palavra e use a função de busca.

```python
# Step 3: The file "invoice_searchable.pdf" now contains selectable text layered over the original invoice image
import subprocess, os

pdf_path = "YOUR_DIRECTORY/invoice_searchable.pdf"
if os.path.exists(pdf_path):
    print(f"✅ PDF created successfully: {pdf_path}")
    # Optionally open the file (works on macOS, Windows, Linux with appropriate commands)
    subprocess.run(["open", pdf_path] if os.name == "posix" else ["start", pdf_path], shell=True)
else:
    print("❌ Something went wrong – PDF not found.")
```

### Saída esperada

Ao executar o script, o console imprime:

```
✅ PDF created successfully: YOUR_DIRECTORY/invoice_searchable.pdf
```

Ao abrir o arquivo, você deverá ver a imagem original da nota fiscal com uma camada de texto tênue e invisível. Selecione qualquer palavra e perceberá que ela é selecionável — **esse é o texto pesquisável** que você acabou de adicionar.

---

## Adicionando Texto pesquisável a PDFs Existentes (Bônus)

Às vezes você já tem um PDF, mas precisa **adicionar texto pesquisável** a ele. O mesmo motor pode sobrepor resultados de OCR a um PDF existente:

```python
# Bonus: Add searchable text to an existing PDF file
existing_pdf = engine.load_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result = engine.recognize_pdf("YOUR_DIRECTORY/old_scanned.pdf")
ocr_result.apply_to(existing_pdf).save_as_pdfa("YOUR_DIRECTORY/old_scanned_searchable.pdf")
```

Aqui `apply_to` mescla a camada oculta com as páginas originais, permitindo que você **crie PDFs pesquisáveis** sem re‑digitalizar.

---

## Armadilhas Comuns e Dicas

| Armadilha | Como evitar |
|---------|-----------------|
| **Imagens de origem de baixa resolução** (< 150 dpi) | Amplie ou solicite uma digitalização de resolução maior; a precisão do OCR cai drasticamente abaixo de 150 dpi. |
| **Dados de idioma ausentes** | Instale os pacotes de idioma apropriados para seu motor de OCR (`pip install pdfocr[eng,spa]`). |
| **Pasta de saída não gravável** | Execute o script com permissões suficientes ou escolha outro diretório. |
| **Falha na validação PDF/A** | Certifique‑se de que não está incorporando fontes não suportadas ou JavaScript; a maioria dos SDKs lida com isso automaticamente ao usar `save_as_pdfa`. |

---

## Script Completo – Solução de Um Arquivo

Abaixo está um script autônomo que une tudo. Copie‑e‑cole, substitua os caminhos de placeholder e você estará pronto para **converter imagem para PDF/A** em segundos.

```python
#!/usr/bin/env python3
"""
How to OCR PDF – Complete script to create a searchable PDF/A from an image.
Works with any OCR engine exposing `recognize_image` and `save_as_pdfa`.
"""

import os
import subprocess

# ----------------------------------------------------------------------
# CONFIGURATION – change these paths to match your environment
# ----------------------------------------------------------------------
INPUT_IMAGE = "YOUR_DIRECTORY/invoice.png"
OUTPUT_PDF  = "YOUR_DIRECTORY/invoice_searchable.pdf"

# ----------------------------------------------------------------------
# INITIALIZE THE OCR ENGINE (replace with your SDK's init call)
# ----------------------------------------------------------------------
# Example for a fictional `pdfocr` package:
# from pdfocr import Engine
# engine = Engine(api_key="YOUR_API_KEY")
# If you use a different library, adjust the import and init accordingly.
engine = Engine()  # placeholder – insert real initialization here

def main():
    # Step 1 – Recognize the image
    print(f"🔎 Recognizing text from {INPUT_IMAGE} …")
    result = engine.recognize_image(INPUT_IMAGE)

    # Step 2 – Save as searchable PDF/A
    print(f"💾 Saving searchable PDF/A to {OUTPUT_PDF} …")
    result.save_as_pdfa(OUTPUT_PDF)

    # Step 3 – Verify the file exists
    if os.path.isfile(OUTPUT_PDF):
        print("✅ Success! Searchable PDF/A created.")
        # Open the file for a quick visual check (optional)
        try:
            if os.name == "posix":
                subprocess.run(["open", OUTPUT_PDF])
            else:
                subprocess.run(["start", OUTPUT_PDF], shell=True)
        except Exception:
            pass
    else:
        print("❌ Error: PDF not created.")

if __name__ == "__main__":
    main()
```

**O que este script faz:**  
1. Carrega o motor de OCR.  
2. Lê a imagem escolhida e extrai o texto.  
3. Grava um **PDF/A pesquisável** que você pode distribuir ou arquivar imediatamente.  

Sinta‑se à vontade para envolver a lógica `main` em uma função que processe uma pasta inteira — basta iterar sobre `os.listdir()` e repetir as três etapas para cada arquivo.

---

## Próximos Passos e Tópicos Relacionados

Agora que você dominou **como fazer OCR em PDF**, considere explorar estas ideias de continuação:

- **Processamento em lote:** Use `concurrent.futures` para fazer OCR em dezenas de notas fiscais em paralelo.  
- **Injeção de metadata:** Adicione datas de criação ou números de nota fiscal aos metadados do PDF para indexação mais fácil.  
- **PDFs híbridos:** Combine texto pesquisável com imagens originais incorporadas para um “gêmeo digital” do documento em papel.  
- **Saídas alternativas:** Exporte para **DOCX** ou **HTML** se sistemas posteriores precisarem de formatos editáveis.  

Cada um desses se baseia nos conceitos centrais que você acabou de aprender — reconhecer, exportar, validar.

---

## Conclusão

Em resumo, agora você sabe **como fazer OCR em PDF** ao transformar uma imagem simples em um **PDF/A pesquisável** com apenas três linhas de Python. O script cuida do trabalho pesado, preserva os gráficos originais e fornece um documento em conformidade com padrões que você pode pesquisar, arquivar ou compartilhar.  

Experimente com suas próprias notas fiscais, recibos ou contratos escaneados. Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação oficial do SDK — geralmente repleta de exemplos adicionais. Boa codificação e aproveite a nova capacidade de tornar qualquer imagem instantaneamente pesquisável! 

![Exemplo de como fazer OCR em PDF mostrando a imagem original e a sobreposição do PDF pesquisável](placeholder.png "Exemplo de como fazer OCR em PDF")

## O que você deve aprender a seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Como fazer OCR em PDF em .NET com Aspose.OCR](/ocr/english/net/text-recognition/recognize-pdf/)
- [Reconhecer Texto em PDF – Operações de OCR com Aspose.OCR para Java](/ocr/english/java/ocr-operations/)
- [Converter Imagens para PDF C# – Salvar Resultado OCR de Múltiplas Páginas](/ocr/english/net/ocr-optimization/save-multipage-result-as-document/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}