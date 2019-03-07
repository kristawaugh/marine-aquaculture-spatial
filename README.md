
[![Build Status](https://travis-ci.com/espm-157/2018-spatial-spatial_zexuan_krista.svg?token=TJpEEbz7PiUQtcZQe2Sj&branch=master)](https://travis-ci.com/espm-157/2018-spatial-spatial_zexuan_krista)

## Team Members:

- Zexuan Zhao, @ZexuanZhao
- Krista Waugh, @kristawaugh



## Assignment

In this report, we will analysize sea surface temperature, net primary productivity, and marine protected areas along the west coast of the United States to map potential areas of marine aquaculture for the Pacific spiny Lumpsucker (Eumicrotremus orbis). Our conclusion of the study is that the majority of Pacific spiny Lumpsuckers can be found off the coast of the California and Oregon border, with populations spanning the coast of California all the way down to Los Angeles, where there is another large population. 

Here is our [spatial assignment](https://github.com/espm-157/2018-spatial-spatial_zexuan_krista/blob/master/spatial/spatial-assignment.md)

## Special files

All team repositories will also include most of the special files found here:

### Common files

- `README.md` this file, a general overview of the repository in markdown format.  
- `.gitignore` Optional file, ignore common file types we don't want to accidentally commit to GitHub. Most projects should use this. 
- `<REPO-NAME>.Rproj` Optional, an R-Project file created by RStudio for it's own configuration.  Some people prefer to `.gitignore` this file.


### Infrastructure for Testing

- `.travis.yml`: A configuration file for automatically running [continuous integration](https://travis-ci.com) checks to verify reproducibility of all `.Rmd` notebooks in the repo.  If all `.Rmd` notebooks can render successfully, the "Build Status" badge above will be green (`build success`), otherwise it will be red (`build failure`).  
- `DESCRIPTION` a metadata file for the repository, based on the R package standard. It's main purpose here is as a place to list any additional R packages/libraries needed for any of the `.Rmd` files to run.
- `tests/render_rmds.R` an R script that is run to execute the above described tests, rendering all `.Rmd` notebooks. 




