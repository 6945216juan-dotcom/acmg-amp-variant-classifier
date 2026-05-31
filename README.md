# ACMG/AMP Variant Classifier Skill

Codex skill for germline sequence variant interpretation using the ACMG/AMP 2015 framework together with a Bayesian point-based scoring model.

This skill is designed for structured pathogenicity assessment of novel or known germline variants. It annotates ACMG/AMP evidence codes, assigns Bayesian points, and reports a final 5-tier classification.

## What It Does

- Extracts and summarizes core variant information.
- Applies ACMG/AMP 2015 evidence codes: `PVS1`, `PS1-4`, `PM1-6`, `PP1-5`, `BA1`, `BS1-4`, and `BP1-7`.
- Calculates Bayesian point scores using standard evidence strength weights.
- Classifies variants as:
  - Pathogenic
  - Likely Pathogenic
  - Variant of Uncertain Significance (VUS)
  - Likely Benign
  - Benign
- Lists missing information when evidence is insufficient.

## Bayesian Point Model

| Evidence strength | Points |
|---|---:|
| Very strong pathogenic | +8 |
| Strong pathogenic | +4 |
| Moderate pathogenic | +2 |
| Supporting pathogenic | +1 |
| Supporting benign | -1 |
| Strong benign | -4 |
| Stand-alone benign | -8 |

| Total score | Classification |
|---:|---|
| >= 10 | Pathogenic |
| 6 to 9 | Likely Pathogenic |
| 0 to 5 | VUS |
| -1 to -6 | Likely Benign |
| <= -7 | Benign |

## Installation

Clone this repository into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/6945216juan-dotcom/acmg-amp-variant-classifier.git ~/.codex/skills/acmg-amp-variant-classifier
```

Restart Codex or start a new session so the skill can be discovered.

## Example Prompt

```text
Use the ACMG/AMP variant classifier skill to assess this variant:

Gene: LDLR
Variant: NM_000527.5:c.681C>A, p.Cys227Ter
Zygosity: heterozygous
Phenotype: familial hypercholesterolemia
Population frequency: absent from gnomAD
Inheritance: autosomal dominant
Functional evidence: none
Segregation: affected parent carries the variant
```

## Expected Output

The skill produces structured Markdown with:

1. Basic variant information.
2. ACMG/AMP evidence annotation table.
3. Bayesian scoring table and total score.
4. Final integrated classification.
5. Missing evidence that could change the classification.

## Important Notes

- This skill is intended for evidence-based variant interpretation, not direct medical diagnosis.
- Gene-specific ClinGen Variant Curation Expert Panel specifications should be preferred when available.
- ClinVar entries should be treated as supporting context, not automatic evidence.
- Incomplete data should be reported explicitly rather than filled with assumptions.
