## Additive Manufacturing Suitability Factor
<p><b>If you use this notebook, please refer to the following papers:</b></p>
<p><b>1. A. Yankin, H.A. Murtaza, A. Ospanov, G. Zharkynbekova, D. Yuldasheva, A. Perveen, D. Talamona, "Comprehensive analysis of ultrasonically atomized 316L stainless steel powder using adjusted additive manufacturing suitability factor," Powder Technology, vol. 444, 2024, p. 120004</b>. https://doi.org/10.1016/j.powtec.2024.120004 </p>
<p><b>2. [Add reference here]</b></p>

To quantify the processability of Additive Manufacturing, [Brika et al](https://doi.org/10.1016/j.addma.2019.100929) introduced a metric known as the Additive Manufacturing Suitability (AMS) factor, which is defined as:
<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/ea1eb40753f4c1123c492340cbf80920914f20db/1.png" width="800" title="hover text">
</p>

In this equation, all parameters are normalized according to their maximum values among all tested powders. Notably, the CBD is multiplicatively inversed and then normalized. It is also crucial to emphasize that while each parameter in Equation 1 holds an equal weight of 1/7, adjusting the weighting factors can offer advantages in different scenarios [[Habibnejad-korayem et al](https://doi.org/10.1016/j.powtec.2021.07.026)].

Combining all the aforementioned considerations into a unified perspective, the AMS with weighting factors (w) can be reformulated as follows:
<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/2.png" width="800" title="hover text">
</p>

where k = 1,…,K represents the number of powders analyzed, n = 1,…,N denotes the number of parameters utilized for comparative analysis, and Pkn signifies a parameter (such as CBD, CI, PD, etc.).


It is crucial to note that Equation 2 can sometimes yield contentious outcomes. For instance, let's examine two powders with parameters outlined in Fig. 1, each assigned equal weights for simplification. Following normalization and calculation of AMS, it appears that the 1st powder surpasses the 2nd. However, upon introducing a new powder, the results can invert, as depicted in Fig. 1, where the 2nd powder outperforms the 1st.

This discrepancy arises because the relationship between AMS1 and AMS2 at k = 2 may not necessarily mirror that at k = 3, given that the denominator of Equation 6 (max{P1n,…,PKn}) could change with the inclusion of a new powder. In the provided example, values of the first parameter of the first and second powders are substantially smaller than those of the third powder. Consequently, the normalized values of the first parameter for the first and second powders approach zero, thereby amplifying the contribution of the second parameter to AMS.

However, the models purpose is to yield consistent outcomes regardless of the quantity of powders considered. To address this issue, we can implement a logarithmic transformation:

<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/3.png" width="800" title="hover text">
</p>

While AMS ranges from 0 to 1, the transformation (3) spans from -∞ to 0. To standardize it with the range of Equation 2, let's elevate (3) to the 10th power. After all transformations, the modified AMS can be expressed as follows:

<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/4.png" width="800" title="hover text">
</p>

Now, the relationship between AMSF1 and AMSF2 at k = 2 is equal to that at k = 3, as the denominator of Equation 4 (max{P1n,…,PKn}) cancels out during division (Fig. 1).

<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/Fig_1.png" width="700" title="hover text">
  <p align="center">Fig. 1. Comparison of the controversial results from the conventional AM suitability factor versus the consistent outcomes of the modified version.</p>  
</p>

Weighting factors could vary depending on the situation; for instance, in scenarios involving prolonged cyclic loading, parameters affecting fatigue resistance might carry greater significance (assigned a higher weight). Similarly, in scenarios focusing on corrosion protection, parameters influencing corrosion resistance would be prioritized. 

When there is no clear understanding of the relationships between powder parameters and the desired behavior of printed parts, parameter weights can be determined based on the accuracy of their measurement. Parameters with higher coefficients of variation should have less impact on the resulting AMS values and thus be assigned smaller weighting factors, thereby reducing the influence of parameters with greater uncertainty. The formula for calculating these weights is as follows:

<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/5.png" width="800" title="hover text">
</p>

where CVn denotes the coefficient of variation for the nth parameter in the experiment.

In the [paper](https://doi.org/10.1016/j.powtec.2024.120004), weighting factors for CBD, CI, PD, SE, AE, BFE, and 'c' were calculated based on the median values of coefficients of variation for the rheological parameters derived from an extensive literature review. Specifically, the weighting factors were 0.54 for CBD, 0.1 for CI, 0.1 for PD, 0.11 for SE, 0.02 for AE, 0.11 for BFE, and 0.02 for 'c'.

<p align="center">
  <img src="https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/Fig_2.png" width="600" title="hover text">
  <p align="center">Fig. 2. Methodology steps for calculating AMSF.</p>
</p>

Therefore, the presented approach enables the formulation of a unified methodology for conducting comparative analysis of two or more similar powders, based on specific parameters. The method is illustrated schematically in Figure 2 and implemented in [Jupyter + Python](https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/AMSF.ipynb) or [MS Excel](https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/4c3d5f8a8449e30a3c611a0b5377d3ccc476a5b9/AMSF.xlsx) software.

All used libraries were saved in files [requirements.txt](https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/8a81c3b342c34bb39dda704d5b840af72d43fae8/requirements.txt) and [environment.yaml](https://github.com/yanicen1/Additive-Manufacturing-Suitability-Factor/blob/8a81c3b342c34bb39dda704d5b840af72d43fae8/environment.yml) for conda.

<p><b>If you use this notebook, please refer to the following papers:</b></p>
<p><b>1. A. Yankin, H.A. Murtaza, A. Ospanov, G. Zharkynbekova, D. Yuldasheva, A. Perveen, D. Talamona, "Comprehensive analysis of ultrasonically atomized 316L stainless steel powder using adjusted additive manufacturing suitability factor," Powder Technology, vol. 444, 2024, p. 120004</b>. https://doi.org/10.1016/j.powtec.2024.120004 </p>
<p><b>2. [Add reference here]</b></p>

If you have questions, please feel free to contact me: 
Andrei Iankin, yas.cem.yanicen@gmail.com
