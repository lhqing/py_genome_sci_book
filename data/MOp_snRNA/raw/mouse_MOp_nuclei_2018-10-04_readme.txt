=================================
Mouse MOp
=================================

RNA sequencing data of single nuclei isolated from mouse primary motor cortex (MOp).
The data set includes 6847 single nuclei collected from six cortical layers of MOp.
The sequencing results were aligned to exons and introns in the GRCm38.p3 reference genome using the STAR algorithm, and aggregated counts at the gene level were calculated.
For more details, please see the Documentation tab in the Cell Types web application.

Gene expression data matrices
	mouse_MOp_nuclei_2018-10-04_exon-matrix.csv
		Contains the (row, column) matrix of read counts obtained for each (gene, nucleus) based on alignment to exons.
		The first row contains the unique identifiers of the samples (nuclei)
		The first column contains the unique identifiers of the genes
	mouse_MOp_nuclei_2018-10-04_intron-matrix.csv
		Contains the (row, column) matrix of read counts obtained for each (gene, nucleus) based on alignment to introns.
		The first row contains the unique identifiers of the samples (nuclei)
		The first column contains the unique identifiers of the genes
		

Sample information (mouse_MOp_nuclei_2018-10-04_columns-samples.csv)
	seq_name
		Unique identifier for sequencing
	sample_id
		Numeric id for FACS well
	sample_type
		Nuclei, Cell or Control
	organism
		Donor species
	donor
		Unique donor mouse identifier
	sex
		Sex of donor mouse. F, female; M, male
	age_days
		Age of donor in days
	genotype
		Full genotype of donor
	driver_lines
		Cre and/or Flp driver line(s) for each donor, when used
	reporter_lines
		Cre and/or Flp-dependent reporter(s) for each donor, when used
	brain_hemisphere
		Brain hemisphere of dissected samples
	brain_region
		Brain region targeted for sampling
	brain_subregion
		Brain subregion targeted for sampling	
	facs_date
		Date on which samples were collected by FACS. All dissections were performed on the same date as the FACS date for each sample.
	facs_container
		FACS container unique identifier
	sample_name
		FACS well id identifying sample	
	facs_sort_criteria
		Gating criteria used to select samples for sorting
	rna_amplification_set
		Amplificaiton plate
	library_prep_set
		Library plate
	library_prep_avg_size_bp
		Average bp size of Library (Fragment Analyzer™ Automated CE)
 	seq_tube
		Sequencing Lane
	seq_batch
		Sequencing Batch
	total_reads
		Total number of sequencing reads
	percent_exon_reads
		% unique genomic reads aligned to exons (STAR)
	percent_intron_reads
		% unique genomic reads aligned to introns (STAR)
	percent_intergenic_reads
		% unique genomic reads aligned to intergenic sequence (STAR)
	percent_rrna_reads
		% total reads aligned to rRNA (STAR)
	percent_unique_reads
		% total reads aligned to genome and unique (STAR)
	percent_synth_reads
		% total reads aligned to ERCC synthetic mRNA (STAR)      
	percent_ecoli_reads
		% total reads aligned to E. coli (STAR)
	percent_aligned_reads_total
		% total reads aligned (STAR)
	complexity_cg
		Dinucleotide odds ratio (PRINSEQ)
	genes_detected_cpm_criterion
		# of genes with CPM values greater than 0, intron and exon counts included
	genes_detected_fpkm_criterion
		# of genes with FPKM values greater than 0, only exon counts included
	tdt_cpm
		# of reads mapping to tdTamato transgenic insert sequence, normalized to counts per million
	gfp_cpm
		# of reads mapping to gfp transgenic insert sequence, normalized to counts per million
	
		
Gene information (mouse_MOp_nuclei_2018-10-04_genes-rows.csv)
	gene
		Gene symbol
	chromosome
		Chromosome location of gene
	entrez_id
		NCBI Entrez ID
	gene_name
		Gene name
