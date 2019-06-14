---
layout: page
title: Research
published: true
---
## Overview ##
The primary area of research is optimization with a focus on developing fast and memory efficient iterative
fixed point methods in a general Hilbert space setting. This includes specialty interests in parallel asynchronous methods and "learning to optimize", where machine learning is incoporated into algorithmic development for situations where an individual problem must be repeatedly solved, each time with new (but similar) data. 
 
 
_(Published research papers and slides are available at the bottom of this page.)_

### *Fixed Point Problems* ###
Let \\(T:\mathcal{H}\rightarrow\mathcal{H}\\) be an operator on a Hilbert space \\(\mathcal{H}\\) with a nonempty fixed point set \\( \textrm{fix}(T) \\). Many optimization problems may be abstractly written in the form of a fixed point problem

 \\[  \textrm{Find} \   x^\star \in \textrm{fix}(T). \\]

For example, see the operators used for [Forward Backward Splitting (FBS)](https://en.wikipedia.org/wiki/Proximal_gradient_methods_for_learning) and Douglas Rachford Splitting (DRS). Iterative methods for solving this type of problem often use a sequence of operators \\( \lbrace T_k \rbrace_{k=1}^\infty \\) with fixed point sets whose common intersection equals \\( \textrm{fix}(T) \\). Such methods define a sequence of points \\(\lbrace x^k \rbrace_{k=1}^\infty \\) with an arbitrary initial point \\(x^1\\)  and updates computed via
 \\[ x^{k+1} := T_k \left( x^k \right), \ \ \forall \ k \geq 1. \\]
The main sort of result is usually to assert the chosen sequence of operators and update iteration yields
\\[ \lim_{k\rightarrow\infty} x^k = x^\star \in C, \\]
noting whether the convergence is weak or strong. Second to this, we often seek results regarding the rate at which \\(x^k\longrightarrow x^*\\). Current research on this subject pertains to generating rapid algorithms that scale for massive data sets and also developing methods that improve resilience to noisy and /or corrupted data.

> For other examples of operators and fixed point problems, we refer the reader to [ADMM](https://web.stanford.edu/~boyd/admm.html) and to the method of [alternating projections](https://en.wikipedia.org/wiki/Projections_onto_convex_sets).
  
### *Asynchronous Methods* ###
Asynchronous algorithms are of practical interest primarily since they open the door to greater utilization of processing power than anologous synchronous algorithms, particularly as the number of computing agents (e.g., GPU cores) increases. Let \\(\tau\\) be a nonnegative integer, identifying how out-of-date of information (a.k.a. "stale")  we wish for processors to be able to utilize. For synchronous methods \\(\tau =0\\), but for asynchronous methods we assume \\(\tau > 0\\). Asynchronous methods replace each component \\(x_i^k\\) of the vector \\(x^k\\) in the update above with \\( {\hat{x}^k_i} = x_i^{k-j} \\),  where \\(j \in \lbrace 0, 1, 2, \ldots, \tau \rbrace \\). This means the vector \\( \hat{x}^k\\) may possibly be out-of-date. We need not know particular values of each \\(j\\) at individual iteration steps; instead it suffices to know \\(j\leq \tau\\) for all \\(k\\). In mathematical terms, we write
 \\[ x^{k+1} := x^k - \lambda_k S_k \left( \hat{x}^k \right), \ \ \forall \ k \geq 1, \\]
 where each \\(\lambda_k\\) gives a step-size and each operator \\(S_k\\) is related to \\(T_k\\) above.
This enables, in practice, each processor to perform its computations at its own speed (rather than remain idle waiting for the slowest processor to catch up) and speeds up computations. This also introduces robustness to dropped network transmissions. With appropriate assumptions on the delays and step-sizes used, performing asynchronous updates generates a sequence that converges to a solution \\( x^\star \\). Moreover, in some cases, asynchronous algorithms can require _fewer_ iterations to converge than their synchronous counterpart.

### *Machine Learning* ###
The term "machine learning" is a common buzz phrase nowadays. Although there are many wonderful applications, my particular research interest related to this field falls under the category of "learning to optimize" as described by Li and Malek [here](https://arxiv.org/pdf/1606.01885.pdf). A recent paper proposed the [ALISTA](https://openreview.net/pdf?id=B1lnzn0ctQ) method, a follow-up to the [LISTA](https://dlnext.acm.org/doi/abs/10.5555/3104322.3104374) paper. In their work proposing LISTA, the authors took the idea of the iterative shrinking thresholding algorithm (ISTA) and generalized the form of this algorithm to enable various parameters to be "learned" by solving an optimization problem using relevant data sets. The idea here is that once parameters are found that are roughly "ideal", these could be used with the algorithm for new inputs that are similar to the data in the training set. The ensuing result is rapid execution time. The ALISTA paper refined the LISTA method by using fewer/simpler parameters to learn, thereby simplifying and speeding up the training for solving the associated machine learning problem.

### *Variational Models in Image Processing* ###
Let \\(\mathcal{H}\\) be a Hilbert space of functions  \\(u:\Omega\rightarrow\mathbb{R}\\), where \\(\Omega\subset\mathbb{R}^n\\). In the context of images, \\(u\\) is often used rather than \\(x\\). A variational method defines an energy functional \\(J(u)\\) for which a minimizer \\(u\\) possesses desirable properties, making the underlying problem
\\[ \min_{u\in\mathcal{H}} J(u). \\]
For example, if \\(f\\) is a blurry and grainy image, the classic Rudin-Osher-Fatemi (ROF) model proposes using the energy  \\(J(u)\\) for denoising, which is defined by
  \\[ J(u) := \int_\Omega |\nabla u | \ dx + \lambda \int_\Omega |u-f|^2 \ dx. \\] 
Here \\(\nabla\\) denotes the gradient and \\(\lambda > 0\\) is a regularization parameter. Many image processing models exist and there are various sets of desirable features in different contexts. Nonlocal variational methods, which generalize local operators (e.g., gradients), have also been demonstrated to be quite effective in this field. Several algorithms also exist for solving these variational problems, often using fixed point algorithms.


 


 
 
<div class = "featured">
  <!-- This snippet gives a break in sections -->
  <br />
</div>
 

## Papers ##
Below is a paper that presents the asynchronous sequential inertial (ASI) algorithm that weaves together convex feasibility problems and asynchronous methods in a simple manner while also introducing inertial terms. Additionally, there is a paper on superiorization, which is a heuristic methodology that lies somewhere between the feasibility-seaking and constrained minimization branches of optimization. This methodology takes the hypothesis above and provides a general framework that has been shown in many papers to be quite efficacious. Although the superiorization method generates a sequence \\(\lbrace x^k \rbrace_{k=1}^\infty \\) that provably converges to a feasibile point, limited results are known regarding the cost function values \\(\phi(x^k)\\) as \\(k\longrightarrow \infty\\). See Professor Yair Censor's [webpage](http://math.haifa.ac.il/YAIR/bib-superiorization-censor.html) for a comprehensive bibliography of papers on this topic. More results on the "learning to optimize" subject will be shared later this year.

> H. Heaton and Y. Censor, Asynchronous Sequential Inertial Iterations for Common Fixed Points Problems with an Application to Linear Systems. _Journal of Global Optimization_, Published February 14, 2019. DOI:10.1007/s10898-019-00747-4.

<div class = "featured">
  <center>
  <table style="width: 260px">
    <tr>
      <th align="center">Reprint</th>
      <th align="center">Preprint</th>
      <th align="center">Citation</th>
      <th align="center">Slides</th>
    </tr>         
    <tr>
        <td align="center" width = "25%">
        <div class="brightness">
          <a href="https://rdcu.be/bmTXV"><img src="/public/images/reprint-icon2.png" alt="reprint" class="image" style="width:48px">
          </a> 
        </div>
      </td> 
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/papers/2019-01-23-ASI-arXiv-Preprint.pdf"><img src="/public/images/preprint-icon2.png" alt="preprint" class="image" style="width:48px">
          </a> 
        </div>
      </td>
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/bib-files/2019-ASI.bib"><img src="/public/images/cite-icon4.png" alt="bib-file" class="image" style="width:50px">
          </a> 
        </div>
      </td>  
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/papers/2018-12-13-Heaton-ASI-Talk-Handout.pdf"><img src="/public/images/preprint-icon2.png" alt="code" class="image" style="width:50px">
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
  <table style="width: 180px">
    <tr>
      <th align="center">Reprint</th>
      <th align="center">Preprint</th>
      <th align="center">Citation</th>
      <!--<th align="center">Code</th>-->
    </tr>
    <tr>
      <td align="center" width = "33%">
        <div class="brightness">
          <a href="https://rdcu.be/LjcS"><img src="/public/images/reprint-icon2.png" alt="reprint" class="image" style="width:48px">
          </a> 
        </div>
      </td>      
      <td align="center" width = "33%">
        <div class="brightness">
          <a href="/public/papers/2018-03-28-Der-Free-Sup-Preprint.pdf"><img src="/public/images/preprint-icon2.png" alt="preprint" class="image" style="width:48px">
          </a> 
        </div>
      </td>
      <td align="center" width = "33%">
        <div class="brightness">
          <a href="/public/bib-files/2018-Der-Free-Sup.bib"><img src="/public/images/cite-icon4.png" alt="bib-file" class="image" style="width:50px">
          </a> 
        </div>
      </td>  
      <!--
      <td align="center" width = "25%">
        <div class="brightness">
          <a href="/public/code/2018-Der-Free-Sup.zip"><img src="/public/images/code-icon.png" alt="code" class="image" style="width:50px">
          </a>
        </div>
  	  </td>
	  -->
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
  <!-- Start of StatCounter Code for Default Guide -->
  <script type="text/javascript">
  var sc_project=11458818; 
  var sc_invisible=0; 
  var sc_security="c3a494a0"; 
  var scJsHost = (("https:" == document.location.protocol) ?
  "https://secure." : "http://www.");
  document.write("<sc"+"ript type='text/javascript' src='" + scJsHost+
  "statcounter.com/counter/counter.js'></"+"script>");
  </script>
  <noscript><div class="statcounter"><a title="Web Analytics Made Easy -
  StatCounter" href="http://statcounter.com/" target="_blank"><img
  class="statcounter" src="//c.statcounter.com/11458818/0/c3a494a0/0/"
  alt="Web Analytics Made Easy - StatCounter"></a></div></noscript>
  <!-- End of StatCounter Code for Default Guide -->  
</div>
