---
category: general
date: 2026-03-26
description: Aprenda como realizar OCR em Python e reconhecer texto a partir de arquivos
  de imagem. Este guia mostra como extrair texto de PNG e converter a imagem em texto
  rapidamente.
draft: false
keywords:
- how to perform ocr
- recognize text from image
- extract text from png
- ocr tutorial python
- convert image to text
language: pt
og_description: Como fazer OCR em Python? Siga este guia para reconhecer texto a partir
  de imagens, extrair texto de PNG e converter imagem em texto com uma licença de
  avaliação.
og_title: Como Realizar OCR em Python – Tutorial Completo
tags:
- OCR
- Python
- Image Processing
title: Como Realizar OCR em Python – Tutorial Completo Passo a Passo
url: /pt/python-java/general/how-to-perform-ocr-in-python-complete-step-by-step-tutorial/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Como Realizar OCR em Python – Tutorial Completo Passo a Passo  

Já se perguntou **como realizar OCR** em uma foto que você acabou de tirar com o seu telefone? Você não está sozinho—desenvolvedores em todo lugar precisam de uma forma confiável de reconhecer texto a partir de arquivos de imagem sem lutar com bibliotecas nativas complexas.  

Neste tutorial vamos percorrer um exemplo prático que mostra **como realizar OCR**, **reconhecer texto a partir de imagem** e **extrair texto de PNG** usando um wrapper leve em Python. Ao final você será capaz de **converter imagem em texto** em apenas algumas linhas de código, e não precisará se preocupar com dores de cabeça de licenciamento porque usaremos o modo de avaliação integrado.

## O que Você Vai Aprender  

* Como configurar uma licença de avaliação para o motor OCR (sem necessidade de caminho de arquivo).  
* A sequência exata de chamadas para **reconhecer texto a partir de imagem** objetos.  
* Formas de **extrair texto de PNG** arquivos e lidar com armadilhas comuns como fontes ausentes.  
* Dicas para escalar a solução quando você passar de uma avaliação para uma licença de produção.  

**Pré‑requisitos** – você precisa de Python 3.8+ e do pacote `ocr` (instalável via `pip install ocr`). Nenhuma outra ferramenta externa é necessária.

---  

![exemplo de como realizar OCR](https://example.com/ocr-demo.png "como realizar OCR em Python – texto reconhecido exibido")  

*Texto alternativo da imagem: como realizar OCR em Python – exemplo de saída*  

## Etapa 1 – Ativar uma Licença de Avaliação (Sem Necessidade de Caminho de Arquivo)  

Antes que o motor possa ler qualquer coisa, ele precisa de uma licença válida. O modo de avaliação é perfeito para experimentos e pequenos projetos.

```python
# Step 1: Activate a trial license (no file path needed for trial mode)
import ocr

trial_license = ocr.TrialLicense()
trial_license.apply()
```

*Por que isso importa:* O objeto de licença informa à biblioteca OCR que você está operando em um sandbox. Se você pular esta etapa, o motor lançará um `LicenseError` no momento em que chamar `recognize()`.  

**Dica profissional:** Quando você migrar para uma licença paga, substitua as duas linhas acima por `ocr.License("path/to/your/license.key").apply()`.

## Etapa 2 – Criar a Instância do Motor OCR  

Agora que a avaliação está ativa, instanciamos o motor principal. Pense nele como o “cérebro” que observará a imagem e decidirá quais caracteres estão onde.

```python
# Step 2: Create an OCR engine instance
ocr_engine = ocr.OcrEngine()
```

*Por que isso importa:* O `OcrEngine` mantém configurações como pacotes de idioma e definições de DPI. Você pode ajustar isso depois, mas o padrão funciona para a maioria dos PNGs apenas em inglês.

## Etapa 3 – Carregar o PNG que Você Deseja Processar  

É aqui que **reconhecemos texto a partir de imagem**. O método `ocr.Imaging.Image.load()` suporta PNG, JPEG, BMP e alguns outros formatos.

```python
# Step 3: Load the image you want to recognize
input_image = ocr.Imaging.Image.load("YOUR_DIRECTORY/sample1.png")
ocr_engine.set_image(input_image)
```

*Caso de borda:* Se o seu PNG usar uma paleta indexada (comum em capturas de tela), o carregador converterá automaticamente para um buffer RGB de 24 bits. Essa conversão pode causar uma pequena perda de desempenho, mas garante resultados precisos de OCR.

## Etapa 4 – Executar o OCR e Capturar o Texto  

Finalmente, pedimos ao motor que faça seu trabalho e então extraímos o resultado em texto puro.

```python
# Step 4: Perform OCR and print the recognized text
recognized_text = ocr_engine.recognize().get_text()
print(recognized_text)
```

**Saída esperada** (exemplo para uma imagem simples contendo “Hello World”):

```
Hello World
```

Se a imagem contiver várias linhas, a saída preservará quebras de linha, facilitando a alimentação de processos posteriores como analisadores CSV ou pipelines de NLP.

## Opcional: Ajuste Fino para Melhor Precisão  

* **Pacotes de idioma:** `ocr_engine.set_language("eng")` (padrão) ou `"fra"` para francês.  
* **Escala de DPI:** `ocr_engine.set_dpi(300)` pode melhorar resultados em digitalizações de baixa resolução.  
* **Pré‑processamento:** Aplicar um limiar binário (`ocr.Imaging.Image.threshold()`) antes de `set_image` costuma gerar texto mais limpo em fundos ruidosos.

Esses ajustes são úteis quando você passa de uma demonstração rápida para um **ocr tutorial python** de nível produção que processa centenas de arquivos por dia.

## Script Completo – Pronto para Copiar e Colar  

Abaixo está o script completo e executável que combina todas as etapas acima. Salve-o como `run_ocr.py` e substitua `YOUR_DIRECTORY/sample1.png` pelo caminho do seu próprio PNG.

```python
# run_ocr.py
# Complete example showing how to perform OCR, recognize text from image,
# and extract text from PNG using the ocr Python package.

import ocr

def main():
    # Activate trial license
    trial_license = ocr.TrialLicense()
    trial_license.apply()

    # Create engine
    ocr_engine = ocr.OcrEngine()

    # Load image (PNG, JPEG, etc.)
    image_path = "YOUR_DIRECTORY/sample1.png"
    input_image = ocr.Imaging.Image.load(image_path)
    ocr_engine.set_image(input_image)

    # Run OCR
    result = ocr_engine.recognize().get_text()
    print("=== Recognized Text ===")
    print(result)

if __name__ == "__main__":
    main()
```

Execute-o a partir da linha de comando:

```bash
python run_ocr.py
```

Você deverá ver o texto extraído impresso no console. Se receber uma string vazia, verifique novamente se a imagem realmente contém texto claro e de alto contraste e se a licença de avaliação foi aplicada sem erros.

## Perguntas Frequentes & Armadilhas  

* **“Isso funciona com JPEG?”** – Absolutamente. O método `load()` detecta o formato automaticamente, então você pode trocar PNG por JPEG sem mudar o código.  
* **“E se a imagem estiver rotacionada?”** – O motor pode detectar a orientação automaticamente, mas para obter os melhores resultados você pode pré‑rotacionar com `input_image.rotate(90)` antes de `set_image`.  
* **“Posso processar várias imagens em um loop?”** – Sim. Basta mover as chamadas de carregamento e `recognize()` para dentro de um `for` loop; a mesma instância `ocr_engine` pode ser reutilizada, economizando um pequeno overhead.  

## Próximos Passos – De Demo a Produção  

Agora que você sabe **como realizar OCR**, considere estes tópicos complementares:

* **Processamento em lote** – Combine este script com `os.listdir()` para **extrair texto de PNG** arquivos em massa.  
* **Integração com PDF** – Use `pdf2image` para converter páginas PDF em PNG e, em seguida, alimentá‑las na mesma pipeline.  
* **Pós‑processamento** – Aplique regex ou correspondência difusa para limpar erros comuns de OCR (ex.: “0” vs “O”).  

Cada um desses itens se baseia na ideia central de **converter imagem em texto** e amplia a utilidade do seu fluxo de trabalho OCR.

---  

### TL;DR  

Cobremos tudo o que você precisa saber para **como realizar OCR** em Python: ativar uma licença de avaliação, criar um motor, carregar um PNG, executar o reconhecimento e imprimir o resultado. Com apenas algumas linhas você pode **reconhecer texto a partir de imagem**, **extrair texto de PNG** e **converter imagem em texto** para qualquer aplicação posterior.  

Experimente, ajuste o DPI ou as configurações de idioma, e deixe o motor fazer o trabalho pesado. Feliz codificação!

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}