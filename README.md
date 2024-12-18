**Objectif :**
Ce code a pour but d'extraire, de nettoyer et de structurer les informations pertinentes d'un CV en PDF, en utilisant des outils d'extraction de texte et des bibliothèques de traitement du langage naturel (NLP). Le résultat est un fichier JSON contenant des informations organisées sur le candidat.

**Fonctionnement du Code :**,

-Importation des bibliothèques :
*typing et pydantic : Gérer les données structurées et valider leur intégrité.
*os, re, json : Manipuler les fichiers, traiter les chaînes de caractères, et gérer le format JSON.
*pdf2image et pytesseract : Convertir les fichiers PDF en images et extraire le texte des images grâce à l'OCR.
*spacy : Utiliser un modèle NLP pour extraire les entités nommées (NER).

-Configuration initiale :
*Tesseract : Défini le chemin d'installation pour utiliser l'OCR.
*Spacy : Charge le modèle NLP en_core_web_trf pour extraire les entités pertinentes du texte.

-Nettoyage du texte :
*Fonction clean_text(text) :
Supprime les espaces inutiles, réduit les espaces multiples en un seul, met tout le texte en minuscules, et enlève les lignes blanches.
-Modèle de données :

*Classe ResumeData :
Décrit le format attendu des données extraites sous forme d'attributs : noms, occupations, langues, éducation, intérêts, etc.
Utilise Pydantic pour valider que les données extraites correspondent à ce format.

-Extraction des données :
*Conversion du PDF en images :
La bibliothèque pdf2image convertit chaque page du PDF en image.
-Extraction du texte via OCR :
*pytesseract.image_to_string extrait le texte de chaque image.

-Analyse du texte avec Spacy :
*Entités nommées :
Chaque entité nommée (ex. PERSON, ORG, DATE) est analysée et triée dans des catégories pertinentes définies dans le dictionnaire raw_data.
*Mots-clés :
Les mots-clés spécifiques (ex. "engineer", "degree") sont utilisés pour capturer des informations supplémentaires comme les occupations, intérêts ou éducation.
*Post-traitement des données :
Supprime les doublons dans les résultats en utilisant des ensembles Python (set).
Valide les données structurées avec la classe ResumeData.
Convertit les données validées en JSON et les enregistre dans un fichier.

**Résultats :**

Les données extraites sont enregistrées dans un fichier validated_extracted_data.json, prêtes à être utilisées pour des analyses ou des intégrations.
