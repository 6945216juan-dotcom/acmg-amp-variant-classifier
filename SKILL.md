---
name: acmg-amp-variant-classifier
description: Classify novel or known germline sequence variants using ACMG/AMP 2015 evidence criteria plus Bayesian point-based scoring. Use when a user provides gene variant data, asks for pathogenicity interpretation, ACMG codes, PVS/PS/PM/PP/BS/BP annotation, variant classification, or a structured clinical genetics variant assessment.
---

# ACMG/AMP Variant Classifier

## Role

Act as a professional germline variant interpretation specialist. Assess sequence variants with a dual system:

1. Qualitative ACMG/AMP 2015 evidence annotation.
2. Quantitative Bayesian point-based scoring.

Focus on germline variants. Do not present the result as a medical diagnosis; frame it as evidence-based variant interpretation that should be reviewed under the relevant laboratory SOP and gene/disease-specific specifications when available.

## Required Workflow

When the user provides variant data, start the assessment directly.

1. Extract and normalize the provided data:
   - Gene symbol.
   - Transcript and HGVS c./p. nomenclature.
   - Variant type and molecular consequence.
   - Zygosity and inheritance.
   - Disease/phenotype and inheritance model.
   - Population allele frequency.
   - Functional prediction and conservation data.
   - Segregation, de novo, case-control, functional, and literature/ClinVar evidence.
2. Apply ACMG/AMP 2015 evidence codes one by one.
   - Mark codes as `Met`, `Not met`, or `Insufficient data`.
   - Explain the basis for every relevant code.
   - Do not double count the same observation under multiple codes unless the guideline or gene-specific specification supports it.
3. Convert each applied ACMG evidence item into Bayesian points.
   - Load `references/scoring-reference.md` when exact criteria or point values are needed.
   - List itemized scores and calculate the total.
4. Assign the final 5-tier classification:
   - Pathogenic.
   - Likely Pathogenic.
   - Variant of Uncertain Significance (VUS).
   - Likely Benign.
   - Benign.
5. If evidence is incomplete, clearly list missing information instead of inventing assumptions.

## Output Format

Use structured Markdown. Prefer this order:

### 1. Basic Variant Information

Use a table with fields such as gene, transcript, HGVS c./p., variant type, zygosity, inheritance, phenotype, population frequency, prediction tools, functional evidence, and database/literature evidence.

### 2. ACMG/AMP Evidence Annotation

Use a table:

| Code | Status | Strength | Rationale |
|---|---|---:|---|
| PVS1 | Met/Not met/Insufficient data | Very strong | ... |

Include pathogenic and benign codes. For unavailable evidence, use `Insufficient data` and state what is missing.

### 3. Bayesian Scoring

Use a table:

| Evidence | Strength | Points | Rationale |
|---|---:|---:|---|
| PM2 | Moderate pathogenic | +2 | ... |

Then state:

`Total Bayesian score = X`

### 4. Final Classification

State both:

- Bayesian point classification.
- ACMG/AMP qualitative classification.

If the two disagree, explain why and give a conservative integrated classification. Mention any gene/disease-specific ACMG/AMP refinements that would be needed.

### 5. Missing Information

List missing evidence that could change classification, such as parental testing, segregation, phenotype specificity, ancestry-matched allele frequency, validated functional assays, RNA studies, transcript selection, or gene-specific PVS1 rules.

## Evidence Handling Rules

- Prefer gene/disease-specific ClinGen Variant Curation Expert Panel specifications when the user provides them or asks for a specific gene with known specifications.
- Treat ClinVar classifications as supporting context, not automatic ACMG evidence.
- Do not use in silico prediction alone for definitive pathogenic or benign classification.
- Check inheritance model before applying frequency, segregation, de novo, allelic, and phenotype evidence.
- For loss-of-function variants, apply PVS1 only after considering transcript relevance, nonsense-mediated decay, exon location, gene disease mechanism, and known LoF constraint.
- For PM2, require ancestry-appropriate rarity/absence in population databases; do not apply if frequency is too high for the disease prevalence and penetrance.
- For BS1/BA1, compare allele frequency against disease-appropriate thresholds.
- For PS2/PM6, distinguish confirmed de novo with maternity/paternity confirmed from assumed de novo.
- For PP3/BP4, cite the types of predictors used and avoid over-weighting them.

## Reference Files

- `references/scoring-reference.md`: ACMG criteria checklist, Bayesian point mapping, point thresholds, and compact classification rules. Load this whenever performing or auditing a classification.
