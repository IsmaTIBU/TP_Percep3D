# Système de Contrôle Qualité en Vision 3D

Une implémentation pratique du contrôle qualité d'objets 3D utilisant des données de capteurs RGB-D et des techniques de traitement de nuages de points.

# Index
### - [À Quoi Ça Sert ?](#à-quoi-ça-sert)  
### - [Comment Ça Marche ?](#comment-ça-marche-en-termes-simples)  
### - [Fichiers du Projet](#fichiers-du-projet-expliqués)  
### - [Applications dans le Monde Réel](#applications-dans-le-monde-réel)  
### - [Concepts Clés](#concepts-clés)

## À Quoi Ça Sert ?

Imaginez que vous fabriquez des pièces dans une usine et que vous devez vérifier si chaque pièce correspond à un modèle de référence parfait. Ce système fait exactement cela - mais en 3D ! Il utilise des caméras de profondeur (comme Microsoft Kinect) pour capturer des scans 3D d'objets et détecter automatiquement les défauts comme les trous, les bosses ou les pièces manquantes.

## Comment Ça Marche ? (En Termes Simples)

### 1. **Capture de Données 3D**
- Un **capteur RGB-D** (une caméra spéciale qui voit à la fois la couleur et la profondeur) scanne un objet
- Cela crée un **nuage de points** - imaginez des milliers de petits points dans l'espace 3D qui forment ensemble la forme de l'objet
- Chaque point a des coordonnées X, Y, Z nous indiquant exactement où il se situe dans l'espace

### 2. **Construction d'un Modèle de Référence**
- D'abord, nous scannons un objet parfait et sans défaut pour l'utiliser comme notre "étalon de référence"
- Nous supprimons l'arrière-plan (table, murs, etc.) pour isoler uniquement l'objet
- Celui-ci devient notre modèle de référence auquel tous les objets futurs seront comparés

### 3. **Alignement des Objets de Test (Algorithme ICP)**
- Lorsque nous scannons un nouvel objet à vérifier, il peut être tourné ou positionné différemment
- L'algorithme **ICP (Iterative Closest Point)** est comme un résolveur intelligent de puzzle - il détermine comment faire pivoter et déplacer l'objet de test pour qu'il s'aligne parfaitement avec la référence
- Pensez-y comme à la superposition de deux feuilles transparentes jusqu'à ce qu'elles correspondent le mieux possible

### 4. **Détection de Défauts**
- Une fois alignés, nous comparons les deux nuages de points
- Les points qui ne correspondent pas indiquent des défauts :
  - **Points supplémentaires** = matériau indésirable ou résidus
  - **Points manquants** = trous ou pièces manquantes
  - **Points déplacés** = déformations ou dimensions incorrectes

## Fichiers du Projet Expliqués

| Fichier | Ce Qu'il Fait |
|---------|---------------|
| `datatools.py` | Fonctions auxiliaires pour charger, sauvegarder et visualiser les nuages de points 3D |
| `icp.py` | L'algorithme d'alignement qui fait correspondre les objets de test à la référence |
| `qualitycheck.py` | Script principal qui exécute le processus complet de contrôle qualité |
| `data01.xyz` | Scan brut de la scène de référence (avec arrière-plan) |
| `data01_segmented.xyz` | Objet de référence propre (arrière-plan supprimé) |
| `data02_object.xyz` | Objet de test #1 à vérifier |
| `data03_object.xyz` | Objet de test #2 à vérifier |

## Technologies Spécifiques Utilisées

- **CloudCompare** - Logiciel professionnel de visualisation de nuages de points 3D

## Applications dans le Monde Réel

- **Contrôle qualité en fabrication** - Vérifier si les pièces correspondent aux spécifications
- **Vérification d'impression 3D** - S'assurer que les objets imprimés correspondent à la conception
- **Archéologie** - Comparer des artefacts ou des travaux de restauration
- **Imagerie médicale** - Détecter des anomalies dans les scans 3D
- **Robotique** - Aider les robots à reconnaître et manipuler des objets

## Comprendre les Résultats

Le système produit :
- **Des visualisations** montrant la référence (rouge) et l'objet de test (bleu) superposés
- **Des graphiques d'erreur** montrant l'efficacité de l'alignement
- **Des mesures numériques** des différences entre les objets
- **Des fichiers exportés** avec les nuages de points alignés pour une inspection détaillée

## Concepts Clés

### Nuage de Points
Une collection de points dans l'espace 3D qui représente la surface d'un objet. Comme un dessin de points à relier en 3D avec des milliers de points.

### Recalage
Le processus d'alignement de deux scans 3D pour qu'ils soient dans le même système de coordonnées. Essentiel pour la comparaison.

### Capteur RGB-D
Une caméra qui capture à la fois des images couleur régulières (RGB) et des informations de profondeur (D), lui permettant de voir en 3D.

### ICP (Iterative Closest Point)
Un algorithme qui répète :
1. Trouve les points les plus proches entre deux formes
2. Calcule la meilleure rotation et translation pour les aligner
3. Applique la transformation et répète jusqu'à convergence

---

**Note :** Il s'agit d'un projet éducatif conçu pour enseigner les fondamentaux de la vision par ordinateur en 3D, du traitement de nuages de points et des systèmes automatisés de contrôle qualité.
