#Methods

Each database entry corresponds to the overall literature-based evidence of a particular gene-disease association. 

GeneID (from literature)
Disease (from literature)
Variant  (not applicable)
Confidence (not applicable 1.0)
Severity (not applicable 1.0)
Frequency (relative proportion compared to other gene/disease linkages)

Frequency
Frequency captures the relative number of entries linking a particular gene-disease pair compared to the total number of records linking either entry. Alternative normalization schemes will be compared. See Section 1.

For the EuroPMC literature mining, the concept is to identify co-occurrences of the target (Uniprot mapping) and disease term (EFO including synonyms) within a paper, and then to score a paper based on the count of co-occurrences and their positions in the sections of a paper.  The score is the sum of the co-occurrences, scaled by the section in which they occur, plus a factor that represents the number of time the target is mentioned overall in the abstract (count * 0.3).  

The scale factors are

..Title 10
..Abstract/Results/Fig/Table 5
..Introduction/Case study/Appendix/Other 1
..Discussion 3
..Conclusion 2

So the score is
 
	 sum ((section co-occurrence count) * section factor)

JSON is provided for each Target - Disease association itemising the papers and their score.

To get the overall score we set S = 1, and f =1 and calculate a confidence 

	 paper scores for target associated with disease / Median score for all papers that contain co-occurrences for either target or disease

The score will have to be scaled for use in the web app as with the other scores.
