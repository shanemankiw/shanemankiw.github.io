### Notes on Fast Bilateral Solver(FBS)

![image-20200505143511143](.\assets\Academic\fbs_paper.png)

This paper is originally from ECCV 2016, and it's selected as oral presentation. It aims at developing a fast and edge-aware smoothing method which can be used in many different scenarios, even including semantic segmentation as a way to refine the result, kind of similar to dense-CRF in terms of usage, but way faster.

#### Before start...

We have to mention another paper *'Fast Bilateral-Space Stereo for Synthetic Defocus'* of Dr. Barron in CVPR 2015, which analyze something about bilateral filtering and a fast way to solve it by transforming it into **bilateral space**, which sounds quite like Fourier space.

So the **bilateral filtering** can be formulated as this(from wikipedia):
$$
y(i,j) = \frac{\sum_{k,l}x(k,l)w(i,j,k,l)}{\sum_{k,l}w(i,j,k,l)}
$$
The above formula is useless, kind of. No definitions of the $w$ anyway. But in the paper, it gives a more specific definition of bilateral filtering as a normalized matrix-vector multiplication:
$$
\mathbf{y} = (A\mathrm{x})/(A\mathbf{1})
$$
$\mathrm{x}$ is the input image, and $\mathbf{y}$ is the filtered output image,  and $\mathbf{1}$ is an ones-vector. And A is defined as:
$$
A_{i,j} = \exp(-\frac{\parallel [x_i,y_i]-[x_j,y_j]\parallel^2}{2\sigma_{xy}^2}-\frac{\parallel [r_i,g_i,b_i]-[r_j,g_j,b_j]\parallel^2}{2\sigma_{rgb}^2})
$$
And actually, there is a way to factorize A into sub-matrices. It can be denoted as "splat/blur/slice".

- splat: pixel values are “splatted” onto a small set of vertices in a grid or lattice (a soft histogram operation).
- blur: those vertex values are blurred.
- slice: the ﬁltered values for each pixel are produced via a “slice” (an interpolation) of the blurred vertex values.

Then A can be written as(in approximation):
$$
A = S^T \bar{B}S
$$
These 3 actions are turned into matrix multiplication. Now $\mathbf{y}$ is:
$$
\mathbf{y} = \frac{S^T \bar{B}S \mathrm{x}}{S^T \bar{B}S \mathbf{1}}
$$
And the bilateral grid construction is often referred to as the projection to 'bilateral space'.

#### Simplified Bilateral Grid

Dr. Barron built on the above mentioned, and start a technique called "simplified" bilateral grid. The above matrix is as follows:
$$
\hat{W} = S^TD_\mathbf{m}^{-1}D_\mathbf{n}\bar{B}D_\mathbf{n}D_\mathbf{m}^{-1}S , \;SS^T = D_\mathbf{m}
$$
This also reformulate the original signal with all the pixels into a lower dimensional bilateral vertices:
$$
\mathbf{x} = S^T\mathbf{y}
$$
