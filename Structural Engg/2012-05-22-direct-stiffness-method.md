title: Direct Stiffness Method - An Overview
date: 2012-05-22
slug: direct-stifness-method-overview
tags: Structural Analysis, Direct Stiffness Method


A brief overview of the direct stiffness method as applicable to skeletal structures. <!-- PELICAN_END_SUMMARY -->

The direct stiffness method is a matrix method of structural analysis. This post pertains only to the analysis of skeletal structures, that is, structures that can be modelled using only 1D truss/beam elements in either 2D or 3D space. Further, element stiffness is explicitly derived from first principles.

In general, a direct stiffness method such as the Finite Element Method, is quite general and can model structures using 1D, 2D (Plate, Plane Stress, Plane Strain elements) and 3D (solid elements) elements in 2D or 3D space.

Subject to the above mentioned limitations, the direct stiffness method is a procedure to solve the structure stiffness equation, namely

$$ [k]\\{ x \\} = \\{ P \\} $$

where $\left[ K \right]$ is the structure stiffness matrix, $\{ x \}$ is the displacement vector and $\{ P \}$  is the load vector. Depending on the specific problem being solved, $[K]$, $\{ x \}$ and $\{ P \}$  can be partitioned into sub-matrices, as follows:

$$ \begin{bmatrix} K_{11} & K_{12} & K_{13} \\\\ K_{21} & K_{22} & K_{23} \\\\ K_{31} & K_{32} & K_{33} \end{bmatrix} \begin{Bmatrix} x_1 \\ x_2 \\ x_3 \end{Bmatrix} = \begin{Bmatrix} P_1 \\ P_2 \\ P_3 \end{Bmatrix}$$

* Row 1: $[K_{11}]$, $\{ P_1 \}$ are known and $\{ x_1 \}$ is unknown and to be determined.

* Row 2: $[K_{22}]$, $\{ x_2 \}$ are known and $\{ x_2 \}$ has non-zero elements.  $\{ P_2 \}$ corresponds reaction components corresponding to known non-zero displacements $\{ x_2 \}$ and can be determined.

* Row 3: $[K_{33}]$, $\{ x_3 \}$ are known and $\{ x_3 \}$ has all zero elements.  $\{ P_3 \}$ corresponds reaction components corresponding to known zero displacements $\{ x_3 \}$ and can be determined. Since reactions can be computed indirectly from the force components at the ends of members meeting at the support, it is possible to leave out this part of the equation.

We can rewrite the above equation as three separate equations and each equation can then be rearranged to obtain the unknown in terms of the known, to obtain the following:

$$[K_{11}] \\{x_1=?\\} + [K_{12}] \\{x_2\\} + [K_{13}] \\{x_3=0\\} = \\{P_1\\} \Rightarrow \\{x_1\\} = [K_{11}]^{-1} (\\{P_1\\}  - [K_{12}] \{x_2\}) \\\\
[K_{21}] \\{x_1\\} + [K_{22}] \\{x_2\\} + [K_{23}] \\{x_3=0\\} = \\{P_2=?\\} \Rightarrow \\{P_2\\} = [K_{21}]\\{x_1\\} + [K_{22}] \\{x_2\\} \\\\
[K_{31}] \\{x_1\\} + [K_{32}] \\{x_2\\} + [K_{33}] \\{x_3=0\\} = \\{P_3=?\\} \Rightarrow \\{P_3\\} = [K_{31}]\\{x_1\\} + [K_{32}] \\{x_2\\}
$$

In the above equations, unknown vectors are indicated by the question mark. Since {x3}={0}, its multiplication with any matrix is also zero.

If the structure has only known zero displacements at supports and no known non-zero displacements (support settlements), the entire second row and second column of $[K]$, namely, $[K_{22}]$ as well as second sub-matrix $\{P_2\}$ and $\{x_2\}$ are null. In that case, it is only necessary to assemble $[K_{11}]$ in order to determine the unknown displacements $\{x_1\}$. In order to determine the reactions corresponding to known zero displacements, it is sufficient to assemble $[K_{31}]$ so that $[K_{31}]\{x_1\}=\{P_3\}$.

According to this scheme of solving the stiffness equation, the degrees of freedom are numbered in the sequence adopted above, namely, unknown displacements first, known non-zero displacements (if any) next and known zero displacements last.

Accordingly, while assembling the stiffness matrix, the following stiffness matrices are assembled:

* $[K_{11}]$ is required always

* $[K_{12}]$, $[K_{22}]$ and $[K_{32}]$ are required only if the the structure has one or more known non-zero displacements. None of them is required if the structure has no known non-zero displacements.

* $[K_{31]}$ and $[K_{32}]$ are required if reactions are to be computed. $[K_{31}]$ is not required if reactions are computed from member end forces.

Since it is possible to compute the reactions from the known forces at the ends of members (which in turn are obtained from known displacements at nodes), it is not necessary to use the second and third equations above (expanded from the stiffness equation expanded in terms of sub-matrices) to calculate the reactions. However, if there are known non-zero displacements in a structure, it is necessary to assemble $[K_{12}]$ in order to calculate $\{x_1\}$.





