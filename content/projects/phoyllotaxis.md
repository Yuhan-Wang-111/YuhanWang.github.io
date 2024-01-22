---
title : 'TDA on Phoyllotaxis'
# date : 2024-01-14T21:36:42-05:00
draft : false
summary: "Apply Topological Data Analysis on the study of Phyllotaxis plant patterns in Prof. Christophe Golé's lab"
description: "Apply Topological Data Analysis on the study of Phyllotaxis plant patterns in Prof. Christophe Golé's lab"
tags: ["plant","Topological Data Analysis","visual","research","interdisciplinary"]
cover:
  image: /img/projects/phyllotaxis/hexagons.png
  alt: Heatmap from TDA results
  hidden: false
author: ["Summer 2023 - now"]
hideMeta: false
weight: 35
---
## Overview
This project is the part that I was mostly involved in as a research assistant in Prof. Christophe Golé's Phyllotaxis Plant lab. Phyllotaxis is the arrangement of plant organs on a stem, and we are studying the Fibonacci ones from the Quasi Symmtery ones, the latter being more irregular. By applying topological data analysis on phyllotaxis, we can measure and quantify the irregularity of both kinds.

This is an example species,and how we unroll the plant, generate triangulation of the points to output the data for analyisis.
{{< figure width="800" alt="plant example and its unrolled data" src=/img/projects/phyllotaxis/tripetala.png >}}

Apart from real plant data, we also have a Python simulation model, a disk stacking model, that systematically represent plants growth and the pattern transformation. As disk stacking implies, we use disks to represent the points in the plant, and created the ideal situation where all the points are equally distributed, attaching to each other. The model will take in uv coordinates, which represent points in a hexagon. The model represents the mathematical theory that Prof. Golé's proposed to represent conditions that will prompt plant models to have Fibonacci phyllotaxis or Quasi-symmetry phyllotaxis.

---
## Topological Data Analysis (TDA)

### TDA based on periodicity
To perform TDA on the plant data, we will generate a brave lattice from the points. A brave lattice is a regular pointcloud, which can be represented by 2 vectors, u & v, both being unit vectors. To generate a brave lattice, the 1st attempt we used is to remove points from the disk stacking model based on certain pattern. According to Prof. Golé's prior study, disk stacking model generated under different circumstances have different periodicity, meaning that the model will have a pattern repeating after certain points, so we can keep the points of the model by period, which will generate a regular pattern. With this pattern, we will use TDA to measure the difference between the original model and the brave lattice we generated, to quantify irregularity in different areas.

{{}}

### TDA from megatile
Theere is a limitation in our first approach. TDA studies the geometry of pointcloud, but since we are removing points to form a brave lattice, we might have removed features in the original pointcloud that is what TDA is interested in. To make sure we keep as many details as we can, we designed a second variation. A fact about the disk stacking model is that disks at the bottom of the model represent the early stage of plant growth, which is unstable and does not have a clear period. Based on this fact, we can create a "megatile" that is a power set of the points in the last period. Since a period of points have up and down vectors, we will create a up_vectors * down_vectors point cloud that is regular as well, and use TDA to measure the difference between the bottom disks with this regular pattern generated from the top disks. This variation allows us to preserve geometric features of the disk model.

{{}}

### Delaunay Triangulation
The last variation is different from the previous 2, where we compare the original pointcloud to a regular pattern, and see how different they are. Though we have preserved a good amount of geometric features, we are still not looking at the entire model. Because of this, we decided to apply delaunay triangulation of the whole disk stacking model, and then record the differences between the sides and angles of whole the triangulation. This would take the whole pointcloud into consideration.

{{}}

---
## TDA on real specices
At the end of the day, we want to land theories in practice. In Fall 2023, we mainly worked on transforming plant data to be applicable for TDA, and then apply TDA on different species. The first step is to normalize the pointcloud so that all point data from different species will be relatively the same size. We implemented procrustes, an algorithm that scales the translates the points toward the origin. Then coming to the choice of which TDA to apply, we noticed that the plant data is horizontally longer. As they are not stacking tall enough to be regular, we observe periods of 30 to 50 for a pointcloud of around 80 points, which means that if we apply TDA based on periodicity, we might end up with only 2 points to look at, so the 1st variation of TDA is abandoned. Delaunay Triangulation, on the other hand, was easy to implement and record its measurement. So the challenge is to apply TDA from megatile.

To implement TDA from megatile, we need to find a period of points that best conclude the whole geometry. However, as the plant points are not as ideal and regular, the choice of the period of points is arbitrary and might vary from plant to plant. Thus, we redesigned the megatile generation to create a mega-megatile. We will look at every period of points from the model, roughly 7-8, record all the up and down vectors from the model, and then build the power set of all_up_vectors * all_down_vectors. This mega-megatile preserves all the geometric relationships between points in a period, and thus conclude the plant model geneogically.

Unlike TDA on plant simulation data where we are more interested in irregularity of areas in the hexagon, for TDA on real plant data, we want to have a detailed look for each species. Thus, instead of heatmap, we generated persistence diagram to show the geometric relationship. Persistence diagram shows how many points will be connected and form a small group after we reach each length, and thus shows how the points are geometrically related. This concludes our TDA on plants so far, and will be applied systematically across species in the spring.

---
## Brief Abstract for SURF
(*This part does not include TDA on real species.)

Phyllotaxis is the arrangement of plant organs on a stem. Frequently, these organs are arranged into spirals; the numbers of spirals in each direction are often two consecutive Fibonacci numbers. However, some plants display similar numbers of spirals in each direction. Stephane Douady coined the term “quasi-symmetric” to describe this. The goal of our research is to statistically distinguish quasi-symmetric from Fibonacci phyllotaxis, and determine which conditions prompt the formation of each. Throughout, we use the geometric tool of primordia fronts, which gives a local count of spirals.

During SURF, I worked on a Python program that simulates phyllotactic pattern growth, built by previous students and was based on programs generated by Professor Christophe Golé. The program generates disks to a cylinder's surface without overlap, providing numerical and visual simulations of how the system stabilizes into periodic rhombic tiling structures. 

Annie Karitonze, Evelyn Gao, and I first transcripted and updated a topological data analysis (TDA) program created by Professor Robin Belton from Jupyter Notebook to Python. TDA allows us to quantify the irregularity of the pattern in one simulation. Then, Evelyn and I applied a different version of the TDA analysis. The old TDA takes disks out from the cylinder to generate a regular pattern as a comparison, while the new TDA generates a regular pattern from the last fronts that are rhombic tiling structures as a comparison. Moreover, we added Delaunay Triangulation as the third analysis measurement, which focuses on the geometric relationship between the disks. We combined these 3 measurements using Principal component analysis and produced a Mapper Graph as a high-level understanding of the data. Lastly, we generated graphs like barplot, swarmplot, and stripplot to compare the regularity of Fibonnaci pattern and Quasi Symmetry pattern. 

Besides these new additions to the program, we also debugged disk generation in the original code, improved the data generation algorithm for more accurate visualization, and updated the overall flow of the program.
