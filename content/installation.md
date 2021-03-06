---
author: Gabriel Carrasco and Antony Barja
date: "2019-03-10"
description: Installation of rgee step by step in the differents Operative System
tags:
  - installation
title: Installation of rgee
---

In this section, you're going to learn to how to install rgee step by step for different Operating Systems. Remember it's necessary to have previously installed R, Rtools, and Rstudio in your desktop.

---

<img src="https://user-images.githubusercontent.com/23284899/151858857-e98d6216-73be-4ffd-a95e-0b93fedbc0df.png" width="25px" align="center"><b> Information:</b>

- _Rtools is only necessary for Windows OS users. You can download Rtools [here 📥.](https://cran.r-project.org/bin/windows/Rtools/rtools40.html)_

---

</br>

### 🔴 **1. Installation on a Linux distribution**

For a distribution like **Ubuntu** and its derivatives, you must have set up and installed some dependencies of spatial libs in your Operative System. The following bash commands should install key geographic R packages on **Ubuntu 20.10**.

```
# install system dependencies:
sudo apt install libudunits2-dev libgdal-dev libgeos-dev libproj-dev libfontconfig1-dev libjq-dev libprotobuf-dev protobuf-compiler

# binary versions of key R packages:
sudo apt install r-cran-rgee r-cran-geojsonio
```

For a distribution like **Manajaro, Archilinux or derivatives**, the installation uses the following bash commands

```
# install system dependencies:
sudo pacman -S gcc-fortan gdal proj geos
git clone https://aur.acrhlinux.org/udunits.git
cd udunits
makepkg -si
```

```
# Starting with R
R
# Installation of rgee and geojsonio:
install.packages("rgee")
install.packages("geojsonio")
```

**rgee set up and registration of credentials**

rgee depends on the Python packages **numpy** and **ee** for its installation. There are two methods for this, and we will explain the most recommended way for new users without experience handling the Python virtual environment.

For the installation of rgee dependencies, use the following function (this function can only be used once):

```{r, eval = FALSE}
rgee::ee_install()
```

<center>
 <video controls width="100%">
    <source src="https://user-images.githubusercontent.com/23284899/151856231-345773f5-fb60-4b4d-a584-d6c532ad1aa4.mp4">
 </video>
</center>

After the installation of the rgee dependencies, you need to have a registered account on [Google Earth Engine](https://earthengine.google.com/).

<img src="https://user-images.githubusercontent.com/23284899/151848117-90f4dcfc-13cb-413c-9802-0207e84f2c9f.png" width="25px" align="center"><b> Observation:</b>

- _To register on Google Earth Engine, you only need a gmail account and to answer a few short questions._

---

Finally, with your verified gmail account, you can authenticate and initialize the Earth Engine R API.

<center>
 <video controls width="100%">
    <source src="https://user-images.githubusercontent.com/23284899/151863010-c37708a5-a23c-4cb3-a7ab-7fe1daeea3c5.mp4">
 </video>
</center>
<br>

### 🔴 **2. Installation on Windows**

On windows, the rgee installation is accessible, but you need to have **miniconda** or **anaconda** previously installed. To use the rgee package, you must have **python3** installed.
For a perfect installation on Windows, activate the reticulate library in your R session, and then activate rgee.

```{r,eval = FALSE}
# Installation of rgee and geojsonio:
install.packages("rgee")
install.packages("geojsonio")
```

```{r,eval = FALSE}
# Activation of packages:
library(rgee)
library(reticulate)
```

The <mark style="background-color: blue;color:white;">py_discover_config()</mark> function of the reticulate package will allow you to know which version of python will be used for the installation of **numpy** and **ee** libraries.

```
> py_discover_config()
python:         C:/Users/Windows 10/anaconda3/python.exe
libpython:      C:/Users/Windows 10/anaconda3/python39.dll
pythonhome:     C:/Users/Windows 10/anaconda3
version:        3.9.7 (default, Sep 16 2021, 16:59:28) [MSC v.1916 64 bit (AMD64)]
Architecture:   64bit
numpy:          C:/Users/Windows 10/anaconda3/Lib/site-packages/numpy
numpy_version:  1.20.3
```

---

<img src="https://user-images.githubusercontent.com/23284899/151858857-e98d6216-73be-4ffd-a95e-0b93fedbc0df.png" width="25px" align="center"><b> Information:</b>

- The function <mark style="background-color: blue;color:white;">py_config()</mark> we allow list all version of python discovered in our System.

---

After identifying the python version, the next step is to set the path for the new Python environment for rgee, for this you can use the following function <mark style="background-color: blue;color:white;">use_python("PUT-HERE-THE-PYTHON3-VERSION-PATH")</mark>

```
use_python("C:/Users/Windows 10/anaconda3/python.exe")
```

You can verify the selection of python to work with rgee.

```
> py_config()
python:         C:/Users/Windows 10/anaconda3/python.exe
libpython:      C:/Users/Windows 10/anaconda3/python39.dll
pythonhome:     C:/Users/Windows 10/anaconda3
version:        3.9.7 (default, Sep 16 2021, 16:59:28) [MSC v.1916 64 bit (AMD64)]
Architecture:   64bit
numpy:          C:/Users/Windows 10/anaconda3/Lib/site-packages/numpy
numpy_version:  1.20.3
ee:             [NOT FOUND]
NOTE: Python version was forced by use_python function
```

Finally, we set up our rgee environment, install the necessary python dependencies.

<center>
<img src="https://user-images.githubusercontent.com/23284899/151891145-20fe5dab-3515-47f6-ade3-ca5891931b49.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/151892441-1ed646ea-763a-4ac4-98cb-6750a07934bc.png" width="100%">
</center>
<br>

Then initialize Google Earth Engine from R and save your credentials.

```
ee_Initialize("GMAIL_ACCOUNT",drive = TRUE)
```

<center>
<img src="https://user-images.githubusercontent.com/23284899/151892339-0b02eddb-4ce9-451e-bf82-7f7a43c09022.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/151892817-4a2f05cb-ed2d-4f89-86fe-d7691439e818.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152574104-afb0e2d6-ae9c-4db6-b229-404d4b572def.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152574130-b394f43a-8cf2-48f4-b61f-8587fd170a3b.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152574150-58118849-5f34-46c0-96ef-6ce182f9407d.png" width="100%">
</center>
<br>

### 🔴 **3. Instalacion on Mac OS**

Installation on Mac OS is very similar to a GNU/Linux distribution. In the following code section, you'll find the codes and some screenshots of some key points to consider.

---

<img src="https://user-images.githubusercontent.com/23284899/151858857-e98d6216-73be-4ffd-a95e-0b93fedbc0df.png" width="25px" align="left"><b> Information:</b>

- For Mac OS it is recommended to work with the development version of rgee.

```
library(remotes)
install_github("r-spatial/rgee")
```

---

```{r, eval=FALSE}
# Installation of rgee and geojsonio:
install.packages("sf")
install.packages("geojsonio")
```

```{r, eval = FALSE}
# Installation of Python dependence libraries:
rgee::ee_install()
```

<center>
<img src="https://user-images.githubusercontent.com/23284899/152569835-3f2841fb-e889-459c-927d-6d8288e5633f.png " width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152569946-5c264487-b132-4e8a-af37-8e2dfb5434dc.png" width="100%">
</center>
<br>

Initialize Google Earth Engine from R and save your credentials.

```
ee_Initialize("GMAIL_ACCOUNT",drive = TRUE)
```

<center>
<img src="https://user-images.githubusercontent.com/23284899/152569973-c55e9633-6b7a-4217-ad7f-c9a9d056e9ad.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152569999-0f29eeb6-6bb7-4193-9e98-47a4fa1933cf.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152570037-1e6b30cb-4db6-4955-9346-576c06f51a2d.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152570558-23ba8513-a956-4b78-8a8a-2c445272dbcf.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152570578-87421f32-638a-4be9-a658-bb6dffbe2d69.png" width="100%">
</center>
<br>

### 🔴 **4. Additional packages**

```{r , eval=FALSE}
pkgs <- c("tmap","mapview","ggspatial","viridis","raster","sf",
          "stars","geojsonio","tidyverse","patchwork","lubridate")
install.packages(pkgs)
```

- tmap: <https://github.com/r-tmap/tmap>

- mapview: <https://github.com/r-spatial/mapview>

- ggspatial: <https://github.com/paleolimbot/ggspatial>

- viridis: <https://github.com/sjmgarnier/viridis>

- raster: <https://github.com/rspatial/raster>

- sf: <https://github.com/r-spatial/sf>

- stars: <https://github.com/r-spatial/stars>

- geojsonio: <https://github.com/ropensci/geojsonio>

- tidyverse: <https://github.com/tidyverse/tidyverse>

- patchwork: <https://github.com/thomasp85/patchwork>

- lubridate: <https://github.com/tidyverse/lubridate>
