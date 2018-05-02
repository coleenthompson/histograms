# histograms
Makes histograms of the nucleotide diversity of organisms outside of protected areas and adds a red line to  indicate the nucleotide diversity inside the areas. 


##############
##histograms##
##############

library(readr)

#list all species folders
folders <- list.dirs(path = "/Users/coleenthompson/Desktop/newtest", full.names = F, recursive = F)

#loop through speies folders
for (f in folders) {
  tryCatch({
  #change to species f directory
  dir<-(paste("/Users/coleenthompson/Desktop/newtest/",f,sep=""))
  setwd(dir)
  #read in table with nucleotide data
  sampletable<-paste(f,"_sampletable.txt",sep="")  
  sample_table<-read.table(sampletable, header=F, sep="\t")
  sample_table<-sample_table[sample_table$V2== "FALSE_cytb.fas",]

  #create histogram based on data
  pdf(paste(f,"_histogram",sep=""))
  hist(sample_table$V4, xlab= "π outside", main= paste(f," nucleotide diversity", sep=""))
  #add line for pi inside 
  abline(v=sample_table$V3, col="red")
  dev.off()
  
  
  }, error=function(e){ print("separatefilesdonotexist")}  )
}
  
