# Souvenirs de jeunesse — Félix Berloty (1886–1951)

[![Validation LaTeX & Publication](https://github.com/grostim/FelixBerloty/actions/workflows/ci-release.yml/badge.svg)](https://github.com/grostim/FelixBerloty/actions/workflows/ci-release.yml)
[![Dernière version](https://img.shields.io/github/v/release/grostim/FelixBerloty?label=Version&color=blue)](https://github.com/grostim/FelixBerloty/releases/latest)

Projet de transcription intégrale, d'édition critique et de mise en page sous **LaTeX** du tapuscrit dactylographié <u>« Souvenirs de jeunesse »</u> de **Félix Berloty** (1886–1951), notaire à Lyon. Le document, rédigé vers 1940–1951 et conservé dans les archives familiales, couvre sa jeunesse lyonnaise (ca. 1886–1914) : naissance à Saint-Paul, famille de notaires, enfance et formation.

> **Projet jumeau** de [grostim/BenoitCoste](https://github.com/grostim/BenoitCoste) — mêmes principes éditoriaux, même pipeline de publication.

---

## 📥 Téléchargements (Dernière version à jour)

Les documents sont automatiquement compilés et mis à disposition dans les trois formats suivants à chaque mise à jour :

| Format | Description | Lien de téléchargement |
| :--- | :--- | :---: |
| 📕 **PDF** | Version paginée officielle (mise en page typographique LaTeX) | [**Télécharger le PDF**](https://github.com/grostim/FelixBerloty/releases/latest/download/Souvenirs_de_Jeunesse_de_Felix_Berloty.pdf) |
| 📱 **EPUB** | Version numérique adaptée aux liseuses, tablettes et smartphones | [**Télécharger l'EPUB**](https://github.com/grostim/FelixBerloty/releases/latest/download/Souvenirs_de_Jeunesse_de_Felix_Berloty.epub) |
| 📄 **Markdown** | Version texte structurée pour consultation et traitement textuel | [**Télécharger le Markdown**](https://github.com/grostim/FelixBerloty/releases/latest/download/Souvenirs_de_Jeunesse_de_Felix_Berloty.md) |

*(Vous pouvez également retrouver l'historique complet des versions sur la page des [Releases GitHub](https://github.com/grostim/FelixBerloty/releases)).*

---

## 📖 Présentation du tapuscrit

Félix Berloty (1886–1951), notaire à Lyon, fils d'Adrien Berloty et d'Anne-Marie Demoustier, retrace dans ce document dactylographié de 72 pages ses souvenirs de jeunesse :

- **Naissance et famille (1886–1890?)** : naissance à Lyon 5ᵉ (Montée des Carmes Déchaussés), une famille de notaires lyonnais, le grand-père Félix Berloty premier notaire du nom (1840–1871).
- **Enfance lyonnaise** : le quartier Saint-Paul, les traditions familiales, la parenté (Boffard, Madinier, Demoustier).
- **Formation et jeunesse (années 1900)** : études, vie lyonnaise de la Belle Époque, jusqu'à la veille de la Grande Guerre environ.

Le tapuscrit est conservé dans les archives familiales ; les scans originaux (couverture + 72 pages) sont archivés dans [`Originaux/`](./Originaux/).

---

## 📊 État d'avancement de la transcription

- **Pages transcrites** : **61 / 72** (p. 1–51, puis p. 52–61).
- **Particularité de séquençage** : la numérotation des scans suit l'ordre matériel du carnet à spirale, pas l'ordre de lecture. Deux inversions vérifiées mot à mot : **03 avant 02** (p. 2–11) et **50 → 49 → 48 entre 47 et 51** (p. 42–51). Pages 52–61 : ordre séquentiel, raccords tous continus.
- **Statut** : 🚧 Transcription en cours.

Consultez le tableau détaillé dans [`CONVENTIONS_TRANSCRIPTION.md`](./CONVENTIONS_TRANSCRIPTION.md#5-état-davancement-de-la-transcription).

---

## 🗂 Structure du Dépôt

```
FelixBerloty/
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── config.yml               # Désactivation des issues vierges
│   │   └── erreur-transcription.yml # Template de signalement d'erreur
│   └── workflows/
│       └── ci-release.yml           # Pipeline CI/CD (compilation LaTeX, génération multi-format & release)
├── Originaux/                       # Scans du tapuscrit (Couverture + 72 pages)
│   ├── Couverture.jpg
│   ├── Page 01.jpg
│   ├── ...
│   └── Page 72.jpg
├── Illustrations/                    # Images éditoriales du livre
│   └── Portrait_Felix_Berloty.jpg    # Portrait utilisé sur la couverture
├── Souvenirs de Jeunesse de Felix Berloty.tex   # Source LaTeX principal du document
├── CONVENTIONS_TRANSCRIPTION.md     # Guide des conventions éditoriales et typographiques
├── README.md                        # Présentation du projet et liens de téléchargement
└── .gitignore                       # Exclusion des fichiers temporaires LaTeX
```

---

## 🛠 Conventions et Principes d'Édition

1. **Transcription par agy (Gemini 3.1 Pro)** : lecture visuelle directe des scans haute résolution ; erreurs mécaniques (I pour 1, espacements, césures) et erreurs de syntaxe manifestes corrigées ; vocabulaire, tournures et graphies d'époque conservés.
2. **Fidélité au texte et corrections manuscrites** : La transcription intègre le texte final en tenant compte de toutes les ratures et ajouts manuscrits portés sur le tapuscrit.
3. **Notes de bas de page** : Notes de l'auteur conservées via `\footnote{...}` ; notes du transcripteur explicitement marquées `(Note du transcripteur)`.
4. **Commits conventionnels en français** : Chaque transcription de page ou correction fait l'objet d'un commit unitaire (`feat: ...`, `fix: ...`, `docs: ...`).
5. **Gestion automatisée des releases** :
   - Ajout d'une nouvelle tranche de transcription $\rightarrow$ **Release majeure** (`v2.0.0`, etc.).
   - Correction de coquille ou ajustement de mise en page $\rightarrow$ **Release mineure** (`v1.1.0`, etc.).

Pour le détail complet des règles typographiques et éditoriales, consultez le fichier [`CONVENTIONS_TRANSCRIPTION.md`](./CONVENTIONS_TRANSCRIPTION.md).

---

## 🔗 Provenance documentaire

- Tapuscrit : document familial, « Souvenirs de Jeunesse de Félix BERLOTY », 72 pages dactylographiées (ca. 1940–1951), couvrant ca. 1886–1914.
- Référence dans l'arbre généalogique familial : [citation C1285](https://gramps.famillegros.com/citation/C1285) (source S1675, médias O0165–O0237).