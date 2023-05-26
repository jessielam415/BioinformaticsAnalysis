# Procedure 
## Selecting an expression dataset
- Interested in working with stroke gene expression 
- Used lecture 3 finding expression (Isserlin, 2021) data code with minor modification to find my dataset 
```
if (!requireNamespace("BiocManager", quietly = TRUE))
  install.packages("BiocManager")

if (!requireNamespace("GEOmetadb", quietly = TRUE))
  BiocManager::install("GEOmetadb")
library(GEOmetadb)
library(BiocManager)
if(!file.exists('GEOmetadb.sqlite')) getSQLiteFile()
file.info('GEOmetadb.sqlite')
con <- dbConnect(SQLite(),'GEOmetadb.sqlite')
geo_tables <- dbListTables(con)
geo_tables
dbListFields(con,'gse')
results <- dbGetQuery(con,'select * from gpl limit 5')
knitr::kable(head(results[,1:5]), format = "html")
num_platforms <- dbGetQuery(con,'select count(*) from gpl')
num_platforms
dbListFields(con,'gpl')
uniq_tech <- dbGetQuery(con,'select distinct technology 
                        from gpl')
nrow(uniq_tech)
mod_table <- cbind(uniq_tech[1:(nrow(uniq_tech)/2),1],
     uniq_tech[((nrow(uniq_tech)/2)+1):nrow(uniq_tech),1])
knitr::kable( mod_table, format = "html") #<<
num_uniq_tech <- dbGetQuery(con,'select technology,count(*) 
                            from gpl group by technology')
colnames(num_uniq_tech)[2] <- "Num_Platforms"
plot_df <- num_uniq_tech[!is.na(num_uniq_tech$technology),]
p<-ggplot(data=plot_df, aes(technology, Num_Platforms)) +
  geom_col() + coord_flip()
p
num_uniq_tech_human <- dbGetQuery(con,'select technology,
                                  count(*) from gpl 
                                  where 
                                  organism = "human" 
                                  group by technology')
colnames(num_uniq_tech_human)[2] <- "Num_Platforms"
dim(num_uniq_tech_human)
species_ids <- dbGetQuery(con,'select organism,count(*) 
                          as num_plat from gpl 
                          where organism like "%homo%" 
                          group by organism 
                          order by num_plat desc')
num_uniq_tech_human <- dbGetQuery(con,'select technology,count(*) 
                                  as num_plat 
                                  from gpl 
                                  where organism = "Homo sapiens" 
                                  group by technology  
                                  order by num_plat desc')
colnames(num_uniq_tech_human)[2] <- "Num_Platforms"
dim(num_uniq_tech_human)
num_uniq_tech_contain_human <- dbGetQuery(con,'select technology,
                                          count(*) as num_plat 
                                          from gpl 
                                          where 
                                          organism like "%Homo sapiens%" 
                                          group by technology 
                                          order by num_plat desc')
colnames(num_uniq_tech_contain_human)[2] <- "Num_Platforms"
dim(num_uniq_tech_contain_human)
num_uniq_tech_contain_human <- dbGetQuery(con,'select technology,
                                          count(*) as num_plat 
                                          from gpl 
                                          where 
                                          organism like "%Homo sapiens%" 
                                          group by technology 
                                          order by num_plat desc')
colnames(num_uniq_tech_contain_human)[2] <- "Num_Platforms"
dim(num_uniq_tech_contain_human)
knitr::kable(num_uniq_tech_human, format = "html")
uniq_tech_human <- rbind(data.frame(num_uniq_tech_human, 
                                    type="human only"),
                         data.frame(num_uniq_tech_contain_human, 
                                    type = "contains human"))
knitr::kable(uniq_tech_human[c(1,2,16,17),], format = "html")
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title",
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gpl.title LIKE '%HiSeq%' ", #<<
             sep=" ")
rs <- dbGetQuery(con,sql)
dim(rs)
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title",
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gpl.technology = 'high-throughput sequencing' ", #<<
             sep=" ")
rs <- dbGetQuery(con,sql)
dim(rs)
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title",
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gpl.title LIKE '%HiSeq%' AND ",
             " gpl.organism = 'Homo sapiens'", #<< 
             sep=" ")
rs <- dbGetQuery(con,sql)
dim(rs)
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title,",
             " gse.submission_date",
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gse.submission_date > '2017-01-01' AND", #<<
             "  gpl.organism LIKE '%Homo sapiens%' AND",
             "  gpl.technology LIKE '%high-throughput seq%' ",
             sep=" ")
rs <- dbGetQuery(con,sql)
dim(rs)
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title,",
             " gse.submission_date",
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gse.submission_date > '2017-01-01' AND",
             "  gse.title LIKE '%stroke%' AND ", #<<
             "  gpl.organism LIKE '%Homo sapiens%' AND",
              "  gpl.technology LIKE '%high-throughput seq%' "
             ,sep=" ")
rs <- dbGetQuery(con,sql)
dim(rs)
sql <- paste("SELECT DISTINCT gse.title,gse.gse, gpl.title,",
             " gse.submission_date,",
             " gse.supplementary_file", #<<
             "FROM",
             "  gse JOIN gse_gpl ON gse_gpl.gse=gse.gse",
             "  JOIN gpl ON gse_gpl.gpl=gpl.gpl",
             "WHERE",
             "  gse.submission_date > '2017-01-01' AND",
             "  gse.title LIKE '%stroke%' AND", 
             "  gpl.organism LIKE '%Homo sapiens%' AND",
             "  gpl.technology LIKE '%high-throughput sequencing%' ",
             "  ORDER BY gse.submission_date DESC",sep=" ")
rs <- dbGetQuery(con,sql)
counts_files <- rs$supplementary_file[grep(rs$supplementary_file,
                              pattern = "count|cnt",ignore.case = TRUE)]

series_of_interest <- rs$gse[grep(rs$supplementary_file,
                              pattern = "count|cnt",ignore.case = TRUE)]

shortened_filenames <- unlist(lapply(counts_files,
              FUN = function(x){x <- unlist(strsplit(x,";")) ;
              x <- x[grep(x,pattern= "count|cnt",ignore.case = TRUE)];
                tail(unlist(strsplit(x,"/")),n=1)}))
shortened_filenames[1:10]
num_series <- dbGetQuery(con, 
                         paste("select * from gsm where series_id in ('", 
                               paste(series_of_interest,collapse="','"), 
                               "')", collapse = ""))
gse.count <- as.data.frame(table(num_series$series_id))
series_of_interest_with_counts <- gse.count[which(gse.count$Freq>6),1]
gse.count[which(gse.count$Freq>6),]
```
- Resulted in 2 datasets: 
GSE122709 and GSE155257
- Searched the IDs on gene expression omnibus and read through the paper associated with each dataset 
- chose [GSE155257](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE155257)
    - column names in supplementary file are not indicative of which sample it is. Emailed the first author Andrew Carlson to ask about mapping
    - Considered using GSE122709 instead, also ran GEOmetadb code to search for cancer data instead of stroke data to see if I can find an alternate dataset. Emailed professor about potentially switching to GSE122709 instead. However, am unsure where the GeneID column for GSE122709 is from. Tried briefly to figure it out with BridgeDB but was confused.
    - When I was looking through additional datasets I noticed that usually, the order samples that show up in the GSE accession display correspond to supplementary file column order
    - The order the samples show up in GSE155257 is:


        [GSM4698234](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698234)	Brain_non-stroke_rep1


        [GSM4698235](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698235)	Brain_non-stroke_rep2


        [GSM4698236](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698236)	Brain_non-stroke_rep3


        [GSM4698237](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698237)	Brain_stroke_rep1


        [GSM4698238](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698238)	Brain_stroke_rep2


        [GSM4698239](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698239)	Brain_stroke_rep3


        [GSM4698240](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698240)	Brain_stroke_rep4


        [GSM4698241](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSM4698241)	Brain_stroke_rep5


    - When I assume that the columns are also in this order and ran an MDS plot after removing for low-counts. I see that the non-stroke and stoke samples are clustered separately. Code used to generate this plot is in  the linked notebook


      <img width="856" alt="image" src="https://user-images.githubusercontent.com/48389380/219874803-dc324561-6c38-4d39-8730-14f67dfa5b0f.png">

    - From this I believe I can safely assume that the columns in the supplementary file follow the order or samples showing up in the GSE accession display [GSE155257](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE155257)

# References
Isserlin, R. (2021). Lecture 3: Finding Expression Data. University of Toronto BCB430 - Computational Systems Biology

Isserlin, R. (2022). Lecture 4: Exploring the data and basics of Normalization. University of Toronto BCB430 - Computational Systems Biology

Isserlin, R. (2022). Lecture 5: Data exploration and Identifier mapping. University of Toronto BCB430 - Computational Systems Biology

Isserlin, R. (2023). Assignment #1 - Data set selection and initial Processing (Instructions & Assignment rubric). University of Toronto BCB430 - Computational Systems Biology

Carlson, Andrew P, William McKay, Jeremy S Edwards, Radha Swaminathan, Karen S SantaCruz, Ron L Mims, Howard Yonas, and Tamara Roitbak. 2021. “Microrna Analysis of Human Stroke Brain Tissue Resected During Decompressive Craniectomy/Stroke-Ectomy Surgery.” Genes 12 (12): 1860.
