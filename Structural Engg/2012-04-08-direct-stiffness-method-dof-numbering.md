title: Direct Stiffness Method - Degree of Freedom Numbering
date: 2012-04-08
slug: direct-stiffness-method-dof-numbering
tags: Structural Analysis, Direct Stiffness Method

An introduction to numbering degree of freedom numbers for direct stiffness method of analysis of skeletal structures.
<!-- PELICAN_END_SUMMARY -->

Direct stiffness method of analysis of skeletal structures represents skeletal structures using one dimensional truss or beam elements and sets up the stiffness equation, namely:

$$[K]\{x\} = \{P\}$$

where $[K]$ is the structure stiffness matrix, $\{x\}$ is the column vector of unknown displacements at nodes of the structure and {P} is the column vector of applied loads corresponding to unconstrained degrees of freedom.

The structure stiffness matrix $[K]$ is symmetric and usually sparse (many elements are zero, and remain zero while solving the stiffness equation). Its size is equal to the number of unknown displacements. Further, number of rows in $\{x\}$ and $\{P\}$ is the same as the number of rows in $[K]$. Each row of $[K]$ corresponds to one unknown displacement (degree of freedom), and the corresponding rows of $\{x\}$ and $\{P\}$ are related to the displacement associated with a particular row of [K]. Therefore, the process of identifying the number of unknown displacements (degree of kinematic indeterminacy) and assigning a number to each unknown displacement is an important first step in the direct stiffness method.

Sequence of numbering degrees of freedom is usually arbitrary and any sequence can be followed, as long as numbering is continuous. However, sequence of numbering degrees of freedom becomes important when the structure has known non-zero displacement boundary conditions (sometimes called settlement of supports).

Even here, numbering sequence within each group is arbitrary, but degrees of freedom must be divided into groups (unknown, known non-zero and known zero displacements) and the groups must be numbered in a particular sequence. This post describes an algorithm to determine the number of degrees of freedom and assigning degree of freedom numbering to the unknown displacements and known non-zero displacements.

I will use a plane frame to illustrate how the algorithm works, but it could easily be extended to space frames or generalized for other types of structures such as plane or space trusses, floor grids etc. It can even be extended to structures that use elements with more than two nodes per element.

In general, the number of degrees of freedom (unknown independent displacement components) at a node in a space structure is 6 (3 linear displacements $u_x$, $u_y$ and $u_z$ and 3 rotational displacements $r_x$, $r_y$ and $r_z$ measured with respect to structure coordinate system). However, this can be different for special considerations. For example, consider a plane frame that has all its members lying in a single plane, and all loads applied in the plane of the members. This implies that there are no displacements out of the plane, at any of the nodes. Thus, if a plane frame lies in the x-y plane, the displacements out of the plane, namely, $u_z$, $r_x$ and $r_y$ are zero at each node of the plane frame. Similarly, for a grid floor with all members lying in the horizontal x-z plane and all loads applied in the vertical direction (y direction), the following displacements at each node are zero, $u_x$, $u_z$ and $r_y$.

There is another way the degrees of freedom per node could be reduced to less than 6. This happens with truss structures (structures where in ALL members are connected at their ends by frictionless hinges). Since nodes in such structures experience only linear displacements and there are no rotational displacements of the nodes, the number of degrees of freedom per node in a plane truss lying in the x-y plane is 2 ($u_x$ and $u_y$) and in a space truss is 3 ($u_x$, $u_y$ and $u_z$).

Once we know the number of nodes and the degrees of freedom per node, we can easily arrive at the total number of degrees of freedom of the structure. However, every structure must have a sufficient number of degrees of freedom constrained otherwise it will experience rigid body displacements. The constrained displacements are the known zero displacement boundary conditions at nodes which are called supports. Thus, the degree of kinematic indeterminacy is the total number of possible degrees of the structure, less the number of known zero displacement boundary conditions.

In the direct stiffness method, only that part of the stiffness matrix is assembled that corresponds to the unknown displacements. However, if a structure has known non-zero displacements, those degrees of freedom also have to be included in the assembled stiffness matrix. It is also required to order the displacements such that all unknown displacements are numbered first before numbering the known non-zero displacements.

One important aspect of numbering the degrees of freedom is how we represent the information about the known zero and known non-zero displacements while describing the input to the program. While there can be many ways in which this could be done, this algorithm adopts the following approach. By default, all displacement components of a node are assumed to be unknown. If one or more displacements at a node are either known zero or known non-zero displacements, it will be considered a support. Only description of displacements at a support is input and all displacements at the rest of the nodes are treated as unknown. Description of displacements at a support is coded as follows:
1 (one) if the displacement component is constrained (known zero displacement)
-1 (negative 1) if the displacement is known non-zero displacement, and
0 (zero) if the displacement is unknown.
For example, consider a fixed support in a plane frame in the x-y plane. Since all displacement components (ux, uy, rz) at a fixed support are constrained, it is coded as (1, 1, 1). The following figure describes the coding for a few selected supports in plane frames in the x-y plane assuming x-axis is horizontal and y-axis is vertical:


A support in a space frame will have 6 dof per node, but the coding remains the same, that is 1, -1 and zero for known zero, known non-zero and unknown displacement components.

Here is an algorithm to accomplish the task of numbering the degrees of freedom:
Input

n, the number of nodes in the structure
dof_per_node, the number of degrees of freedom for each node in the structure. It is 2 for plane trusses in the x-y plane (ux, uy), 3 for plane frames in the x-y plane (ux, uy, rz), 3 for space trusses (ux, uy, uz), 6 for space frames (ux, uy, uz, rx, ry, rz)
bc, the array describing the known zero and known non-zero displacement boundary conditions at support nodes, Number of rows is equal to the number of support nodes. Number of columns is dof_per_node+1. First column is the number of the node which is a support and the remaining columns are coded as described above
Algorithm
Compute the total number of possible unknown displacements (n * dof_per_node)
Initialize an array of size (n x dof_per_node) with all elements zeros. Let us call it the location matrix (lm). Each row of  lm  corresponds to one node of the structure. Each column of  lm  corresponds to one displacement component at the specific node. At this point of time, all elements are zero.
Copy the columns (except the first, which is the number of the node whose constraint conditions are described by the row) from bc into the row corresponding to the row of  lm  corresponding to the number of the node available in column 1 of bc, that is, if the first column of a row in bc is i, place the remaining columns of that row of bc in row i of lm.
Initialize a variable ndof to count the degrees of freedom of the structure
Scan the location matrix lm element by element and do the following:
If an element is 1, replace it with a zero, 
If an element is 0, increment ndof by 1 and replace that element of lm with the updated value of ndof
If an element is -1, leave it as it is
When all elements have been scanned, save the value of variable ndof in a variable ndof_known
Rescan the elements of lm element by element and do the following:
If an element is -1, increment ndof by 1 and replace that element of lm with the updated value of ndof
If an element is anything other than -1, leave it as it is
Output
ndof_unknown, the number of known zero displacements
ndof, the total number of unknown and known non-zero displacements
lm, the location matrix of the structure containing the degree of freedom numbering of each displacement component of all nodes of the structure
Example Problem
The example problem is a plane frame in the x-y plane with 4 nodes and 3 members. Two of the nodes are supports. Node 1 is a pinned support (1, 1, 0) and node 4 is a fixed support with a known non-zero vertical displacement (1, -1, 1). Following figure shows the plane frame being considered:


The input for the frame is as shown in the figure below:


At the start of the algorithm, we initialize all elements of the location matrix lm to zero, as shown in the figure below:


After copying the codes for the support nodes, the numbers in lm are as follows:


After the first pass of scanning the elements of location matrix lm, replacing 1s with zero and replacing 0s with updated dof numbers, the elements of lm are as follows:



After the second pass of scanning the elements of lm, replacing -1s with updated dof numbers, the elements of lm are as follows:



Here is the python code to implement the algorithm and its output:
import numpy as np

~~~python
def dof_numbering(dof_per_node, num_nodes, bc):
    lm = np.zeros([num_nodes, dof_per_node], dtype=int)

    for r in bc:
        n = r[0] - 1
        lm[n, :] = r[1:]

    ndof = 0
    for i in range(len(lm)):
        for j in range(len(lm[i, :])):
            if lm[i, j] == 1:
                lm[i, j] = 0
            elif lm[i, j] == 0:
                ndof += 1
                lm[i, j] = ndof
    ndof_unknown = ndof

    for i in range(len(lm)):
        for j in range(len(lm[i, :])):
            if lm[i, j] == -1:
                ndof += 1
                lm[i, j] = ndof
    return ndof_unknown, ndof, lm

if __name__ == '__main__':
    dof_per_node = 3
    num_nodes = 4
    bc = np.array([[1, 1, 1, 0], [4, 1, -1, 1]])
    ndof_unknown, ndof, lm = dof_numbering(dof_per_node, num_nodes, bc)
    print 'Unknown displacements = ', ndof_unknown
    print 'Total dof = ', ndof
    print 'Location Matrix\n', lm
~~~

Output of the program is as follows:

~~~
Unknown displacements = 7
Total dof = 8
Location Matrix
[[0 0 1]
 [2 3 4]
 [5 6 7]
 [0 8 0]]
 
~~~

To learn more, read my short document (but code in Scilab, not Python) Support independent publishing: Buy this e-book on Lulu.
