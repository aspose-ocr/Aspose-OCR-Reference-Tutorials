---
category: general
date: 2026-03-26
description: Extrair tabelas de imagem e converter a imagem em planilha usando OCR
  em Python. Aprenda como carregar a imagem para OCR, ler tabelas e extrair os dados
  da tabela.
draft: false
keywords:
- extract tables from image
- convert image to spreadsheet
- load image for ocr
- ocr read tables
- ocr extract table data
language: pt
og_description: Extraia tabelas de imagem com OCR em Python. Este guia mostra como
  carregar a imagem para OCR, ler tabelas e convertê‑las em uma planilha.
og_title: Extrair tabelas de imagem – Tutorial completo de OCR
tags:
- OCR
- Python
- Data Extraction
title: Extrair Tabelas de Imagem – Guia OCR Passo a Passo
url: /pt/python-java/general/extract-tables-from-image-step-by-step-ocr-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Tabelas de Imagem – Tutorial Completo de OCR

Já precisou **extrair tabelas de imagem** mas não sabia por onde começar? Você não está sozinho. Muitos desenvolvedores se deparam com um obstáculo quando um PDF ou captura de tela contém dados tabulares que precisam se tornar linhas e colunas editáveis. A boa notícia? Algumas linhas de código Python, combinadas com um motor OCR robusto, podem transformar essa imagem em uma planilha utilizável em segundos.

Neste tutorial vamos percorrer o carregamento de uma imagem para OCR, a execução do motor de reconhecimento e a extração de cada linha da tabela. Ao final, você será capaz de **converter imagem em planilha**, e também verá como **ocr read tables** e **ocr extract table data** para processamento posterior. Sem mágica oculta, apenas código claro e executável que você pode inserir no seu projeto hoje.

---

## O que você vai precisar

Antes de mergulharmos, certifique‑se de que tem o seguinte à mão:

- **Python 3.9+** – a versão estável mais recente funciona melhor.  
- A biblioteca **`ocr`** (ou qualquer SDK OCR compatível que exponha `OcrEngine`, `Image` e métodos relacionados a tabelas). Instale com `pip install ocr‑sdk` (substitua pelo nome real do pacote).  
- Um arquivo de imagem (`.png`, `.jpg`, etc.) que contenha uma tabela impressa de forma clara.  
- Opcional: **pandas** se quiser gravar os dados extraídos diretamente em um CSV ou arquivo Excel (`pip install pandas`).

Tudo pronto? Ótimo — vamos começar.

---

## Etapa 1: Importar o SDK OCR e preparar seu ambiente

Primeiro de tudo: precisamos trazer as classes do OCR para o nosso script e configurar um pequeno helper que mais tarde transformará os dados brutos da tabela em um DataFrame.

```python
# Step 1 – Imports and basic setup
import ocr                     # The OCR SDK
from pathlib import Path      # Handy for file paths
import pandas as pd           # For converting tables to spreadsheets

# Optional: configure logging to see what the engine is doing
import logging
logging.basicConfig(level=logging.INFO)
```

**Por que isso importa:** Importar `ocr` nos dá acesso a `OcrEngine`, `Imaging.Image` e aos objetos de tabela que percorreremos. `pandas` não é obrigatório para a extração, mas facilita muito a parte de **converter imagem em planilha**.

---

## Etapa 2: Carregar a imagem que você deseja processar

Agora vamos realmente **carregar a imagem para OCR**. O SDK espera um objeto `Image`, então vamos envolver o caminho do arquivo com o método auxiliar `Image.load()`.

```python
# Step 2 – Load the image that contains a table
image_path = Path("YOUR_DIRECTORY/table_image.png")

# Verify the file exists early to avoid cryptic SDK errors
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Create an OCR engine instance
ocr_engine = ocr.OcrEngine()

# Attach the image to the engine
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))
```

**Dica profissional:** Mantenha seus arquivos de imagem em uma pasta dedicada (`assets/` ou `data/`) e use caminhos relativos. Assim o script permanece portátil entre diferentes máquinas.

---

## Etapa 3: Executar o processo de reconhecimento

Com a imagem anexada, podemos finalmente instruir o motor a **ocr read tables**. A chamada `recognize()` devolve um objeto de resultado que contém tudo que o motor descobriu — blocos de texto, linhas e, mais importante para nós, tabelas.

```python
# Step 3 – Perform OCR and obtain results
ocr_result = ocr_engine.recognize()

# Quick sanity check: did the engine find any tables?
if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
else:
    logging.info(f"Found {len(ocr_result.get_tables())} table(s).")
```

**Por que verificamos:** Algumas imagens podem estar ruidosas ou as bordas da tabela fracas, fazendo com que o motor as ignore. Registrar um aviso fornece feedback precoce sem interromper o script.

---

## Etapa 4: Extrair as linhas e células de cada tabela

É aqui que a verdadeira magia acontece. Vamos iterar sobre cada tabela detectada, extrair cada linha e, em seguida, o texto de cada célula. A compreensão de lista interna deixa o código conciso, mas ainda explicaremos o fluxo.

```python
# Step 4 – Iterate over detected tables and collect data
all_tables = []   # Will hold a list of pandas DataFrames

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")

    rows_data = []   # Temporary storage for this table's rows

    for row_obj in table_obj.get_rows():
        # Extract text from each cell in the current row
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    # Convert the raw list of rows into a DataFrame
    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    # Print a human‑readable version to the console
    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))
```

**O que está acontecendo?**  

- `enumerate(..., start=1)` fornece um número de tabela amigável para o log.  
- `row_obj.get_cells()` devolve cada objeto de célula; `cell.get_text()` obtém a string decodificada pelo OCR.  
- Armazenamos as linhas em `rows_data` e as passamos para `pandas.DataFrame`, que alinha as colunas automaticamente.  
- O bloco `print` reproduz a **saída essencial** mostrada no trecho original, permitindo que você verifique os resultados imediatamente.

**Tratamento de casos extremos:** Se uma linha possuir um número diferente de células das demais, o `pandas` preencherá os espaços ausentes com `NaN`. Você pode limpar o DataFrame depois com `df.fillna('')` caso prefira strings vazias.

---

## Etapa 5: Salvar as tabelas extraídas em uma planilha

Agora que temos uma lista de DataFrames, transformá‑los em um workbook Excel (ou arquivos CSV) é muito fácil. Isso cumpre o objetivo de **converter imagem em planilha**.

```python
# Step 5 – Export tables to Excel (one sheet per table)
output_path = Path("extracted_tables.xlsx")
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        sheet_name = f"Table_{idx}"
        df.to_excel(writer, sheet_name=sheet_name, index=False)

logging.info(f"All tables saved to {output_path}")
```

**Por que Excel?** A maioria dos usuários de negócios prefere `.xlsx`. Se você preferir CSV, substitua o loop por `df.to_csv(f"table_{idx}.csv", index=False)`.

---

## Script completo, pronto para executar

Juntando tudo, aqui está o programa completo que você pode copiar‑colar e executar.

```python
import ocr
from pathlib import Path
import pandas as pd
import logging

logging.basicConfig(level=logging.INFO)

# ---------- Configuration ----------
image_path = Path("YOUR_DIRECTORY/table_image.png")
output_path = Path("extracted_tables.xlsx")
# ----------------------------------

# Verify image exists
if not image_path.is_file():
    raise FileNotFoundError(f"Image not found: {image_path}")

# Initialize OCR engine
ocr_engine = ocr.OcrEngine()
ocr_engine.set_image(ocr.Imaging.Image.load(str(image_path)))

# Run recognition
ocr_result = ocr_engine.recognize()

if not ocr_result.get_tables():
    logging.warning("No tables detected in the image.")
    exit(0)

all_tables = []

for table_idx, table_obj in enumerate(ocr_result.get_tables(), start=1):
    logging.info(f"Processing Table #{table_idx}")
    rows_data = []

    for row_obj in table_obj.get_rows():
        cell_texts = [cell.get_text() for cell in row_obj.get_cells()]
        rows_data.append(cell_texts)

    df = pd.DataFrame(rows_data)
    all_tables.append(df)

    print("\n=== New Table ===")
    for row in rows_data:
        print("\t".join(row))

# Save to Excel
with pd.ExcelWriter(output_path, engine="openpyxl") as writer:
    for idx, df in enumerate(all_tables, start=1):
        df.to_excel(writer, sheet_name=f"Table_{idx}", index=False)

logging.info(f"All tables saved to {output_path}")
```

**Saída esperada no console** (supondo uma tabela simples 2×3):

```
=== New Table ===
Header1    Header2    Header3
Row1Col1   Row1Col2   Row1Col3
Row2Col1   Row2Col2   Row2Col3
```

E você encontrará `extracted_tables.xlsx` na pasta do script, cada tabela em sua própria aba.

---

## Perguntas Frequentes & Dicas

| Pergunta | Resposta |
|----------|----------|
| **Posso usar uma biblioteca OCR diferente?** | Absolutamente. O padrão permanece o mesmo: carregar imagem → reconhecer → iterar sobre `get_tables()`. Basta substituir a importação e os nomes dos objetos. |
| **E se minha imagem estiver ruidosa?** | Pré‑procese com OpenCV (limiarização, correção de inclinação) antes de enviá‑la ao motor OCR. A redução de ruído costuma melhorar a precisão de **ocr extract table data**. |
| **Preciso instalar `openpyxl`?** | Sim, o `pandas` o utiliza nos bastidores para gerar arquivos Excel. Instale com `pip install openpyxl`. |
| **Como lidar com células mescladas?** | Alguns SDKs expõem `cell.is_merged()`; você pode detectar e propagar o valor ao longo do intervalo mesclado manualmente. |
| **Existe uma forma de extrair apenas tabelas específicas?** | Filtre por `table_obj.get_confidence()` ou verifique palavras‑chave no cabeçalho antes de processar. |

---

## Conclusão

Agora você tem uma solução completa, de ponta a ponta, para **extrair tabelas de imagem**, converter o resultado em uma planilha organizada e até lidar com múltiplas tabelas em uma única foto. O script demonstra como **carregar imagem para OCR**, **ocr read tables** e **ocr extract table data**, mantendo a flexibilidade necessária para variações do mundo real.

Qual o próximo passo? Experimente alimentar o motor OCR com uma página PDF renderizada como imagem, ou teste diferentes idiomas e fontes. Você também pode encaminhar os DataFrames diretamente para um banco de dados ou ferramenta de relatórios — sua imaginação é o limite.

Se este guia foi útil, sinta‑se à vontade para compartilhá‑lo, dar uma estrela ao repositório que hospeda o SDK ou deixar um comentário com suas próprias dicas. Boa codificação, e que suas tabelas estejam sempre perfeitamente analisadas!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}