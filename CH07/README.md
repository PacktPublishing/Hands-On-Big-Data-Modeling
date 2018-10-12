# Modeling with Unstructured Data

## Data Ingestion

```
> res <- XML::readHTMLTable(paste0('http://cran.r-project.org/',
+     'web/packages/available_packages_by_name.html'), which = 1)
```

R comes with a bunch of functions that can be used to read different types of files. In this tutorial, we are going to use tm and XML. If you do not have XML package installed, it can be installed using the following command:

```
install.packages("XML")

```

In order to see supported text file formats, we can use the function getReaders.

```
> getReaders()
 [1] "readDataframe" "readDOC"
 [3] "readPDF" "readPlain"
 [5] "readRCV1" "readRCV1asPlain"
 [7] "readReut21578XML" "readReut21578XMLasPlain"
 [9] "readTagged" "readXML"
 ```

 At the time of writing this book, the snippet downloaded 12658 R libraries name and their short descriptions. A new term to get familiar is corpus which is basically a collection of text documents that we can include in the analytics. We can use the getSources function to see the available options to import a corpus with the tm package.

```
> library(tm)
Loading required package: NLP
> getSources()
[1] "DataframeSource" "DirSource" "URISource" "VectorSource"
[5] "XMLSource" "ZipSource"
```

Building a corpus from the vector source of package descriptions downloaded from R package lists can be done using one of the above options. In this case, we can go ahead and use VectorSource.

```
> v <- Corpus(VectorSource(res$V2))
> v
<<SimpleCorpus>>
Metadata: corpus specific: 1, document level (indexed): 0
Content: documents: 12658
```


This step created a VCorpus (in-memory) object which currently holds 12658 packages descriptions. We can use inspect and head function to view the output of processed statements. So, in order to see the first 5 documents in the corpus, we can run the following command:
```
> inspect(head(v, 5))
<<SimpleCorpus>>
Metadata: corpus specific: 1, document level (indexed): 0
Content: documents: 3
[1] Accurate, Adaptable, and Accessible Error Metrics for Predictive\nModels
[2] Access to Abbyy Optical Character Recognition (OCR) API
[3] Tools for Approximate Bayesian Computation (ABC)
[4] Data Only: Tools for Approximate Bayesian Computation (ABC)
[5] Array Based CpG Region Analysis Pipeline
```