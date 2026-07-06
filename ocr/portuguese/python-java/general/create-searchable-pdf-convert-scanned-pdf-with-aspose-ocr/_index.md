---
category: general
date: 2026-03-18
description: Crie PDF pesquisável a partir dos seus arquivos digitalizados usando
  o Aspose OCR. Aprenda como converter PDF digitalizado, extrair texto de PDF e reconhecer
  texto em PDF rapidamente.
draft: false
keywords:
- create searchable pdf
- convert scanned pdf
- extract text from pdf
- recognize text pdf
- convert image pdf
language: pt
og_description: Crie PDF pesquisável instantaneamente. Siga este guia para converter
  PDF escaneado, extrair texto de PDF e reconhecer texto em PDF usando o Aspose OCR.
og_title: Criar PDF pesquisável – Passo a passo com Aspose OCR
tags:
- OCR
- PDF
- Aspose
- Python
title: Criar PDF pesquisável – Converter PDF escaneado com Aspose OCR
url: /pt/python-java/general/create-searchable-pdf-convert-scanned-pdf-with-aspose-ocr/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Criar PDF pesquisável – Guia passo a passo  

Já precisou **create searchable PDF** a partir de um conjunto de páginas escaneadas, mas não sabia por onde começar? Você não está sozinho—a maioria dos desenvolvedores encontra esse obstáculo quando o primeiro escaneamento chega ao servidor.  

A boa notícia é que, com o Aspose OCR, você pode **convert scanned pdf** em apenas algumas linhas, **extract text from pdf** para validação e até **recognize text pdf** em tempo real. Neste tutorial, percorreremos todo o processo, desde a instalação da biblioteca até a gravação de um documento totalmente pesquisável, e incluiremos algumas dicas para lidar com casos extremos de **convert image pdf**.  

## O que você alcançará  

* Carregar um PDF escaneado (ou um PDF somente de imagens) no Aspose OCR.  
* Informar ao motor quais páginas processar – útil quando você precisa apenas de um subconjunto.  
* Incorporar os resultados do OCR de volta ao arquivo original para que a saída seja um verdadeiro **searchable PDF**.  
* Verificar a operação imprimindo a contagem de páginas e, se desejar, exibindo o texto extraído.  

Sem serviços externos, sem mágica oculta—apenas Python puro e a própria API da Aspose.  

## Pré-requisitos  

* Python 3.8 ou superior.  
* Pacote `aspose-ocr` – instale com `pip install aspose-ocr`.  
* Um arquivo PDF escaneado (ou um PDF que contém apenas imagens).  
* Familiaridade básica com scripts Python.  

Se você já tem tudo isso, ótimo—vamos mergulhar.

<img src="searchable-pdf-workflow.png" alt="Fluxo de criação de PDF pesquisável">  

*(Ilustração do pipeline OCR – não necessária para o código, mas ajuda aprendizes visuais.)*  

## Etapa 1 – Inicializar o motor OCR  

Primeiro de tudo: você precisa de uma instância `OcrEngine`. Pense nela como o cérebro que lerá cada pixel e o transformará em caracteres Unicode.

```python
# Step 1: Import the required classes and create the engine
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

# Initialize the OCR engine – this object holds all settings
ocr_engine = OcrEngine()
```

**Por que isso importa:** Sem o motor, você não pode definir opções ou executar o reconhecimento. Inicializá-lo cedo também lhe dá um local para anexar quaisquer dicionários personalizados posteriormente.  

## Etapa 2 – Carregar seu PDF de origem  

O Aspose OCR pode ler PDFs diretamente, o que significa que você não precisa rasterizar cada página manualmente. Basta apontar o motor para o arquivo.

```python
# Step 2: Load the scanned PDF (replace with your actual path)
input_path = "YOUR_DIRECTORY/input.pdf"
ocr_engine.setImageFromFile(input_path)
```

*Dica profissional:* Se o PDF for grande, considere carregá‑lo a partir de um stream para evitar bloquear o arquivo no disco.  

## Etapa 3 – Configurar opções de reconhecimento de PDF  

Aqui é onde as palavras‑chave secundárias começam a brilhar. Você pode dizer ao motor para **convert scanned pdf** apenas em determinadas páginas, incorporar o texto reconhecido ou até manter as imagens originais intactas.

```python
# Step 3: Create and configure PDF recognition options
pdf_options = PdfRecognitionOptions()
pdf_options.setEmbedRecognisedText(True)          # Makes the PDF searchable
pdf_options.setPageRange(1, 3)                    # Process only pages 1‑3 (optional)
pdf_options.setTextExtractionMode(True)          # Enables text extraction for verification
```

**Por que isso importa:**  
* `setEmbedRecognisedText(True)` é a chave para transformar um PDF raster em um **searchable PDF**.  
* `setPageRange` ajuda você a **convert image pdf** seletivamente—útil para documentos grandes onde você precisa OCR apenas de algumas páginas.  
* Habilitar a extração de texto permite que você depois **extract text from pdf** sem abrir um visualizador.  

## Etapa 4 – Anexar opções ao motor  

Agora vincule as opções ao motor. Essa etapa é fácil de esquecer, mas pular isso significa que o motor roda com configurações padrão (sem texto pesquisável).

```python
# Step 4: Attach the options to the OCR engine
ocr_engine.setPdfRecognitionOptions(pdf_options)
```

## Etapa 5 – Executar OCR nas páginas selecionadas  

Com tudo conectado, o reconhecimento real é uma única chamada de método.

```python
# Step 5: Perform OCR – this may take a few seconds per page
ocr_result = ocr_engine.recognize()
```

Se você estiver processando um documento de vários megabytes, pode ser interessante envolver isso em um bloco try/except para capturar `OcrException` e registrar a página problemática.  

## Etapa 6 – Verificar o resultado  

Uma verificação rápida de sanidade é imprimir quantas páginas o motor acredita ter processado. Você também pode extrair o texto bruto se precisar **extract text from pdf** para análise adicional.

```python
# Step 6: Show how many pages were processed
print("Pages processed:", ocr_result.getPageCount())

# Optional: dump extracted text for the first page (helps debugging)
first_page_text = ocr_result.getPageText(0)   # 0‑based index
print("\n--- Extracted Text (Page 1) ---\n", first_page_text[:500])  # show first 500 chars
```

**Por que isso importa:** Ver a contagem de páginas confirma que `setPageRange` funcionou, e o trecho de texto extraído prova que o OCR realmente reconheceu caracteres.  

## Etapa 7 – Salvar o PDF pesquisável  

Finalmente, grave a saída de volta ao disco. A constante `ImageFormats.PDF` indica ao Aspose que o arquivo deve permanecer como PDF, agora enriquecido com texto pesquisável.

```python
# Step 7: Save the searchable PDF
output_path = "YOUR_DIRECTORY/output.pdf"
ocr_engine.save(output_path, ImageFormats.PDF)

print(f"Searchable PDF saved to: {output_path}")
```

Abra o arquivo resultante em qualquer leitor de PDF e tente uma pesquisa de texto—voilà, você **created searchable pdf**!  

## Lidando com casos extremos comuns  

### Quando a fonte é um PDF *somente‑imagem*  

Se o seu PDF de entrada contém apenas imagens (nenhuma camada de texto), o mesmo código funciona—basta garantir que `setEmbedRecognisedText(True)` permaneça habilitado. Você também pode querer aumentar o DPI para melhor precisão:

```python
pdf_options.setResolution(300)  # 300 DPI gives sharper OCR results
```

### Lidando com múltiplos idiomas  

O Aspose OCR suporta pacotes de idioma. Carregue um idioma antes de chamar `recognize()`:

```python
ocr_engine.setLanguage("spa")   # Spanish language pack
```

### Documentos grandes  

Processar um PDF escaneado de 500 páginas pode consumir muita memória. Divida o trabalho:

1. Percorra intervalos de páginas (`setPageRange(start, end)`).  
2. Salve cada trecho como um PDF pesquisável temporário.  
3. Mescle os trechos com `PdfMerger` (outro componente da Aspose).  

## Exemplo completo em funcionamento (Todas as etapas juntas)

```python
# Full script – create searchable PDF from a scanned document
from aspose.ocr import OcrEngine, PdfRecognitionOptions, ImageFormats

def create_searchable_pdf(input_file: str, output_file: str, start_page: int = 1, end_page: int = 0):
    """
    Convert a scanned or image‑only PDF into a searchable PDF.
    :param input_file: Path to the source PDF.
    :param output_file: Destination path for the searchable PDF.
    :param start_page: First page to process (1‑based). Default = 1.
    :param end_page: Last page to process. 0 means “till the end”.
    """
    # Initialize engine
    ocr_engine = OcrEngine()
    ocr_engine.setImageFromFile(input_file)

    # Set options
    pdf_opts = PdfRecognitionOptions()
    pdf_opts.setEmbedRecognisedText(True)          # embed searchable text
    pdf_opts.setTextExtractionMode(True)           # allow text extraction
    if end_page > 0:
        pdf_opts.setPageRange(start_page, end_page)  # selective processing
    else:
        pdf_opts.setPageRange(start_page, start_page)  # process from start_page onward

    # Attach options
    ocr_engine.setPdfRecognitionOptions(pdf_opts)

    # Run OCR
    result = ocr_engine.recognize()
    print("Pages processed:", result.getPageCount())

    # Optional verification
    print("\nSample extracted text (first page):")
    print(result.getPageText(0)[:300])

    # Save searchable PDF
    ocr_engine.save(output_file, ImageFormats.PDF)
    print(f"Searchable PDF saved to: {output_file}")

if __name__ == "__main__":
    create_searchable_pdf(
        input_file="YOUR_DIRECTORY/input.pdf",
        output_file="YOUR_DIRECTORY/output.pdf",
        start_page=1,
        end_page=3   # change or set to 0 to process the whole file
    )
```

Executar este script lhe dará um **searchable PDF** que você pode abrir no Adobe Reader, Chrome ou qualquer visualizador de PDF e pesquisar palavras instantaneamente.  

## Conclusão  

Agora você tem uma solução completa, de ponta a ponta, para **create searchable PDF** usando o Aspose OCR. Desde o carregamento da fonte, configuração de opções que **convert scanned pdf**, extração e verificação de texto, até a gravação final do resultado pesquisável, cada etapa está coberta.  

Em seguida, você pode querer explorar cenários de **convert image pdf** onde a fonte é uma série de JPEGs empacotados em um PDF, ou aprofundar-se no OCR específico por idioma para melhorar a precisão em documentos multilíngues. De qualquer forma, o padrão permanece o mesmo: definir opções, executar `recognize()`, e salvar.  

Sinta‑se à vontade para experimentar—alterar o intervalo de páginas, ajustar o DPI, ou conectar um dicionário personalizado. Se encontrar algum problema, deixe um comentário abaixo ou consulte a documentação oficial da Aspose para as nuances mais recentes da API. Feliz OCR  

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}