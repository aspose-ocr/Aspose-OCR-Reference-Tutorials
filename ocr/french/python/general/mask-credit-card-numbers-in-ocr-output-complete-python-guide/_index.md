---
category: general
date: 2026-04-26
description: Masquez rapidement les numéros de carte de crédit à l'aide du post‑traitement
  OCR d’AsposeAI. Apprenez la conformité PCI, le masquage par expression régulière
  et la désinfection des données dans un tutoriel étape par étape.
draft: false
keywords:
- mask credit card numbers
- PCI compliance
- OCR post‑processing
- AsposeAI
- regular expression masking
- data sanitization
language: fr
og_description: Masquez les numéros de carte de crédit dans les résultats OCR avec
  AsposeAI. Ce tutoriel couvre la conformité PCI, le masquage par expression régulière
  et l’assainissement des données.
og_title: Masquer les numéros de carte de crédit – Guide complet de post‑traitement
  OCR en Python
tags:
- OCR
- Python
- security
title: Masquer les numéros de carte de crédit dans la sortie OCR – Guide complet Python
url: /fr/python/general/mask-credit-card-numbers-in-ocr-output-complete-python-guide/
---

{{< blocks/products/pf/main-wrap-class >}}
{{< blocks/products/pf/main-container >}}
{{< blocks/products/pf/tutorial-page-section >}}

# Masquer les numéros de carte de crédit – Guide complet Python

Vous avez déjà eu besoin de **masquer les numéros de carte de crédit** dans du texte provenant directement d’un moteur OCR ? Vous n’êtes pas le seul. Dans les secteurs réglementés, exposer un PAN complet (Primary Account Number) peut vous mettre dans l’eau chaude avec les auditeurs de conformité PCI. La bonne nouvelle ? Avec quelques lignes de Python et le hook de post‑processing d’AsposeAI, vous pouvez masquer automatiquement les huit chiffres du milieu et rester du bon côté.

Dans ce tutoriel, nous allons parcourir un scénario réel : exécuter l’OCR sur une image de reçu, puis appliquer une fonction personnalisée de **post‑processing OCR** qui assainit toutes les données PCI. À la fin, vous disposerez d’un extrait réutilisable que vous pourrez intégrer à n’importe quel workflow AsposeAI, ainsi que d’une série de conseils pratiques pour gérer les cas limites et faire évoluer la solution.

## Ce que vous apprendrez

- Comment enregistrer un post‑processor personnalisé avec **AsposeAI**.
- Pourquoi une approche de **masquage par expression régulière** est à la fois rapide et fiable.
- Les bases de la **conformité PCI** liées à l’assainissement des données.
- Des moyens d’étendre le motif pour plusieurs formats de cartes ou des numéros internationaux.
- Le résultat attendu et comment vérifier que le masquage a fonctionné.

> **Prérequis** – Vous devez disposer d’un environnement Python 3 fonctionnel, du package Aspose.AI for OCR installé (`pip install aspose-ocr`), et d’une image d’exemple (par ex., `receipt.png`) contenant un numéro de carte de crédit. Aucun autre service externe n’est requis.

---

## Étape 1 : Définir un post‑processor qui masque les numéros de carte de crédit

Le cœur de la solution réside dans une petite fonction qui reçoit le résultat OCR, exécute une routine de **masquage par expression régulière**, et renvoie le texte assaini.

```python
def mask_pci(data, settings):
    """
    Replace the middle 8 digits of any 16‑digit card number with asterisks.
    Keeps the first and last four digits visible for reference.
    """
    import re
    # Pattern captures groups: first 4 digits, middle 8, last 4
    pattern = r'(\d{4})\d{8}(\d{4})'
    # Replace middle portion with ****
    return re.sub(pattern, r'\1****\2', data.text)
```

**Pourquoi cela fonctionne :**  
- L’expression régulière `(\d{4})\d{8}(\d{4})` correspond exactement à 16 chiffres consécutifs, le format commun pour Visa, MasterCard et bien d’autres.  
- En capturant les quatre premiers et les quatre derniers chiffres (`\1` et `\2`), nous conservons suffisamment d’informations pour le débogage tout en respectant les règles de **conformité PCI** qui interdisent le stockage du PAN complet.  
- La substitution `\1****\2` masque les huit chiffres sensibles du milieu, transformant `1234567812345678` en `1234****5678`.

> **Astuce pro** : Si vous devez prendre en charge les numéros American Express à 15 chiffres, ajoutez un second motif comme `r'(\d{4})\d{6}(\d{5})'` et exécutez les deux remplacements séquentiellement.

## Étape 2 : Initialiser le moteur AsposeAI

Avant de pouvoir attacher notre post‑processor, nous avons besoin d’une instance du moteur OCR. AsposeAI regroupe le modèle OCR et une API simple pour le traitement personnalisé.

```python
from aspose.ocr import AsposeAI

# Initialise the AI engine – it will handle image loading, recognition, and post‑processing
ai = AsposeAI()
```

**Pourquoi initialiser ici ?**  
Créer l’objet `AsposeAI` une fois et le réutiliser pour plusieurs images réduit la surcharge. Le moteur met également en cache les modèles linguistiques, ce qui accélère les appels suivants—pratique lorsque vous scannez des lots de reçus.

## Étape 3 : Enregistrer la fonction de masquage personnalisée

AsposeAI expose une méthode `set_post_processor` qui vous permet de brancher n’importe quel callable. Nous passons notre fonction `mask_pci` ainsi qu’un dictionnaire de paramètres optionnel (vide pour l’instant).

```python
# Register our masking routine; custom_settings can hold flags like "log_masked" if you expand later
ai.set_post_processor(mask_pci, custom_settings={})
```

**Ce qui se passe en coulisses**  
Lorsque vous invoquez plus tard `run_postprocessor`, AsposeAI transmet le résultat OCR brut à `mask_pci`. La fonction reçoit un objet léger (`data`) contenant le texte reconnu, et vous renvoyez une nouvelle chaîne. Cette conception garde le cœur de l’OCR intact tout en vous permettant d’appliquer des politiques de **sanitisation des données** en un seul endroit.

## Étape 4 : Exécuter l’OCR sur l’image du reçu

Maintenant que le moteur sait comment nettoyer la sortie, nous lui fournissons une image. Pour les besoins de ce tutoriel, nous supposons que vous avez déjà un objet `engine` configuré avec les bons paramètres de langue et de résolution.

```python
# Assume `engine` is a pre‑configured OCR object (e.g., with language='en')
ocr_engine = engine
raw_result = ocr_engine.recognize_image("receipt.png")
```

> **Conseil** : Si vous n’avez pas d’objet pré‑configuré, vous pouvez en créer un avec :

```python
from aspose.ocr import OcrEngine
ocr_engine = OcrEngine(language='en')
```

L’appel `recognize_image` renvoie un objet dont l’attribut `text` contient la chaîne brute, non masquée.

## Étape 5 : Appliquer le post‑processor enregistré

Avec les données OCR brutes en main, nous les transmettons à l’instance AI. Le moteur exécute automatiquement la fonction `mask_pci` que nous avons enregistrée précédemment.

```python
# This triggers the post‑processor and returns a new result object
final_result = ai.run_postprocessor(raw_result)
```

**Pourquoi utiliser `run_postprocessor` au lieu d’appeler la fonction manuellement ?**  
Cela maintient le flux de travail cohérent, surtout lorsque vous avez plusieurs post‑processors (par ex., correction orthographique, détection de langue). AsposeAI les place dans la file d’attente dans l’ordre d’enregistrement, garantissant une sortie déterministe.

## Étape 6 : Vérifier la sortie assainie

Enfin, affichons le texte assaini et confirmons que tous les numéros de carte de crédit sont correctement masqués.

```python
print(final_result.text)
```

**Sortie attendue** :

```
Purchase at Café Latte – Total: $4.75
Card: 1234****5678
Date: 2026-04-25
Thank you!
```

Si le reçu ne contenait aucun numéro de carte, le texte reste inchangé—rien à masquer, rien à craindre.

## Gestion des cas limites et des variations courantes

### Plusieurs numéros de carte dans un même document
Si un reçu inclut plus d’un PAN (par ex., une carte de fidélité plus une carte de paiement), l’expression régulière s’exécute globalement, masquant automatiquement toutes les correspondances. Aucun code supplémentaire n’est nécessaire.

### Formatage non standard
Parfois l’OCR insère des espaces ou des tirets (`1234 5678 1234 5678` ou `1234-5678-1234-5678`). Étendez le motif pour ignorer ces caractères :

```python
pattern = r'(\d{4})[ -]?\d{4}[ -]?\d{4}[ -]?\d{4}'
```

Le `[ -]?` ajouté tolère les espaces ou tirets optionnels entre les blocs de chiffres.

### Cartes internationales
Pour les PAN à 19 chiffres utilisés dans certaines régions, vous pouvez élargir le motif :

```python
pattern = r'(\d{4})\d{11,15}(\d{4})'
```

N’oubliez pas que la **conformité PCI** impose toujours le masquage des chiffres du milieu, quelle que soit la longueur.

### Journalisation des valeurs masquées (optionnel)
Si vous avez besoin de pistes d’audit, transmettez un drapeau via `custom_settings` et ajustez la fonction :

```python
def mask_pci(data, settings):
    import re, logging
    pattern = r'(\d{4})\d{8}(\d{4})'
    def repl(match):
        masked = f"{match.group(1)}****{match.group(2)}"
        if settings.get('log'):
            logging.info(f"Masked PAN: {masked}")
        return masked
    return re.sub(pattern, repl, data.text)
```

Puis enregistrez avec :

```python
ai.set_post_processor(mask_pci, custom_settings={'log': True})
```

## Exemple complet fonctionnel (prêt à copier‑coller)

```python
# ------------------------------------------------------------
# Mask Credit Card Numbers in OCR Output – Complete Example
# ------------------------------------------------------------
import re
from aspose.ocr import AsposeAI, OcrEngine

# 1️⃣ Define the post‑processor
def mask_pci(data, settings):
    """
    Hide the middle eight digits of any 16‑digit credit‑card number.
    """
    pattern = r'(\d{4})\d{8}(\d{4})'          # keep first & last 4 digits
    return re.sub(pattern, r'\1****\2', data.text)

# 2️⃣ Initialise the OCR engine and AsposeAI wrapper
ocr_engine = OcrEngine(language='en')       # configure as needed
ai = AsposeAI()

# 3️⃣ Register the masking function
ai.set_post_processor(mask_pci, custom_settings={})

# 4️⃣ Run OCR on a sample receipt
raw_result = ocr_engine.recognize_image("receipt.png")

# 5️⃣ Apply post‑processing (masking)
final_result = ai.run_postprocessor(raw_result)

# 6️⃣ Display sanitized text
print("Sanitized OCR output:")
print(final_result.text)
```

Exécuter ce script sur un reçu contenant `4111111111111111` produira :

```
Sanitized OCR output:
Purchase at Bookstore – $12.99
Card: 4111****1111
Date: 2026-04-26
```

Voici l’ensemble du pipeline—du OCR brut à la **sanitisation des données**—emballé en quelques lignes claires de Python.

## Conclusion

Nous venons de vous montrer comment **masquer les numéros de carte de crédit** dans les résultats OCR en utilisant le hook de post‑processing d’AsposeAI, une routine concise d’expression régulière, et une série de bonnes pratiques pour la **conformité PCI**. La solution est entièrement autonome, fonctionne avec n’importe quelle image que le moteur OCR peut lire, et peut être étendue pour couvrir des formats de cartes plus complexes ou des exigences de journalisation.

Prêt pour l’étape suivante ? Essayez de coupler ce masque avec une routine **d’insertion en base de données** qui ne conserve que les quatre derniers chiffres à titre de référence, ou intégrez un **processeur par lots** qui analyse un dossier complet de reçus pendant la nuit. Vous pouvez également explorer d’autres tâches de **post‑processing OCR** comme la normalisation d’adresses ou la détection de langue—toutes suivent le même schéma que celui présenté ici.

Des questions sur les cas limites, les performances, ou l’adaptation du code à une autre bibliothèque OCR ? Laissez un commentaire ci‑dessous, et continuons la discussion. Bon codage, et restez sécurisés !  



![Diagram illustrating how mask credit card numbers works in an OCR pipeline](https://example.com/images/ocr-mask-flow.png "Diagram of OCR post‑processing masking flow")

{{< /blocks/products/pf/tutorial-page-section >}}
{{< /blocks/products/pf/main-container >}}
{{< /blocks/products/pf/main-wrap-class >}}
{{< blocks/products/products-backtop-button >}}