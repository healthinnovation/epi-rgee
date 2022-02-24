---
author: Gabriel Carrasco y Antony Barja
date: "2019-03-10"
description: rgeeExtra a complement package of rgee
tags:
  - rgeeExtra
title: rgee + rgeeExtra
---

In this post, you going to learn how to integrate rgeeExtra with rgee. The philosophy of rgeeExtra is to make availablea functional programming type, more friendly with R users, also rgee extends the following Earth Engine classes:

- **ee.Feature**
- **ee.FeatureCollection**
- **ee.Geometry**
- **ee.Image**
- **ee.ImageCollection**

In this we will calculate the Normalized Difference Vegetation Index, (NDVI) from a Landsat 8 image.

---

<img src="https://user-images.githubusercontent.com/23284899/151858857-e98d6216-73be-4ffd-a95e-0b93fedbc0df.png" width="25px" align="center"><b> Information:</b>

- _`rgeeExtra` due is official in CRAN, but you can install using the `remote` package_.
- For this section is neccesary to hace install `rgee`, `rgeeExtra`,`sf` ,`cptcity` and `tidyverse`

---

#### 1. Requeriments

```{r, eval = FALSE}
remotes::install_github("r-earthengine/rgeeExtra")
library(tidyverse)
library(rgee)
library(rgeeExtra)
library(sf)
library(cptcity)
ee_Initialize()
```

```
> ee_Initialize()
── rgee 1.1.2 ──────────────────── earthengine-api 0.1.292 ──
 ✓ user: not_defined
 ✓ Initializing Google Earth Engine:  DONE!
 ✓ Earth Engine account: users/ambarja
─────────────────────────────────────────────────────────────
```

#### 2. Vector layer reading of our study area

```{r, eval = FALSE}
hcyo <- st_read(
  "https://github.com/ambarja/gpkg-pe/raw/main/prov_huancayo.gpkg",
  quiet = TRUE) %>%
  summarise()
```

#### 3. Cooking with dataset with rgee

```{r, eval = FALSE}
landsat <-ee$ImageCollection("LANDSAT/LC08/C02/T1_TOA")$
  select(sprintf("B%s",c(1:7)))$
  filterDate("2021-01-01","2021-12-31")$
  filterBounds(hcyo_ee)$
  filterMetadata("CLOUD_COVER","less_than",30)$
  first()$
  clip(hcyo_ee)
```

#### 4. Calculate of NDVI index with rgee

```{r, eval = FALSE}
ndvi <- landsat$
  normalizedDifference(c("B5", "B4"))
```

#### 5. Indentifying min and max value of index

```{r, eval = FALSE}
(minmax <- ndvi$reduceRegion(
  reducer = ee$Reducer$minMax(),
  geometry = hcyo_ee,
  scale = 1000)$
    getInfo()
    )
```

```
$nd_max
[1] 0.7902563
$nd_min
[1] -0.07480448
```

##### 6. Parameter of visualization

```{r, eval = FALSE}
viz <- list(
  min = -0.08,
  max = 0.63,
  palette = cpt("grass_ndvi")
)
Map$centerObject(ndvi,zoom=9)
```

##### 7. NDVI map wih rgee

```
m1 <- Map$addLayer(ndvi,visParams = viz) +
  Map$addLegend(visParams = viz,name = "ndvi")
```

##### 8. Calculate of NDVI index with rgeeExtra

```{r, eval = FALSE}
ndvi <- (landsat[["B5"]] - landsat[["B4"]])/(landsat[["B5"]] + landsat[["B4"]])
```

##### 9. NDVI map wih rgeeExtra

```
m2 <- Map$addLayer(ndvi,visParams = viz) +
  Map$addLegend(visParams = viz,name = "ndvi_ee")
```

#### 10. Two map in only display

```{r, eval = FALSE}
m1 | m2
```

<center>
   <img src="https://user-images.githubusercontent.com/23284899/152658877-b36596da-0e7c-4853-9ee8-8e8f05e21f80.png" width="100%">
</center>
