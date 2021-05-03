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
Cell detection and counting is fundamental in biomedical and cancer research and it is regarded as the basis of image-based cellular research. So up until recently, a lot of research depended on manually hand-counting the cells you see in an image. And with recent advances in technology and higher image processing capabilities, a lot of methods and softwares have been developed to automating this process. 

However, a great number of them still show limitations when it comes to analyzing a cluster of cells that are in close proximity and especially in 3D culture environments. So the main motivation behind our project was to come up with a method to an accurate measure of the number of cells in volumes and especially in clusters.  

# Our Dataset

# Method #1: The Graph-Cut Algorithm
The first algorithm we explored was a graph-cut algorithm highlighted in a paper {1} from the 2012 IEEE conference. The main intuition is straightforward: cells typically exhibit an ellipsoid shape. We can exploit this pattern to guide our cut and at the same time help reduce computational complexity. The specific equation used is below. 

The graph-cut itself is done by locating the nuclei of cells and expanding the nuclei through a vector field. The detection of the nuclei is inspired by another paper that uses multiscale products to detect locations of interest. We calculate Hessian eigenvalues at different pixels p and with different smoothness scale σ to form connected components within the image. Each connected component acts as the seed of an individual cell. We then use an input diameter to "grow" the seeds via Euclidean distance from each individual seed's center and taking its gradient. 

The results on an individual cell image can be seen below. The algorithm did well when working with isolated cells of various sizes, but struggled with clusters of cells. The ellipsoid nature of the algorithm backfired here because we do not restrict the growth to a strict shape and instead allow it to form a "blob-like" pattern. Thus, the algorithm cannot distinguish those clusters as individual cells. While we could change the input diameter to accomodate these clusters, the change would also negatively affect detection on isolated cells.

# Method #2: CellProfiler

# Method #3: Machine Learning

# Comparison

# Future Improvements

# References (will reformat later)
{1}: https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.471.5473&rep=rep1&type=pdf
