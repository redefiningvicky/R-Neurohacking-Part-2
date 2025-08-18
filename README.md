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
pkgbuild::check_build_tools(debug = TRUE)
```
remotes::install_github("stnava/ANTsRCore")
library(ANTsRCore)
```
### 01 MPRAGE Mean
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113-01-MPRAGE_Mean.png" width="300" />

```
#compute mean
mean_val_113_01_MPRAGE <- mean(nim_113_01_MPRAGE)
mean_text_113_01_MPRAGE <- paste0("113-01-MPRAGE.nii.gz Mean: ", round(mean_val_113_01_MPRAGE, 2))
```

### 02 MPRAGE Mean
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113-02-MPRAGE_Mean.png" width="300" />

```
#compute mean
mean_val_113_02_MPRAGE <- mean(nim_113_02_MPRAGE)
mean_text_113_02_MPRAGE <- paste0("113-02-MPRAGE.nii.gz Mean: ", round(mean_val_113_02_MPRAGE, 2))
```
### 01 MPRAGE Difference
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113-01-MPRAGE_Difference.png" width="400" />

```
#diverging color palettes
fcol1 <- div_gradient_pal(low="blue", mid="yellow", high="red")
fcol2 <- div_gradient_pal(low="blue", mid="yellow", high="red")

#113-01-MPRAGE difference image
sub_bias_113_01_MPRAGE <- nim_113_01_MPRAGE - fast_img_113_01_MPRAGE
q1 <- quantile(sub_bias_113_01_MPRAGE[sub_bias_113_01_MPRAGE != 0], probs = seq(0,1,by=0.1))
```
### 02 MPRAGE Difference
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113-02-MPRAGE_Difference.png" width="400" />

```
#diverging color palettes
fcol1 <- div_gradient_pal(low="blue", mid="yellow", high="red")
fcol2 <- div_gradient_pal(low="blue", mid="yellow", high="red")

#113-02-MPRAGE difference image
sub_bias_113_02_MPRAGE <- nim_113_02_MPRAGE - fast_img_113_02_MPRAGE
q2 <- quantile(sub_bias_113_02_MPRAGE[sub_bias_113_02_MPRAGE != 0], probs = seq(0,1,by=0.1))
```
### 01 MPRAGE Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113_01_MPRAGE_Slices_01_22_Histogram.png" width="750" />

```
#slices to plot
slices_01_22 <- 1:22

#113-01-MPRAGE histogram slices 01-22
vals_113_01_MPRAGE <- lapply(slices_01_22, function(x) {
  data.frame(
    Original = c(nim_113_01_MPRAGE[,,x]),
    BiasCorrected = c(fast_img_113_01_MPRAGE[,,x]),
    slice = x
  )
})
vals_113_01_MPRAGE <- do.call(rbind, vals_113_01_MPRAGE)
v_113_01_MPRAGE <- melt(vals_113_01_MPRAGE, id.vars="slice", variable.name="ImageType", value.name="Value")
```
### 02 MPRAGE Histogram
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/394becd7dc384856c0a6b971c2237026b922f682/R_Neurohacking_Results_Part_14/113_02_MPRAGE_Slices_01_22_Histogram.png" width="750" />

```
#slices to plot
slices_01_22 <- 1:22

#113-02-MPRAGE histogram slices 01-22
vals_113_02_MPRAGE <- lapply(slices_01_22, function(x) {
  data.frame(
    Original = c(nim_113_02_MPRAGE[,,x]),
    BiasCorrected = c(fast_img_113_02_MPRAGE[,,x]),
    slice = x
  )
})
vals_113_02_MPRAGE <- do.call(rbind, vals_113_02_MPRAGE)
v_113_02_MPRAGE <- melt(vals_113_02_MPRAGE, id.vars="slice", variable.name="ImageType", value.name="Value")
```
### 01 MPRAGE Original
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/b8e02f3c818a545571870cdec0270d646722a4ba/R_Neurohacking_Results_Part_15/113_01_MPRAGE_Original.png" width="400" />

```
#read original 113-01-MPRAGE.nii.gz
nim_113_01_MPRAGE <- readNIfTI(win_file_113_01_MPRAGE)

#read extracted brain 113-01-MPRAGE.nii.gz
bet_fast_113_01_MPRAGE <- readNIfTI(win_file_113_01_MPRAGE, reorient=FALSE)
```
### 01 MPRAGE BET Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/b8e02f3c818a545571870cdec0270d646722a4ba/R_Neurohacking_Results_Part_15/113_01_MPRAGE_BET_Overlay.png" width="400" />

```
#read original images 113-01-MPRAGE.nii.gz
fast_img_113_01_MPRAGE <- readNIfTI(win_file_113_01_MPRAGE, reorient=FALSE)

#create masks 113-01-MPRAGE.nii.gz
bet_fast_mask_113_01_MPRAGE <- bet_fast_113_01_MPRAGE
bet_fast_mask_113_01_MPRAGE[bet_fast_113_01_MPRAGE <= 0] <- NA
```
### 02 MPRAGE Original
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/b8e02f3c818a545571870cdec0270d646722a4ba/R_Neurohacking_Results_Part_15/113_02_MPRAGE_Original.png" width="400" />

```
#read original 113-02-MPRAGE.nii.gz
nim_113_02_MPRAGE <- readNIfTI(win_file_113_02_MPRAGE)

#read extracted brain 113-02-MPRAGE.nii.gz
bet_fast_113_02_MPRAGE <- readNIfTI(win_file_113_02_MPRAGE, reorient=FALSE)
```
### 02 MPRAGE BET Overlay
<img src="https://github.com/redefiningvicky/R-Neurohacking-Part-2/blob/b8e02f3c818a545571870cdec0270d646722a4ba/R_Neurohacking_Results_Part_15/113_02_MPRAGE_BET_Overlay.png" width="400" />

```
#read original images 113-02-MPRAGE.nii.gz
fast_img_113_02_MPRAGE <- readNIfTI(win_file_113_02_MPRAGE, reorient=FALSE)

#create masks 113-02-MPRAGE.nii.gz
bet_fast_mask_113_02_MPRAGE <- bet_fast_113_02_MPRAGE
bet_fast_mask_113_02_MPRAGE[bet_fast_113_02_MPRAGE <= 0] <- NA
```
