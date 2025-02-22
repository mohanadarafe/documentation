LivingPark is a collection of Jupyter notebooks that reproduce published
MRI measures of Parkinson's Disease. It also contains tools to work with
data from the Parkinson's Progression Markers Initiative
([PPMI](https://www.ppmi-info.org/)). A (very) brief introduction to
LivingPark is available
[here](https://docs.google.com/presentation/d/1PqyRLhB9PoqW2UCnvVX8CuqEW2TfPiECQlMEheeiorg/edit#slide=id.g12ed72e6175_0_106).

# How to write Jupyter Notebooks that use PPMI data

We are currently working on reproducing MRI measures using the PPMI dataset. 
The main contributions are expected to be in the form of Jupyter Notebooks
using PPMI data. However, PPMI's Data Usage Agreement prevents us from sharing
patient ids or any other individual-level data. Therefore, notebooks should 
follow the following practices:


* DON'T include any PPMI data or metadata with your notebook. Instead, your notebook 
should download data from the PPMI website directly. We are developping a [Python
API](https://github.com/LivingPark-MRI/ppmi-scraper) to help with this
step. Be careful not to commit your PPMI login/password!

* DON'T display individual-level data or patient ids in your notebook.
If you need to display data, make sure to represent aggregate measures
such as histograms or counts. Check Pandas' `hist` and `group_by` functions!

* DON'T use "magic files" that can't be retrieved from the PPMI database or 
created by another notebook. If you do so, nobody will be able to run your notebook.

* DON'T commit your PPMI login or password with your notebook. We'll soon update the API 
to prevent this. 

* DO "Restart and Run all" your notebook before committing it.

* DO save important files produced by your notebook, so that other notebooks could start from them 
  after running your notebook.
  
* DO make random selections when building a cohort using a random seed and sort the dataframe in order to keep reproducing the same cohort.

# How to build a PPMI cohort

The first step to reproduce a published paper is to reproduce a cohort with
similar clinical, behavioral and demographics variables. PPMI contains a
number of metadata files to retrieve these variables, accessible from the
["Study Data"](https://ida.loni.usc.edu/pages/access/studyData.jsp) page.
This page also includes a Data Dictionary and a Code List to help interpreting 
the variables. 

LivingPark's [PPMI API](https://github.com/LivingPark-MRI/ppmi-scraper)
will allow your notebooks to download these metadata files.

LivingPark also contains notebooks to clean variables (remove mistakes,
impute missing data, etc), which produce the following files:
| Filename | Produced by | Contains |
|----------|-------------|----------|
| `MRI_info.csv` | [ppmi-MRI-metadata](https://github.com/LivingPark-MRI/ppmi-MRI-metadata) | 3D T1-weighted images by visit |
| `MDS_UPDRS_Part_III_clean.csv` | [ppmi-treatment-and-on-off-status](https://github.com/LivingPark-MRI/ppmi-treatment-and-on-off-status) | Cleaned-up PDSTATE and PDTRTMNT|

Your cohort-building notebooks should start from these files rather than redoing similar cleanups.
