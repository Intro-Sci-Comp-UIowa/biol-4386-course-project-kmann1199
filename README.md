# biol-4386-course-project-kmann1199
biol-4386-course-project-kmann1199 created by GitHub Classroom

**Introduction**

Orofacial clefting (OFC) is a common genetic abnormality occurring 1 in every 1,000 births. It results after one or more facial primordia fail to fuse during development. This can present as cleft lip (CL), cleft palate (CP) or a mixture of both (CL/CP). These abnormalities can often be accompanied by difficulties eating and talking and social impacts including negative self-image and decreased social skills. A colleague is looking into the copy number variants (CNV) that could be causing these abnormalities. CNVs are structural variants that result in the amplification or deletion of a gene. Facial development is heavily dependent on precise timing of gene expression to form normally. Previous experiments have identified isthmin1 (*ISM1*) as a clefting gene that when it is knocked down, causes craniofacial dysmorphologies and clefting in the model system *Xenopus laevis*. 

My colleague made her figure by taking single-cell RNA sequencing in the form of Fastq files and running them through a Python pipeline to map the transcripts to actual genes. We still have the Fastq files of data, and I have full access to these files. The pipeline is from the Allon Klein’s Lab’s GitHub page, and using the sequences can plot them on the spring plot based on the determinants of how similar the cells are to one another. The program can determine how to group the cells based on what they are/are not expressing compared to other cells, based on how many groups it is told to separate into. My colleague made this visualization using a spring-plot in python. Using the GitHub page https://github.com/AllonKleinLab/SPRING_dev I should be able to find the code necessary to recreate my colleague’s visualization. 

Main Steps:
