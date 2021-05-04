Cluster Analysis on Neural Cell Imaging
=======================================

## Page URL
[https://weiyuzh.github.io/CS766-Project/](https://weiyuzh.github.io/CS766-Project/)

## CS 766 Project: Cluster Analysis on Neural Cell Imaging
Group Members:
- Nomin Khishigsuren
- Roy Sun
- Trevor Zachman-Brockmeyer
- Weiyu Zhang

## Proposal
[https://weiyuzh.github.io/CS766-Project/proposal.html](https://weiyuzh.github.io/CS766-Project/proposal.html)

## Midterm Report
[https://weiyuzh.github.io/CS766-Project/midterm.html](https://weiyuzh.github.io/CS766-Project/midterm.html)


# Motivation
Cell detection and counting is fundamental in biomedical and cancer research and it is regarded as the basis of image-based cellular research. Cell counting can be perfomed manually using a hemocytometer, flow cytometry or simply by hand-counting from images taken with the microscope. Manual hand-counting is the most affordable option, yet it is very time-consuming and is often subject to bias of the observer[1](http://europepmc.org/article/PMC/5226253). These drawbacks are often exarcebated by the complexity of cell structures that could lead to detection ambiguity and poor image quality for 3D volumetric images that is usually constrained by the specs of the microscope that is being used.  
To overcome these obstacles, a great number of methods and approaches have been developed to detect and count cells automatically using image processing algorithms.  Although these softwares and tools prove to be faster and more robust method to get a cell count from microscope images, many still show limitations when it comes to analyzing a cluster of cells that are in close proximity, and in 3D culture environments[2](https://www.frontiersin.org/articles/10.3389/fnana.2014.00027/full). Therefore, our two main areas of focus were: 

- Clusters containing multiple cells 

Due to the complexity of the cell structures in 3D *in-vitro* culture environments, multiple cells are found clustered into a single blob. A lot of tools don't segment these clusters correctly which leads to inaccurate cell counts. 

<img src="./images/dataset.png"> 

- Using z-stacks to detect neighboring cells 

Volumetric images are obtained by acquiring 2D images along the z-dimension or height of the sample. Using the information that the z-stacks provide, it is possible to determine vertically adjacent/neighboring images and infer additional information about each image (e.g. two disjoint but closeby cells in one image may appear as a single blob in the neighboring image). 

<img src="./images/dataset.png">

As part of this project, we reviewed existing methods and explored image processing enhancements for cell detection, segmentation and counting. Our interest lied in the potential of developing a method that factors in the 3D nature of cells in the image processing and counting analysis. 


# Our Dataset
The dataset we used for our project is a 3D volumetric image of neurons which is obtained by getting 2D images at different heights z. In this case, this image had 187 cross sectional 2D images that were stacked together.   
<br>
<img src="./images/dataset.png">

# Method #1: The Graph-Cut Algorithm
The first algorithm we explored was a graph-cut algorithm highlighted in a paper {1} from the 2012 IEEE conference. The main intuition is straightforward: cells typically exhibit an ellipsoid shape. We can exploit this pattern to guide our cut and at the same time help reduce computational complexity. The specific equation used is below. 
<br>
<img src="./images/graphcut/ellipsoid equation.png" width="600" height="35">

The graph-cut itself is done by locating the nuclei of cells and expanding the nuclei through a vector field. The detection of the nuclei is inspired by another paper that uses multiscale products to detect locations of interest. We calculate Hessian eigenvalues at different pixels p and with different smoothness scale σ to form connected components within the image. Each connected component acts as the seed of an individual cell. We then use an input diameter to "grow" the seeds via Euclidean distance from each individual seed's center and taking its gradient. 
<br>
<img src="./images/graphcut/graphcut expand.png" width="400" height="65">

The results on an individual cell image can be seen below. The algorithm did well when working with isolated cells of various sizes, but struggled with clusters of cells. The ellipsoid nature of the algorithm backfired here because we do not restrict the growth to a strict shape and instead allow it to form a "blob-like" pattern. Thus, the algorithm cannot distinguish those clusters as individual cells. While we could change the input diameter to accomodate these clusters, the change would also negatively affect detection on isolated cells. 
<img src="./images/graphcut/graphcut result.png">

In addition, this algorithm can only take 2D inputs, while we do have 3D images for analysis. Thus, we moved on to other methods.

# Method #2: CellProfiler

# Method #3: Machine Learning

# Comparison
<img src="./images/comparison.png">

# Future Improvements

# References
[1]: O'Brien J, Hayder H, Peng C. Automated Quantification and Analysis of Cell Counting Procedures Using ImageJ Plugins. J Vis Exp. 2016 Nov . doi:10.3791/54719. PMID: 27911396; PMCID: PMC5226253
[2]: 1.Schmitz, C. et al. Current automated 3D cell detection methods are not a suitable replacement for manual stereologic cell counting. Frontiers in Neuroanatomy 8, 27 (2014).



https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.471.5473&rep=rep1&type=pdf
