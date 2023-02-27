Single-Cell Visualization of Genes in the Head of Wildtype *Xenpus laevis*

#**Reference**
Sydney Arlis. unpublished Fall 2022 COSMOS Presentation. Elucidating the Function of the Clefting Gene ISM1. Manak and Houston Labs.  

#**Introduction**
	Orofacial clefting (OFC) is a common genetic abnormality occurring 1 in every 1,000 births. It results after one or more facial primordia fail to fuse during development. This can present as cleft lip (CL), cleft palate (CP) or a mixture of both (CL/CP). These abnormalities can often be accompanied by difficulties eating and talking and social impacts including negative self-image and decreased social skills. Another Ph.D. student in my/the Manak lab is looking into the copy number variants (CNV) that could be causing these abnormalities. CNVs are structural variants that result in the amplification or deletion of a gene. The Manak lab has previously collected human patient samples and then used array-based comparative genomic hybridization (aCGH) to identify CNVs in individuals with OFC. These experiments identified the novel clefting gene isthmin 1 (ISM1), which, when knocked out in *Xenopus*, causes craniofacial dysmorphologies and in some cases induces a cleft. Although it is known that ISM1 is important for proper craniofacial development, it is still unclear how perturbation of ISM1 expression results in orofacial clefts. 

#**Figure to Reproduce**
Figure 1. Sydney Arlis unpublished data Fall 2022. Each dot represents a single cell in the head of a wildtype frog. The farther apart the dots are from each other, the more differentiated they are. The cells can be categorized into cell types based on how they have been grouped within the spring plot, the different colors arbitrarily represent these groupings. 
This figure from Sydney Arlis is a visualization of single cells that were identified in a wildtype Xenopus in the head/face region. Each dot is representative of a cell, and the colors align different groups of closely related cells. The different areas are showing where the cell was expressed, and as you move farther away from the center plot, the cells become more differentiated. These cells are being expressed during stage 25; most publications only show cells until stage 22. I am interested in doing a single-cell visualization to show wildtype neural crest development between stages 22 and 25. Current publications only show development up to stage 22, however, the neural crest is still forming until stage 25, so we want to see what different cell populations are present at this stage. It is just common practice to stop around stage 22, Sydney is just specifically focused on the formation of the neural crest, so we want to extend out to stage 25. Eventually we want to do this in an ISM1 knockdown to see what genes are being affected.
Materials and Methods
	My colleague made her figure by taking single-cell RNA sequencing in the form of Fastq files and running them through a Python pipeline to map the transcripts to actual genes. We still have the Fastq files of data, and I have full access to these files. The pipeline is from the Allon Klein’s Lab’s GitHub page, and using the sequences can plot them on the spring plot based on the determinants of how similar the cells are to one another. The program can determine how to group the cells based on what they are/are not expressing compared to other cells, based on how many groups it is told to separate into. My colleague made this visualization using a spring-plot in python. Using the GitHub page https://github.com/AllonKleinLab/SPRING_dev I should be able to find the code necessary to recreate my colleague’s visualization. 

#**Main steps**

1. Installations:
	a. Python Server
		1. As well as a few libraries
		2. Also, miniconda
	b. R
2. Set up the SPRING data directory.
	a. The main directory will need multiple subdirectories.
	b. Then each subdirectory will need to contain other files
3. Run SPRING viewer.
	a. Open FastX.
	b. Start python server.
	c. View the data set.
4. Classify cellular phenotypes.
	a. Using SignacX in R
	b. Generate cellular phenotype labels.
	c. Write cell types to SPRING.
5. Data can now be visualized in SPRING viewer.

