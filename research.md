---
layout: page
title: Research
published: true
---
## Overview ##

The primary of field of research is optimization with a focus on developing fast and scalable iterative methods for large scale and real-time computations. These tools are particularly suited for machine learning applications. Specialty interests pertaining to this focus include asynchronous computing (where GPUs work independently of each other) and the use of machine learning to automate creation of rapid task-specific algorithms, which is called "learning to optimize" (L2O). The latter  subject is of particular interest for situations where an individual problem must be repeatedly solved, each time with new (but similar) data. Such applications include computer vision problems, language processing, CT image reconstruction, etc. Coming L2O extensions include stochastic and nonconvex settings involved in training neural networks.

Below are highlights from these areas of research.
To be sufficiently general to include all major methods for convex optimization, theoretical guarantees are developed using fixed point theory. 

Below is a brief overview of the setting of fixed point problems. Summaries are then provided of asynchronous and L2O methods.  
 
 
_(Published research papers and slides are available at the bottom of this page.)_

### *Fixed Point Problems* ###
Let \\(T:\mathcal{H}\rightarrow\mathcal{H}\\) be an operator on a Hilbert space \\(\mathcal{H}\\) with a nonempty fixed point set \\( \textrm{fix}(T) \\). Many optimization problems may be abstractly written in the form of a fixed point problem

 \\[  \textrm{Find} \   x^\star \in \textrm{fix}(T). \\]

For example, when minimizing the a function \\(f\\) we may, for appropriate \\(\alpha>0\\), take \\(T(x) = x - \alpha \nabla f(x) \\).  Iterative methods for solving this type of problem often use a sequence of operators \\( \lbrace T_k \rbrace_{k=1}^\infty \\) with fixed point sets whose common intersection equals \\( \textrm{fix}(T) \\). Such methods define a sequence of points \\(\lbrace x^k \rbrace_{k=1}^\infty \\) with an arbitrary initial point \\(x^1\\)  and updates computed via
 \\[ x^{k+1} := T_k \left( x^k \right), \ \ \forall \ k \geq 1. \\]
The main sort of result is usually to assert the chosen sequence of operators and update iteration yields
\\[ \lim_{k\rightarrow\infty} x^k = x^\star \in \textrm{fix}(T). \\]
Second to this,  results are often sought regarding the rate at which \\(x^k\longrightarrow x^\star\\) and the behavior of iterates in the presence of different sources of noise. Asynchronous and L2O methods are being developed to further improve convergence of such fixed point methods both for massive scale problems and tasks that must be completed in real time.

> For some other examples of such operators (e.g., for ADMM, Proximal-Gradent, and Douglas-Rachford splitting), we refer the reader to Table 1 in the recent  [paper](https://arxiv.org/pdf/1609.04746.pdf) by Hannah and Yin.
  
### *Asynchronous Methods* ###
Asynchronous algorithms are of practical interest primarily since they open the door to greater utilization of processing power than anologous synchronous algorithms, particularly as the number of computing agents (e.g., GPU cores) increases. Let \\(\tau\\) be a nonnegative integer, identifying how out-of-date of information (a.k.a. "stale")  we wish for processors to be able to utilize. For synchronous methods \\(\tau =0\\), but for asynchronous methods we assume \\(\tau > 0\\). Asynchronous methods replace each component \\(x_i^k\\) of the vector \\(x^k\\) in the update above with \\( {\hat{x}^k_i} = x_i^{k-j} \\),  where \\(j \in \lbrace 0, 1, 2, \ldots, \tau \rbrace \\). This means the vector \\( \hat{x}^k\\) may possibly be out-of-date. Particular values of each \\(j\\) at individual iteration steps do not need to be known; instead it suffices to know \\(j\leq \tau\\) for all \\(k\\). In mathematical terms, this may be written as
 \\[ x^{k+1} := x^k - \lambda_k S_k \left( \hat{x}^k \right), \ \ \forall \ k \geq 1, \\]
 where each \\(\lambda_k\\) gives a step-size and each operator \\(S_k\\) is related to \\(T_k\\) above.
This enables, in practice, each processor to perform its computations at its own speed (rather than remain idle waiting for the slowest processor to catch up) and speeds up computations. This also introduces robustness to dropped network transmissions. With appropriate assumptions on the delays and step-sizes used, performing asynchronous updates generates a sequence that converges to a solution \\( x^\star \\). Moreover, in some cases, asynchronous algorithms can require _fewer_ iterations to converge than their synchronous counterpart.

### *Learning to Optimize* ###
The term "machine learning" is a common buzz phrase nowadays. Although there are many wonderful applications, this section is aimed at the portion of the field that  falls under the category of "learning to optimize". This is   growing field of research that focuses on the automatic development of task-specific algorithms that must be repeatedly executed with new (but similar) data. An example of this in the context of reinforcement learning is described by [Li and Malek](https://arxiv.org/pdf/1606.01885.pdf). A distinct LISTA method by [Gregor and LeCun](https://dlnext.acm.org/doi/abs/10.5555/3104322.3104374) created a network by unfolding an iterative procedure, truncated to a fixed number of iterations, and allowing its parameters to be learned. Their work was applied to a specific problem, and was followed up by the recent ALISTA method of [Liu et al](https://openreview.net/pdf?id=B1lnzn0ctQ). The ALISTA paper refined the LISTA method by using fewer/simpler parameters to learn, thereby simplifying and speeding up the training for solving the associated machine learning problem. The underlying idea in these last two works is that some applications exist where a collection of data is available along with  standard general purpose algorithms for solving a certain type of problem. A machine learning problem can then be formulated by relaxing parameters in the standard algorithm (truncated to a fixed number of iterations) to be learned. A loss function associated with each output from this parameterized algorithm can then be minimized to determine the 'optimal' weights. The ensuing result in these works is for the learned algorithms to reduce computational cost by order(s) of magnitude when compared to than the original standard algorithm. A recent work on this will be shared after the review process is complete.
 


 
 
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
    Click below to see these papers listed on other websites. <br /> <br />
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
  <!-- Default Statcounter code for Heaton Website
http://howardheaton.tech -->
<script type="text/javascript">
var sc_project=11458818; 
var sc_invisible=1; 
var sc_security="c3a494a0"; 
</script>
<script type="text/javascript"
src="https://www.statcounter.com/counter/counter.js"
async></script>
<noscript><div class="statcounter"><a title="Web Analytics"
href="https://statcounter.com/" target="_blank"><img
class="statcounter"
src="https://c.statcounter.com/11458818/0/c3a494a0/1/"
alt="Web Analytics"></a></div></noscript>
<!-- End of Statcounter Code -->
</div>
