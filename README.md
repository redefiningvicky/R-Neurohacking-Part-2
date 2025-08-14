# 🔬 R Neurohacking Part 2
## 🎯 Objective <br>
This project uses the R programming language and its neuroimaging packages to manipulate, process, and analyze structural brain MRI data in the NIfTI (Neuroimaging Informatics Technology Initiative) format. It focuses on performing inhomogeneity correction, brain extraction, image registration, and visualization to enable comprehensive exploration of neuroimaging data. <p>
## 🛠️ Tools <br>
• <b>Language:</b> R <p>
## 📦 FSLR Installation
## Windows PowerShell
```
 wsl --update
 wsl --shutdown
 wsl --set-default-version 2
 wsl --install -d Ubuntu-22.04
```

# Ubuntu
```
sudo apt update
sudo apt -y upgrade
sudo apt-get install dc python3 bzip2 mesa-utils gedit firefox libgomp1

sudo apt update && sudo apt install bzip2

curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s

curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s -- ~/fsl/ --extra truenet

curl -Ls https://fsl.fmrib.ox.ac.uk/fsldownloads/fslconda/releases/getfsl.sh | sh -s -- ~/fsl/ --extra osl-dynamics
```
