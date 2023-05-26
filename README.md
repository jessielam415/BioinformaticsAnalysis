# Bioinformatics Analysis for Computation System Biology
Bioinformatics analysis using R for the U of T course BCB420 - Computational System Biology

My analysis was on the dataset from MicroRNA analysis of human stroke brain tissue resected during decompressive craniectomy/stroke-ectomy surgery analysis (Carlson et al. 2021).
All analysis is primarily done through R, with environments controlled using Docker

## Steps

Phase 1 - Data set selection and initial Processing (Steps and code can easily be viewed [here](https://htmlpreview.github.io/?https://github.com/jessielam415/ComputationalBiologyAnalysis/blob/main/A1/A1.html))
-  Selecting a data set based on interest. 
    - I was particularly interested in selecting a stroke dataset as I am particularly interested in stroke recovery, and have previously been involved in research projects that investigate the molecules that affect stroke recovery
    - To look for a dataset of interest, I took the steps that are outlined in [SelectingDataset.md](https://github.com/jessielam415/ComputationalBiologyAnalysis/blob/main/A1/SelectingDataset.md)
- Clean the data and map to HUGO symbols
- Apply Normalization
- Interpret and document results

Phase 2 - Data set selection and initial Processing (Steps and code can be easily viewed [here](https://htmlpreview.github.io/?https://github.com/jessielam415/ComputationalBiologyAnalysis/blob/main/A2/A2_Wing_Lam.html))
- Conduct differential gene expression analysis
- Conduct thresholded over-representation analysis 
- Intepret results

Phase 3 - Data set Pathway and Network Analysis (Steps can be easily viewed [here](https://htmlpreview.github.io/?https://github.com/jessielam415/ComputationalBiologyAnalysis/blob/main/A3/A3_Wing_Lam.html))
- Conduct Non-thresholded gene set enrichment analysis 
- Visualize gene set enrichment analysis in cytoscape
- Interpret results 


## References
Ruth Isserlin, BCB420 Lectures (2023)

GeneCaRNA the human ncRNA Gene Database (2023) 

Ensembl (2023)

Anacharis B. Sá-Nakanishi, Vanesa O. Pateis, Monique Cristine de Oliveira. 2020. “Glycemic Homeostasis and Hepatic Metabolism Are Modified in Rats with Global Cerebral Ischemia.” Biochim Biophys Acta Mol Basis Dis 1866 (12).

Anwen Shao, Yihan Yao, Yunxiang Zhou. 2019. “The Role and Therapeutic Potential of Heat Shock Proteins in Haemorrhagic Stroke.” Journal of Cellular and Molecular Medicine 23 (9): 5846–58.

Aravind Subramanian, Vamsi K. Mootha, Pablo Tamayo. 2005. “Gene Set Enrichment Analysis: A Knowledge-Based Approach for Interpreting Genome-Wide Expression Profiles.” Proceedings of the National Academy of Sciences 102 (43): 15545–50.

Benjamini, Yoav, and Yosef Hochberg. 1995. “Controlling the False Discovery Rate: A Practical and Powerful Approach to Multiple Testing.” Journal of the Royal Statistical Society 57 (1): 289–300.

Bonnin, Sarah. 2020. 19.11 Volcano Plots. https://biocorecrg.github.io/CRG_RIntroduction/volcano-plots.html.

Carlson, Andrew P, William McKay, Jeremy S Edwards, Radha Swaminathan, Karen S SantaCruz, Ron L Mims, Howard Yonas, and Tamara Roitbak. 2021. “Microrna Analysis of Human Stroke Brain Tissue Resected During Decompressive Craniectomy/Stroke-Ectomy Surgery.” Genes 12 (12): 1860.

Damian Smedley, Benoit Ballester, Syed Haider. 2009. “BioMart – Biological Queries Made Easy.” BMC Genomics 10 (22).

Iván Alquisiras-Burgos, Penélope Aguilera. 2022. “Involvement of Glucose Transporter Overexpression in the Protection or Damage After Ischemic Stroke.” Neural Regerenation Research 17 (4): 783–84.

Jong Youl Kim, Jong Eun Lee, Yeonseung Han. 2018. “The 70-kDa Heat Shock Protein (Hsp70) as a Therapeutic Target for Stroke.” Expert Opinion on Therapeutic Targets 22 (3): 191–99.

Kolberg, Liis, Uku Raudvere, Ivan Kuzmin, Jaak Vilo, and Hedi Peterson. 2020. “Gprofiler2– an r Package for Gene List Functional Enrichment Analysis and Namespace Conversion Toolset g:profiler.” F1000Research 9 (ELIXIR) (709).

Mark D. Robinson, Davis J. McCarthy, and Gordon K. Smyth. 2010. “edgeR: A Bioconductor Package for Differential Expression Analysis of Digital Gene Expression Data.” Bioinformatics 26 (1): 139–40.

Uku Raudvere, Ivan Kuzmin, Liis Kolberg. 2019. “G:profiler: A Web Server for Functional Enrichment Analysis and Conversions of Gene Lists (2019 Update).” Nucleic Acids Research 47 (1): 191–W198.

Vamsi K Mootha, Karl-Fredrik Eriksson, Cecilia M Lindgren. 2003. “PGC-1α-Responsive Genes Involved in Oxidative Phosphorylation Are Coordinately Downregulated in Human Diabetes.” Nature Genetics 34 (3): 267–73.

Warde-Farley D, Comes O, Donaldson SL. 2010. “The GeneMANIA Prediction Server: Biological Network Integration for Gene Prioritization and Predicting Gene Function.” Nucleic Avids Research 28 (2): W214–20.


Yun Mo, Yin-Yi Sun, and Kang-Yong Liu. 2020. “Autophagy and Inflammation in Ischemic Stroke.” Neural Regeneration Research 15 (8): 1388–96.
