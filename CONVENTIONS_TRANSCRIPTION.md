# Conventions de transcription des Souvenirs de jeunesse de Félix Berloty

Ce document consigne l'ensemble des règles éditoriales, typographiques, techniques et organisationnelles pour la transcription en LaTeX du tapuscrit dactylographié de <u>« Souvenirs de jeunesse »</u> de **Félix Berloty** (1886–1951), notaire à Lyon. Le document original compte une page de couverture et 72 pages de texte (vues O0165 à O0237 dans GrampsWeb, citation C1285, source S1675).

---

## 1. Organisation du projet & Gestion de version (Git)

### 1.1 Dépôt Git
- Le projet est versionné sous Git dans le répertoire racine.
- Les scans originaux du tapuscrit sont conservés dans `Originaux/` (`Couverture.jpg`, `Page 01.jpg` à `Page 72.jpg`).
- Le portrait utilisé sur la page de titre est conservé dans `Illustrations/Portrait_Felix_Berloty.jpg` (média GrampsWeb O0390).
- Le document principal est `Souvenirs de Jeunesse de Felix Berloty.tex`.
- Les fichiers auxiliaires LaTeX (`*.aux`, `*.log`, `*.toc`, etc.) sont exclus via `.gitignore`.

### 1.2 Conventional Commits (en français uniquement)
Tous les messages de commit doivent strictement suivre la norme des *Conventional Commits* rédigés en français, avec la structure suivante :

```
<type>[portée optionnelle]: <description en français au présent de l'indicatif/infinitif>

[corps optionnel explicatif]
```

#### Types autorisés :
- `feat:` : Ajout d'une nouvelle transcription de page ou de contenu textuel majeur (ex. `feat: transcription des pages 2 à 5`).
- `fix:` : Correction de transcription, de coquille, de ponctuation ou d'erreur LaTeX (ex. `fix: correction d'une coquille dans la page 4`).
- `docs:` : Mise à jour de la documentation, du fichier de conventions ou de métadonnées (ex. `docs: ajout des règles de transcription`).
- `style:` : Ajustements de mise en page, d'espacement, de formatage LaTeX sans modification du texte (ex. `style: harmonisation des tirets d'incise`).
- `refactor:` : Réorganisation structurelle du code LaTeX (ex. `refactor: normalisation des titres de sections`).
- `chore:` : Tâches de maintenance, mise à jour du `.gitignore` ou scripts de travail.

---

## 2. Structure et Préambule LaTeX

### 2.1 Configuration globale
Le document utilise la classe `report` avec les packages suivants :
```latex
\documentclass[11pt,a4paper]{report}
\usepackage[utf8]{inputenc}
\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage[french]{babel}
\usepackage{amsmath}
\usepackage{graphicx}
\usepackage{geometry}
\geometry{margin=2.5cm, headheight=14pt}
\usepackage{parskip}
\usepackage{setspace}
\usepackage{fancyhdr}
\usepackage{hyperref}
\usepackage{qrcode}
```

### 2.2 Titre et métadonnées
```latex
\title{\Huge \textbf{Souvenirs de jeunesse}}
\author{\textbf{Félix Berloty}}
\date{}
```

Le workflow CI injecte le numéro de release via `\releaseversion` (défini par `\providecommand` dans le préambule, remplacé par la CI sur une copie `*.release.tex`).

---

## 3. Règles de Transcription et Mise en Page

### 3.1 Préservation de la structure et du séquençage
- Le tapuscrit comporte une page de couverture et **72 pages** correspondant aux scans (`Page 01.jpg` à `Page 72.jpg`).
- La couverture n'est pas transcrite : le titre normalisé et le portrait d'illustration sont intégrés à la page de titre LaTeX.
- Le document original est organisé en grandes sections numérotées à la machine (ex. `I) Naissance et Enfance`). Chaque grande section correspond à un `\chapter{...}` du document LaTeX, avec un bloc de commentaires standardisé :
  ```latex
  % ===================================================
  % CHAPITRE X — Page NN à NN
  % ===================================================
  \chapter{Titre normalisé de la section (Période)}
  ```
- Un paragraphe interrompu par le saut de page du tapuscrit est **réuni en un seul paragraphe** dans la transcription : jamais deux blocs séparés au milieu d'une phrase. Le commentaire de page devient alors `% --- Page X (fin) + Page Y (début) — phrase continue`.
- Le découpage exact en chapitres sera arrêté après lecture complète du tapuscrit et consigné au § 5.

### 3.2 Normalisation des titres de chapitres
- Les intitulés tapés du tapuscrit sont conservés dans le corps du texte (sous-titres `\section*{...}`) et normalisés dans la commande `\chapter{...}`.
- Structure générale : `\chapter{Titre de la section (Année--Année)}` ; quand la période n'est pas connue avec certitude, la faire suivre d'un point d'interrogation (ex. `(1886--1890?)`) jusqu'à validation.

### 3.3 En-tête récurrent du tapuscrit → ignoré
- Chaque page du tapuscrit porte l'en-tête tapé « Souvenirs de Jeunesse de Felix BERLOTY (15/8/1886 - 16/12/1951) » suivi d'un filet. Cet en-tête, répété mécaniquement, n'est **pas transcrit** : il est représenté par les en-têtes LaTeX (`\fancyhead`).

### 3.4 Mentions et annotations manuscrites
- Les corrections manuscrites (mots barrés, ajouts interlinéaires ou marginaux) sont intégrées au texte final lorsqu'elles sont clairement lisibles ; **règle absolue** : la transcription reflète le texte final tel que corrigé par la main de l'auteur.
- Une correction manuscrite incertaine est signalée par une note de bas de page décrivant la lecture retenue et l'alternative.

### 3.5 Notes de bas de page (`\footnote`)
- Toutes les notes tapées de l'auteur sont scrupuleusement préservées via `\footnote{...}`.
- Les notes ajoutées par le transcripteur (lecture incertaine, clarification, référence) doivent porter la mention explicite `(Note du transcripteur)`.

### 3.6 Fidélité au texte et corrections
- Transcription réalisée par **agy** avec le modèle **Gemini 3.1 Pro** (`gemini-3.1-pro-high`), en lecture visuelle directe des scans à haute résolution ; pas d'OCR parallèle ni de double lecture.
- **Corrections systématiques des erreurs mécaniques** de la machine à écrire :
  - lettre `I` majuscule tapée à la place du chiffre `1` dans les nombres et dates : `I886` → `1886`, `I920` → `1920`, `IO` → `10` ;
  - espacements mécaniques anormaux : `dit ,bien` → `dit, bien`, `naissance,par` → `naissance, par` ;
  - césures de fin de ligne réunies : `Bonaven-ture` → `Bonaventure`.
- **Corrections des erreurs de syntaxe et d'orthographe manifestes** : accords grammaticaux évidents (`mariée` → `mariés`), accents manquants évidents (`Aout` → `Août`), fautes banales (`plustôt` → `plutôt`, `prénons` → `prénoms`).
- **Conservation stricte** : vocabulaire et tournures d'époque, abréviations (`St`, `Ste`, `5me`, `23 hrs 30`), guillemets et graphies d'époque.
- Les mots coupés en fin de ligne sont réunis lorsque la lecture est certaine ; en cas de doute, note du transcripteur.
- Les passages illisibles sont signalés `[ILLISIBLE: hypothèse]` avec note de bas de page si un contexte aide à la lecture.
- Les citations latines ou étrangères reçoivent une note de bas de page avec source et traduction, mention `(Note du transcripteur)`.

### 3.7 Casse des noms propres
- Dans le tapuscrit d'origine, les noms propres de personnes apparaissent en capitales d'imprimerie intégrales (ex. `DEMOUSTIER`, `POULAT`, `BOFFARD`, `BERLOTY`).
- **Règle de normalisation :** tous les noms propres de personnes, de lieux ou d'institutions sont uniformisés en bas de casse avec initiale majuscule (Title Case) : `Demoustier`, `Poulat`, `Boffard`, `Berloty`, `Brunet-Lecomte`, `Neyrat`. Seuls les chiffres romains (ex. `Louis XI`) et les sigles d'époque (ex. `OTL`) conservent des majuscules multiples.
- Les prénoms et noms au fil du texte suivent la casse du tapuscrit (ex. `Felix` sans accent sur la majuscule, conformément au texte tapé).

---

## 4. Règles Typographiques et Orthotypographiques

### 4.1 Dialogues et incises
- Les répliques de dialogue sont introduites par un tiret demi-cadratin (`--`) si l'original le fait ; les incises suivent la ponctuation de l'original.

### 4.2 Intervalles de dates et nombres
- Utiliser le double tiret pour les plages temporelles : `(1900--1920)`, `(1886--1914)`.

### 4.3 Abréviations et exposants
- Conserver les abréviations du tapuscrit : `5me`, `St Paul`, `Ste Vierge`, `23 hrs 30`.
- Les nombres et dates sont normalisés : le `I` majuscule tapé à la place du chiffre `1` est corrigé (`I886` → `1886`, `I87I` → `1871`).

### 4.4 Ligatures et caractères spéciaux
- Utiliser les ligatures françaises : `cœur`, `sœur`, `œuvre`, `vœu` (quand le tapuscrit les porte).
- Conserver les majuscules accentuées (`À`, `É`, `È`) selon le tapuscrit.
- Les termes latins ou en langue étrangère sont mis en italique.

---

## 5. État d'avancement de la transcription

Découpage provisoire (à affiner à la lecture) : chaque grande section numérotée du tapuscrit devient un chapitre.

| Vue | Fichier source | Contenu | Statut |
| :---: | :---: | :--- | :---: |
| Couverture | `Originaux/Couverture.jpg` | Page de couverture (titre, dates) | Non transcrite (titre normalisé en page de titre) |
| p. 1 | `Originaux/Page 01.jpg` | I) Naissance et Enfance | Transcrite |
| p. 2–11 | `Originaux/Page 02.jpg` … `Page 11.jpg` | Suite de « Naissance et Enfance » (résidences, Favorite, guerre de 1870, enfance) | Transcrites — **ordre logique : 03 avant 02** (inversion matérielle du carnet à spirale, raccords vérifiés) |
| p. 12–21 | `Originaux/Page 12.jpg` … `Page 21.jpg` | Assassinat de Sadi Carnot (1894), marins russes, Première Scolarité, Mongré, Externat rue de Sèze, équitation, prix et vie matérielle | Transcrites — ordre séquentiel, raccords continus |
| p. 22–31 | `Originaux/Page 22.jpg` … `Page 31.jpg` | Travaux place de la Bourse, tramways électriques, Tamaris, réceptions, premiers films Lumière, l'automobile (1898), voyage en Bavière et Autriche (Oberammergau 1900) | Transcrites — ordre séquentiel, raccords continus |
| p. 32–41 | `Originaux/Page 32.jpg` … `Page 41.jpg` | Retour rue Ste Hélène (1900), loi de 1901, cession de l'étude, achat des Massues, sports (cheval, escrime, patinage), changement de siècle, voyage à Oran et Tlemcen (1902) | Transcrites — ordre séquentiel, raccords continus |
| p. 42–51 | `Originaux/Page 42.jpg` … `Page 51.jpg` | Installation aux Massues, voisins, l'Audibert-Lavirotte (1901), permis à 15 ans (07/08/1902), Berliet torpédo, bac à Aix (1903), croisière en Écosse (1904), études supérieures, maladie du Père | Transcrites — **ordre logique : 50 → 49 → 48 entre 47 et 51** (inversion matérielle du carnet, raccords vérifiés) |
| p. 52–61 | `Originaux/Page 52.jpg` … `Page 61.jpg` | Service militaire (23 R.I. Bourg, 1905), mort du Père (15/10/1905), peloton des dispensés, pleurésie et convalescence, manœuvres de Langres, fort de Joux, libération (Pilain 24X35), généraux Pau et Langle de Carry, reprise des études et escrime | Transcrites — ordre séquentiel, raccords continus |
| p. 62–72 | `Originaux/Page 62.jpg` … `Page 72.jpg` | Fin des études (licence ès sciences, droit), mariage d'Elisabeth (1910), voyages (Dolomites, Belgique-Hollande, Lot), périodes militaires (Belfort), rencontre des Roque, mariage avec Lucy Roque (25/11/1913), voyage de noces (Monténégro, Corfou) jusqu'au 1er janvier 1914 | Transcrites — ordre séquentiel, raccords continus ; **fin du tapuscrit** |

**La transcription intégrale est terminée** : couverture non transcrite (titre normalisé en page de titre), 72/72 pages transcrites et reliées par des raccords vérifiés mot à mot.
