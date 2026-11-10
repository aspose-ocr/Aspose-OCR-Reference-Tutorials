---
category: general
date: 2026-01-12
description: Aprenda como fazer OCR de PDF em Python e tornar PDFs pesquisáveis rapidamente.
  Converta PDFs escaneados, extraia texto de PDFs e faça OCR de PDFs escaneados em
  Python usando Aspose OCR.
draft: false
keywords:
- how to ocr pdf
- make pdf searchable
- convert scanned pdf
- extract text pdf
- ocr scanned pdf python
language: pt
og_description: Como fazer OCR de PDF em Python? Este tutorial passo a passo mostra
  como converter arquivos PDF digitalizados em PDFs pesquisáveis e extrair texto com
  o Aspose OCR.
og_title: Como fazer OCR em PDF e torná-lo pesquisável – Guia Python
tags:
- OCR
- Python
- PDF processing
title: Como fazer OCR em PDF e torná‑lo pesquisável – Guia Python
url: /pt/python-java/general/how-to-ocr-pdf-and-make-it-searchable-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como fazer OCR em PDF e torná-lo pesquisável – Guia Python

Já se perguntou **como fazer OCR em PDF** sem gastar uma fortuna em software comercial? Você não está sozinho. Muitos desenvolvedores encontram um obstáculo quando precisam transformar um contrato escaneado, uma fatura ou qualquer PDF baseado em imagem em um documento pesquisável. A boa notícia? Com algumas linhas de Python e Aspose OCR você pode converter PDF escaneado, extrair texto de PDF e, finalmente, tornar o PDF pesquisável em minutos.

Neste tutorial vamos percorrer tudo o que você precisa: desde a instalação da biblioteca, configuração do idioma, processamento de um PDF escaneado, até a gravação do resultado como um PDF pesquisável que contém tanto a imagem original quanto uma camada de texto oculta. Ao final, você terá um script reutilizável que pode ser inserido em qualquer projeto—sem necessidade de copiar e colar manualmente.

---

## O que você precisará

- **Python 3.8+** (o código funciona em 3.9, 3.10 e versões mais recentes)
- Uma licença ativa do **Aspose OCR for Python** (uma avaliação gratuita serve para experimentação)
- Um arquivo PDF escaneado (por exemplo, `scanned_contract.pdf`) que você deseja tornar pesquisável
- Familiaridade básica com a linha de comando e ambientes virtuais (opcional, mas recomendado)

> **Dica profissional:** Se ainda não tem uma licença, inscreva‑se para um teste de 30 dias no site da Aspose; a versão de avaliação é totalmente funcional para fins de desenvolvimento.

## Como fazer OCR em PDF com Aspose OCR (Palavra‑chave principal em H2)

O primeiro passo é obter o pacote correto. Aspose OCR fornece uma API limpa e de alto nível que abstrai os detalhes de processamento de imagem de baixo nível.

```bash
# Create a virtual environment (optional but tidy)
python -m venv venv
source venv/bin/activate   # On Windows use `venv\Scripts\activate`

# Install the Aspose OCR package
pip install aspose-ocr
```

Depois que o pacote estiver instalado, você pode começar a escrever o script.

```python
# Step 1: Import the Aspose OCR module
import asposeocr as ocr

# Step 2: Create an OCR engine instance and set the recognition language
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.ENGLISH
```

> **Por que definir o idioma?**  
> A precisão do OCR depende fortemente do modelo de idioma. Ao informar explicitamente ao motor que ele deve esperar texto em inglês, você reduz falsos positivos e acelera o processamento.

## Etapa 2: Converter PDF escaneado em um PDF pesquisável

Agora que o motor está pronto, aponte‑o para o seu documento escaneado. O método `process_pdf` retorna um objeto `PdfResult` que contém tanto os dados da imagem original quanto o texto reconhecido.

```python
# Step 3: Process the scanned PDF to extract text
input_pdf_path = "YOUR_DIRECTORY/scanned_contract.pdf"
pdf_result = ocr_engine.process_pdf(input_pdf_path)
```

Se precisar **converter PDF escaneado** em lote, basta percorrer um diretório e chamar `process_pdf` para cada arquivo. O motor lida com PDFs de várias páginas pronto para uso.

## Etapa 3: Salvar o Resultado como um PDF pesquisável (Tornar PDF pesquisável)

A última peça do quebra‑cabeça é persistir a versão pesquisável. Aspose OCR faz isso em uma única linha:

```python
# Step 4: Define the output path for the searchable PDF
searchable_pdf_path = "YOUR_DIRECTORY/contract_searchable.pdf"

# Step 5: Save the result as a searchable PDF (image + hidden text layer)
pdf_result.save_as_searchable_pdf(searchable_pdf_path)
```

Ao abrir `contract_searchable.pdf` em qualquer visualizador de PDF, você verá a imagem escaneada original, mas agora pode **pesquisar por qualquer palavra** que o motor OCR reconheceu. A camada de texto oculta é invisível ao olho, mas totalmente indexável.

### Script completo – Pronto para executar

A seguir está o exemplo completo e executável. Copie‑e cole em um arquivo chamado `make_searchable.py` e ajuste os caminhos para corresponder ao seu ambiente.

```python
# make_searchable.py
# -------------------------------------------------
# Complete script to OCR a scanned PDF and make it searchable
# -------------------------------------------------

import os
import asposeocr as ocr

def ocr_to_searchable(input_path: str, output_path: str, language=ocr.Language.ENGLISH):
    """
    Convert a scanned PDF into a searchable PDF.
    
    Parameters
    ----------
    input_path : str
        Path to the scanned PDF file.
    output_path : str
        Destination path for the searchable PDF.
    language : ocr.Language, optional
        OCR language model (default is English).
    """
    if not os.path.isfile(input_path):
        raise FileNotFoundError(f"Input file not found: {input_path}")

    # Initialize OCR engine
    engine = ocr.OcrEngine()
    engine.language = language

    # Process the PDF (extracts images + hidden text)
    result = engine.process_pdf(input_path)

    # Save as searchable PDF
    result.save_as_searchable_pdf(output_path)
    print(f"✅ Searchable PDF saved to: {output_path}")

if __name__ == "__main__":
    # Example usage – replace with your actual file locations
    INPUT_PDF = "YOUR_DIRECTORY/scanned_contract.pdf"
    OUTPUT_PDF = "YOUR_DIRECTORY/contract_searchable.pdf"
    ocr_to_searchable(INPUT_PDF, OUTPUT_PDF)
```

**Saída esperada:**  
Ao executar o script, ele imprime uma linha de confirmação e cria `contract_searchable.pdf`. Abra o arquivo, pressione `Ctrl + F` e digite qualquer palavra que apareça na imagem escaneada original—você verá correspondências instantaneamente.

## Perguntas frequentes e casos de borda

### 1. E se o PDF contiver vários idiomas?

Você pode passar uma lista de idiomas para o motor:

```python
engine.language = [ocr.Language.ENGLISH, ocr.Language.SPANISH]
```

Aspose OCR tentará reconhecer texto em ambos os idiomas na mesma página.

### 2. Como lidar com digitalizações de baixa resolução?

Se as imagens de origem estiverem abaixo de 150 dpi, a precisão do OCR pode sofrer. Pré‑procese o PDF com uma ferramenta como `pdfimages` para extrair as páginas, aumente a resolução com Pillow e alimente as imagens de alta resolução de volta ao `process_pdf`.

### 3. Posso extrair o texto puro sem criar um PDF pesquisável?

Com certeza. O objeto `PdfResult` expõe uma propriedade `text`:

```python
plain_text = pdf_result.text
print(plain_text[:500])  # preview first 500 characters
```

Isso atende ao caso de uso **extract text pdf** quando você só precisa dos caracteres brutos.

### 4. Existe uma maneira de processar em lote uma pasta de PDFs?

Sim—envolva a função `ocr_to_searchable` em um loop simples:

```python
import glob

for src in glob.glob("scans/*.pdf"):
    dst = src.replace("scans/", "searchable/").replace(".pdf", "_searchable.pdf")
    ocr_to_searchable(src, dst)
```

Agora você pode **converter scanned pdf** em massa com um único comando.

## Dicas de desempenho

- **Reutilizar o motor**: Criar um novo `OcrEngine` para cada arquivo adiciona sobrecarga. Instancie‑o uma vez e reutilize em múltiplas chamadas.
- **Processamento paralelo**: Para lotes grandes, considere o `concurrent.futures.ThreadPoolExecutor` do Python—Aspose OCR é thread‑safe para operações somente de leitura.
- **Gerenciamento de memória**: Se você processar PDFs muito grandes (centenas de páginas), chame `gc.collect()` após cada arquivo para liberar memória.

## Conclusão

Cobremos **como fazer OCR em PDF** usando Python, transformamos essas digitalizações em **PDFs pesquisáveis** e ainda mostramos como **extrair texto PDF** diretamente. Com Aspose OCR você obtém um motor confiável que lida com documentos multipágina, múltiplos idiomas e reconhecimento de alta precisão—tudo com apenas algumas linhas de código.

Experimente em seus próprios contratos, faturas ou artigos de pesquisa arquivados. Depois de dominar o básico, experimente os recursos avançados—como dicionários personalizados, pré‑processamento de imagens ou integração da saída em um índice de busca full‑text como Elasticsearch.

Tem mais perguntas sobre **ocr scanned pdf python** ou precisa de ajuda para solucionar uma digitalização complicada? Deixe um comentário abaixo e feliz codificação! 

--- 

![how to ocr pdf example](image-placeholder.png){alt="exemplo de como fazer ocr pdf"}

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}