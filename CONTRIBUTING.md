# Contributing to Open Data Mauritania

Thank you for helping build open NLP resources for Mauritania's national languages!

## Ways to contribute

### 1. Add or correct data
- Fork the repository and create a branch: `git checkout -b add/pulaar-healthcare-sentences`
- Edit or add JSON files following the existing schema
- Open a Pull Request with a clear description

### 2. Report issues
- Use GitHub Issues to report errors, duplicates, or encoding problems
- Label: `data-error`, `duplicate`, `encoding`

### 3. Propose a new dataset
- Open an Issue with label `new-dataset`
- Describe the language, domain, size, and collection method

## Data quality standards
- UTF-8 encoding required for all text files
- JSON must be valid and pass `python -m json.tool file.json`
- No personally identifiable information (PII)
- Indicate the source of each data contribution
- For field-collected data, include a collection protocol description

## Schema conventions
Keep schemas consistent within each language folder.  
Add a `DATA_CARD.md` entry for any new dataset you contribute.

## Code of Conduct
Be respectful of all contributors and language communities.
This is a community project — kindness is required.
