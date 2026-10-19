---
category: general
date: 2026-04-26
description: 'como fazer OCR em Python: Aprenda a extrair texto de imagens e ler arquivos
  TIFF em Python usando um exemplo básico de OCR. Código rápido e executável incluído.'
draft: false
keywords:
- how to ocr python
- extract text from image
- read tiff file python
- basic ocr example
- convert scanned image text
language: pt
og_description: 'como fazer OCR python: um guia passo a passo que mostra como extrair
  texto de imagens, ler arquivos TIFF em Python e converter texto de imagens escaneadas
  com um script simples e executável.'
og_title: como fazer OCR em Python – Exemplo básico de OCR para extrair texto
tags:
- OCR
- Python
- Image Processing
title: Como fazer OCR em Python – Exemplo básico de OCR para extrair texto
url: /pt/python-java/general/how-to-ocr-python-basic-ocr-example-for-extracting-text/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# como fazer OCR python – Exemplo Básico de OCR para Extrair Texto

Já se perguntou **como fazer OCR python** quando tem um TIFF escaneado na sua mesa? Você não é o único que olha para um monte de arquivos de imagem e pergunta: “Como eu tiro as palavras disso?” A boa notícia é que transformar uma foto em texto simples é muito fácil com a biblioteca certa e alguns passos claros.

Neste tutorial vamos percorrer um **exemplo básico de OCR** que lê um arquivo TIFF, extrai o texto e o imprime no console. Ao final, você saberá exatamente como **extrair texto de arquivos de imagem**, como lidar com as particularidades dos formatos TIFF e o que ajustar se precisar **converter texto de imagem escaneada** em algo mais útil. Sem mágica escondida — apenas Python direto que você pode copiar‑colar e executar hoje.

## O que Você Precisa

Antes de mergulharmos, certifique‑se de que tem:

- Python 3.9+ instalado (a versão estável mais recente é a melhor).
- Uma biblioteca OCR instalável via pip. Para este guia usaremos um pacote fictício `aocr` que imita ferramentas populares como Tesseract; você pode substituí‑lo por `pytesseract` ou `easyocr` depois.
- Uma imagem TIFF que você queira processar – nomeie‑a como `input.tiff` e coloque‑a em uma pasta que será referenciada no código.
- Familiaridade básica com a linha de comando (apenas para instalar o pacote).

É isso. Sem dependências pesadas, sem contêineres Docker, apenas algumas linhas de código.

## Passo 1 – Instalar e Importar Dependências (como fazer OCR python)

Primeiro, obtenha o pacote OCR. Abra um terminal e execute:

```bash
pip install aocr
```

Se preferir uma biblioteca real, troque `aocr` por `pytesseract` e instale o motor Tesseract separadamente.

Agora importe o que precisamos. A classe `Path` de `pathlib` nos dá uma forma limpa de trabalhar com caminhos de arquivos em diferentes sistemas operacionais.

```python
# Step 1: Import the Path class for handling file paths
from pathlib import Path

# Import the OCR engine and image loader from the chosen library
from aocr import OcrEngine, Image
```

*Por que usar `Path`?* Porque ela abstrai as barras (`/` vs `\`) e permite juntar diretórios sem se preocupar com o SO subjacente. Esse pequeno detalhe costuma salvar dores de cabeça quando você move o script para um servidor de CI.

## Passo 2 – Criar a Instância do Motor OCR (exemplo básico de OCR)

Em seguida, inicialize o motor OCR. Pense no `OcrEngine` como o cérebro que vai ler a imagem e gerar caracteres.

```python
# Step 2: Create an instance of the OCR engine
ocr_engine = OcrEngine()
```

A maioria das bibliotecas OCR permite ajustar idioma, DPI ou limites de confiança aqui. Para este **exemplo básico de OCR** vamos ficar com as configurações padrão, mas você pode explorar `ocr_engine.config` depois se precisar lidar com documentos multilíngues.

## Passo 3 – Carregar Sua Imagem TIFF (ler arquivo tiff python)

É aqui que entra a parte **ler arquivo tiff python**. TIFFs podem ter várias páginas, mas `Image.load` captura a primeira página por padrão — perfeito para um escaneamento de página única.

```python
# Step 3: Load the image you want to recognize
# Using a generic placeholder path makes it easy to adapt the example
ocr_engine.image = Image.load(Path("YOUR_DIRECTORY/input.tiff"))
```

Substitua `"YOUR_DIRECTORY"` pela pasta real que contém `input.tiff`. Se não souber onde o script está sendo executado, `Path.cwd()` imprime o diretório de trabalho atual — útil para depurar problemas de caminho.

## Passo 4 – Executar o Processo OCR (extrair texto de imagem)

Agora a mágica acontece. Chamar `process()` envia a imagem pelo pipeline OCR e devolve um objeto de resultado.

```python
# Step 4: Run the OCR process to extract text from the image
ocr_result = ocr_engine.process()
```

Nos bastidores, o motor pode estar convertendo a imagem para escala de cinza, aplicando limiarização e alimentando uma rede neural. Você não precisa gerenciar esses passos; a biblioteca os abstrai.

## Passo 5 – Imprimir o Texto Reconhecido (converter texto de imagem escaneada)

Por fim, exiba o texto. Em projetos reais você provavelmente gravaria isso em um arquivo ou banco de dados, mas imprimir mantém o exemplo simples.

```python
# Step 5: Print the recognized text to the console
print(ocr_result.text)
```

Ao executar o script, você deverá ver algo como:

```
Hello, world!
This is a sample scanned document.
```

Se a saída parecer confusa, verifique se a imagem fonte está nítida e se o idioma do OCR corresponde ao texto.

## Script Completo Funcionando

Juntando tudo, aqui está o programa completo, pronto para ser executado:

```python
# Full script: how to ocr python – basic OCR example

from pathlib import Path
from aocr import OcrEngine, Image  # Replace with your OCR library if needed

def main():
    # Initialize the OCR engine
    ocr_engine = OcrEngine()

    # Load the TIFF image (adjust the path as needed)
    image_path = Path("YOUR_DIRECTORY/input.tiff")
    if not image_path.is_file():
        raise FileNotFoundError(f"Could not find {image_path}. Make sure the file exists.")
    
    ocr_engine.image = Image.load(image_path)

    # Perform OCR
    ocr_result = ocr_engine.process()

    # Output the extracted text
    print("=== OCR Output ===")
    print(ocr_result.text)

if __name__ == "__main__":
    main()
```

### Saída Esperada

```
=== OCR Output ===
Your scanned document’s text appears here, line by line.
```

Se precisar **converter texto de imagem escaneada** em um PDF pesquisável, você pode encaminhar `ocr_result.text` para um gerador de PDF como `reportlab` — mas isso é um tutorial inteiro por si só.

## Armadilhas Comuns & Dicas Profissionais

- **Escaneamentos de baixa resolução**: OCR tem dificuldade abaixo de 150 DPI. Se seu TIFF estiver borrado, aumente a resolução primeiro com Pillow (`Image.open(...).resize(...)`).
- **Múltiplas páginas**: Para TIFFs de várias páginas, itere sobre `Image.load_multi_page()` (se sua biblioteca suportar) e concatene os resultados.
- **Suporte a idiomas**: Muitos motores padrão são em inglês. Defina `ocr_engine.language = "spa"` para espanhol, por exemplo.
- **Tratamento de espaços em branco**: OCR costuma inserir quebras de linha indesejadas. Use `str.splitlines()` ou expressões regulares para limpar a saída.
- **Desempenho**: Para processamento em massa, reutilize uma única instância de `OcrEngine` ao invés de criar uma nova para cada arquivo.

## Expandindo o Exemplo

Agora que você domina **como fazer OCR python** para uma única imagem, considere os próximos passos:

1. **Processamento em lote** – Percorra um diretório de TIFFs e grave cada resultado em um arquivo `.txt`.
2. **Integração com Pandas** – Armazene o texto extraído junto com metadados para análise rápida.
3. **Abordagem híbrida** – Combine OCR com bibliotecas de NLP como `spaCy` para extrair entidades (nomes, datas, valores) de faturas escaneadas.
4. **Formatos de arquivo alternativos** – Troque `Image.load` por `Image.from_bytes` para lidar com imagens vindas de uma API ou banco de dados.

Todos esses passos se baseiam na ideia central de **extrair texto de imagem** e **converter texto de imagem escaneada** em algo que máquinas podem entender.

## Conclusão

Percorremos um **exemplo básico de OCR** que demonstra **como fazer OCR python**, como **ler arquivo tiff python** e como **extrair texto de imagem** usando apenas algumas linhas de código. O script é autocontido, inclui tratamento de erros e imprime o resultado diretamente, servindo como base sólida para qualquer projeto que precise transformar documentos escaneados em texto editável.

Sinta‑se à vontade para experimentar — troque o backend OCR, ajuste o pré‑processamento ou conecte a saída a um fluxo de trabalho posterior. O céu é o limite quando você pode **converter texto de imagem escaneada** em dados pesquisáveis e utilizáveis.

Tem dúvidas sobre casos extremos, pacotes de idioma ou otimização de desempenho? Deixe um comentário abaixo, e feliz codificação! 

![exemplo de como fazer OCR python](/images/ocr-python-example.png "Captura de tela da saída do script como fazer OCR python")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}