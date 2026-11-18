---
category: general
date: 2026-06-25
description: Initialiser le moteur OCR en Python pour extraire le texte de PDF multi‑pages
  en utilisant des dictionnaires personnalisés, des paramètres de langue et le ciblage
  de région.
draft: false
keywords:
- initialize OCR engine
- configure OCR language
- OCR image preprocessing
- OCR custom dictionary
- recognize multi-page PDF
language: fr
og_description: Initialisez le moteur OCR en Python pour lire de manière fiable les
  PDF vietnamiens, configurez la langue, le prétraitement et le dictionnaire personnalisé
  afin d'obtenir des résultats précis.
og_title: Initialiser le moteur OCR – Guide d'extraction PDF étape par étape
schemas:
- author: Aspose
  dateModified: '2026-06-25'
  description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  headline: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  type: TechArticle
- description: Initialize OCR engine in Python to extract text from multi‑page PDFs
    using custom dictionaries, language settings, and region targeting.
  name: Initialize OCR Engine – Complete Guide for PDF Text Extraction
  steps:
  - name: Prerequisites
    text: '- Python 3.8+ installed. - An OCR library that exposes an `OcrEngine` class
      (the sample uses a hypothetical `ocr` package; replace with your actual SDK).
      - A sample multi‑page PDF (`sample.pdf`) placed in a known directory. - Basic
      familiarity with Python dictionaries and loops.'
  - name: Pro tip
    text: If you ever need to support multiple languages in the same run, you can
      switch `ocr_engine.language` on the fly before processing each page. Just remember
      to re‑initialize any heavy models if the SDK requires it.
  - name: Expected Output
    text: 'Running the script against a three‑page invoice PDF might produce:'
  type: HowTo
tags:
- OCR
- Python
- PDF processing
title: Initialiser le moteur OCR – Guide complet pour l'extraction de texte PDF
url: /fr/python-java/general/initialize-ocr-engine-complete-guide-for-pdf-text-extraction/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Initialiser le moteur OCR – Guide complet pour l'extraction de texte PDF

Vous avez déjà eu besoin d'**initialiser le moteur OCR** pour un lot de factures vietnamiennes mais vous ne saviez pas par où commencer ? Vous n'êtes pas le seul. Dans de nombreux projets réels, le premier obstacle est de faire communiquer la bibliothèque OCR avec vos PDF, surtout lorsque vous devez ajuster la langue, le prétraitement ou un dictionnaire personnalisé.  

Dans ce guide, nous parcourrons un exemple complet et exécutable qui vous montre comment **initialiser le moteur OCR**, configurer la langue, activer le prétraitement d'image intelligent, ajouter un dictionnaire personnalisé, puis extraire des données structurées de chaque page d’un PDF multi‑pages. À la fin, vous disposerez d’un script autonome que vous pourrez intégrer à votre propre projet—sans pièces manquantes, sans raccourcis « voir la documentation ».

## Ce que vous apprendrez

- Comment **initialiser le moteur OCR** avec le support de la langue vietnamienne.  
- Pourquoi **configurer la langue OCR** est important pour la précision.  
- Utilisation des options de **prétraitement d'image OCR** comme auto‑deskew et auto‑binarize.  
- Ajout d'un **dictionnaire personnalisé OCR** pour améliorer la reconnaissance des termes spécifiques au domaine.  
- **Reconnaître les PDF multi‑pages** et extraire une région spécifique (par ex., le montant total).  
- Transformer les résultats bruts en une structure propre de type JSON pour le traitement en aval.

### Prérequis

- Python 3.8+ installé.  
- Une bibliothèque OCR qui expose une classe `OcrEngine` (l'exemple utilise un package hypothétique `ocr` ; remplacez-le par votre SDK réel).  
- Un PDF multi‑pages d'exemple (`sample.pdf`) placé dans un répertoire connu.  
- Une familiarité de base avec les dictionnaires Python et les boucles.

Si vous avez tout cela, plongeons‑y.

---

## Étape 1 : Comment initialiser le moteur OCR en Python

La toute première chose à faire est **d'initialiser le moteur OCR**. Pensez-y comme allumer une machine et lui indiquer quelle langue vous allez lui fournir.

```python
import ocr  # Replace with your actual OCR package

# Create the engine instance
ocr_engine = ocr.OcrEngine()

# Set the language to Vietnamese – this tells the engine which character set to expect
ocr_engine.language = ocr.Language.Vietnamese
```

> **Pourquoi c’est important :**  
> La plupart des moteurs OCR sont fournis avec des packs de langues génériques. En définissant explicitement `ocr_engine.language`, vous évitez que le moteur ne devine mal les caractères, ce qui réduit considérablement les erreurs de reconnaissance pour les diacritiques courants en vietnamien.

### Astuce pro
Si vous devez un jour prendre en charge plusieurs langues dans la même exécution, vous pouvez changer `ocr_engine.language` à la volée avant de traiter chaque page. N'oubliez pas de ré‑initialiser les modèles lourds si le SDK l'exige.

---

## Étape 2 : Activer les options de prétraitement d'image OCR

Les numérisations brutes sont rarement parfaites. Des pages inclinées, un éclairage inégal ou un faible contraste peuvent perturber même les meilleurs reconnaisseurs. C’est pourquoi nous **configurons le prétraitement d'image OCR** juste après l'initialisation.

```python
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,      # Auto‑rotate to correct tilt
    auto_binarize=True    # Convert to black‑and‑white for sharper edges
)
```

Ces deux indicateurs suffisent souvent à nettoyer la plupart des factures numérisées. Si vos PDF sources sont déjà de haute qualité, vous pouvez les désactiver pour gagner quelques millisecondes par page.

---

## Étape 3 : Ajouter un dictionnaire personnalisé OCR

Les termes spécifiques au domaine—comme les codes de commande, les ID produit ou les abréviations juridiques—apparaissent rarement dans les modèles de langue génériques. En fournissant un **dictionnaire personnalisé OCR**, vous donnez au moteur une feuille de triche.

```python
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]
```

> **Que se passe-t-il en coulisses ?**  
> Le moteur augmente les scores de confiance pour chaque mot qui correspond à une entrée de cette liste, le rendant beaucoup moins susceptible d’être mal lu comme autre chose.

---

## Étape 4 : Reconnaître les PDF multi‑pages – Extraire tout le texte d’un coup

Maintenant que le moteur est entièrement configuré, nous pouvons **reconnaître les PDF multi‑pages**. La méthode `recognize_multi_page` renvoie une liste où chaque élément représente une page unique, déjà traitée par OCR.

```python
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)
```

Si vous devez traiter des PDF gigantesques (des centaines de pages), envisagez de les traiter par lots afin de limiter l’utilisation de la mémoire. Le SDK propose généralement une API de streaming pour ce scénario.

---

## Étape 5 : Extraire une région spécifique de chaque page

La plupart des factures possèdent un champ « Montant total » qui se trouve au même endroit sur chaque page. Au lieu d’analyser tout le texte de la page, nous pouvons demander au moteur de se concentrer sur un rectangle.

```python
from ocr import Rectangle  # Adjust import based on your SDK

for page_index, page in enumerate(pages, start=1):
    # Define the rectangle (x, y, width, height) that encloses the total amount
    total_region = Rectangle(400, 650, 200, 50)

    # Run OCR only on that region
    region_result = ocr_engine.recognize_region(page.image, total_region)
```

> **Pourquoi cibler une région ?**  
> Limiter l’OCR à une petite zone accélère le traitement et réduit les faux positifs, surtout lorsque le reste de la page est bruyant.

---

## Étape 6 : Assembler un dictionnaire de type JSON pour chaque page

Avoir le texte brut, c’est bien, mais les systèmes en aval attendent généralement des données structurées. Ci‑dessous, nous construisons un dictionnaire propre qui capture le numéro de page, le texte complet de la page, le total extrait, et une liste de tous les mots reconnus avec leurs scores de confiance.

```python
    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    # Step 7: Output the result for the current page
    print(page_output)
```

Exécuter le script émettra une série de dictionnaires—un par page—ressemblant à ceci :

```json
{
  "page": 1,
  "full_text": "....",
  "total_amount": "1,250,000 VND",
  "words": [
    {"text": "MãĐơnHàng", "conf": 0.98},
    {"text": "KháchHàng", "conf": 0.96},
    ...
  ]
}
```

Vous pouvez facilement rediriger la sortie vers un fichier (`> results.jsonl`) pour un traitement par lots ultérieur.

---

## Exemple complet fonctionnel

En réunissant tous les éléments, voici le script complet que vous pouvez copier‑coller et exécuter :

```python
import ocr
from ocr import Rectangle

# -------------------------------------------------
# 1️⃣ Initialize the OCR engine and configure it
# -------------------------------------------------
ocr_engine = ocr.OcrEngine()
ocr_engine.language = ocr.Language.Vietnamese
ocr_engine.image_preprocessing = ocr.ImagePreProcessingOptions(
    auto_deskew=True,
    auto_binarize=True
)
ocr_engine.custom_dictionary = ["MãĐơnHàng", "KháchHàng", "SốTiền"]

# -------------------------------------------------
# 2️⃣ Recognize all pages of a multi‑page PDF
# -------------------------------------------------
pdf_path = "YOUR_DIRECTORY/sample.pdf"
pages = ocr_engine.recognize_multi_page(pdf_path)

# -------------------------------------------------
# 3️⃣ Iterate through each page, extract region, and build output
# -------------------------------------------------
for page_index, page in enumerate(pages, start=1):
    total_region = Rectangle(400, 650, 200, 50)          # region of interest
    region_result = ocr_engine.recognize_region(page.image, total_region)

    page_output = {
        "page": page_index,
        "full_text": page.text,
        "total_amount": region_result.text,
        "words": [
            {"text": word.text, "conf": word.confidence}
            for word in page.words
        ]
    }

    print(page_output)   # Replace with logging or file write as needed
```

### Résultat attendu

Exécuter le script sur un PDF de facture de trois pages pourrait produire :

```
{'page': 1, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.99}, ...]}
{'page': 2, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.98}, ...]}
{'page': 3, 'full_text': '...', 'total_amount': '1,250,000 VND', 'words': [{'text': 'MãĐơnHàng', 'conf': 0.97}, ...]}
```

N’hésitez pas à le passer dans `jq` ou tout autre analyseur JSON pour vérifier la structure.

---

## Questions fréquentes & cas particuliers

| Question | Réponse |
|----------|--------|
| **Et si mon PDF est protégé par mot de passe ?** | La plupart des SDK permettent de passer un argument `password` à `recognize_multi_page`. Il suffit d’ajouter `password="mySecret"` à l’appel. |
| **Mes scans sont en niveaux de gris, pas en noir et blanc.** | L’option `auto_binarize` gérera cela, mais vous pouvez également convertir manuellement avec `Pillow` avant d’alimenter l’image à `recognize_region`. |
| **Le montant total apparaît parfois à une coordonnée différente.** | Calculez le rectangle dynamiquement (par ex., via un appariement de modèle) ou effectuez un OCR plein‑page puis recherchez le texte avec une expression régulière comme `r'\d{1,3}(,\d{3})* VND'`. |
| **Les performances sont lentes sur des PDF de 500 pages.** | Traitez les pages par lots : traitez 50 pages, écrivez les résultats, puis videz la liste `pages` pour libérer la mémoire. Désactivez également `auto_deskew` si vos scans sont déjà droits. |
| **Comment gérer d’autres langues plus tard ?** | Changez simplement `ocr_engine.language = ocr.Language.English` (ou tout autre enum supporté) avant d’appeler `recognize_multi_page`. Le reste du pipeline reste identique. |

---

## Conseils pour des déploiements prêts pour la production

1. **Gestion des erreurs** – Enveloppez les appels OCR dans des blocs `try/except` ; journalisez l’indice de page en cas d’échec afin de pouvoir réessayer plus tard.  
2. **Journalisation** – Utilisez le module `logging` de Python au lieu de `print` pour une verbosité flexible.  
3. **Parallélisme** – Si votre bibliothèque OCR est thread‑safe, créez un `ThreadPoolExecutor` pour traiter les pages en parallèle.  
4. **Fichier de configuration** – Stockez la langue, le dictionnaire et les coordonnées du rectangle dans un fichier JSON/YAML ; cela rend le script réutilisable entre projets.  
5. **Tests** – Créez une petite suite de tests avec des PDF connus et vérifiez que le `total_amount` extrait correspond aux valeurs attendues.  

---

## Conclusion

Vous venez d’apprendre **

## Que devriez‑vous apprendre ensuite ?

Les tutoriels suivants couvrent des sujets étroitement liés qui s’appuient sur les techniques démontrées dans ce guide. Chaque ressource inclut des exemples de code complets et fonctionnels avec des explications pas à pas pour vous aider à maîtriser des fonctionnalités API supplémentaires et explorer des approches d’implémentation alternatives dans vos propres projets.

- [Reconnaître le texte PDF – Opérations OCR avec Aspose.OCR pour Java](/ocr/english/java/ocr-operations/)
- [Reconnaître le texte d'image avec Aspose OCR pour plusieurs langues](/ocr/english/net/ocr-settings/working-with-different-languages/)
- [Extraire le texte d'une image – Optimisation OCR avec Aspose.OCR pour .NET](/ocr/english/net/ocr-optimization/)

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}