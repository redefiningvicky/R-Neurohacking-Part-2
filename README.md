# 🔬 R Neurohacking Part 2
## 🎯 Objective <br>
This project uses the R programming language and its neuroimaging packages to manipulate, process, and analyze structural brain MRI data in the NIfTI (Neuroimaging Informatics Technology Initiative) format. It focuses on performing inhomogeneity correction, brain extraction, image registration, and visualization to enable comprehensive exploration of neuroimaging data. <p>
## 🛠️ Tools <br>
• <b>Language:</b> R <p>
## 📦 FSL Installation for Windows
### Windows PowerShell
```
 wsl --update
 wsl --shutdown
 wsl --set-default-version 2
 wsl --install -d Ubuntu-22.04
```

### Ubuntu
```
sudo apt update
sudo apt -y upgrade
sudo apt-get install dc python3 bzip2 mesa-utils gedit firefox libgomp1
```
```
sudo apt update && sudo apt install bzip2
```
```
curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s
```
```
curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s -- ~/fsl/ --extra truenet
```
```
curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s -- ~/fsl/ --extra osl-dynamics
```

### WSL
```
sudo apt install r-base
```
## 📦 ANTsR Installation in R
```
install.packages("remotes")
remotes::install_github("stnava/ANTsR")
library(ANTsR)
```
## 📦 ANTsR Installation in R
```
install.packages("remotes")
remotes::install_github("stnava/ANTsR")
library(ANTsR)
```
## 📦 ANTsRCore Installation in R
This is an alternative to ANTsR if there are errors for Window installation. 
```
remotes::install_github("stnava/ANTsRCore")
library(ANTsRCore)
```
## 📦 RTools Installation and Compile ANTsRCore
This is an alternative to ANTsRCore Installation in R if there are failures from Github.
```
https://cran.r-project.org/bin/windows/Rtools/
```
```
pkgbuild::check_build_tools(debug = TRUE)
```
```
remotes::install_github("stnava/ANTsRCore")
```
```
devtools::install_github("ANTsX/ANTsRCore")
```
```
library(ANTsRCore)
```
```
Sys.setenv(R_REMOTES_NO_ERRORS_FROM_WARNINGS = "true")
devtools::install_github("ANTsX/ANTsRCore", build_vignettes = FALSE, INSTALL_opts="--no-multiarch")
```
