---
category: general
date: 2026-04-29
description: Extraia texto de PDF usando Aspose OCR em Python. Aprenda o processamento
  em lote de OCR de PDF, converta texto de PDF escaneado e trate páginas de baixa
  confiança.
draft: false
keywords:
- extract text from pdf
- ocr pdf with python
- convert scanned pdf text
- batch ocr pdf processing
language: pt
og_description: Extraia texto de PDF com Aspose OCR em Python. Este guia mostra o
  processamento em lote de OCR de PDF, a conversão de texto de PDFs escaneados e o
  tratamento de resultados de baixa confiança.
og_title: Extrair Texto de PDF – OCR PDF com Python
tags:
- OCR
- Python
- PDF processing
title: Extrair Texto de PDF – OCR de PDF com Python
url: /pt/python/general/extract-text-from-pdf-ocr-pdf-with-python/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de PDF – OCR PDF com Python

Já precisou **extrair texto de PDF** mas o arquivo é apenas uma imagem escaneada? Você não está sozinho—muitos desenvolvedores encontram essa barreira ao tentar transformar PDFs em dados pesquisáveis. A boa notícia? Com Aspose OCR for Python você pode converter texto de PDF escaneado em poucas linhas, e até executar **processamento em lote de OCR PDF** quando tem dezenas de arquivos para tratar.

Neste tutorial vamos percorrer todo o fluxo de trabalho: configurar a biblioteca, executar OCR em um PDF único, escalar para um lote e lidar com páginas de baixa confiança para que você saiba quando uma revisão manual é necessária. Ao final você terá um script pronto‑para‑executar que extrai texto de qualquer PDF escaneado, e entenderá o porquê de cada passo.

## O que você precisará

- Python 3.8 ou mais recente (o código usa f‑strings, então 3.6+ funciona, mas 3.8+ é recomendado)
- Uma licença Aspose OCR for Python ou uma chave de avaliação gratuita (você pode obter uma no site da Aspose)
- Uma pasta com um ou mais PDFs escaneados que você deseja processar
- Uma quantidade moderada de espaço em disco para os relatórios *.txt* gerados

É isso—sem dependências externas pesadas, sem acrobacias com OpenCV. O motor Aspose OCR faz o trabalho pesado para você.

## Configurando o Ambiente

Primeiro, instale o pacote Aspose OCR a partir do PyPI:

```bash
pip install aspose-ocr
```

Se você tem um arquivo de licença (`Aspose.OCR.lic`), coloque‑o na raiz do seu projeto e ative‑o assim:

```python
# Activate Aspose OCR license (optional but removes trial watermark)
from aspose.ocr import License

license = License()
license.set_license("Aspose.OCR.lic")
```

> **Dica profissional:** Mantenha o arquivo de licença fora do controle de versão; adicione‑o ao `.gitignore` para evitar exposição acidental.

## Executando OCR em um PDF Único

Agora vamos extrair texto de um PDF escaneado único. Os passos principais são:

1. Crie uma instância de `OcrEngine`.
2. Aponte‑a para o arquivo PDF.
3. Recupere um `OcrResult` para cada página.
4. Grave a saída de texto simples no disco.
5. Descarte o engine para liberar recursos nativos.

Aqui está o script completo e executável:

```python
# Step 1: Import the OCR engine and create an instance
from aspose.ocr import OcrEngine

# Optional: activate license (see previous section)
# from aspose.ocr import License
# License().set_license("Aspose.OCR.lic")

ocr_engine = OcrEngine()

# Step 2: Specify the PDF file to be processed
pdf_file_path = r"YOUR_DIRECTORY/input.pdf"

# Step 3: Extract OCR results – one OcrResult object per page
ocr_pages = ocr_engine.extract_from_pdf(pdf_file_path)

# Step 4: Iterate through the results, show confidence, flag low‑confidence pages, and save the plain text
for ocr_page in ocr_pages:
    print(f"Page {ocr_page.page_number}: confidence {ocr_page.confidence:.2%}")

    # If confidence is below 80 %, flag it for manual review
    if ocr_page.confidence < 0.80:
        print("  Low confidence – consider manual review")

    # Build the output filename
    output_txt = f"YOUR_DIRECTORY/Report_page{ocr_page.page_number}.txt"
    with open(output_txt, "w", encoding="utf-8") as f:
        f.write(ocr_page.text)

# Step 5: Release resources used by the engine
ocr_engine.dispose()
```

**O que você verá:** Para cada página o script imprime algo como `Page 1: confidence 97.45%`. Se uma página ficar abaixo do limite de 80 %, um aviso aparece, informando que o OCR pode ter perdido caracteres.

### Por que isso funciona

- **`OcrEngine`** é o gateway para a biblioteca nativa Aspose OCR; ele lida com tudo, desde o pré‑processamento de imagens até o reconhecimento de caracteres.
- **`extract_from_pdf`** rasteriza automaticamente cada página do PDF, então você não precisa converter o PDF em imagens manualmente.
- **Pontuações de confiança** permitem automatizar verificações de qualidade—crítico quando você está processando documentos legais ou médicos onde a precisão importa.

## Processamento em Lote de OCR PDF com Python

A maioria dos projetos do mundo real envolve mais de um arquivo. Vamos estender o script de arquivo único para um **processamento em lote de OCR PDF** que percorre um diretório, processa cada PDF e armazena os resultados em uma sub‑pasta correspondente.

```python
import os
from pathlib import Path
from aspose.ocr import OcrEngine

def ocr_pdf_file(pdf_path: Path, output_dir: Path, engine: OcrEngine, confidence_threshold: float = 0.80):
    """Extract text from a single PDF and write per‑page .txt files."""
    ocr_pages = engine.extract_from_pdf(str(pdf_path))
    for page in ocr_pages:
        print(f"{pdf_path.name} – Page {page.page_number}: {page.confidence:.2%}")
        if page.confidence < confidence_threshold:
            print("  ⚠️ Low confidence – manual review may be needed")

        out_file = output_dir / f"{pdf_path.stem}_page{page.page_number}.txt"
        out_file.write_text(page.text, encoding="utf-8")

def batch_ocr_pdf(input_folder: str, output_folder: str):
    """Iterate over all PDFs in input_folder and run OCR."""
    engine = OcrEngine()
    input_path = Path(input_folder)
    output_path = Path(output_folder)
    output_path.mkdir(parents=True, exist_ok=True)

    pdf_files = list(input_path.glob("*.pdf"))
    if not pdf_files:
        print("🚫 No PDF files found in the specified folder.")
        return

    for pdf_file in pdf_files:
        # Create a sub‑folder for each PDF to keep pages organized
        pdf_out_dir = output_path / pdf_file.stem
        pdf_out_dir.mkdir(exist_ok=True)
        ocr_pdf_file(pdf_file, pdf_out_dir, engine)

    # Clean up native resources
    engine.dispose()
    print("✅ Batch OCR completed.")

# Example usage:
if __name__ == "__main__":
    batch_ocr_pdf("YOUR_DIRECTORY/input_pdfs", "YOUR_DIRECTORY/ocr_output")
```

#### Como isso ajuda

- **Escalabilidade:** A função percorre a pasta uma vez, criando uma sub‑pasta de saída dedicada para cada PDF. Isso mantém tudo organizado quando você tem dezenas de documentos.
- **Reutilização:** `ocr_pdf_file` pode ser chamada a partir de outros scripts (por exemplo, um serviço web) porque é uma função pura.
- **Tratamento de erros:** O script imprime uma mensagem amigável se a pasta de entrada estiver vazia, evitando falhas silenciosas.

## Convertendo Texto de PDF Escaneado – Lidando com Casos Limite

Embora o código acima funcione para a maioria dos PDFs, você pode encontrar algumas particularidades:

| Situação | Por que acontece | Como mitigar |
|-----------|------------------|--------------|
| **PDFs criptografados** | O PDF está protegido por senha. | Passe a senha para `extract_from_pdf(pdf_path, password="yourPwd")`. |
| **Documentos multilíngues** | Aspose OCR tem como padrão o inglês. | Defina `ocr_engine.language = "spa"` para espanhol, ou forneça uma lista para idiomas mistos. |
| **PDFs muito grandes (>500 páginas)** | O uso de memória aumenta porque cada página é carregada na RAM. | Processe o PDF em blocos usando `engine.extract_from_pdf(pdf_path, start_page=1, end_page=100)` e faça loop. |
| **Qualidade de escaneamento ruim** | DPI baixo ou muito ruído reduz a confiança. | Pré‑procese o PDF com `engine.image_preprocessing = True` ou aumente o DPI via `engine.dpi = 300`. |

> **Cuidado:** Ativar o pré‑processamento de imagem pode aumentar o tempo de CPU de forma perceptível. Se você estiver executando um lote noturno, agende tempo suficiente ou inicie um worker separado.

## Verificando a Saída

Depois que o script terminar, você encontrará uma estrutura de pastas como:

```
ocr_output/
├─ invoice_2023/
│  ├─ invoice_2023_page1.txt
│  ├─ invoice_2023_page2.txt
│  └─ …
└─ contract_A/
   ├─ contract_A_page1.txt
   └─ …
```

Abra qualquer arquivo `.txt`; você deverá ver texto limpo, codificado em UTF‑8, que espelha o conteúdo escaneado original. Se notar caracteres estranhos, verifique as configurações de idioma do PDF e assegure‑se de que os pacotes de fontes corretos estejam instalados na máquina.

## Liberando Recursos

Aspose OCR depende de DLLs nativas, portanto é essencial chamar `engine.dispose()` assim que terminar. Esquecer esse passo pode causar vazamentos de memória, especialmente em jobs de lote de longa duração.

```python
# Always the last line of your script
engine.dispose()
```

## Exemplo Completo de ponta a ponta

Juntando tudo, aqui está um único

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}