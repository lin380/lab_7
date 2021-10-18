# Lab 7: 

<!-- NOTE: 
You can preview this README.md document by clicking the 'Preview' button in the RStudio toolbar. 
-->

## Preparation

- Read/ annotate: [Recipe \#7](https://lin380.github.io/tadr/articles/recipe_7.html). You can refer back to this document to help you at any point during this lab activity.
- Note: do your best to employ what you've learned and use other existing resources (R documentation, web searches, etc.).

## Objectives

- Gain experience working with coding strategies reshaping data using tidyverse functions and regular expressions.
- Practice reading/ writing data from/ to disk
- Implement organizational strategies for organizing and documenting a dataset in reproducible fashion.

## Instructions

### Setup

1. Create a new R Markdown document. Title it "Lab 7" and provide add your name as the author. 
2. Edit the front matter to have rendered R Markdown documents print pretty tabular datasets.
3. Delete all the material below the front matter.
4. Add a code chunk directly below the header named 'setup' and add the code to load the following packages and any others you end up using in this lab report. Add `message=FALSE` to this code chunk to suppress messages. 
  - tidyverse
  - readtext
  - tidytext
  - also include `source()` to source the `functions/functions.R` file

### Tasks

1. Create two level-1 header sections named: "Overview" and "Tasks". 
2. Under "Tasks" create four level-2 header sections named: "Orientation", "Tidy the data", "Write the dataset", and "Documentation".
3. Follow the instructions that follow adding the relevant prose description and code chunks to the corresponding sections.
  - **Make sure to provide descriptions of your steps between code chunks and code comments within the code chunks!**

#### Orientation

- Read information about the [ACTIV-ES Corpus](https://github.com/francojc/activ-es)
- Quick description of the `plain` data
- View one or two of the `.run` files in the `data/original/actives/` directory
- Propose an idealized tidy dataset structure (use `tribble()` function) where the unit of analysis is 'sentence'.

#### Tidy the dataset

- Read the `.run` corpus files into the R session using the `readtext()` function. 
- Inspect and provide a prose description of the structure of the resulting object.

**Metadata**

- Curate the metadata found in the `doc_id` column of the data frame. Use the `separate()` function to segment the values found in `doc_id` by underscores `_` into seven new columns corresponding to the metadata found in each.
  - Preview the dataset structure to ensure that the process was successful.
- Next, clean the `title` and `imbd_id` columns:
  - `title` contains hyphens `-`. Replace all the hyphens with a whitespace. You will most likely use the `mutate()` function to create a new column (overwriting the existing column) and the `str_replace_all()` function to find the hyphens and replace them with whitespace.
  - `imdb_id` contains a trailing `.run` on each of the ids. Remove this information leaving only the imdb ID. Again use `mutate()` to overwrite the existing `imdb_id` column and use the `str_remove()` function to remove the `.run` characters. (Note: you will need to escape the `.` as it has a special meaning in regular expressions!)
  - Preview the dataset structure to ensure that the process was successful.

**Text**

- Curate the `text` column by segmenting the individual TV/ Movie transcripts into sentences. You will use the `unnest_tokens()` function from the tidytext package.
  - Specify the input and output columns, use the `token = 'sentences'` argument-value to segment the text into sentences, and include the argument-value `to_lower = FALSE` to avoid lowercasing the text in the output.
  - Preview the dataset structure to ensure that the process was successful.
- Inspect the overall structure of the dataset using `glimpse()`. Report the number of columns (i.e. sentences) contained in the curated dataset. 

#### Write the dataset

- Write the curated dataset to disk as a `.csv` file. Add this file to the `data/derived/actives/` directory.
  - Note you will need to create a subdirectory (`data/derived/actives/`) using the `fs::dir_create()` function.

You can add a preview of the structure of the `data/derived/` directory using the following code inside a code chunk. 

```r
fs::dir_tree("data/derived/")
```

#### Document

- Use the `data_dic_starter()` function that was sourced from the `functions/functions.R` file to create the starter documentation file. Be sure to name your documentation file so that it is clear that this data dictionary file corresponds to the curated dataset you've just created.
- Download the starter documentation `.csv` file from RStudio Cloud to your computer and edit this `.csv` file in a spreadsheet software (such as MS Excel or Apple Numbers) adding the relevant documentation information.
- After updating this `.csv` file in spreadsheet software save it as a `.csv` and upload it to RStudio Cloud, overwriting the original starter documentation.
- Read the updated documentation `.csv` file and print the table structure to your R Markdown output. 

#### Overview

Now that you have conducted the steps to curate and document the ACTIVE-ES corpus files, provide a prose overview of what the goals of this script are and resulting data structure and files created.

### Assessment

Add a level-1 section which describes your learning in this lab.

Some questions to consider: 

  - What did you learn?
  - What was most/ least challenging?
  - What resources did you consult? 
  - What more would you like to know about?

## Submission

1. To prepare your lab report for submission on Canvas you will need to Knit your R Markdown document to PDF or Word. 
  - Note since the data/ dataset in this lab includes accented characters (Spanish), you will need to change the latex engine if you knit this document to a PDF file. To do this use the RStudio shortcut button to the 'Output options...' and select format output 'PDF', then select 'Advanced' and choose 'xelatex' as the latex engine.
2. Download this file to your computer.
3. Go to the Canvas submission page for Lab #7 and submit your PDF/Word document as a 'File Upload'. Add any comments you would like to pass on to me about the lab in the 'Comments...' box in Canvas.
