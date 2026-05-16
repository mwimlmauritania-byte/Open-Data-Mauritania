# 🇲🇷 Open Data Mauritania — NLP Hub

> **Initiated by [MWiML — Mauritanian Women in Machine Learning](https://www.mwiml.com)**  
> Open, community-driven NLP resources for Mauritania's national languages.

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![Contributions Welcome](https://img.shields.io/badge/contributions-welcome-brightgreen.svg)](CONTRIBUTING.md)
[![Languages](https://img.shields.io/badge/languages-Pulaar%20%7C%20Soninke%20%7C%20Hassaniya%20%7C%20Wolof-blue)](.)

---

## 🌍 Why This Project Exists

Most AI systems today perform well only in high-resource languages like English, French,
or Modern Standard Arabic. **Mauritania's national languages — Pulaar, Soninke, Wolof,
and Hassaniya Arabic — are severely underrepresented.**

This means healthcare AI, automated public services, and language tools simply don't work
for most Mauritanians. This repository is our open answer: a community hub for collecting,
cleaning, and publishing NLP datasets so that anyone can build tools that serve every citizen.

---

## 📦 Datasets in This Repository

### Pulaar / Fulfulde

| File | Description | Size |
|---|---|---|
| `datasets/pulaar/pulaar_mauritania_sentences.json` | Sentences about Mauritanian geography, institutions, culture | 81 sentences |
| `datasets/pulaar/pulaar_french_parallel_corpus.json` | Pulaar ↔ French parallel translation pairs | 991 pairs |
| `datasets/pulaar/pulaar_arabic_parallel_corpus_raw.json` | Pulaar ↔ Arabic parallel corpus (needs cleaning) | ~350 pairs |

**Schema** (`pulaar_mauritania_sentences.json`):
```json
{ "sentence": "Moritani ina jeyaa e leyɗe ɓurɗe alɗude..." }
```

**Schema** (`pulaar_french_parallel_corpus.json`):
```json
{ "Original": "...", "Translated": "..." }
```

---

### Soninke

| File | Description | Size |
|---|---|---|
| `datasets/soninke/soninke_french_dictionary.json` | Soninke ↔ French bilingual dictionary | 708 entries |
| `datasets/soninke/soninke_field_collection_session_1.pdf` | Field transcription sheets — session 1 | PDF |
| `datasets/soninke/soninke_field_collection_session_2.pdf` | Field transcription sheets — session 2 | PDF |

**Schema** (`soninke_french_dictionary.json`):
```json
{ "sonike": "...", "farancais": "..." }
```

---

### Hassaniya Arabic

| File | Description | Size |
|---|---|---|
| `datasets/hassaniya/hassaniya_stories_collection.json` | Articles and stories in Hassaniya Arabic | 100 entries |

**Schema**:
```json
{
  "title": "...",
  "url": "...",
  "category": "...",
  "original_language": "hassaniya",
  "context": "...",
  "sentence": "..."
}
```

---

### Multilingual

| File | Description | Size |
|---|---|---|
| `datasets/multilingual/arabic_hassaniya_pulaar_trilingual.json` | 3-way aligned: Modern Arabic / Hassaniya / Pulaar | 100 entries |

**Schema**:
```json
{ "arabic": "...", "hassanya": "...", "pulaar": "..." }
```

---

## 🔗 External Sources & Related Projects

### 📚 Datasets & Research

| Source | Language | Type | Link |
|---|---|---|---|
| **HASSANIYA Dataset** — El Arby, Med El Moustapha (2025) | Hassaniya Arabic | Annotated NLP dataset | [Mendeley Data — doi:10.17632/m2swkr2bhx.1](https://data.mendeley.com/datasets/m2swkr2bhx/1) |
| **GeoPoll Real Human Data** | Hassaniya, Pulaar | LLM fine-tuning data | [geopoll.com](https://www.geopoll.com/real-human-data-from-mauritania-to-finetune-your-llm-models/) |
| **Mauritanian Arabic Grammar Handbook** (Peace Corps) | Hassaniya Arabic | Grammar / Language reference | [SciSpace PDF](https://scispace.com/pdf/mauritanian-arabic-grammar-handbook-peace-corps-language-1exwifb43q.pdf) |
| **Peace Corps Pulaar Manuel** (2015) | Pulaar | Language learning / reference | [peace-corps-pulaar-manuel-2015.pdf](docs/references/peace-corps-pulaar-manuel-2015.pdf) |
| **RIM-AI** | Mauritanian Arabic | AI research initiative | [rim-ai.com](https://www.rim-ai.com/en) |

### 🤝 Community Projects

| Project | Language | Description | Link |
|---|---|---|---|
| **Hassan-IA / حسّانية** | Hassaniya Arabic | Community documenting the Hassaniya dialect — dialect resources, transcriptions, NLP tools | [GitHub](https://github.com/Hassan-IA) |
| **Galsen AI** | Wolof, Pulaar, Soninke | Senegalese open AI datasets and models | [galsenai.com](https://galsenai.com) |
| **Hassaniya AI** | Hassaniya Arabic | NLP datasets for Hassaniya Arabic dialect | [GitHub](https://github.com/HassaniyaAI) |
| **PularAI** | Pulaar / Fulfulde | AI resources for the Pulaar language family | [GitHub](https://github.com/PularAI) |
| **Masakhane** | 50+ African languages | Pan-African NLP community and research | [masakhane.io](https://www.masakhane.io) |

### 📖 Soninke Language Resources

The Soninke language has a small but growing set of online resources:

| Resource | Description | Link |
|---|---|---|
| **Soninkara** | Community platform with Soninke language content | [soninkara.com](https://www.soninkara.com) |
| **Sooninke** | Soninke language learning and vocabulary | [sooninke.com](https://www.sooninke.com) |
| **Asawan.org — Section Soninké** | Soninke section of the Asawan cultural platform | [asawan.org](https://www.asawan.org) |
| **Gallica — Recherche Soninké** | BnF digital library — historical Soninke texts | [gallica.bnf.fr](https://gallica.bnf.fr/Search?adva=1&adv=1&lang=fr&q=sonink%C3%A9) |

### 🏛️ Official Data Sources

| Source | Description | Link |
|---|---|---|
| **Open Data Mauritania** | Government open data portal | [data.gov.mr](https://data.gov.mr) |
| **IMROP** | Mauritanian fisheries & ocean research | [imrop.mr](https://www.imrop.mr) |
| **ONISPA** | Agricultural and livestock statistics | [onispa.mr](https://www.onispa.mr) |

---

## 🚀 Quick Start

```bash
git clone https://github.com/YOUR_ORG/Open-Data-Mauritania.git
cd Open-Data-Mauritania
```

```python
import json

# Soninke dictionary
with open("datasets/soninke/soninke_french_dictionary.json", encoding="utf-8") as f:
    snk = json.load(f)
print(f"{len(snk)} entries | sample: {snk[0]}")

# Hassaniya stories
with open("datasets/hassaniya/hassaniya_stories_collection.json", encoding="utf-8") as f:
    stories = json.load(f)
print(f"{len(stories)} stories | fields: {list(stories[0].keys())}")

# Pulaar–French parallel corpus
with open("datasets/pulaar/pulaar_french_parallel_corpus.json", encoding="utf-8") as f:
    corpus = json.load(f)
print(f"{len(corpus)} pairs | sample: {corpus[0]}")

# Trilingual
with open("datasets/multilingual/arabic_hassaniya_pulaar_trilingual.json", encoding="utf-8") as f:
    tri = json.load(f)
print(f"{len(tri)} trilingual entries | sample: {tri[0]}")
```

---

## 📁 Repository Structure

```
Open-Data-Mauritania/
├── datasets/
│   ├── pulaar/
│   │   ├── pulaar_mauritania_sentences.json
│   │   ├── pulaar_french_parallel_corpus.json
│   │   └── pulaar_arabic_parallel_corpus_raw.json
│   ├── soninke/
│   │   ├── soninke_french_dictionary.json
│   │   ├── soninke_field_collection_session_1.pdf
│   │   └── soninke_field_collection_session_2.pdf
│   ├── hassaniya/
│   │   └── hassaniya_stories_collection.json
│   ├── wolof/
│   │   └── .gitkeep
│   └── multilingual/
│       └── arabic_hassaniya_pulaar_trilingual.json
├── notebooks/
│   ├── 01_data_exploration.ipynb
│   └── 02_baseline_tokenizer.ipynb
├── docs/
│   ├── DATA_CARD.md
│   └── references/
├── tools/
│   └── collection/
├── CONTRIBUTING.md
├── LICENSE
└── README.md
```

---

## 🤲 How to Contribute

### Native speakers
- Validate and correct existing transcriptions
- Add new sentences or vocabulary
- Tag data with domain labels: healthcare, education, government, agriculture

### Developers
- Write data cleaning and normalisation scripts
- Build baseline models (tokeniser, language ID, translation)
- Create data loaders for HuggingFace Datasets

### Researchers
- Benchmark models on existing datasets
- Write data cards following [Bender & Friedman (2018)](https://aclanthology.org/Q18-1041/)
- Propose annotation schemas

### Getting started
1. Read [CONTRIBUTING.md](CONTRIBUTING.md)
2. Browse open [Issues](../../issues) — look for `good first issue`
3. Fork → branch → PR

---

## 📜 License

All datasets produced by MWiML are released under **Creative Commons Attribution 4.0 (CC BY 4.0)**
unless otherwise noted. External datasets linked above retain their original licenses — please
check each source before use.

---

## 📬 Contact

**MWiML — Mauritanian Women in Machine Learning**  
🌐 [mwiml.com](https://www.mwiml.com) · 📍 Nouakchott, Mauritania  

*Built with 💚 by MWiML — because AI should work for every Mauritanian.*
