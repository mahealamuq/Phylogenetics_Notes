# Phylogenetics-Sequence-Homology-Evolutionary-Distance-and-Tree-Reconstruction

This repository contains study notes and example workflows for understanding phylogenetics in bioinformatics. It explains how biological sequences are compared, how evolutionary distances are calculated, how phylogenetic trees are represented, and how tree reconstruction methods such as distance-based methods, maximum parsimony, maximum likelihood, and Bayesian approaches are used.

The repository is designed for learning introductory bioinformatics, molecular evolution, and computational biology.

---
## Aim of This Repository

The aim of this repository is to explain the basic concepts and workflow of phylogenetic analysis step by step:

- Understand sequence homology, orthology, and paralogy
- Learn why multiple sequence alignment is important
- Understand phylogenetic tree terminology
- Learn how trees are represented using Newick format
- Calculate evolutionary distance between sequences
- Understand evolutionary models such as JC69, K80, HKY85, and GTR
- Learn bootstrap support and tree confidence
- Understand maximum parsimony and the Small Parsimony Problem

---

## 1. Introduction to Phylogenetics

Phylogenetics is the study of evolutionary relationships among organisms, genes, proteins, or other biological sequences.

A phylogenetic tree is a hypothesis about evolutionary history. It shows how sequences or species may have diverged from common ancestors.

Phylogenetic analysis usually starts with homologous sequences. These sequences are aligned, compared, and then used to reconstruct a tree.

---

## 2. Why Phylogenetics Is Important

Phylogenetics helps answer questions such as:

- How are species related?
- Did two genes come from a common ancestor?
- Did a gene duplicate before or after speciation?
- Which sequences are orthologs or paralogs?
- How much evolutionary change separates two sequences?
- What is the most likely evolutionary tree?

Phylogenetic trees are also useful data structures because they represent evolutionary change over time.

---

## 3. Homology, Orthology and Paralogy

**Homology**

Homology means that two biological features are derived from a common ancestor.

Examples:

- Two genes from different species may be homologous.
- Two proteins may be homologous.
- Two anatomical structures may be homologous.

Important point:

- Homology is all-or-nothing.
- Sequences are either homologous or not homologous.
- There are no degrees of homology.

However, we can talk about different levels of sequence similarity or confidence in homology.

**Orthology**

Orthologs are homologous genes that separated because of a speciation event.

Example:
Human gene A and mouse gene A may be orthologs if they came from the same ancestral gene during species divergence.

Orthologs are often used to infer species relationships

**Paralogy**

Paralogs are homologous genes that separated because of a gene duplication event.

Example:

Gene X duplicated into Gene X and Gene X'.
Both copies may later evolve different functions.

Paralogs can make phylogenetic interpretation difficult because a gene tree may not match the species tree.

---

## 4. Species Tree vs Gene Tree

**Species Tree**

A species tree represents the evolutionary relationship among species.

Example:

Human
Chicken
Frog
Fish
Fly
Shrimp

A species tree should ideally be built using strictly orthologous genes.

**Gene Tree**

A gene tree represents the evolutionary history of homologous genes.

Gene trees may include:

- Orthologs
- Paralogs
- Duplicated genes
- Lost genes

Because of gene duplication and gene loss, a gene tree may not always match the species tree.

---

## 5. Multiple Sequence Alignment

Multiple sequence alignment is often the input for phylogenetic analysis.

Before building a tree, sequences are aligned so that homologous positions are compared.

Example:

| Sequence | Nucleotides |
|----------|-------------|
| Seq1 | A T G C A A |
| Seq2 | A T G T A A |
| Seq3 | A C G C A A |

Aligned columns allow us to identify:

- Conserved positions
- Mutated positions
- Insertions and deletions
- Sequence similarity
- Evolutionary distance

---

## 6. Phylogenetic Tree Terminology

Important tree terms:

| Term | Meaning |
|------|---------|
| Root | Common ancestor of all taxa in a rooted tree |
| Leaf / Tip / Terminal node | Observed sequence or species |
| Internal node | Hypothetical ancestor |
| Branch / Edge | Evolutionary connection between nodes |
| Branch length | Amount of evolutionary change |
| Clade | Group containing an ancestor and all descendants |
| Bifurcating tree | Tree where each internal node has two descendants |
| Multifurcating tree | Tree where a node has more than two descendants |

---

## 7. Rooted vs Unrooted Trees

**Rooted Tree**

A rooted tree shows the direction of evolutionary time.

        Root
        /  \
       A    B

Rooted trees can suggest ancestor-descendant relationships.

**Unrooted Tree**

An unrooted tree shows relationships but does not show the direction of time.

```
A ----- B
 \     /
   C
```
Unrooted trees show similarity or relatedness, but not ancestry direction.

---

## 8. Types of Phylogenetic Trees

**Cladogram**

A cladogram shows relationships, but branch lengths are not proportional to evolutionary change.

**Additive Tree**

An additive tree includes branch lengths that represent evolutionary distance.

**Ultrametric Tree**

An ultrametric tree assumes a molecular clock, meaning all lineages evolve at a constant rate.

**Tree with Outgroup**

An outgroup is a more distantly related taxon used to root the tree.

---

## 9. Newick Format

Newick format is a standard text format for representing phylogenetic trees.

Example:

```
((raccoon,bear),((sea_lion,seal),((monkey,cat),weasel)),dog);
```

A simple tree:

(A,B);

A tree with three taxa:

((A,B),C);

A tree with branch lengths:

((A:0.1,B:0.2):0.3,C:0.4);

Branch lengths usually represent the number of substitutions per site.

---

## 10. Bootstrap Support

Bootstrap analysis estimates confidence in tree branches.

Basic idea:

- Resample alignment columns with replacement
- Build a tree for each resampled dataset
- Count how often each branch appears
- Report this percentage as bootstrap support

Example:

Bootstrap value = 85

This means that the branch appeared in 85% of bootstrap trees.

Low-support branches may be collapsed in a condensed tree.

---

## 11. Evolutionary Distance

Evolutionary distance measures how different two sequences are.

A distance matrix stores pairwise distances between sequences.

Example:

|      | Seq1 | Seq2 | Seq3 |
|------|------|------|------|
| Seq1 | 0.00 | 0.20 | 0.35 |
| Seq2 | 0.20 | 0.00 | 0.30 |
| Seq3 | 0.35 | 0.30 | 0.00 |

       

---

## 12. p-distance

The simplest evolutionary distance is p-distance.

p = D / L

Where:

D = number of different positions
L = total number of aligned positions

Example:

Seq1: A A A B B A
Seq2: A B A B A A

Differences = 2
Length = 6

p = 2 / 6 = 0.333

Limitation:

p-distance does not correct for multiple mutations at the same site.

---

## 13. Poisson Distance Correction

Poisson correction accounts for hidden mutations that happened more than once at the same site.

Formula:

d = -ln(1 - p)

Where:

p = observed p-distance
d = corrected evolutionary distance

This correction becomes more important when sequences are highly divergent.

---

## 14. Gamma Distance Correction

Gamma correction accounts for site-specific mutation rates.

Some sites evolve quickly, while others are highly conserved.

Formula:

dΓ = a[(1 - p)^(-1/a) - 1]

Where:

a = gamma shape parameter
p = observed p-distance

Small a values mean stronger rate variation among sites.

---

## 15. Molecular Clock

The molecular clock hypothesis suggests that mutations accumulate at an approximately constant rate over time.

This can be useful for estimating divergence time.

However, mutation rates can vary because of:

Generation time
Population size
Species-specific biology
Natural selection
Functional constraints
Different rates at different sites

---

## 16. Transition and Transversion

DNA substitutions can be classified into transitions and transversions.

Transition

A transition is a substitution within the same nucleotide group:

A ↔ G
C ↔ T
Transversion

A transversion is a substitution between purine and pyrimidine groups:

A or G ↔ C or T

Transitions often occur more frequently than transversions.

---

## 17. Codon Position and Mutation Rate

Different codon positions evolve at different rates.

Codon Position	Effect
1st position	Often non-synonymous
2nd position	Often non-synonymous
3rd position	Often synonymous

Third codon positions often evolve faster because mutations may not change the amino acid.

---

## 18. Evolutionary Models

Evolutionary models describe how sequences change over time.

They connect sequence alignment to tree reconstruction algorithms.

Models may consider:

Equal or unequal base frequencies
Different transition and transversion rates
Different codon position rates
Site-specific rate variation
DNA or protein substitution behaviour
Common DNA Evolutionary Models
Model	Base Composition	Transition/Transversion Difference	Notes
JC69	Equal	No	Simplest model
F81	Variable	No	Allows unequal base frequencies
K80	Equal	Yes	Different transition and transversion rates
HKY85	Variable	Yes	Common DNA model
TN93	Variable	Yes	More flexible
GTR	Variable	Yes	General time-reversible model

---

## 19. Jukes-Cantor Model

The Jukes-Cantor model assumes:

Equal base frequencies
Equal mutation rates between all nucleotides
Independent sites
Same rate across all sites

Rate matrix idea:

      A    C    G    T
A   -3α   α    α    α
C    α   -3α   α    α
G    α    α   -3α   α
T    α    α    α   -3α

Each row sums to zero because the total probability must remain constant.

---

## 20. Protein Evolution Models

Protein models estimate amino acid substitution rates.

Examples:

Dayhoff PAM
Whelan and Goldman model
JTT
LG
WAG

Protein models are useful because amino acids have different biochemical properties and do not substitute equally.

---

## 21. Tree Reconstruction Methods

### Common methods include:

**Distance-Based Methods**

These methods first calculate a distance matrix, then build a tree.

Examples:

- UPGMA
- Neighbor-Joining
- Character-Based Methods

These methods use aligned characters directly.

Examples:

- Maximum Parsimony
- Maximum Likelihood
- Bayesian inference

---
## 22. Maximum Parsimony

Maximum parsimony chooses the tree that requires the fewest evolutionary changes.

Basic idea:

Best tree = tree with minimum number of mutations

Parsimony is simple and intuitive but can be misleading when mutation rates vary greatly.

---

## 23. Small Parsimony Problem

The Small Parsimony Problem asks:

Given a fixed tree and labeled leaves, what labels should be assigned to internal nodes to minimize the total number of changes?

Input:

Tree T with leaves labeled by character strings

Output:

Internal node labels that minimize the parsimony score

---

## 24. Fitch Algorithm

The Fitch algorithm solves the unweighted Small Parsimony Problem.

Steps:

Assign each leaf a set containing its observed character
Move upward from leaves to root
For each internal node:
If child sets overlap, take the intersection
If child sets do not overlap, take the union and add one mutation
Move downward from root to assign actual labels

Example rule:

If Su ∩ Sw is not empty:
    Sv = Su ∩ Sw

Otherwise:
    Sv = Su ∪ Sw
    score = score + 1

---
    
## 25. Sankoff Algorithm

The Sankoff algorithm solves a weighted version of the Small Parsimony Problem.

It uses a scoring matrix where different substitutions can have different costs.

General recurrence:

s_t(v) = min_i [s_i(u) + δ_i,t] + min_j [s_j(w) + δ_j,t]

Where:

- v = internal node
- u and w = children of v
- δ = substitution cost matrix
- s_t(v) = minimum score if node v has character t

---

## 26. Large Parsimony Problem

The Large Parsimony Problem asks:

Which tree topology gives the minimum parsimony score?

This is much harder than Small Parsimony because the tree itself is unknown.

For many taxa, the number of possible trees becomes extremely large, so heuristic methods are often used.

Example heuristic:

Nearest Neighbor Interchange

---

## 27. Basic Phylogenetic Workflow

A simple phylogenetic workflow:

1. Collect homologous sequences
2. Perform multiple sequence alignment
3. Inspect and clean alignment
4. Choose an evolutionary model
5. Build phylogenetic tree
6. Estimate branch support using bootstrap
7. Visualize and interpret the tree
   
---  

## 28. Key Takeaways
    
- Phylogenetic trees are hypotheses, not absolute truth.
- Homologous sequences should be used for phylogenetic analysis.
- Orthologs are best for species tree reconstruction.
- Paralogs can mislead species tree interpretation.
- Multiple sequence alignment is usually required before tree building.
- p-distance is simple but does not correct for hidden mutations.
- Poisson and Gamma corrections estimate more realistic evolutionary distances.
- Evolutionary models improve tree reconstruction.
- Bootstrap support helps evaluate confidence in tree branches.
- Maximum parsimony finds the tree with the fewest changes.
  
---
