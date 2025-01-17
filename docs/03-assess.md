

```r
library(tidyverse)
library(knitr)
library(kableExtra)
temp_eval <- TRUE
options(tinytex.verbose = TRUE)
```

# Assessment

In this stage, you will review and describe in detail the available reproduction materials, and assess levels of computational reproducibility for the selected outputs, as well as for the overall paper. This stage is designed to record as much of the learning process behind a reproduction as possible to facilitate incremental improvements, and allow future reproducers to pick up easily where others have left off.

First, you will provide a detailed description of the reproduction package. Second, you will connect the outputs you’ve chosen to reproduce with their corresponding inputs. With these elements in place, you can score the level of reproducibility of each output, and report on paper-level dimensions of reproducibility.  

In the *Scoping* stage, you declared a paper, identified the specific claims you will reproduce, and recorded the main estimates that support the claims. In this stage, you will identify all outputs that contain those estimates. You will also decide if you are interested in assessing the reproducibility of that entire output (e.g., "Table 1"), or will assess only a pre-specified estimates (e.g., "rows 3 and 4 of Table 1"). Additionally, you can include other outputs of interest.

**Use *Survey 2* to record your work as part of this step.**

*Tip:* We recommend that you first focus on one specific output (e.g., “Table 1”). After completing the assessment for this output, you will have a much easier time translating improvements to other outputs.


## Describe the inputs. {#describe-inputs}
This section explains how to list *all* input materials found or referred to in the reproduction package. First, you will identify data sources and connect them with their raw data files (when available). Second, you will locate and provide a brief description of the analytic data files. Finally, you will locate, inspect, and describe the analytic code used in the paper.

The following terms will be used in this section:     

 -	**Cleaning code:** A script associated primarily with data cleaning. Most of its content is dedicated to actions like deleting variables or observations, merging data sets, removing outliers, or reshaping the structure of the data (from long to wide, or vice versa).  

 -	**Analysis code:** A script associated primarily with analysis. Most of its content is dedicated to actions like running regressions, running hypothesis tests, computing standard errors, and imputing missing values.



### Describe the data sources and raw data. {#desc-sourc}

In the paper you chose, find references to all *data sources* used in the analysis. A data source is usually described in narrative form. For example, if in the body of the paper you see text like “…for earnings in 2018 we use the Current Population Survey…”, the data source is “Current Population Survey 2018”. If it is mentioned for the first time on page 1 of the Appendix, its location should be recorded as “A1”. Do this for all the data sources mentioned in the paper.

Data sources also vary by unit of analysis, with some sources matching the same unit of analysis used in the paper (as in previous examples), while others are less clear (e.g., "our information on regional minimum wages comes from the Bureau of Labor Statistics." This should be recorded as "regional minimum wages from the Bureau of Labor Statistics").

When filling out the cited and provided sections for data in the assessment stage, make sure to check that the data is actually cited. Usually, we want to encourage the authors to cite the dataset itself. If the cited source is a study instead, you should use your own judgement on determining whether or not you can count the data as cited.

Next, look at the reproduction package and map the *data sources* mentioned in the paper to the *data files* in the available materials. Record their folder locations relative to the main reproduction folder^[a relative location takes the form of `/folder_in_rep_materials/sub_folder/file.txt`, in contrast to an absolute location that takes the form of `username/documents/projects/repros/folder_in_rep_materials/sub_folder/file.txt`]. In addition to looking at the existing data files, we recommend that you review the first lines of all code files (especially cleaning code), looking for lines that call the datasets. Inspecting these scripts may help you understand how different data sources are used, and possibly identify any files that are missing from the reproduction package.

One thing to note is that if the data is pulled from a source such as a database, there should be detailed instructions on how to retrieve this information from the source in order for the dataset to be considered raw data. If this information on how to acquire/query the data is not clear or does not yield the same results, the data should not be considered raw data.

Record this information in this [standardized spreadsheet](https://docs.google.com/spreadsheets/d/1LUIdVFH0OfR70C7z07TYeE-uWzKI_JIeWUMaYhqEKK0/edit#gid=0&range=A1) (download it or make a copy for yourself), using the following structure:    
<table class="table" style="margin-left: auto; margin-right: auto;">
<caption>(\#tab:raw-data-information)Raw data information</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> data_source </th>
   <th style="text-align:left;"> page </th>
   <th style="text-align:left;"> data_files </th>
   <th style="text-align:left;"> known_missing </th>
   <th style="text-align:left;"> directory </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> "Current Population Survey 2018" </td>
   <td style="text-align:left;"> A1 </td>
   <td style="text-align:left;"> cepr_march_2018.dta </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> /data/ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> "DHS 2010 - 2013" </td>
   <td style="text-align:left;"> 4 </td>
   <td style="text-align:left;"> nicaraguaDHS_2010.csv; boliviaDHS2010.csv; nicaraguaDHS_2011.csv; nicaraguaDHS_2012.csv; boliviaDHS_2012.csv; nicaraguaDHS_2013.csv; boliviaDHS_2013.csv </td>
   <td style="text-align:left;"> boliviaDHS_2011.csv </td>
   <td style="text-align:left;"> /rawdata/DHS/ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> "2017 SAT scores" </td>
   <td style="text-align:left;"> 4 </td>
   <td style="text-align:left;"> Not available </td>
   <td style="text-align:left;">  </td>
   <td style="text-align:left;"> /data/to_clean/ </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
  </tr>
</tbody>
</table>


          Raw data information:
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|
          | data_source          | page | data_files                                    | known_missing       | directory           |
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|
          | "Current Population  | A1    | cepr_march_2018.dta                          |                     | \data\              |
          | Survey 2018"         |      |                                               |                     |                     |
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|
          | "DHS 2010 - 2013"    | 4    | nicaraguaDHS_2010.csv;                        | boliviaDHS_2011.csv | \rawdata\DHS\       |
          |                      |      | boliviaDHS_2010.csv; nicaraguaDHS_2011.csv;   |                     |                     |
          |                      |      | nicaraguaDHS_2012.csv; boliviaDHS_2012.csv;   |                     |                     |
          |                      |      | nicaraguaDHS_2013.csv; boliviaDHS_2013.csv    |                     |                     |
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|
          | "2017 SAT scores"    | 4    | Not available                                 |                     | \data\to_clean\     |
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|
          | ...                  | ...  | ...                                           | ...                 | ...                 |
          |----------------------|------|-----------------------------------------------|---------------------|---------------------|

**Note:** lists if files in the data_files and known_missing columns should have entries separated by a semi-colon to for the spreadsheet to be compatible with the ACRE Diagram Builder.

### Describe the analytic data sets. {#desc-analy}

List all the analytic files you can find in the reproduction package, and identify their locations relative to the main reproduction folder. Record this information in the [standardized spreadsheet](https://docs.google.com/spreadsheets/d/1LUIdVFH0OfR70C7z07TYeE-uWzKI_JIeWUMaYhqEKK0/edit#gid=1299317837&range=A1).

As you progress through the exercise, add to the spreadsheet a one-line description of each file's main content (for example: `all_waves.csv` has the simple description `data for region-level analysis`). This may be difficult in an initial review, but will become easier as you go along.

The resulting report will have the following structure:  

<table class="table" style="margin-left: auto; margin-right: auto;">
<caption>(\#tab:analysis-data-information)Analysis data information</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> analysis_data </th>
   <th style="text-align:left;"> location </th>
   <th style="text-align:left;"> description </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> final_data.csv </td>
   <td style="text-align:left;"> /analysis/fig1/ </td>
   <td style="text-align:left;"> data for figure1 </td>
  </tr>
  <tr>
   <td style="text-align:left;"> all_waves.csv </td>
   <td style="text-align:left;"> /final_data/v1_april/ </td>
   <td style="text-align:left;"> data for region-level analysis </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
  </tr>
</tbody>
</table>

          Analysis data information:
          |----------------|-----------------------|--------------------------------|
          | analysis_data  | location              | description                    |
          |----------------|-----------------------|--------------------------------|
          | final_data.csv | /analysis/fig1/       | data for figure1               |
          |----------------|-----------------------|--------------------------------|
          | all_waves.csv  | /final_data/v1_april/ | data for region-level analysis |
          |----------------|-----------------------|--------------------------------|
          | ...            | ...                   | ...                            |
          |----------------|-----------------------|--------------------------------|


### Describe the code scripts.{#desc-scripts}

List all code files that you found in the reproduction package and identify their locations relative to the master reproduction folder. Review the beginning and end of each code file and identify the inputs required to successfully run the file. Inputs may include data sets or other code scripts that are typically found at the beginning of the script (e.g., `load`, `read`, `source`, `run`, `do` ). For each code file, record all inputs together and separate each item with ";". Outputs may include other datasets, figures, or plain text files that are typically at the end of a script (e.g., `save`, `write`, `export`). For each code file, record all outputs together and separate each item with ";". Provide a one-line description of what each code file does. Record all of this information in the [standardized spreadsheet](https://docs.google.com/spreadsheets/d/1LUIdVFH0OfR70C7z07TYeE-uWzKI_JIeWUMaYhqEKK0/edit#gid=1617799822&range=A1), using the following structure:

<div style="border: 0px;overflow-x: scroll; width:100%; "><table class="table" style="margin-left: auto; margin-right: auto;">
<caption>(\#tab:code-files-information)Code files information</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> file_name </th>
   <th style="text-align:left;"> location </th>
   <th style="text-align:left;"> inputs </th>
   <th style="text-align:left;"> outputs </th>
   <th style="text-align:left;"> description </th>
   <th style="text-align:left;"> primary_type </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> output_table1.do </td>
   <td style="text-align:left;"> /code/analysis/ </td>
   <td style="text-align:left;"> analysis_data01.csv </td>
   <td style="text-align:left;"> output1_part1.txt </td>
   <td style="text-align:left;"> produces first part of table 1 (unformatted) </td>
   <td style="text-align:left;"> analysis </td>
  </tr>
  <tr>
   <td style="text-align:left;"> data_cleaning02.R </td>
   <td style="text-align:left;"> /code/cleaning </td>
   <td style="text-align:left;"> admin_01raw.csv </td>
   <td style="text-align:left;"> analysis_data02.csv </td>
   <td style="text-align:left;"> removes outliers and missing vals from raw admin data </td>
   <td style="text-align:left;"> cleaning </td>
  </tr>
  <tr>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
  </tr>
</tbody>
</table></div>

          Code files information:
          |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
          | file_name         | location         | inputs              | outputs             | description          | primary_type |
          |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
          | output_table1.do  | /code/analysis/  | analysis_data01.csv | output1_part1.txt   | produces first part  | analysis     |
          |                   |                  |                     |                     | of table 1           |              |
          |                   |                  |                     |                     | (unformatted)        |              |
          |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
          | data_cleaning02.R | /code/cleaninig/ | admin_01raw.csv     | analysis_data02.csv | removes outliers     | cleaning     |
          |                   |                  |                     |                     | and missing vals     |              |
          |                   |                  |                     |                     | from raw admin data  |              |
          |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
          | ...               | ...              | ...                 | ...                 | ...                  | ...          |
          |-------------------|------------------|---------------------|---------------------|----------------------|--------------|


As you gain an understanding of each code script, you will likely find more inputs and outputs -- we encourage you to update the [standardized spreadsheet](https://docs.google.com/spreadsheets/d/1LUIdVFH0OfR70C7z07TYeE-uWzKI_JIeWUMaYhqEKK0/edit#gid=1617799822&range=A1). Once finished with the reproduction exercise, classify each code file as *analysis* or *cleaning*. We recognize that this may involve subjective judgment, so we suggest that you conduct this classification based on each script's main role.

**Note:** If a code script takes multiple inputs and/or produces multiple outputs they should be listed as semicolon separated lists in order to be compatible with the ACRE Diagram Builder.

## Connect each output to all its inputs {#diagram}

Using the information collected above, you can trace your output-to-be-reproduced to its primary sources. Email the standardized spreadsheets from above (sections \@ref(desc-sourc), \@ref(desc-analy) and \@ref(desc-scripts)) to the ACRE Diagram Builder at acre@berkeley.edu. You should receive an email within 24 hours with a reproduction diagram tree that represents the information available on the workflow behind a specific output.


<!--
Upload the standardized table you build to the describe the code above into the [ACRE workflow diagram builder](ADD LINK).
-->
### Complete workflow information

If you were able to identify all the relevant components in the previous section, the ACRE Diagram Builder will produce a tree diagram that looks similar to the one below.

<!-- Emma: add a label to this figure below -->  

        table1.tex
            |___[code] analysis.R
                |___analysis_data.dta
                    |___[code] final_merge.do
                        |___cleaned_1_2.dta
                        |   |___[code] clean_merged_1_2.do
                        |       |___merged_1_2.dta
                        |           |___[code] merge_1_2.do
                        |               |___cleaned_1.dta
                        |               |   |___[code] clean_raw_1.py
                        |               |       |___raw_1.dta
                        |               |___cleaned_2.dta
                        |                   |___[code] clean_raw_2.py
                        |                       |___raw_2.dta
                        |___cleaned_3_4.dta
                            |___[code] clean_merged_3_4.do
                                |___merged_3_4.dta
                                    |___[code] merge_3_4.do
                                        |___cleaned_3.dta
                                        |   |___[code] clean_raw_3.py
                                        |       |___raw_3.dta
                                        |___cleaned_4.dta
                                            |___[code] clean_raw_4.py
                                                |___raw_4.dta

This diagram, built with the information you provided, is already an important contribution to understanding the necessary components required to reproduce a specific output. It summarizes key information to allow for more constructive exchanges with original authors or other reproducers. For example, when contacting the authors for guidance, you can use the diagram to point out specific files you need. Formulating your request this way makes it easier for authors to respond and demonstrates that you have a good understanding of the reproduction package.  

### Incomplete workflow information

In many cases, some of the components of the workflow will not be easily identifiable (or missing) in the reproduction package. Here the Diagram Builder will return a partial reproduction tree diagram. For example, if the files `merge_1_2.do`, `merge_3_4.do`, and `final_merge.do` are missing from the previous diagram, the ACRE Diagram Builder will produce the following diagram:

        cleaned_3.dta
            |___[code] clean_raw_3.py
                |___raw_3.dta

        table1.tex
            |___[code] analysis.R
                |___analysis_data.dta

        cleaned_3_4.dta
            |___[code] clean_merged_3_4.do
                |___merged_3_4.dta

        cleaned_1.dta
            |___[code] clean_raw_1.py
                |___raw_1.dta

        cleaned_2.dta
            |___[code] clean_raw_2.py
                |___raw_2.dta

        cleaned_4.dta
            |___[code] clean_raw_4.py
                |___raw_4.dta

        cleaned_1_2.dta
            |___[code] clean_merged_1_2.do
                |___merged_1_2.dta
        Unused data sources: None.


In this case, you can still manually combine this partial information with your knowledge from the paper and own judgement to produce a "candidate" tree diagram (which might lead to different reproducers recreating different diagrams). This may look like the following:


        table1.tex
            |___[code] analysis.R
                |___analysis_data.dta
                    |___MISSSING CODE FILE(S) #3
                        |___cleaned_3_4.dta
                        |       |___[code] clean_merged_3_4.do
                        |           |___merged_3_4.dta
                        |               |___MISSSING CODE FILE(S) #2
                        |                   |___cleaned_3.dta
                        |                   |       |___[code] clean_raw_3.py
                        |                   |           |___raw_3.dta    
                        |                   |___cleaned_4.dta
                        |                           |___[code] clean_raw_4.py
                        |                               |___raw_4.dta
                        |___cleaned_1_2.dta
                                |___[code] clean_merged_1_2.do
                                    |___merged_1_2.dta
                                        |___MISSSING CODE FILE(S) #1
                                            |___cleaned_1.dta
                                            |       |___[code] clean_raw_1.py
                                            |           |___raw_1.dta
                                            |   
                                            |___cleaned_2.dta
                                                    |___[code] clean_raw_2.py
                                                        |___raw_2.dta


To leave a record of the reconstructed diagrams, you will have to amend the input spreadsheets using placeholders for the missing components. In the example above, you should add the following entries to the code description spreadsheet:
<table class="table" style="margin-left: auto; margin-right: auto;">
<caption>(\#tab:adding-rows)Adding rows to code spreadsheet</caption>
 <thead>
  <tr>
   <th style="text-align:left;"> file_name </th>
   <th style="text-align:left;"> location </th>
   <th style="text-align:left;"> inputs </th>
   <th style="text-align:left;"> outputs </th>
   <th style="text-align:left;"> description </th>
   <th style="text-align:left;"> primary_type </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
   <td style="text-align:left;"> ... </td>
  </tr>
  <tr>
   <td style="text-align:left;"> missing_file1 </td>
   <td style="text-align:left;"> unknown </td>
   <td style="text-align:left;"> cleaned_1.dta, cleaned_2.dta </td>
   <td style="text-align:left;"> merged_1_2.dta </td>
   <td style="text-align:left;"> missing code </td>
   <td style="text-align:left;"> unknown </td>
  </tr>
  <tr>
   <td style="text-align:left;"> missing_file2 </td>
   <td style="text-align:left;"> unknown </td>
   <td style="text-align:left;"> cleaned_3.dta, cleaned_4.dta </td>
   <td style="text-align:left;"> merged_3_4.dta </td>
   <td style="text-align:left;"> missing code </td>
   <td style="text-align:left;"> unknown </td>
  </tr>
  <tr>
   <td style="text-align:left;"> missing_file3 </td>
   <td style="text-align:left;"> unknown </td>
   <td style="text-align:left;"> merged_3_4.dta, merged_1_2.dta </td>
   <td style="text-align:left;"> analysis_data.dta </td>
   <td style="text-align:left;"> missing code </td>
   <td style="text-align:left;"> unknown </td>
  </tr>
</tbody>
</table>

        Adding rows to code spreadsheet:
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
        | file_name         | location         | inputs              | outputs             | description          | primary_type |
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
        | ...               | ...              | ...                 | ...                 | ...                  | ...          |
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
        | missing_file1     | unknown          | cleaned_1.dta;      | merged_1_2.dta      | missing code         | unknown      |
        |                   |                  | cleaned_2.dta       |                     |                      |              |
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
        | missing_file2     | unknown          | cleaned_3.dta;      | merged_3_4.dta      | missing code         | unknown      |
        |                   |                  | cleaned_4.dta       |                     |                      |              |                  
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|
        | missing_file3     | unknown          | merged_3_4.dta;    | analysis_data.dta   | missing code         | unknown      |
        |                   |                  | merged_1_2.dta     |                     |                      |              |                  
        |-------------------|------------------|---------------------|---------------------|----------------------|--------------|

As in the cases with complete workflows, these diagrams (fragmented or reconstructed trees) provide important information for assessing and improving the reproducibility of specific outputs. Reproducers can compare reconstructed trees and/or contact original authors with highly specific inquiries.

For more examples of diagrams connecting final outputs to initial raw data, [see here](#additional-diagrams).  

### Unused Data Sources

It is possible that not all data included in a replication package are actually used in code scripts in the reproduction package. This would be the case if, for example, the raw data and analysis data are included, but not the script that generates the analysis data. As a concrete example, consider what the original diagram above would look like if the only code included in the reproduction package were analysis.R:

        table1.tex
            |___[code] analysis.R
                |___analysis_data.dta
        
        Unused data sources:
        raw_1.dta
        raw_2.dta
        raw_3.dta
        raw_4.dta
        
        Unused analysis data:
        cleaned_1.dta
        cleaned_2.dta
        cleaned_3.dta
        cleaned_4.dta
        merged_1_2.dta
        merged_3_4.dta
        cleaned_1_2.dta
        cleaned_3_4.dta
        
In this case, there are many data files that were listed in the raw data and analytic data spreadsheets that are not used by any code script in the replication package. 

## Assign a reproducibility score. {#score}

Once you have identified all possible inputs and have a clear understanding of the connection between the outputs and inputs, you can start to assess the output-specific level of reproducibility.

Take note of the following concepts in this section:     

 - **Computationally Reproducible from Analytic data (CRA):** The output can be reproduced with minimal effort starting from the *analytic* datasets.

 - **Computationally Reproducible from Raw data (CRR):** The output can be reproduced with minimal effort from the *raw* datasets.

 - **Minimal effort:** One hour or less is required to run the code, not including computing time.

### Levels of Computational Reproducibility for a Specific Output  

Each level of computational reproducibility is defined by the availability of data and materials, and whether or not the available materials faithfully reproduce the output of interest. The description of each level also includes possible improvements that can help advance the reproducibility of the output to a higher level. You will learn in more detail about the possible improvements.

Note that the assessment is made *at the output level* -- a paper can be highly reproducible for its main results, but suffer from low reproducibility for other outputs. The assessment includes a 10-point scale, where 1 represents that, under current circumstances, reproducers cannot access any reproduction package, while 10 represents access to all the materials and being able to reproduce the target outcome from the raw data.

 - **Level 1 (L1):** No data or code are available. Possible improvements include adding: raw data (+AD), analysis data (+RD), cleaning code (+CC), and analysis code (+AC).

 You will have detected papers that are reproducible at Level 1 as part of the Scoping stage (unsuccessful candidate papers). Make sure to take record them in Survey 1.

 - **Level 2 (L2):** Code scripts are available (partial or complete), but no data are available. Possible improvements include adding: raw data (+AD) and analysis data (+RD).

 - **Level 3 (L3):** Analytic data and code are partially available, but raw data and cleaning code are not. Possible improvements include: completing analysis data and/or code, adding raw data (+RD), and adding analysis code (+AC).  

 - **Level 4 (L4):** All analytic data sets and analysis code are available, but code does not run or produces results different than those in the paper (not CRA). Possible improvements include: debugging the analysis code (DAC) or obtaining raw data (+RD).      

 - **Level 5 (L5):** Analytic data sets and analysis code are available. They produce the same results as presented in the paper (CRA). The reproducibility package may be improved by obtaining the original raw data sets.

This is the highest level that most published research papers can attain currently. Computational reproducibility *from raw data* is required for papers that are reproducible at Level 6 and above.

 - **Level 6 (L6):** Cleaning code is partially available, but raw data is not. Possible improvements include: completing cleaning code (+CC) and/or raw data (+RD).   

 - **Level 7 (L7):** Cleaning code is available and complete, but raw data is not. Possible improvements include: adding raw data (+RD).  

 - **Level 8 (L8):** Cleaning code is available and complete, and raw data is partially available. Possible improvements include: adding raw data (+RD).

 - **Level 9 (L9):**  All the materials (raw data, analytic data, cleaning code, and analysis code) are available. The analysis code produces the same output as presented in the paper (CRA). However, the cleaning code does not run or produces different results that those presented in the paper (not CRR). Possible improvements include: debugging the cleaning code (DCC).  

 - **Level 10 (L10):** All the materials are available and produce the same results as presented in the paper with minimal effort, starting from the analytic data (yes CRA) or the raw data (yes CRR).  Note that Level 10 is aspirational and may be very difficult to attain for most research published today.

The following figure summarizes the different levels of computational reproducibility (for any given output). For each level, there will be improvements that have been made (`✔`) or can be made to move up one level of reproducibility (-).

<table>
<caption>(\#tab:levels-of-computational-reproducibility)Levels of Computational Reproducibility \
 (P denotes "partial", C denotes "complete")</caption>
 <thead>
<tr>
<th style="border-bottom:hidden" colspan="1"></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="10"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Availability of materials, and reproducibility</div></th>
</tr>
<tr>
<th style="border-bottom:hidden" colspan="1"></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Analysis Code</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Analysis Data</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">CRA</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Cleaning Code</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Raw Data</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">CRR</div></th>
</tr>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;">   </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;border-bottom: 1px solid"> L1: No materials </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L2: Only code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L3: Partial analysis data &amp; code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L4: All analysis data &amp; code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;border-bottom: 1px solid"> L5: Reproducible from analysis </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L6: Some cleaning code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L7: All cleaning code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L8: Some raw data </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L9: All raw data </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L10: Reproducible from raw data </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
  </tr>
</tbody>
</table>


                            Levels of Computational Reproducibility
                           (P denotes "partial", C denotes "complete")
    
                                       | Availability of materials, and reproducibility |
                                       |------------------------------------------------|
                                       |Analysis| Analysis|     | Cleaning| Raw   |     |
                                       |Code    | Data    | CRA | Code    | Data  | CRR |
                                       | P | C  | P  | C  |     | P  |  C | P | C |     |
                                       ---------|---------|-----|---------|-------|-----|
      L1: No materials.................| -   -  | -    -  |  -  |  -    - | -   - |  -  |
      ---------------------------------|--------|---------|-----|---------|-------|-----|
      L2: Only code ...................| ✔   ✔  | -    -  |  -  |  -    - | -   - |  -  |
      L3: Partial analysis data & code.| ✔   ✔  | ✔    -  |  -  |  -    - | -   - |  -  |
      L4: All analysis data & code.....| ✔   ✔  | ✔    ✔  |  -  |  -    - | -   - |  -  |
      L5: Reproducible from analysis...| ✔   ✔  | ✔    ✔  |  ✔  |  -    - | -   - |  -  |
      ---------------------------------|--------|---------|-----|---------|-------|-----|
      L6: Some cleaning code...........| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    - | -   - |  -  |
      L7: All cleaning code............| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | -   - |  -  |
      L8: Some raw data................| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   - |  -  |
      L9: All raw data.................| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   ✔ |  -  |
      L10:Reproducible from raw data...| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   ✔ |  ✔  |


You may disagree with some of the levels outlined above, particularly wherever subjective judgment may be required. If so, you are welcome to interpret the levels as unordered categories (independent from their sequence) and suggest improvements using the "Edit" button above (top left corner if you are reading this document in your browser).

#### Adjusting Levels To Account for Confidential/Proprietary Data {-}

A large portion of published research in economics uses confidential or proprietary data, most often government data from tax records or service provision and what is generally referred to as *administrative data*. Since administrative and proprietary data are rarely publicly accessible, some of the reproducibility levels presented above only apply once modified. The underlying theme of these modifications is that when data cannot be provided, you can assign a reproducibility score based on the level of detail in the instructions for accessing the data. Similarly, when reproducibility cannot be verified based on publicly available materials, the reproduction materials should demonstrate that a competent and unbiased third party (not involved in the original research team) has been able to reproduce the results.

 - **Levels 1 and 2** can be applied as described above.

 - **Adjusted Level 3 (L3\*):** All analysis code is provided, but only partial instructions on how to access the ***analysis data*** are available. This means that the authors have provided some, but not all, of the following information:
    a. *Contact information*, including name of the organization(s) that provides access to the data and contact information of at least one individual.
    b. *Terms of use*, including licenses and eligibility criteria for accessing the data, if any.
    c. *Information on data files (meta-data)*, including the name(s) and number of files, file size(s), relevant file version(s), and number of variables and observations in each file. Though not required, other relevant information may be included, including a description dataset dictionary, summary statistics, and synthetic data (fake data with the same statistical properties as the original data)
    d. *Estimated costs for access*, including monetary costs such as fees and licences required to access the data, and non-monetary costs such as wait times and specific geographical locations from where researchers need to access the data.  

 - **Adjusted Level 4 (L4\*):** All analysis code is provided, and complete and detailed instructions on how to access the *analysis data* are available.

 - **Adjusted Level 5 (L5\*):** All requirements for Level 4\* are met, and the authors provide a certification that the output can be reproduced from the analysis data (CRA) by a third party. Examples include a signed letter by a disinterested reproducer or an official reproducibility certificate from a certification agency for data and code (e.g., see [cascad](https://www.cascad.tech/)).

 - **Levels 6 and 7** can be applied as described above.

 - **Adjusted Level 8 (L8\*):** All requirements for Level 7\* are met, but instructions for accessing the ***raw data*** are incomplete. Use the instructions described in Level 3 above to assess the instructions' completeness.

 - **Adjusted Level 9 (L9\*):**  All requirements for Level 8\* are met, and instructions for accessing the ***raw data*** are complete.

 - **Adjusted Level 10 (L10\*):** All requirements for Level 9\* are met, and a certification that the output can be reproduced from the raw data is provided.

<table>
<caption>(\#tab:levels-of-computational-reproducibility-adjusted)Levels of Computational Reproducibility with Proprietary/Confidential Data \
 (P denotes "partial", C denotes "complete")</caption>
 <thead>
<tr>
<th style="border-bottom:hidden" colspan="1"></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="10"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Availability of materials, and reproducibility</div></th>
</tr>
<tr>
<th style="border-bottom:hidden" colspan="1"></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Analysis Code</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Instr. Analysis Data</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">CRA</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Cleaning Code</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="2"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">Instr. Raw Data</div></th>
<th style="border-bottom:hidden; padding-bottom:0; padding-left:3px;padding-right:3px;text-align: center; " colspan="1"><div style="border-bottom: 1px solid #ddd; padding-bottom: 5px; ">CRR</div></th>
</tr>
  <tr>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;">   </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;"> P </th>
   <th style="text-align:left;"> C </th>
   <th style="text-align:left;">   </th>
  </tr>
 </thead>
<tbody>
  <tr>
   <td style="text-align:left;border-bottom: 1px solid"> L1: No materials </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L2: Only code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L3: Partial analysis data &amp; code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L4*: All analysis data &amp; code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;border-bottom: 1px solid"> L5*: Proof of third party CRA </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> ✔ </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
   <td style="text-align:left;border-bottom: 1px solid"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L6: Some cleaning code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L7: All cleaning code </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L8*: Some instr. for raw data </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L9*: All instr. for raw data </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> -- </td>
  </tr>
  <tr>
   <td style="text-align:left;"> L10*: Proof of third party CRR </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
   <td style="text-align:left;"> ✔ </td>
  </tr>
</tbody>
</table>
                 Levels of Computational Reproducibility with Proprietary/Confidential Data
                               (P denotes "partial", C denotes "complete")    
      
                                         | Availability of materials, and reproducibility |
                                         |------------------------------------------------|
                                         |        | Instr.  |     |         | Instr.|     |
                                         |Analysis| Analysis|     | Cleaning| Raw   |     |
                                         |Code    | Data    | CRA | Code    | Data  | CRR |
                                         | P | C  | P  | C  |     | P  |  C | P | C |     |
                                         ---------|---------|-----|---------|-------|-----|
        L1: No materials.................| -   -  | -    -  |  -  |  -    - | -   - |  -  |
        ---------------------------------|--------|---------|-----|---------|-------|-----|
        L2: Only code ...................| ✔   ✔  | -    -  |  -  |  -    - | -   - |  -  |
        L3: Partial analysis data & code.| ✔   ✔  | ✔    -  |  -  |  -    - | -   - |  -  |
        L4*: All analysis data & code....| ✔   ✔  | ✔    ✔  |  -  |  -    - | -   - |  -  |
        L5*: Proof of third party CRA....| ✔   ✔  | ✔    ✔  |  ✔  |  -    - | -   - |  -  |
        ---------------------------------|--------|---------|-----|---------|-------|-----|
        L6: Some cleaning code...........| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    - | -   - |  -  |
        L7: All cleaning code............| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | -   - |  -  |
        L8*: Some instr. for raw data....| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   - |  -  |
        L9*: All instr. for raw data.....| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   ✔ |  -  |
        L10*:Proof of third party CRR....| ✔   ✔  | ✔    ✔  |  ✔  |  ✔    ✔ | ✔   ✔ |  ✔  |


### Reproducibility dimensions at the paper level   

In addition to the output-specific assessment and improvement of computational reproducibility, several practices can facilitate reproducibility at the level of the overall paper. You can read about such practices in greater detail in the next chapter, dedicated to Stage 3: *Improvements*. In this  Assessment section, you should only verify whether the original reproduction package made use of any of the following:

- Master script that runs all steps
- Readme file
- Standardized file organization       
- Version control
- Open source (statistical) software  
- Dynamic document        
- Computing capsule (e.g. CodeOcean, Binder, etc.)     

Congratulations! You have now completed the *Assessment* stage of this exercise. You have provided a concrete building block of knowledge to improve understanding of the state of reproducibility in Economics.

Please continue to the [next section](#improvements) where you can help improve it!
