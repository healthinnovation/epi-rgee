---
author: Gabriel Carrasco y Antony Barja
date: "2019-03-10"
description: Installation of rgee step by step in the differents Operative System
tags:
- installation
title: Installation of rgee 
---

In this post, you going to learn to install rgee in the different Operative Systems steps by steps. Remind is necessary to have previously install R, Rtools and Rstudio in your desktop, here in the following video show the steps to be taken for a proper installation. 

---
<img src="https://user-images.githubusercontent.com/23284899/151858857-e98d6216-73be-4ffd-a95e-0b93fedbc0df.png" width="25px" align="center"><b> Information:</b>
- *Rtools only is necesarry for the Operative Systen Windows.*
---

<center><iframe width="90%" height="350" src="https://www.youtube.com/embed/h2IPWVXaUuU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe></center>

</br>

### 🔴 **1. rgee in a Linux distribution**

For a distribution like **Ubuntu** and theirs derivatives is necesarry to have set-up and installed some dependences of spatial libs our Operative System. The following bash commands should install key geographic R packages on **Ubuntu 20.10**.

```
# install system dependencies:
sudo apt install libudunits2-dev libgdal-dev libgeos-dev libproj-dev libfontconfig1-dev libjq-dev libprotobuf-dev protobuf-compiler

# binary versions of key R packages:
sudo apt install r-cran-rgee r-cran-geojsonio
```

For a distribution like **Manajaro, Archilinux o derivatives**, the installation is using the following bash commands

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

**Set-up of rgee and register of credentiales**

rgee depends on the Python packages **numpy** and **ee**, for its installation there are two methods, however we have used the most recommended way for new users without experience in handling the Python virtual environment.   

For the installation of rgee dependences use for once only, the following function:

````{r, eval = FALSE}
rgee::install_ee()
````
<center>
 <video controls width="100%">
    <source src="https://user-images.githubusercontent.com/23284899/151856231-345773f5-fb60-4b4d-a584-d6c532ad1aa4.mp4">
 </video>
</center>

After of the installation of the rgee dependences is necessary to have a registered acount on [Google Earth Engine]().

---
<img src="https://user-images.githubusercontent.com/23284899/151848117-90f4dcfc-13cb-413c-9802-0207e84f2c9f.png" width="25px" align="center"><b> Observation:</b>
- *For register on Google Earth Engine only is necesarry to have a acount of gmail and answer short questions.*
---

Finally with your acount of gmail registered, you can authenticate and initialize in the Earth Engine R API.

<center>
 <video controls width="100%">
    <source src="https://user-images.githubusercontent.com/23284899/151863010-c37708a5-a23c-4cb3-a7ab-7fe1daeea3c5.mp4">
 </video>
</center>
<br>

### 🔴 **2. Instalacion on Windows**

On windows the installation of rgee is accessible, but you need to have installed **miniconda** or **anaconda**, remind that rgee uses **python3**.
For a perfect installation on Windows is necessary activate the reticulate library in your R sesion together rgee.


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

The <mark style="background-color: blue;color:white;">py_discover_config()</mark> function of reticulate package we allow to know the version of python that will to be used for the installation of Packages **numpy** and **ee**.


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

Having identified the python version, the next step is to set the path as the new Python environment for rgee, for this we use the following function <mark style="background-color: blue;color:white;">use_python("PUT-HERE-THE-PYTHON3-VERSION-PATH")<mark>

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

Finally, we set up our rgee environment, install the necessary python dependencies, then initialise Google Earth Engine from R and save our credentials.

<center>
<img src="https://user-images.githubusercontent.com/23284899/151891145-20fe5dab-3515-47f6-ade3-ca5891931b49.png" width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/151892441-1ed646ea-763a-4ac4-98cb-6750a07934bc.png" width="100%">
</center>
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

### 🔴 **2. Instalacion on Mac OS**

Installation on Mac OS is very similar to a GNU/Linux distribution, in the following code section, we share the codes and some screenshots of some key points to consider.

```{r, eval=FALSE}
# Installation of rgee and geojsonio:
install.packages("sf")
install.packages("geojsonio")
```
````{r, eval = FALSE}
# Installation of Python dependence libraries:
rgee::install_ee()
````
<center>
<img src="https://user-images.githubusercontent.com/23284899/152569835-3f2841fb-e889-459c-927d-6d8288e5633f.png " width="100%">
</center>
<center>
<img src="https://user-images.githubusercontent.com/23284899/152569946-5c264487-b132-4e8a-af37-8e2dfb5434dc.png" width="100%">
</center>
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