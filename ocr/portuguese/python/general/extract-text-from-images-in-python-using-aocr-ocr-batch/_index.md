---
category: general
date: 2026-06-25
description: Extrair texto de imagens com a biblioteca Python aocr – aprenda OCR em
  lote, configure o modo de reconhecimento como impresso e adicione um pós-processador
  de IA.
draft: false
keywords:
- extract text from images
- Python OCR batch
- aocr library
- recognition mode printed
- AI postprocessor
language: pt
og_description: Extraia texto de imagens usando a biblioteca Python aocr. Este tutorial
  apresenta OCR em lote, modo de reconhecimento de texto impresso e pós-processador
  de IA opcional.
og_title: Extrair texto de imagens em Python – Guia completo de lote aocr
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  headline: Extract Text from Images in Python Using aocr OCR Batch
  type: TechArticle
- description: Extract text from images with Python aocr library – learn batch OCR,
    set recognition mode printed, and add an AI postprocessor.
  name: Extract Text from Images in Python Using aocr OCR Batch
  steps:
  - name: Prerequisites
    text: '- Python 3.8 or newer installed on your machine. - Basic familiarity with
      Python scripting (loops, imports, etc.). - Access to a folder of scanned images
      (PNG, JPG, TIFF, etc.).'
  - name: 1. Unsupported File Types
    text: '`aocr` silently skips files it can’t decode. If you suspect you have PDFs
      or BMPs mixed in, filter them beforehand:'
  - name: 2. Large Batches and Memory Consumption
    text: 'Running thousands of high‑resolution scans can balloon memory usage. Mitigate
      this by processing in chunks:'
  - name: 3. Empty or Low‑Contrast Pages
    text: 'If a page yields fewer than 10 characters, you might want to flag it for
      manual review:'
  type: HowTo
- questions:
  - answer: Not out‑of‑the‑box. `aocr` only handles raster images. Convert PDFs to
      PNG/TIFF first (e.g., using `pdf2image`).
    question: Does this work on PDFs?
  - answer: Absolutely—just replace `aocr.RecognitionMode.PRINTED` with `aocr.RecognitionMode.HANDWRITTEN`.
      Expect a slower run time but better results on cursive notes.
    question: Can I change the recognition mode to handwritten?
  - answer: 'The library ships with language packs. Install the desired language module
      (`pip install aocr-lang-fr` for French, etc.) and set `ocr_batch.language =
      "fr"` before running. ## Next Steps and Related Topics - **Parallel processing:**
      Wrap the batch execution in a `concurrent.futures.ThreadPoolExecuto'
    question: What if I need multilingual support?
  type: FAQPage
tags:
- OCR
- Python
- image processing
title: Extrair texto de imagens em Python usando aocr OCR em lote
url: /pt/python/general/extract-text-from-images-in-python-using-aocr-ocr-batch/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Extrair Texto de Imagens em Python Usando um Lote OCR aocr

Já precisou **extrair texto de imagens** mas se sentiu sobrecarregado com dezenas de pequenos passos? Você não está sozinho. Seja digitalizando formulários escaneados, extraindo dados de recibos ou construindo um arquivo pesquisável, obter resultados de OCR confiáveis em escala pode parecer escalar uma colina íngreme.

A boa notícia? Com a **biblioteca aocr** você pode criar um **lote OCR Python** em apenas algumas linhas. Neste guia, vamos percorrer a criação de um lote OCR, carregar todas as imagens suportadas de uma pasta, escolher o **modo de reconhecimento printed**, e até anexar um **postprocessador de IA** para aquele impulso extra de precisão. Ao final, você terá um script pronto‑para‑executar que extrai texto de imagens e informa quanto foi capturado por arquivo.

## O que você aprenderá

- Como instalar e importar o pacote `aocr`.
- Configurar um `OcrBatch` para lidar automaticamente com milhares de arquivos.
- Escolher o modo de reconhecimento ideal para documentos impressos.
- (Opcional) Conectar um post‑processador de IA para limpar resultados ruidosos.
- Exibir o caminho de cada arquivo ao lado do comprimento do texto extraído.
- Dicas para lidar com casos extremos, como formatos não suportados ou páginas vazias.

### Pré‑requisitos

- Python 3.8 ou mais recente instalado na sua máquina.  
- Familiaridade básica com scripts Python (loops, imports, etc.).  
- Acesso a uma pasta de imagens escaneadas (PNG, JPG, TIFF, etc.).  

Se você tem isso, vamos mergulhar — sem serviços externos necessários.

## Etapa 1: Instalar a Biblioteca aocr

Primeiro de tudo. O pacote `aocr` não faz parte da biblioteca padrão, então você precisará obtê‑lo do PyPI.

```bash
pip install aocr
```

> **Dica profissional:** Use um ambiente virtual (`python -m venv .venv`) para manter as dependências isoladas.  

Depois de instalado, você pode importar as classes principais.

```python
# core imports
import aocr
```

## Etapa 2: Criar uma Instância de Lote OCR

Um `OcrBatch` é o motor que percorrerá seu diretório e manterá o controle de cada arquivo de imagem. Pense nele como uma esteira que alimenta as imagens para o motor OCR.

```python
# Step 2: Initialize the batch
ocr_batch = aocr.OcrBatch()
```

Neste ponto o lote está vazio, mas o preencheremos na próxima etapa.

## Etapa 3: Adicionar Todas as Imagens Suportadas de uma Pasta (Recursivamente)

Provavelmente você tem uma estrutura de pastas aninhada — talvez uma subpasta por cliente ou por mês. O método `add_folder` percorre a árvore para você, trazendo todas as imagens que ele sabe ler.

```python
# Step 3: Load images from a directory
ocr_batch.add_folder("YOUR_DIRECTORY/scanned_forms/", recursive=True)
```

Substitua `"YOUR_DIRECTORY/scanned_forms/"` pelo caminho real no seu sistema. Após esta chamada, `ocr_batch.file_paths` contém uma lista de nomes de arquivos absolutos, e o lote sabe exatamente quantos itens ele processará.

## Etapa 4: Escolher o Modo de Reconhecimento para Texto Impresso

O motor `aocr` suporta vários modos (handwritten, printed, mixed). Como estamos lidando com formulários limpos e impressos, defina o modo adequadamente. Essa pequena flag pode melhorar drasticamente a precisão porque o motor ignora as heurísticas pesadas necessárias para scripts cursivos.

```python
# Step 4: Tell the engine we have printed text
ocr_batch.recognition_mode = aocr.RecognitionMode.PRINTED
```

> **Por que isso importa:** Texto impresso tem linhas de base e formas de caracteres consistentes, permitindo que o modelo OCR aplique dicionários de caracteres mais restritos. Se você deixar o modo em “auto”, pode obter ruído extra em digitalizações de baixa resolução.

## Etapa 5: (Opcional) Anexar um Post‑Processador de IA

Se suas digitalizações sofrem de desfoque, baixo contraste ou fontes incomuns, um post‑processador de IA pode limpar a saída bruta do OCR antes de enviá‑la para sistemas subsequentes. O método `set_ai_postprocessor` espera um objeto que implemente a interface `process(text: str) -> str`.

Abaixo está um exemplo mínimo usando uma classe fictícia `SimpleCleaner`. Na prática, você poderia conectar um transformer HuggingFace, um modelo de linguagem customizado ou até mesmo um corretor ortográfico baseado em regras.

```python
# Optional Step 5: Define a tiny post‑processor
class SimpleCleaner:
    def process(self, text: str) -> str:
        # Strip extra whitespace and fix common OCR quirks
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")  # replace em‑dash with hyphen

# Instantiate and attach
ai = SimpleCleaner()
ocr_batch.set_ai_postprocessor(ai)
```

Se você pular esta etapa, o lote simplesmente retornará as strings OCR brutas.

## Etapa 6: Executar OCR em Todo o Lote e Coletar Resultados

Agora começa o trabalho pesado. O método `run` itera sobre cada arquivo, executa o motor OCR, encaminha a saída pelo post‑processador de IA opcional e retorna uma lista de strings — uma por imagem.

```python
# Step 6: Execute the batch
ocr_results = ocr_batch.run()   # list of extracted texts
```

Como o método retorna uma lista Python simples, você pode tratá‑la como qualquer outra coleção — armazená‑la, gravá‑la em um CSV ou inseri‑la em um banco de dados.

## Etapa 7: Exibir Cada Caminho de Arquivo com o Comprimento do Texto Extraído

Uma verificação rápida de sanidade é imprimir quantos caracteres foram extraídos de cada arquivo. Se uma página estiver em branco ou o OCR falhar, você verá um comprimento de `0`.

```python
# Step 7: Show results summary
for file_path, text in zip(ocr_batch.file_paths, ocr_results):
    print(f"{file_path} -> {len(text)} chars")
```

A saída típica se parece com:

```
/data/forms/invoice_001.png -> 1245 chars
/data/forms/invoice_002.jpg -> 0 chars
/data/forms/receipt_2023-04-15.tif -> 876 chars
```

Ver um `0` indica instantaneamente quais arquivos precisam de uma segunda olhada (talvez estejam corrompidos ou não sejam imagens).

## Lidando com Casos Extremos Comuns

### 1. Tipos de Arquivo Não Suportados

`aocr` ignora silenciosamente arquivos que não consegue decodificar. Se você suspeita que há PDFs ou BMPs misturados, filtre‑os antes:

```python
supported_ext = {".png", ".jpg", ".jpeg", ".tif", ".tiff"}
ocr_batch.file_paths = [
    p for p in ocr_batch.file_paths if p.lower().endswith(tuple(supported_ext))
]
```

### 2. Lotes Grandes e Consumo de Memória

Executar milhares de digitalizações em alta resolução pode inflar o uso de memória. Mitigue isso processando em blocos:

```python
batch_size = 200
for i in range(0, len(ocr_batch.file_paths), batch_size):
    sub_batch = aocr.OcrBatch()
    sub_batch.file_paths = ocr_batch.file_paths[i:i+batch_size]
    sub_batch.recognition_mode = aocr.RecognitionMode.PRINTED
    if 'ai' in locals():
        sub_batch.set_ai_postprocessor(ai)
    results = sub_batch.run()
    # handle results (e.g., write to file) before next chunk
```

### 3. Páginas Vazias ou de Baixo Contraste

Se uma página gerar menos de 10 caracteres, você pode querer marcá‑la para revisão manual:

```python
for fp, txt in zip(ocr_batch.file_paths, ocr_results):
    if len(txt.strip()) < 10:
        print(f"⚠️  Low‑confidence result for {fp}")
```

## Exemplo Completo em Funcionamento

Juntando tudo, aqui está um script que você pode copiar‑colar e executar imediatamente. Salve‑o como `batch_ocr.py`.

```python
#!/usr/bin/env python3
"""
Batch OCR script using aocr to extract text from images.
"""

import aocr

# ----------------------------------------------------------------------
# Optional: a tiny AI post‑processor to clean up OCR output
# ----------------------------------------------------------------------
class SimpleCleaner:
    def process(self, text: str) -> str:
        cleaned = " ".join(text.split())
        return cleaned.replace("—", "-")

# ----------------------------------------------------------------------
# Configuration
# ----------------------------------------------------------------------
IMAGE_ROOT = "YOUR_DIRECTORY/scanned_forms/"   # ← change this!
RECOGNITION_MODE = aocr.RecognitionMode.PRINTED

# ----------------------------------------------------------------------
# Build and run the OCR batch
# ----------------------------------------------------------------------
def main():
    # 1️⃣ Create batch
    batch = aocr.OcrBatch()

    # 2️⃣ Load images recursively
    batch.add_folder(IMAGE_ROOT, recursive=True)

    # 3️⃣ Set mode for printed text
    batch.recognition_mode = RECOGNITION_MODE

    # 4️⃣ Attach AI post‑processor (comment out if not needed)
    ai = SimpleCleaner()
    batch.set_ai_postprocessor(ai)

    # 5️⃣ Run OCR
    results = batch.run()

    # 6️⃣ Summarize
    for path, text in zip(batch.file_paths, results):
        print(f"{path} -> {len(text)} chars")

if __name__ == "__main__":
    main()
```

**Saída esperada** (truncada para brevidade):

```
/home/me/scanned_forms/formA.png -> 1342 chars
/home/me/scanned_forms/subfolder/formB.tif -> 0 chars
/home/me/scanned_forms/invoice_2024-01.jpg -> 987 chars
```

Execute‑o com:

```bash
python batch_ocr.py
```

Se tudo estiver configurado corretamente, você verá uma linha para cada imagem, cada uma relatando a contagem de caracteres do texto extraído.

## Perguntas Frequentes

**Q: Isso funciona com PDFs?**  
A: Não imediatamente. `aocr` só lida com imagens raster. Converta PDFs para PNG/TIFF primeiro (por exemplo, usando `pdf2image`).

**Q: Posso mudar o modo de reconhecimento para manuscrito?**  
A: Absolutamente — basta substituir `aocr.RecognitionMode.PRINTED` por `aocr.RecognitionMode.HANDWRITTEN`. Espere um tempo de execução mais lento, mas melhores resultados em notas cursivas.

**Q: E se eu precisar de suporte multilíngue?**  
A: A biblioteca vem com pacotes de idiomas. Instale o módulo de idioma desejado (`pip install aocr-lang-fr` para francês, etc.) e defina `ocr_batch.language = "fr"` antes de executar.

## Próximos Passos e Tópicos Relacionados

- **Processamento paralelo:** Envolva a execução do lote em um `concurrent.futures.ThreadPoolExecutor` para utilizar múltiplos núcleos de CPU.  
- **Armazenamento de resultados:** Grave `ocr_results` em um CSV ou banco de dados SQLite para análises subsequentes.  
- **Integração com IA na nuvem:** Troque o `SimpleCleaner` por um modelo transformer da HuggingFace para correção ortográfica de última geração.  
- **Ajuste fino do aocr:** Se você tem um conjunto de fontes customizado, explore `aocr.Trainer` para melhorar a precisão do modo impresso.

---

É isso — agora você tem uma base sólida


## O que Você Deve Aprender a Seguir?

Os tutoriais a seguir cobrem tópicos intimamente relacionados que se baseiam nas técnicas demonstradas neste guia. Cada recurso inclui exemplos de código completos e funcionais com explicações passo a passo para ajudá‑lo a dominar recursos adicionais da API e explorar abordagens de implementação alternativas em seus próprios projetos.

- [Extrair Texto de Imagem com Aspose OCR – Guia Passo a Passo](/ocr/english/python/general/extract-text-from-image-with-aspose-ocr-step-by-step-guide/)
- [Extrair Texto de Imagens Usando Operação OCR em Pastas](/ocr/english/net/ocr-configuration/ocr-operation-with-folder/)
- [Como Processar OCR em Lote de Imagens com Lista no Aspose.OCR para .NET](/ocr/english/net/ocr-configuration/ocr-operation-with-list/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}