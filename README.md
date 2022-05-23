# Gm over Id methodology
An overview of Gm over Id methodology.

## Why gm controls the speed
From the simple small signal model of a MOSFET (just gm and ro) we calculate Av as vout/vin and we get Av = gm * ro.

Then we calculate the BW, to do that we just put in a load cap CL (we don't even consider device caps), so that gives a simple RC circuit, simple Low Pass filter with one pole given by 1/ro * CL, in this basic single pole system the bandwidth is equal to the pole.

Then we multiply Av * BW to get the Gain-Bandwidth product (this is the same we do in amplifiers where we obtain the unity gain frequency omega_u = Ao * ¦p1¦).

At that point we see that ro cancels out so the only thing that defines GBW is gm.

GBW is what defines speed (responsiveness) of the circuit when we apply negative feedback.

So that's why at the end of the day gm is what defines speed.

![image](https://user-images.githubusercontent.com/95447782/169857997-3428e288-4a72-4d3d-8e8d-21f6f9242d05.png)


## gm also controls the noise
MOSFET thermal noise (input referred noise of the device) ends up being proportional to the INVERSE of gm.

So, more gm less noise.

![image](https://user-images.githubusercontent.com/95447782/169858135-e84d9715-69b5-4bc3-a7c7-8cbc2140d25d.png)

## Motivation for a gm/Id methodology

First, let's define the concept of Transistor Efficiency, TE, as the ratio between gm and the bias current that we need to burn in order to get that gm.

![image](https://user-images.githubusercontent.com/95447782/169858303-a97b762e-cda7-4eb5-bb05-5dca062a0964.png)


### Why a gm/Ic methodology didn't make sense for BJTs

In the BJT the TE (transistor efficiency = gm/Iq) is CONSTANT, regardless of what Ic you give it. Low or high, it doesn't matter. **Your gm/Ic is CONSTANT in the BJT.**

![image](https://user-images.githubusercontent.com/95447782/169858435-94b3e368-41c0-40cf-900a-f0cca1eac66b.png)

For the BJT there is no gm/Id methodology because the TE is CONSTANT. So in the BJT days no one talked about gm/Id methodology.

For the BJT, since the Ic is an exponential of VBE, the LOG (LN) of the Ic is proportional to VBE.

Now, if you differentate the LOG of the Ic with respect to VBE, you get 1/Vt which is the same as gm/Ic we got before.

![image](https://user-images.githubusercontent.com/95447782/169858477-7812e4ee-71e5-452a-81f0-4fec588c1267.png)

We simply OBSERVE THE FACT that the SLOPE OF THE LOGARITHMIC VERSION OF THE CURRENT HAPPENS TO BOIL DOWN TO THE SAME VALUE AS THE GM/ID.

And therefore we say **TRANSISTOR EFFICIENCY TE IS (PROPORTIONAL TO) THE SLOPE OF THE LOGARITHMIC VERSION OF THE CURRENT**.

Later on we will use this PROPERTY as a TOOL, simply because it's HANDY to know that we can PLOT THE CURRENT IN LOGARITHMIC SCALE (i.e. plot the LOG of the Id) VERSUS VGS, LOOK AT THE SLOPE OF THAT, AND THE SLOPE OF THAT GRAPH IS THE GM/ID.

Overall, 
* **the SLOPE OF THE CURRENT (VERSUS VGS) IS GM**
* **the SLOPE OF THE LOGARITHM OF THE CURRENT (VERSUS VGS ALSO) IS "PROPORTIONAL" TO GM/ID** (so it's not the exact gm/Id value but it's an indication of BIG gm/Id or SMALL gm/Id, which is that same as BIG TE or SMALL TE).

At the end of the day what matters here is: **in the BJT the TE is CONSTANT so no point in a gm/Ic methodology for BJTs.**

