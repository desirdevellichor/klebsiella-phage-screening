# Computational Identification of Phage Therapy Candidates Against Multidrug-Resistant *Klebsiella pneumoniae*

## Background

Antimicrobial resistance (AMR) is one of the major global health challenges of the 21st century. According to the Global Research on Antimicrobial Resistance (GRAM) Project, published in *The Lancet* in 2024, more than 39 million people could die as a result of AMR between 2025 and 2050. By 2050, AMR is projected to directly cause around 1.91 million deaths each year, which would represent a nearly 70% increase compared with 2022.

One of the pathogens of particular concern is *Klebsiella pneumoniae*, a Gram-negative bacterium that can cause serious hospital-acquired infections, including pneumonia, bloodstream infections, and urinary tract infections. The increasing occurrence of carbapenem-resistant *K. pneumoniae* is especially concerning because carbapenems are often used when other antibiotics are no longer effective.

Bacteriophage therapy, which uses viruses that specifically infect bacteria, has gained renewed interest as a possible alternative or complementary approach to antibiotics. Because phages target specific bacterial hosts, they may offer a more targeted approach than conventional antibiotics. In this project, I used publicly available genomic data and computational tools to identify and characterize prophage sequences present in a clinically relevant carbapenem-resistant *K. pneumoniae* strain. The aim was to explore whether any of the identified phages showed characteristics or host associations that could make them relevant for further phage therapy research.


---

## Objectives

1. Select a clinically relevant multidrug-resistant (MDR) *K. pneumoniae* strain
2. Characterize its antimicrobial resistance (AMR) profile computationally
3. Identify integrated prophage regions within the genome
4. Predict phage lifestyle (lytic vs. temperate) and host range
5. Evaluate the therapeutic potential of identified phage candidates

---

## Strain Used

| Property | Details |
|---|---|
| Organism | *Klebsiella pneumoniae* subsp. *pneumoniae* |
| Strain | HS11286 |
| Accession | GCF_000240185.1 / NC_016845.1 |
| Genome Size | ~5.33 Mb |
| GC Content | 57.48% |
| Source | Clinical isolate, multidrug-resistant |

---

## Workflow

```
Genome Acquisition (NCBI)
        ↓
AMR Characterization (ResFinder)
        ↓
Prophage Identification (PHASTEST)
        ↓
Phage Lifestyle & Host Prediction (PhaBOX)
        ↓
Results & Interpretation
```

---

## Tools Used

| Tool | Purpose |
|---|---|
| NCBI Datasets | Genome acquisition |
| ResFinder 4.7.2 | AMR gene identification |
| PHASTEST | Prophage identification and annotation |
| PhaBOX | Phage lifestyle and host prediction |

---

## Results

### 1. AMR Profile (ResFinder)

*K. pneumoniae* HS11286 showed resistance to multiple antibiotic classes through both acquired resistance genes and chromosomal mutations:

**Acquired Resistance Genes:**

| Gene | Phenotype | Identity |
|---|---|---|
| blaSHV-182 | Beta-lactam resistance | 99.88% |
| blaSHV-159 | Beta-lactam resistance | 99.88% |
| blaSHV-158 | Beta-lactam resistance | 99.88% |
| fosA6 | Fosfomycin resistance | 98.81% |

**Chromosomal Mutations:**

| Gene | Resistance | Notes |
|---|---|---|
| ompK36 | Cephalosporins, Carbapenems | Multiple frameshift mutations |
| ompK37 | Carbapenems | Multiple mutations |
| acrR | Fluoroquinolones | Efflux pump regulator |
| parC | Ciprofloxacin | p.S80I mutation |
| gyrA | Fluoroquinolones | Chromosomal mutation |

**Key Finding:** This strain is resistant to **carbapenems** — antibiotics of last resort — via mutations in outer membrane porin genes *ompK36* and *ompK37*, making conventional treatment extremely limited and phage therapy a highly relevant alternative.

---

### 2. Prophage Identification (PHASTEST)

PHASTEST identified **6 prophage regions** in the HS11286 chromosome:

| Region | Length | Completeness | Score | Position | Most Similar Phage |
|---|---|---|---|---|---|
| 1 | 13.5 Kb | Questionable | 75 | 581,768–595,336 | PHAGE_Entero_P4 |
| 2 | 50.4 Kb | **Intact** | 150 | 1,288,314–1,338,717 | PHAGE_Edward_GF_2 |
| 3 | 30.3 Kb | **Intact** | 150 | 1,778,297–1,808,597 | PHAGE_Klebsi_ST512_KPC3phi13.2 |
| 4 | 48.0 Kb | **Intact** | 150 | 2,277,469–2,325,549 | PHAGE_Salmon_SEN34 |
| 5 | 39.0 Kb | **Intact** | 150 | 4,046,142–4,085,218 | PHAGE_Klebsi_ST147_VIM1phi7.1 |
| 6 | 14.3 Kb | Questionable | 80 | 4,815,176–4,829,519 | PHAGE_Salmon_118970_sal3 |

**4 intact** prophage regions were identified. Notably, regions 3 and 5 match phages derived from carbapenem-resistant *Klebsiella* strains (KPC3 and VIM1 producers), directly linking these prophages to the AMR context of this study.

---

### 3. Phage Lifestyle & Host Prediction (PhaBOX)

PhaBOX was used to predict the lifestyle (lytic vs. temperate) and likely bacterial host of each prophage region:

| Phage | Length | Prediction | Confidence | Lifestyle | Predicted Host | Method |
|---|---|---|---|---|---|---|
| phage_1 | 13.6 Kb | Virus | High | Temperate | — | — |
| phage_2 | 50.4 Kb | Virus | High | Temperate | *Klebsiella aerogenes* | CRISPR-based |
| phage_3 | 30.3 Kb | Virus | High | Temperate | ***Klebsiella pneumoniae*** | AAI-based |
| phage_4 | 48.1 Kb | Virus | Medium | Temperate | *Raoultella ornithinolytica* | CRISPR-based |
| phage_5 | 39.1 Kb | Virus | High | Temperate | ***Klebsiella pneumoniae*** | AAI-based |
| phage_6 | 14.3 Kb | Virus | Medium | Temperate | *Salmonella enterica* | CRISPR-based |

**Key findings:**
- All 6 prophage regions were confirmed as viral sequences
- **Phage 3** (Genus: *Gegevirus*, Species: *Gegevirus ST437OXA245phi41*) — predicted host *K. pneumoniae*, phylogenetically linked to an OXA-carbapenemase-producing strain
- **Phage 5** (Genus: *Vimunumvirus*, Species: *Vimunumvirus ST147VIM1phi71*) — predicted host *K. pneumoniae*, phylogenetically linked to a VIM-1 metallo-beta-lactamase-producing strain

---

## Discussion

This study demonstrates a fully computational pipeline for identifying phage therapy candidates against a carbapenem-resistant *K. pneumoniae* clinical isolate. The AMR characterization confirmed that HS11286 carries resistance to last-resort antibiotics, underscoring the urgent need for alternative therapeutic strategies.

Prophage analysis revealed 6 integrated phage regions, of which phage_3 (Gegevirus) and phage_5 (Vimunumvirus) are of particular therapeutic interest due to their high-confidence association with *K. pneumoniae* as a host and their phylogenetic links to carbapenem-resistant strains. Although all identified prophages were predicted to be temperate (lysogenic) rather than strictly lytic, temperate phages can be genetically engineered to exhibit lytic behavior — a well-established approach in phage therapy research.

### Limitations

- Analysis is limited to one strain; future work should expand to multiple MDR *K. pneumoniae* clinical isolates
- All identified prophages are temperate; strictly lytic phages would be preferred for direct therapeutic use
- Safety screening for virulence and AMR genes within phage genomes (via PhageLeads) was attempted but the server was unavailable at the time of analysis — this remains an important future step
- Computational predictions require experimental validation (e.g., phage isolation, host range assays, in vitro killing assays)

---

## Repository Structure

```
├── README.md
├── data/
│   ├── klebsiella_HS11286_chromosome.fna       # Input genome (chromosome only)
│   └── klebsiella_HS11286_phage_regions.fna    # Extracted prophage sequences
├── prophage_analysis/
│   └── PHASTEST_summary.txt                    # PHASTEST output
├── amr_analysis/
│   └── ResFinder_results.txt                   # ResFinder output
├── phage_analysis/
│   └── PhaBOX_final_prediction_summary.tsv     # PhaBOX output
├── results/
│   └── summary_table.md                        # Compiled results
├── figures/
│   └── pipeline_overview.png                   # Workflow diagram
└── references.md                               # All tools and papers cited
```

---

## Tools & Resources

- [NCBI Datasets](https://www.ncbi.nlm.nih.gov/datasets/) — Genome acquisition
- [ResFinder 4.7.2](https://cge.food.dtu.dk/services/ResFinder/) — AMR gene identification
- [PHASTEST](https://phastest.ca) — Prophage identification and annotation
- [PhaBOX](https://phage.ee.cityu.edu.hk) — Phage lifestyle and host prediction
- [PhageLeads](https://www.phageleads.dk) — Phage safety screening (server unavailable at time of analysis)
- AMR mortality statistics: [GRAM Project, The Lancet, 2024](https://www.healthdata.org/news-events/newsroom/news-releases/lancet-more-39-million-deaths-antibiotic-resistant-infections-estimated)

---

*This project was conducted as part of a computational biology research portfolio. All analyses were performed using publicly available web-based tools and publicly available genome data from NCBI.*
