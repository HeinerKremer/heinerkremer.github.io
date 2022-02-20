---
layout: page
title: Research
permalink: /research/
---

<style TYPE="text/css">
code.has-jax {font: inherit; font-size: 100%; background: inherit; border: inherit;}
</style>
<script type="text/x-mathjax-config">
MathJax.Hub.Config({
    tex2jax: {
        inlineMath: [['$','$'], ['\\(','\\)']],
        skipTags: ['script', 'noscript', 'style', 'textarea', 'pre'] // removed 'code' entry
    }
});
MathJax.Hub.Queue(function() {
    var all = MathJax.Hub.getAllJax(), i;
    for(i = 0; i < all.length; i += 1) {
        all[i].SourceElement().parentNode.className += ' has-jax';
    }
});
</script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-AMS_HTML-full"></script>


Here you can find high-level introductions into my work in various fields. Check out my [Google scholar](https://scholar.google.com/citations?user=I_9TrpgAAAAJ&hl=en) for a comprehensive list of publications.

 <h2> Causal Inference via Method of Moments </h2>
Important problems in causal inference, economics, and, more generally, robust machine learning can be cast as moment restrictions. 
Moment restrictions identify a parameter of interest by restricting the expectation value of so-called moment functions which depend on the parameter as well as one or more random variables representing the underlying data generating process. 

One prominent example which has gained recent popularity in the machine learning community is nonparametric instrumental variable (IV) regression: we aim to infer the causal relationship $f$ in the structural equation model $Y = f(X) + \varepsilon$ where $\varepsilon$ and $X$ are correlated because of an unobserved confounder $U$ (see below).

<p align="center">
<img width="40%" src="/assets/iv_image.jpg">
</p>


If there exists a random variable $Z$ which causes $X$ (relevance) but is independent of the unobserved confounders (exchangeability) and influences $Y$ only through $X$ (exclusion restriction), then it is possible to alleviate the effect of the unobserved confounders. 
Under these assumptions, the IV problem can be formulated as a conditional moment restriction. 
Traditionally, the IV problem has often been solved via two-stage procedures where one first estimates the conditional expectation $E[X|Z=z]$ and subsequently regress $Y$ on this estimate.
As conditional moment restrictions are difficult to handle directly, an alternative approach consists of transforming them into an infinite number of unconditional moment restrictions.

Our current work (under review) is concerned with developing methods which can take into account such infinite dimensional moment restrictions while maintaining the strong statistical guarantees of their finite dimensional counterparts.
Stay tuned for more information here.


 <h2> Epidemiological Modelling </h2>
Our work on epidemiological modelling was concerned with the development of an agent-based model to investigate the effects of different intervention and contact tracing strategies in the context of the Covid-19 pandemic. The first publication introduces the model and demonstrates its flexibility by exploring various containment measures. The second manuscript provides a comparison between different contact tracing paradigms: user device to user device vs. user device to bluetooth beacon. In this context we introduce PanCast, a beacon-based contact tracing system, which combines the benefits of the latter approach with strong security and privacy guarantees. 

Refer to the description below or the papers for more details.


<details>
<summary> <b> Quantifying the Effects of Contact Tracing, Testing, and Containment Measures in the Presence of Infection Hotspots </b> <a href="https://arxiv.org/abs/2004.07641">(paper)</a> <a href="https://github.com/covid19-model/simulator">(code)</a> </summary>

<br/>
<i> The following description is taken from our <a href="https://github.com/covid19-model/simulator">github page</a>.</i>
<br/>
<br/>


 Motivated by several lines of evidence suggesting for <i>superspreading events</i> or infection hotspots to play a key role in the transmission dynamics of COVID-19, we introduce an epidemiological modeling framework that explicitly represents visits to sites where infections occur or hotspots may emerge. We use temporal point processes to represent the state of each individual over time with respect to their mobility patterns, health, and testing status. The model leverages the locations of publicly available data on real-world sites and population density in a heuristic mobility model of a given region (below: Bern, Switzerland), whose assumptions can be arbitrarily generalized.

<p align="center">
<img width="100%" src="/assets/covid/BE-sites.jpg" style="margin-top: 1em;">
</p>



Bayesian optimization is used to estimate mobility-related exposure parameters by fitting the model to  true observed case counts in a considered area. In our work on COVID-19, we study several regions in Germany and Switzerland, whose models were fit to real case counts over two-month windows before and during the "lockdown" in spring 2020:

<p align="center">
<img width="100%" src="/assets/covid/BE-estimation-1.png" style="margin-top: 1em;">
</p>

Using the estimated parameters of the region-specific models, the sampling algorithm allows for analyses of counterfactual scenarios under various local circumstances. 

Contrary to existing agent-based epidemiological models, under our framework, the number of infections caused by infected individuals naturally emerges to be <i>overdispersed</i>, i.e., exhibiting greater variance than expected under the common Poisson assumption (here: fitted negative binomial distribution of the secondary infections overall and during a single site visit, respectively).



<p align="center">
<img width="49%" src="/assets/covid/BE-nbin-secondary-1.jpg" style="margin-top: 1em;">
<img width="49%" src="/assets/covid/BE-nbin-visit-exposures-1.jpg" style="margin-top: 1em;">
</p>



Amongst several other things, this framework allows for studying the effects of: the effective reproduction number, infections, hospitalizations, and fatalities over time during, e.g., mobility reduction, contact tracing, and testing measures, targeting not only the broader population, but also specific sites or individuals.



<p align="center">
<img width="49%" src="/assets/covid/BE-mobility-reduction-reff-1.jpg" style="margin-top: 1em;">
<img width="49%" src="/assets/covid/BE-mobility-reduction-hosp-1.jpg" style="margin-top: 1em;">
</p>



<p align="center">
<img width="100%" src="/assets/covid/BE-tracing-infected-over-time-1.jpg" style="margin-top: 1em;">
</p>

</details>

<br/>

<details>
<summary> <b>Listening to Bluetooth beacons for epidemic risk mitigation </b> <a href="https://www.medrxiv.org/content/10.1101/2021.01.21.21250209v1.abstract">(paper)</a> <a href="https://github.com/covid19-model/simulator/tree/beacon">(code)</a> </summary>

<br/>

During the ongoing COVID-19 pandemic, there have been burgeoning efforts to develop and deploy smartphone apps to expedite contact tracing and risk notification. Unfortunately, the success of these apps has been limited, partly owing to poor interoperability with manual contact tracing, low adoption rates, and a societally sensitive trade-off between utility and privacy. In this work, we introduce a new privacy-preserving and inclusive system for epidemic risk assessment and notification that aims to address the above limitations. Rather than capturing pairwise encounters between smartphones as done by existing apps, our system captures encounters between inexpensive, zero-maintenance, small devices carried by users, and beacons placed in strategic locations where infection clusters are most likely to originate. Epidemiological simulations using an agent-based model demonstrate several beneficial properties of our system. By achieving bidirectional interoperability with manual contact tracing, our system can help control disease spread already at low adoption. By utilizing the location and environmental information provided by the beacons, our system can provide significantly higher sensitivity and specificity than existing app-based systems. In addition, our simulations also suggest that it is sufficient to deploy beacons in a small fraction of strategic locations for our system to achieve high utility.

<br/>
<br/>

The figure below shows PanCast's architecture: 1. Beacons and user devices are registered with the backend. 2. User devices record encounters with BLE beacons. 3a. Diagnosed users or healthy volunteers may upload their history of encountered beacons to the backend via a terminal. 3b. Optionally, health workers can manually feed inputs from users into the backend system. 4. The backend updates the risk database with uploaded encounters. 5. Risk information is periodically broadcast from the backend to network beacons, which broadcast the information to nearby user devices.
<p align="center">
<img width="100%" src="/assets/covid/arch3.png" style="margin-top: 1em;">
</p>

More details on the functionality of the involved components can be found in below visualization.

<p align="center">
<img width="100%" src="/assets/covid/pancast_overview.pdf" style="margin-top: 1em;">
</p>

<br/>

In the following we provide an extract of our simulation results on the comparison between PanCast (or other beacon-based systems) and <i>smartphone-based pairwise-encounter-based contact tracing systems</i> (SPECTS).

<br/>
<br/>

<b> Interoperation with manual tracing can improve efficacy at low adoption levels </b>

To explore the effect of PanCast's interaction with manual contact tracing, we combine either PanCast or SPECTS with manual contact tracing in a scenario where transmission rates are independent of the site type, i.e., the infection probability of a susceptible person does not depend on the place where the contact with an infected individual happened. This allows us to explore the effect of interaction with manual tracing independent of PanCast's advantage of utilizing environmental information. While SPECTS and manual contact tracing operate independently of each other, PanCast and manual contact tracing can benefit from each other by exchanging information (see \emph{Materials and Methods} for details).

For both systems, tracing is initiated whenever the inferred exposure risk of a person exceeds the threshold of a $15$ minute contact with an infected individual. We assume sufficient testing and isolation capacities for all individuals selected for tracing by a digital system or via manual contact tracing.

The figure below shows the reduction of the number of infections achieved by the tracing systems with respect to the baseline scenario in which only manual contact tracing is employed. By mitigating the $x^{2}$-adoption problem of contact tracing (i.e., if a random person has adopted the tracing system with probability $x$, a random contact can be traced with probability $x^{2}$) via interoperation with manual tracing, we observe that PanCast generally scales more favourably with decreasing adoption levels than SPECTS.

<p align="center">
<img width="100%" src="/assets/covid/comparison-cumu_infected-GER-TU-reduction=True-box_plot=True-beacon_mode=visit_freq-manual_tracing=True-p2p+beacons=False.pdf" style="margin-top: 1em;">
</p>


<br/>

<b>Utilization of environmental information improves tracing accuracy </b> 

Environmental factors such as indoor vs. outdoor, room size, ventilation, and air quality, have been shown to lead to vastly different transmission rates. To evaluate the effect of using such environmental information to improve contact tracing decisions, we simulate scenarios in which different site types have different transmission rates. As an example, we assume contacts with infected individuals at social sites, i.e., restaurants, bars and cafes to be ten times more likely, and contacts at bus stops to be ten times less likely to lead to infection than the default.

Unlike SPECTS, PanCast has access to environmental information and can therefore use the known variable transmission rates to estimate infection probabilities in our simulations. The SPECTS simulation uses an average transmission rate to calculate infection probabilities and make tracing decisions.

The figure below compares PanCast's and SPECTS receiver operating characteristic (ROC) curves computed by varying the tracing threshold, i.e., the infection probability above which contacts are selected for tracing, from $0$ to $1$. We observe that for every fixed sensitivity (true positive rate) PanCast achieves a larger specificity (i.e., smaller false positive rate), implying that PanCast can detect the same proportion of infected individuals as SPECTS while imposing a smaller burden on the population in terms of a smaller number of unnecessarily quarantined individuals. 

<p align="center">
<img width="50%" src="/assets/covid/ROC-GER-TU-multiplot-False-manual-tracing=True-beta-dispersion=10.0.pdf" style="margin-top: 1em;">
</p>

The additional figure below shows the sensitivity and specificity of the two tracing systems against the tracing threshold for different site types. We see that on average PanCast provides larger sensitivity and approximately equal specificity compared to SPECTS for every value of the threshold.

Further, we observe that within our simulation SPECTS overestimate the infection probability at education, office and supermarket sites while underestimating it at social sites, which explains the larger false positive rate for a given true positive rate as compared to PanCast.

<p align="center">
<img width="100%" src="/assets/covid/site-dependent-characteristics-beta_dispersion=10.0.pdf" style="margin-top: 1em;">
</p>

Please refer to the <a href="https://www.medrxiv.org/content/10.1101/2021.01.21.21250209v1.abstract">paper</a> for more information.

</details>

<br/>
 <h2> Computer Generated Holography </h2>
Holography describes the phenomenon of plane waves forming complicated structures by modulation of their phases.
Computer generated holography is concerned with the computation of the required phase modulation in order to produce a desired target intensity pattern. In the optical case the phase modulation can be achieved with a spatial light modulator (SLM). In our case, we are interested in forming ultrasound fields to manipulate particles, which can be described as <a href="https://www.nature.com/articles/nature19755"><i>acoustic holography</i></a>. In this case the phase modulation can be achieved by sending plane waves through 3D-printed plastic plates with spatially varying thickness, such that spatially-dependent phase delays are induced as the wave takes different times to pass at different locations within the plate.

<p align="center">
<img width="100%" src="/assets/holography.jpg" style="margin-top: 1em;">
</p>
Image taken from: Kai Melde, Andrew G. Mark, Tian Qiu & Peer Fischer. Holograms for acoustics. Nature volume 537, pages 518–522 (2016).

Acoustic holography allows for manipulation of acoustic fields in unprecedented detail. Casting the hologram computation for a given target intensity pattern as an inverse problem allows us to leverage optimization and machine learning tools. Our work is concerned with developing novel computation methods to enhance the quality of the generated intensity fields.

See below for a holographically generated Stanford armadillo (Image credits: Kai Melde).
<p align="center">
<img width="150%" src="/assets/armadillo.mp4">
</p>

