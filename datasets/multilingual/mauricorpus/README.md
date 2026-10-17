# MauriCorpus

**Parallel text between Arabic and the African languages of Mauritania: Hassaniya, Pulaar, Soninke and Wolof.**

Mauritania is one of the few countries where Arabic and Sub-Saharan African languages are spoken side by side in the same communities, yet public multilingual resources (OPUS, CCAligned, mC4) contain essentially no sentence pairs linking Arabic to Pulaar, Soninke or Wolof. Soninke is not covered by any major multilingual model (NLLB-200, MADLAD-400, Serengeti, Glot500).

MauriCorpus is a first step towards closing that gap. It contains four Arabic-centred parallel sets of 2,000 pairs each, 8,000 pairs in total.

Presented at **Deep Learning Indaba 2026** (poster IX-40). Published as part of [Open Data Mauritania](../../../README.md), initiated by MWiML (Mauritanian Women in Machine Learning).

## Languages

| Language | ISO 639-3 | Family | Script in this corpus |
|---|---|---|---|
| Arabic (Modern Standard) | `arb` | Afro-Asiatic, Semitic | Arabic |
| Hassaniya | `mey` | Afro-Asiatic, Semitic (Maghrebi Arabic) | Arabic |
| Pulaar | `fuc` | Niger-Congo, Atlantic | Latin |
| Soninke | `snk` | Niger-Congo, Mande | Latin |
| Wolof | `wol` | Niger-Congo, Atlantic | Latin |

## Datasets

All files are in this folder. Each is a UTF-8 JSON array of objects, one object per pair.

| File | Pairs | Languages | Content |
|---|---:|---|---|
| [`arabic_hassaniya.json`](arabic_hassaniya.json) | 2,000 | Arabic, Hassaniya (+ French, English) | Everyday conversational sentences |
| [`arabic_pulaar.json`](arabic_pulaar.json) | 2,000 | Arabic, Pulaar | Cultural and general-interest articles |
| [`arabic_wolof.json`](arabic_wolof.json) | 2,000 | Arabic, Wolof | Same Arabic sentences as the Pulaar set |
| [`arabic_soninke.json`](arabic_soninke.json) | 2,000 | Arabic, Soninke (+ French) | Vocabulary, example sentences and short texts |
| **Total** | **8,000** | | |

### How each dataset was produced

The four sets do not have the same quality. Please read this section before you train or evaluate on them.

| File | Arabic side | Other side | Human-checked? |
|---|---|---|---|
| `arabic_hassaniya.json` | Human-written | **Human translation** | Yes |
| `arabic_pulaar.json` | Human-written | **Machine translation** (Google Cloud Translation, generic Fula `ff`) | No |
| `arabic_wolof.json` | Human-written | **Machine translation** (NLLB-200-distilled-600M, `wol_Latn`) | No |
| `arabic_soninke.json` | **Machine translation** from French (Google Cloud Translation) | Human-written | Soninke and French only |

What this means in practice:

- `arabic_hassaniya.json` is the only set with human text on both sides.
- In `arabic_pulaar.json` and `arabic_wolof.json` the Pulaar and Wolof are machine output. Google Translate only offers a generic Fula code, so the Pulaar side is closer to general Fula than to Mauritanian Pulaar. Treat these two sets as silver data. They are fine for augmentation or pre-training but should not be used as gold test references.
- In `arabic_soninke.json` the Soninke and French come from published sources and the Arabic was machine-translated from the French. About 60% of the entries are single words (`"level": "word"`).
- The Wolof set was produced with NLLB-200. A model fine-tuned from NLLB-200 and tested on it will score higher than it would on human references.
- The sets are kept exactly as used in the baseline experiments. As a result they contain a few duplicate pairs (1 in Hassaniya, 27 in Soninke). Remove them if your use needs unique pairs.

## File formats

### `arabic_hassaniya.json`

```json
{
  "id": 1,
  "arabic": "يمكنني أن آخذها.",
  "hassaniya": "أنگد نگبظها.",
  "french": "Je peux le prendre.",
  "english": "I can take it."
}
```

`french` and `english` are reference translations of the same sentence, taken from the source dataset.

### `arabic_pulaar.json` and `arabic_wolof.json`

The two files share the same 2,000 Arabic sentences in the same order. The `id` values match, so the two sets can be joined into Arabic–Pulaar–Wolof triples.

```json
{
  "id": 1,
  "arabic": "افتتحت رابطة أدباء آدرار ليل السبت موسمها الثقافي ...",
  "pulaar": "Fedde winndooɓe Adrar udditi jamma aset ...",
  "category": "History",
  "source_url": "https://www.culture.gov.mr/index.php/ar/node/112"
}
```

| Field | Description |
|---|---|
| `category` | Topic of the source article: History (909), General (360), Education (262), Environment (167), Health & Wellness (100), Art & Culture (78), and others |
| `source_url` | The article the Arabic sentence came from (Mauritanian Ministry of Culture website). `null` for 93 sentences whose source could not be matched |

### `arabic_soninke.json`

```json
{
  "id": 1,
  "level": "sentence",
  "arabic": "أنا، سوكونا تونكارا، المقيم حاليًا في بالي، سأروي هذه القصة لأبنائي وأحفادي.",
  "soninke": "In ke Soxona Tunkara, in wo taaxunu Balle.",
  "french": "Moi, Sokona Tounkara, actuellement installé à Ballé, vais narrer ce conte pour mes enfants et mes petits-enfants.",
  "category": null,
  "source": "https://www.calameo.com/books/0009039477a9d2d6c6af5"
}
```

| Field | Description |
|---|---|
| `level` | `word` (1,210), `sentence` (780) or `text` (10) |
| `category` | Thematic category for vocabulary items, in French (Animaux, Santé, Verbes, Famille, …). `null` if none |
| `source` | Where the Soninke–French entry was published (see below) |

| Source of the Soninke–French entries | Pairs |
|---|---:|
| *Parlons soninké*, Christian Girier, L'Harmattan, 1996 | 988 |
| *Lexique Soninké (Mali)–Français–Anglais*, SIL | 384 |
| Calaméo publication `0009039477a9d2d6c6af5` | 241 |
| Soninkara.org: *Histoire des forgerons de Barâgo*, Doudou Sakho | 70 |
| *SOONINKARA* magazine, A.P.S., no. 1, 1988 | 29 |
| *Dangamaanu* folk tales, SIL Mali | 10 |
| Unattributed | 278 |

## Loading the data

With plain Python:

```python
import json

with open("datasets/multilingual/mauricorpus/arabic_hassaniya.json", encoding="utf-8") as f:
    pairs = json.load(f)

print(len(pairs), pairs[0]["arabic"], "→", pairs[0]["hassaniya"])
```

With 🤗 Datasets:

```python
from datasets import load_dataset

ds = load_dataset("json", data_files="datasets/multilingual/mauricorpus/arabic_soninke.json", split="train")
sentences = ds.filter(lambda r: r["level"] != "word")
```

## Baseline results

We fine-tuned **NLLB-200-distilled-600M** on the four sets and trained all eight directions jointly. NLLB-200 has no tokens for Soninke or Hassaniya, so we added two new language tokens:

- `snk_Latn` (Soninke), with its embedding initialised from Bambara (`bam_Latn`), a related Mande language,
- `mey_Arab` (Hassaniya), with its embedding initialised from Arabic (`arb_Arab`).

The model was trained for 10 epochs.

| Direction | n | BLEU | chrF++ |
|---|---:|---:|---:|
| Arabic → Pulaar | 400 | 17.9 | 42.9 |
| Pulaar → Arabic | 400 | 7.2 | 32.0 |
| Arabic → Hassaniya | 398 | 5.4 | 30.5 |
| Hassaniya → Arabic | 398 | 12.8 | 35.3 |
| Arabic → Wolof | 400 | 14.2 | 28.8 |
| Wolof → Arabic | 400 | 4.4 | 22.2 |
| Arabic → Soninke | 403 | 0.6 | 10.1 |
| Soninke → Arabic | 403 | 0.7 | 10.1 |

For comparison, MADLAD-400-3B used zero-shot does not support Hassaniya or Soninke, and scores close to zero BLEU on Pulaar and Wolof.

The test references for Pulaar and Wolof, and the Arabic references for Soninke, are machine-generated (see [How each dataset was produced](#how-each-dataset-was-produced)). These scores therefore show how well the model reproduces those references, not how good its translations are in absolute terms. Arabic has rich morphology, which lowers BLEU for translations into Arabic, so chrF++ is the more informative metric for those directions.

## Limitations

- Only the Hassaniya set has human text on both sides. The other three sets are partly machine-generated.
- The Hassaniya set is conversational (travel and everyday situations). The Pulaar and Wolof sets lean towards history and culture articles. The Soninke set is mostly vocabulary. None of the sets is a balanced sample of its language.
- Pulaar, Soninke and Wolof are written in Latin script here. Arabic-script (Ajami) writing is not yet covered.
- Spelling of the African languages varies across sources and has not been standardised.

## License

Unlike most of Open Data Mauritania (CC BY 4.0), MauriCorpus has its own license. The MauriCorpus annotations, translations and alignments are released under [CC BY-NC-SA 4.0](https://creativecommons.org/licenses/by-nc-sa/4.0/) (see [`LICENSE`](LICENSE)). You may use and share them for non-commercial purposes, with attribution, under the same license. For commercial use, contact the authors.

Some source text belongs to third parties and remains under its original terms: *Parlons soninké* (Christian Girier, L'Harmattan, 1996), SIL Mali (Soninke lexicon and folk tales), Soninkara.org, the *SOONINKARA* magazine of the A.P.S., and the Mauritanian Ministry of Culture website (culture.gov.mr). The Wolof side of `arabic_wolof.json` was generated with NLLB-200 (CC BY-NC 4.0).

## Citation

```bibtex
@misc{boughale2026mauricorpus,
  title        = {MauriCorpus: Bridging the Gap Between Arabic and Mauritanian African Languages},
  author       = {Boughale, Rahma and Aw, Mamadou Abdoulaye and Maimouna, Oiga and Ba, Ahmed},
  year         = {2026},
  howpublished = {Poster, Deep Learning Indaba 2026},
  url          = {https://github.com/mwimlmauritania-byte/Open-Data-Mauritania/tree/main/datasets/multilingual/mauricorpus}
}
```

## Acknowledgements

This work is supported by the Mauritanian Machine Intelligence Hub (2MIH). Data collection was helped by native-speaker communities in Mauritania.

## Contact

Rahma Boughale: rahma.boughale@gmail.com
