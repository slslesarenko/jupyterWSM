# Anisotropy of the 3D-printed samples
Date: 2019/04/08

Author: V. Slesarenko
## Summary 
I will answer questions from email and provide some additional experimental observations regarding anisotropy of printed samples.

## Questions 1 and 2 
1. _It seems the structures are 3D-printed. Typically this induces anisotropy based on the print direction. Is this also true here? Do you have a feel for the variability of the experiments with respect to changing the print direction?_ 
2. _Do you have a feel for the variability of the experiments with fixed print direction? I'm wondering if the failure is repeatable (e.g. does it always initiate at the same location? does the peak load change drastically? etc.). I don't have a good feel for whether the failure occurs due to something that could be captured with a model based on a homogeneous continuum or if variations in imperfections from the 3D printing process are dominating the failure response._

You are absolutely right that in general 3D-printed specimens are quite anisotropic. There are two different mechanisms that cause the anisotropic behavior: 
1. Anisotropy due to different orientation in the building tray. This effect can be observed in homogeneous samples which are placed with the various orientation relative to the movement of the printing head. It seems that this effect in relation to the elasic modulus and failure behavior is quite small in our case for pure TangoPlus material (see experiments in the next section)
2. Anisotropy that occurs due to the boundary between materials (like VeroWhite and TangoPlus). This effect can be observed in the multimaterial composites, and it is mainly associated with the formation of transition/interphasial layer on the boundary between materials. This layer has mechanical properties that gradually change through its thickness, and the estimates of its thickness are ranging from 40 microns (2 printing layers) up to 150 microns (apprx. 8 layers). Therefore, if stiff inclusions are quite small, the contribution of this interphasial layer (that also depends on the printing direction) can be significant. There is no simple way to work with this effect, but in many cases we can at least temporary ignore it. 

## Supporting experiments 
The building tray of the printer with the marked direction is shown below. 

<img src="images/objettray.jpg" width="80%" />

I printed three DENT samples with the notch length 3.6 mm (Design 1 from previous report) for each direction. Visually you can see the difference in the orientation on the videos. 

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_smallnotch_dirA_s1.mp4"  width="100%" /> 
</p>

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_smallnotch_dirB_s1.mp4"  width="100%" /> 
</p>

<img src="images/st_force_des1.png" width="80%" />

However suprisingly, all 6 specimens have very similar force-displacement curves. Moreover, closer inspection of the crack surface shows that even for specimens in B directions, the crack path does not necessary follow the boundary between print layers. **Therefore, the mechanical behavior of these homogeneous specimens can be considered as isotropic, and the failure occurs due to the intrinsic behaviour of material, rather than imperfections in 3D printing.**

Additionally I printed two specimens with holes (Design 3) for each of the directions. Their mechanical behavior is also very similar, and the corresponding force-displacement curves can be found below. You can also see a little discrepancy between failure behavior which may be caused by some small imperfections or by not ideal mounting of the specimens into the jigs. I don't think that this discrepancy is very important, because in general failure occurs in the same locations. 

<img src="images/st_force_des3.png" width="80%" />

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_twoholes_dirA_s1.mp4"  width="100%" /> 
</p>

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_twoholes_dirA_s2.mp4"  width="100%" /> 
</p>

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_twoholes_dirB_s1.mp4"  width="100%" /> 
</p>

<p>
<video controls src="videos/phase2/cc_dec_wais2_w24_twoholes_dirB_s2.mp4"  width="100%" /> 
</p>



## Question 3
_Does he have papers that discuss this or attempt to model this material? What additional complexity of the material do the constitutive models fail to predict sufficiently?_

These soft materials can withstand high elongation, but this is not a big problem. Yeoh or even neo-Hookean model desribes them quite well until the rate-dependency of their properties is taken into account. The stiffness and critical strain of failure may depend on the strain rate. While Young's modulus for TangoPlus is not very sensitive in the quasistatic regime, the difference in the critical strain is significant. We tried to describe the behavior of this material (without taking into accout failure) in [this paper](https://doi.org/10.1016/j.ijengsci.2017.11.011). The situation is even more complicated, when the mixed mode failure can happen. I refer you to the recent paper of our colleagues, in which TangoPlus material acts as the interface between stiff components ([link](https://doi.org/10.1016/j.jmps.2018.03.016)). **Therefore, we can do interesting experiments with composites, but we should be extremely careful here. In relation to the failure, we can, for instance, adopt models with energy limiters by Volokh (similar to the applied in the above mentioned paper for mixed modes) or any other failure model, which you are familiar with**

## Remark 1
_I agree with the idea that validation of a constitutive model for this material is likely quite complex. Since I'm not familiar with this material, I don't have a full understanding of the underlying complexity that is referenced. If the experimental variability is high, then I'm not sure what could be done here but if the variability is reasonably low then perhaps one could do the following: 1) Perform some simple tension experiments in order to obtain the undamaged properties. 2) Subsequent calibration of the parameter(s) governing fracture could be performed for some specific simple experiment like the ones you provided with failure. 3) Then, for different geometry, the model prediction could be compared to the experimental data._

As I see for now, the variability is quite low if we are taking into account all above mentioned issues. **Can we characterize material using DENT specimens with different notch length, as I did previously?**

## Remark 2
_Professor Waisman suggests that perhaps for some simple geometry (like the one provided with 3 inclusions) the geometric effect of the spacing or initial notch length could be parametrically studied._

Yes, we can actually do this. Let's initally focus on this problem, because it seems feasible for the first tests.

_A longer-term, significantly more difficult and complex option would be to optimize the shape of the inclusion phase in a two-phase composite (exactly like what you have) in order to maximize the fracture resistance. This has been previously explored without hyperelasticity in this reference for instance:_

I think that this study should be definitely guided from your side. Taking into account our restrictions, we need to select the structure we want to optimize. 

## Remark 3
_The thickness of 2.5mm seems to indicate that a plane-stress assumption would be more accurate if the simulations were performed in 2D (simply to reduce the computational expense). Most of the numerical models I am aware of for hyperelasticity can easily accomodate plane strain but I am not familiar enough with the implementation of a plane stress constraint with large deformations. I will need a little time in order to determine this._

I also don't see any problems with the implementation of hyperelasticity in plane stress. 

## Remark 4
_Finally, when I get some time I could look at trying to use an existing implementation of phase field fracture with hyperelasticity in 2D with a plane-strain assumption (which would introduce some inaccuracy) for one of the simple geometries you provided experimental results for. This would be just to see how far off the prediction is with regard to the failure pattern. Hopefully I will have some time soon to look at this._

It would be great if we could compare failure behavior or even strain field for the cases with inclusions. I will try to randomly play with different arrangements of the inclusions, but for comparison we definitely need the corresponding numerical implementation.

## Summary and future plans
It seems like we on the same page regarding future research. Let me try to obtain set of experimental results on the system with 3 inclusions, while you will look through the implementation of the appropriate models. 

Thanks a lot!




