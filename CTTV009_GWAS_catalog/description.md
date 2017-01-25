#Evidence.variant2disease.association_score
This score is the P value we get from the curated scientific publication for the given variant to disease association.
A P- value is a value representing the significance of the odds ratio (odds of disease for individuals having a specific
allele and the odds of disease for individuals who do not have that same allele) is typically calculated using a simple
chi-squared test. Finding odds ratios that are significantly different from 1 is the objective of the GWA study because
this shows that a SNP is associated with the disease.

#Evidence.variant2gene.association_score

To assign variants to genes we current use the OpenTargets "SNP Assignment Pipeline".

The pipeline uses data from two sources:
* Ensembl VEP REST API
* Ensembl Perl API
If VEP JSON is returned for a given SNP with RS id (or position if not available), it will be assigned gene from transcript that has the most_severe_consequence. For intergenic SNPs (~35% of GWAS Catalog), No VEP JSON is returned. For these the nearest gene at the five prime end is determined using the Ensembl Perl API.

To obtain a score we associate the returned SO terms with a number between 0 and 1 which reflect the severity of the effect
of the snp on the given gene (the closer to 1 and most severe). It also reflects in some degree the likeliness of that snp
to be associated with that gene.
If the snp is in a coding region of a gene and brings a new stop codon it is likely that the snp to gene assignment is right.
If the gene is associated to a snp because it was the nearest gene to this snp, the association can still be right but we're less
sure of it then in the previous example.

Here are the different terms and the scores we associate to them :

| Term | Probability |
| ---- | ----------- |
| transcript_ablation	| 1 |
| splice_acceptor_variant	| 0.971428571 |
| splice_donor_variant	| 0.942857143 |
| stop_gained	| 0.914285714 |
| frameshift_variant	| 0.885714286 |
| stop_lost	| 0.857142857 |
| initiator_codon_variant	| 0.828571429 |
| transcript_amplification	| 0.8 |
| inframe_insertion | 0.771428571 |
| inframe_deletion | 0.742857143 |
| missense_variant | 0.714285714 |
| splice_region_variant | 0.685714286 |
| incomplete_terminal_codon_variant | 0.657142857 |
| stop_retained_variant | 0.628571429 |
| synonymous_variant | 0.6 |
| coding_sequence_variant | 0.571428571 |
| mature_miRNA_variant | 0.542857143 |
| 5_prime_UTR_variant | 0.514285714 |
| non_coding_transcript_exon_variant | 0.457142857 |
| intron_variant | 0.428571429 |
| NMD_transcript_variant | 0.4 |
| non_coding_transcript_variant | 0.371428571 |
| upstream_gene_variant | 0.342857143 |
| downstream_gene_variant | 0.314285714 |
| TFBS_ablation | 0.285714286 |
| TFBS_amplification | 0.257142857 |
| TF_binding_site_variant | 0.228571429 |
| regulatory_region_ablation | 0.2 |
| regulatory_region_amplification | 0.171428571 |
| regulatory_region_variant | 0.142857143 |
| feature_elongation | 0.114285714 |
| feature_truncation | 0.085714286 |
| intergenic_variant | 0.057142857 |
| nearest_gene_five_prime_end | 0.028571429 |

#Overall association_score method for an association
The overall score is the product of the variant2gene score by the variant2disease score.
