---
title: "Mplus Code for Measurement invariance and LCS model"
date: 2024-06-14 16:44:41
author: Yongkang Yang
tags:
  - measurement invariance
  - latent change score model
categories:
  - Research Method
---

#### Info
**Click this link to access the file**  [OSF link](https://osf.io/97yn4/)

**Reference**:

Li, W.-D., Wang, J., Allen, T.,  Zhang, X., Yu, K., Zhang, H., Huang, J. L., Liu, M., & Li, A.  (2024). Getting under the skin? Influences of work–family experiences on personality trait adaptation and reciprocal relationships. *Journal of Personality and Social Psychology, 126*(4), 694–718. [https://doi.org/10.1037/pspp0000476](https://psycnet.apa.org/doi/10.1037/pspp0000476)

<!--more--> 

> Strongly Recommend Prof. Wendong Li's Website for longitudinal research: [https://www.wendongli.com/index.php/for-sharing/ ](https://www.wendongli.com/index.php/for-sharing/) 

<h3><span style="color:#040273;">Latent change score model</span></h3>

<b>A Replication of [Matusik et al (2021)](https://doi.org/10.1177/1094428120963788)</b> 

The results and Mplus code can be found in this repo:

<b>Mplus Code of  [Steffen et al (2021)](https://psycnet.apa.org/doi/10.1037/apl0001042)</b> 

```Mplus syntax
Mplus syntax for hypothesis 1 sensitivity analysis

TITLE:	
    Merger paper H1

DATA: 
    FILE IS 'g:/my drive/merger/latent.dat';

VARIABLE:	
    NAMES ARE merge size js5 js7 abs5 abs7 ss5 ss7;
    USEVARIABLES ARE merge size js5 js7;
    
MODEL: 
    !Latent True Scores
    js1 BY js5@1;
    js2 BY js7@1;

    !Specifies the mean and variance of js1.
    [js1]; js1;
    !Fixes the mean and variance of js2 to 0.
    [js2@0]; js2@0;
    [js5-js7@0];
    !Sets the residual variances of js5 and js7 to be equal and labels them as resvar.
    js5-js7 (resvar);

    !Autoregressions
    js2 ON js1@1;

    !Latent Change Factors
    jsd BY js2@1;
    !Fixes the mean and variance of jsd to 0.
    [jsd@0];
    jsd@0;

    !Hypothesis
    jsd ON merge size;


OUTPUT:
    STAND CINT;
```