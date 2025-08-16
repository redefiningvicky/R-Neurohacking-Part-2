# 🔬 R Neurohacking Part 2
## 🎯 Objective <br>
This project uses the R programming language and its neuroimaging packages to manipulate, process, and analyze structural brain MRI data in the NIfTI (Neuroimaging Informatics Technology Initiative) format. It focuses on performing inhomogeneity correction, brain extraction, image registration, and visualization to enable comprehensive exploration of neuroimaging data. <p>
## 🛠️ Tools <br>
• <b>Language:</b> R <p>
## 📦 FSL Installation
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

#save 113-01-MPRAGE plot as PNG
png("113-01-MPRAGE_Difference.png", width=800, height=800)
if(any(sub_bias_113_01_MPRAGE != 0)){
  ortho2(
    nim_113_01_MPRAGE,
    sub_bias_113_01_MPRAGE,
    col.y = alpha(fcol1(seq(0,1,length.out=10)), 0.5),
    ybreaks = q1,
    ycolorbar = TRUE,
    text = "113-01-MPRAGE:\nOriginal Minus Bias-Corrected",
    cex = 0.7
  )
} else {
  ortho2(
    nim_113_01_MPRAGE,
    text = "113-01-MPRAGE.nii.gz:\nOriginal Image (No Difference)",
    cex = 0.7
  )
}
dev.off()
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

#save 113-02-MPRAGE plot as PNG
png("113-02-MPRAGE_Difference.png", width=800, height=800)
if(any(sub_bias_113_02_MPRAGE != 0)){
  ortho2(
    nim_113_02_MPRAGE,
    sub_bias_113_02_MPRAGE,
    col.y = alpha(fcol2(seq(0,1,length.out=10)), 0.5),
    ybreaks = q2,
    ycolorbar = TRUE,
    text = "113-02-MPRAGE:\nOriginal Minus Bias-Corrected",
    cex = 0.7
  )
} else {
  ortho2(
    nim_113_02_MPRAGE,
    text = "113-02-MPRAGE.nii.gz:\nOriginal Image (No Difference)",
    cex = 0.7
  )
}
dev.off()
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
