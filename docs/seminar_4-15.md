<!-- .slide: data-background="#500000" class="dark" -->

# A Modal Approach to the Space Time Dynamics of Cognitive Biomarkers 

## T. Griffith
#### Defense

#### April 28, 2022

---


<!-- .slide: data-background="#003C71" class="dark" -->

# Adaptive Unknown Input Estimators

---

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Estimator overview </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<dl>
<dt>Three significant uncertainties</dt>
  <dd>- Input $u$ is unknown, external</dd>
  <dd>- State matrix $A$ may have uncertainty</dd>
  <dd>- General process uncertainty $v_x$</dd>
<dt>Can we synthesize $u$ and correct $A$?</dt>
</dl> 
</div>



<div class="col">

\begin{aligned}
    \dot{x}&=Ax+Bu+v_x\\\
    y&=Cx
\end{aligned}
</div>
</div>
</section>

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Modeling unknown inputs </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<dl>
<dt>Approximate input space $\mathbb{U}$</dt>
  <dd>- $\hat{u}=\sum_{i=1}^{N} c_i f_i(t)$</dd>
<dt>Persisten Inputs</dt>
  <dd>- $\dot{z}_u=F_u z_u$</dd>
  <dd>- $\hat{u}=\Theta_u z_u$</dd>
  <dd>- $F_u = \begin{bmatrix} 0 & 1 & 0 \\\ -\omega^2 & 0 & 0 \\\ 0 & 0 & 0 \end{bmatrix}$</dd>
</dl> 
</div>



<div class="col">

<figure>
  <img src="img/defense/uhat.gif" alt="Trulli" height="600">
</figure>


</div>
</div>
</section>

<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Architecture and estimator error </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<figure>
  <img src="img/defense/est_arch.png" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

Recover $A$ with adaptive scheme
`$$ A \equiv A_m +B L_{*} C $$`
`$$ \dot{L} = -e_y y^* \gamma_e - \alpha L; \ \alpha>0, \ \gamma_e > 0 $$`
<br>
Error dynamics

`$$ \dot{e}=(\bar{A}+\bar{K} \bar{C})e+\bar{B}w + v $$`
`$$ \begin{bmatrix} \dot{e}_x \\\ \dot{e}_z \end{bmatrix} = \Big(\begin{bmatrix} A_m & B \Theta_u \\\ 0 & F_u \end{bmatrix} + \begin{bmatrix} K_x \\\ K_u \end{bmatrix} \begin{bmatrix} C & 0 \end{bmatrix} \Big) \begin{bmatrix} e_x \\\ e_z \end{bmatrix} +\begin{bmatrix} B \\\ 0 \end{bmatrix} w +\begin{bmatrix} v_x \\\ v_u \end{bmatrix}$$`
`$$ \begin{bmatrix} \dot{e}_x \\\ \dot{e}_z \end{bmatrix} = \underbrace{\begin{bmatrix} A_m+K_x C & B \Theta_u \\\ K_u C & F_u \end{bmatrix}}_\text{$\bar{A}_c$} \begin{bmatrix} e_x \\\ e_z \end{bmatrix} +\begin{bmatrix} B \\\ 0 \end{bmatrix} w +\begin{bmatrix} v_x \\\ v_u \end{bmatrix}$$`


</div>
</div>
</section>


<section>
<h1> Adaptive Unknown Input Estimators </h1>
<h2> Architecture and estimator error </h2>

<dl>
<dt>ASD plant dynamics</dt>
<dt>Bounded `$L_{*}$`, $v$, and $\gamma_e$</dt>
<dt>Error in state and input converges to an n-ball centered at zero</dt>
  <dd>- `$V(e,\Delta L) = \frac{1}{2} e^* \bar{P} e + \frac{1}{2} \text{tr}(\Delta L \gamma_e^{-1} \Delta L^*)$`</dd>
  <dd>- `$\lim_{t \rightarrow \infty} \sup ||e(t)|| \leq \frac{1+\sqrt{\lambda_{\text{max}}\bar{P}}}{\alpha \sqrt{\lambda_{\text{min}}\bar{P}}} M_v \equiv R^*$`</dd>
</dl> 
</section>


<section>
<h1> Illustrative example</h1>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
\begin{align}
\dot{x}&=A_m x+Bu +v_x\\\
&=\begin{bmatrix}
-4 &1 &2\\\
-1 & -1 & 1\\\
-1 & 1 &-1 
\end{bmatrix}x+B u +v_x \\\
y&=Cx
\end{align}

</div>



<div class="col">
\begin{align}
\dot{x}&=A x+Bu +v_x\\\
&=\begin{bmatrix}
-2.86 &1 &4.7\\\
1.8 & -1 & 6.7\\\
-9 & 1 &-1 7.2
\end{bmatrix}x+B u +v_x\\\
y&=Cx
\end{align}
<br>

</div>

</div>

<br>
`\begin{align}
L*=\begin{bmatrix}
-8 & 1\\\
2 & -7
\end{bmatrix}
\end{align}`


`\begin{align}
u_1(t)&=c_{11} \sin(2t)+ c_{12} \cos(2t) + c_{13} \sin(7t) + c_{14} \cos(7t)
\end{align}`
`\begin{align}
u_2(t)&=c_{11} +c_{22}t+c_{23}t^2+c_{24}t^3
\end{align}`

</section>

<section>
<h1> Illustrative example</h1>
<h3> Both the state error and the input error converge simultaneously </h3>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
<h3> Internal state error as a time series </h3>
<figure>
  <img src="img/defense/x_ex2.gif" alt="Trulli" height="500">
</figure>
</div>



<div class="col">
<h3> Estimating two unknown inputs </h3>
<figure>
  <img src="img/defense/u_ex3.gif" alt="Trulli" height="500">
</figure>

</div>

</div>
</section>




---

<!-- .slide: data-background="#003C71" class="dark" -->

# 6. Reconstructing the Brain's Unknown Input
Recall: Solving the nonstationary problem

---


<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO outperforms static modes </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/square_L.gif" alt="Trulli" height="750">
</figure>
</div>



<div class="col">

<h3> Weighted modes on seen data </h3>
<figure>
  <img src="img/defense/square_noL.gif" alt="Trulli" height="750">
</figure>



</div>

</div>

----


<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO critically updates model as needed </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/square_L.gif" alt="Trulli" height="750">
</figure>
</div>



<div class="col">

<h3> Adaptive gain matrix 2-norm </h3>
<figure>
  <img src="img/defense/Ly.gif" alt="Trulli" height="750">
</figure>



</div>

</div>

----

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Modeling details </h2>

 <ul>
  <li>Unknown input acts evenly over spatial domain</li>
  <li>$F_u$ generates sine-cosine basis</li>
  <li>Static gains per LQR </li>
</ul> 

----

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> aUIO is tolerant to parametric uncertainty in modes </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<h3> aUIO on unseen data </h3>
<figure>
  <img src="img/defense/no_eye.gif" alt="Trulli" height="600">
</figure>
</div>



<div class="col">

<h3> aUIO with wrong $A_m$ </h3>
<figure>
  <img src="img/defense/eye.gif" alt="Trulli" height="600">
</figure>



</div>

</div>

----

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification via estimation </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<figure>
  <img src="img/defense/val_arou.jpg" alt="Trulli" height="400">
</figure>

</div>



<div class="col">

<figure>
  <img src="img/defense/classification_alg.png" alt="Trulli" height="300">
</figure>



</div>

</div>

----

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification via estimation </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
<h3> Valence Classification </h3>
<figure>
  <img src="img/defense/val_acc.png" alt="Trulli" height="600">
</figure>

</div>

<div class="col">
<h3> Arousal Classification </h3>
<figure>
  <img src="img/defense/arou_acc.png" alt="Trulli" height="600">
</figure>


</div>

</div>
<div style="text-align: right"> <sub><sub><sup><a href="https://dl.acm.org/doi/10.5555/3297863.3297883">CNN1</a>, <a href="https://www.sciencedirect.com/science/article/abs/pii/S0010482521005515">CNN2</a>, <a href="https://www.frontiersin.org/articles/10.3389/fnbot.2020.617531/full">MFDF</a></sup></sup></sub></div>


----

<h1> Reconstructing the Brain's Unknown Input </h1>
<h2> Classification validation </h2>
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">
<table style="width:80%">
  <tr>
    <th>Task</th>
    <th>aUIO Acc. [%]</th>
    <th>PSD CNN Acc. [%]</th>
  </tr>
  <tr>
    <td>DEAP Valence</td>
    <td>77.8</td>
    <td>68.1</td>
  </tr>
  <tr>
    <td>DEAP Arousal</td>
    <td>75.2</td>
    <td>63.8</td>
  </tr>
  <tr>
    <td>Like/Dislike</td>
    <td>79.4</td>
    <td>67.3</td>
  </tr>
  <tr>
</table>


</div>

<div class="col">
<h3> Static gain grid search </h3>
<figure>
  <img src="img/defense/DEAP_accs.png" alt="Trulli" height="600">
</figure>


</div>

</div>



---

<!-- .slide: data-background="#003C71" class="dark" -->

# 7. Conclusions


---
# Summary

- Modern, sys-id techniques work on biomarker data
- Modal representation aids interpreation and analysis
- Complete body of UIO work
- Online estimation of nonlinear brain wave dynamics

---

# Future work

- Multiple data types
- Improved analysis and classification
- Probablistic considerations

---

<!-- .slide: data-background="#003C71" class="dark" -->

# Acknowledgements

----

<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<img src="https://engineering.tamu.edu/cse/_files/_images/_profile-images/chaspari-theodora-25April2019.jpg" alt="Trulli" height="500">
  <figcaption>Theodora Chaspari </figcaption>
</div>

<div class="col">
<figure>
  <img src="https://engineering.tamu.edu/mechanical/_files/_images/_profile-images/saripalli.jpg" alt="Trulli" height="500">
    <figcaption>Srikanth Saripalli</figcaption>
</figure>
</div>

</div>

----

<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<img src="https://www.nasa.gov/sites/default/files/styles/side_image/public/thumbnails/image/balas-mark-biowebsite.jpg?itok=LxO5H0UR" alt="Trulli" height="500">
  <figcaption> Mark Balas </figcaption>
</div>

<div class="col">
<figure>
  <img src="img\defense\prof.jpg" alt="Trulli" height="500">
    <figcaption>James Hubbard</figcaption>
</figure>
</div>

</div>

----
<style>
.vertical-center {
  min-height: 100%;  /* Fallback for browsers do NOT support vh unit */
  min-height: 100vh; /* These two lines are counted as one :-)       */

  display: flex;
  align-items: center;
}

.container{
    display: flex;
}
.col{
    flex: 1;
}
</style>

<div class="container vertical-center">

<div class="col">

<a href="https://unsplash.com/photos/OhfWTDyJp3I"><img src="https://images.unsplash.com/photo-1602244547823-8bebf9920b35?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=1173&q=80"></a>

</div>

<div class="col">
 <ul>
  <li> Dr. Vinod Gehlot</li>
  <li> Sarai Barnett </li>
  <li> Dr. JD</li>
  <li> Prof. Zohaib Hasnain </li>
  <li> Prof. Mike Walsh </li>
  <li>Zaryab Shahid</li>
  <li>Lise Ochej</li>
  <li>Kevin Fuentes</li>
</ul> 
</div>

</div>

----


<h3> Good TAMU </h3>
 <ul>
  <li> Sandra Havens </li>
  <li> Rebecca Simon </li>
  <li> Prof. Joanna Tsenn </li>
  <li> Kaustubh Mahesh Tangsali</li>
  <li> Briana Holton </li>
  <li> Bryton Praslicka </li>
  <li>Robert Trépanier</li>
  <li>Harold Gamarro</li>
</ul> 




---

<!-- .slide: data-background="#500000" class="dark" -->
# A Modal Approach to the Space Time Dynamics of Cognitive Biomarkers

> Highly organized research is guaranteed to produce nothing new.














---

<!-- .slide: data-background="#5B6236" class="dark" -->

## Backup: Best Fit B Matricies

----

<!-- .slide: data-background="#ffffff" class="light" -->

# *A* Convex Function for B matrix optimization
- $\min ||y-\hat{y}-C \Delta B \hat{u}||_2$
- ***not*** the only possible minimization

----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix Optimization Example
- 3x3 example
 - $\dot{\hat{x}} = A_m x + B \hat{u}$
 - $A_m \neq A$ 
- ***$\min ||y-\hat{y}-C \Delta B \hat{u}||_2$***
- $B=\begin{bmatrix} 1.2 \\\ 1 \\\ 1.6 \end{bmatrix}$, 
- $B_m=\begin{bmatrix} 1 \\\ 1 \\\ 1 \end{bmatrix}$




----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix Optimization Example
- $\min ||y-\hat{y}-C \Delta B \hat{u}||_2$
- $\Delta B=\begin{bmatrix} 0.18 \\\ 0 \\\ 0.37 \end{bmatrix}$, 
- $B_f=\begin{bmatrix} 1.18 \\\ 1 \\\ 1.37 \end{bmatrix}$

<img class="plain" src="img/bmat/toy_Bopt2.png" alt="Trial 5, Averaged" width="55%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix on EEG Data
<img class="plain" src="img/bmat/Bopt.png" alt="Trial 5, Averaged" width="90%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

# B Matrix on EEG Data
<img class="plain" src="img/bmat/B_ic.jpg" alt="Trial 5, Averaged" width="70%">


----


<!-- .slide: data-background="#ffffff" class="light" -->

# Current models
<img class="plain" src="img/bmat/UIO_opt.png" alt="Trial 5, Averaged" width="45%">
<img class="plain" src="img/bmat/Bmap2.png" alt="Trial 5, Averaged" width="45%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## 5. Application to Emotion Data

----



<!-- .slide: data-background="#ffffff" class="light" -->


## B Matrix on EEG Data: ***Satisfaction (T1)*** 
<img class="plain" src="img/bmat/sat_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Surprise (T2)*** 

<img class="plain" src="img/bmat/surp_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Fear (T8)*** 

<img class="plain" src="img/bmat/fear_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->
## Comparing the same "emotion"

<img class="plain" src="img/bmat/val.jpg" alt="Trial 5, Averaged" width="45%">

<div style="text-align: right"> <small>Mneimne, M., Powers, A. S., Walton, K. E., Kosson, D. S., Fonda, S., & Simonetti, J. (2010). Emotional valence and arousal effects on memory and hemispheric asymmetries. Brain and Cognition, 74(1), 10-17.</small></div>


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***HVHA*** 

<img class="plain" src="img/bmat/HVHA_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***HVLA*** 

<img class="plain" src="img/bmat/HVLA_map.png" alt="Trial 5, Averaged" width="60%">


----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***LVHA*** 

<img class="plain" src="img/bmat/LVHA_map.png" alt="Trial 5, Averaged" width="60%">



----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***LVLA***  

<img class="plain" src="img/bmat/LVLA_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Avg. Quadrants***  

<img class="plain" src="img/bmat/all_emot_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## 6. Application to Movement Data

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Left Hand***  

<img class="plain" src="img/bmat/lh_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Right Hand***  

<img class="plain" src="img/bmat/rh_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***Resting***  

<img class="plain" src="img/bmat/rest_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## B Matrix on EEG Data: ***All Averages***  

<img class="plain" src="img/bmat/all_hand_map.png" alt="Trial 5, Averaged" width="60%">

----

<!-- .slide: data-background="#ffffff" class="light" -->

## A unique solution?
- B matrix is different for everyone
 - A math construct or physical significance?
- A unique input?

