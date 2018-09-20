---
layout: page
title: Research
published: true
---



## Overview
  The primary branch of research interest is optimization. 
  The particular specialization of interest is the intersection of fixed iterative fixed point algorithms, variational modeling for image processing, and asynchronous computations. Below we discuss each of these independently and then how they may be bridged. 
  
### Convex Feasibility Problems
Let \\( \lbrace C_i\rbrace_{i=1}^m \\) be a finite family of closed convex sets with nonempty intersection.  Convex feasibility problems (CFPs) consist of finding a point \\(x\\) in the intersection of the convex sets, i.e.,
  \\[x \in C := \bigcap_{i=1}^m C_i. \\]
Iterative methods for solving this sort of problem often use a sequence of operators \\( \lbrace T_k \rbrace_{k=1}^\infty \\) and define a sequence \\(\lbrace x^k \rbrace_{k=1}^\infty \\) with \\(x^1\\) arbitrary and
 \\[ x^{k+1} := T_k \left( x^k \right), \ \ \forall \ k \geq 1. \\]
Then the main sort of result will be to assert
\\[ \lim_{k\rightarrow\infty} x^k = x^* \in C, \\]
noting whether the convergence is weak or strong, and to assert the rate at which \\(x^k\longrightarrow x^*\\).
  
### Asynchronous Methods
Asynchronous algorithms are of great practical interest as they open the door to greater utilization of processing power than anologous synchronous algorithms.

### Variational Models in Image Processing
On the other hand, variational models are used in many image processing methods, e.g., using the Rudin-Osher-Fatemi (ROF) model we seek the minimizer \\(u:\Omega\rightarrow \mathbb{R}\\) of the energy \\(E(u)\\) defined by
  \\[ E(u) := \int_\Omega |\nabla u | \ dx + \lambda \int_\Omega |u-f|^2 \ dx. \\] 

### The Intersection of Methods

  
 




## Papers

> H. Heaton and Y. Censor, Asynchronous Sequential Inertial Iterations for Common Fixed Points Problems with an Application to Linear Systems. _Technical Report_, August 15, 2018.

<div class = "featured">
  <center>
  <table style="width: 150px; background-color:rgba(0, 0, 0, 0);">
    <tr>
      <th align="center">Preprint</th>
      <th align="center">Citation</th>
      <th align="center">Code</th>
    </tr>
    <tr>
      <td align="center" width = "33%">
        <div class="brightness">
          <a href="https://arxiv.org/abs/1808.04723"><img src="/public/images/preprint-icon2.png" alt="preprint" class="image" style="width:46px">
          </a> 
        </div>
      </td>
      <td align="center" width = "34%">
        <div class="brightness">
          <a href="/public/citations/2018-ASI.bib"><img src="/public/images/cite-icon4.png" alt="Avatar" class="image" style="width:50px">
          </a> 
        </div>
      </td>  
      <td align="center" width = "33%">
        <div class="brightness">
          <a href="/public/code/2018-ASI.zip"><img src="/public/images/code-icon.png" alt="code" class="image" style="width:50px">
          </a>
        </div>
  	  </td>
    </tr>
  </table>
  </center>
</div> 

 

 

> Y. Censor, H. Heaton, and R.W. Schulte, Derivative-free superiorization with component-wise perturbations. _Numerical Algorithms_, Published April 11, 2018. DOI:10.1007/s11075-018-0524-0.

<div class = "featured">
  <center>
  <table style="width: 200px">
    <tr>
      <th align="center">Reprint</th>
      <th align="center">Preprint</th>
      <th align="center">Citation</th>
      <th align="center">Code</th>
    </tr>
    <tr>
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="https://rdcu.be/LjcS"><img src="/public/images/reprint-icon2.png" alt="Avatar" class="image" style="width:46px">
          </a> 
        </div>
      </td>      
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="https://arxiv.org/abs/1804.00123"><img src="/public/images/preprint-icon2.png" alt="Avatar" class="image" style="width:46px">
          </a> 
        </div>
      </td>
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/citations/2018-Der-Free-Sup.bib"><img src="/public/images/cite-icon4.png" alt="Avatar" class="image" style="width:50px">
          </a> 
        </div>
      </td>  
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/code/2018-Der-Free-Sup.zip"><img src="/public/images/code-icon.png" alt="Avatar" class="image" style="width:50px">
          </a>
        </div>
  	  </td>
    </tr>
  </table>
  </center>
</div>

<div class = "featured">
  <center>
    Click below to see my research available on other websites. <br /> <br />
        <div class="brightness">
          <a href="https://scholar.google.com/citations?user=blvaFx4AAAAJ&hl=en"><img src="/public/images/google-scholar-icon.png" alt="google-scholar" class="image" style="width:70px">
          </a>
        </div>
        <b style="word-space:2em">&nbsp;&nbsp;</b>
        <div class="brightness">
          <a href="https://arxiv.org/search/?query=howard+heaton&searchtype=all&source=header"><img src="/public/images/arXiv-icon.png" alt="arXiv" class="image" style="width:70px">
          </a>
       </div>  
  </center>
</div>
