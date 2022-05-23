# Gm over Id methodology
An overview of Gm over Id methodology.

## Why gm controls the speed
From the simple small signal model of a MOSFET (just gm and ro) we calculate Av as vout/vin and we get Av = gm * ro.

Then we calculate the BW, to do that we just put in a load cap CL (we don't even consider device caps), so that gives a simple RC circuit, simple Low Pass filter with one pole given by 1/ro * CL, in this basic single pole system the bandwidth is equal to the pole.

Then we multiply Av * BW to get the Gain-Bandwidth product (this is the same we do in amplifiers where we obtain the unity gain frequency omega_u = Ao * |p1|).

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


## The MOSFET

This is the OLD-SCHOOL MOSFET MODEL, LONG CHANNEL MOSFET model:
* NMOS channel is the **INVERSION LAYER**. Substrate is p-type (if it's an NMOS) but it "becomes" n-type due to the attracted electrons which form the channel.
* **The INVERSION LAYER starts to form when VGS > VTH (channel formation, conduction starts, OFF to ON).**
* Where VTH is any thing from 0.3V to 1V.
* When VGS is larger than VTH (conduction) we say **VGS is equal to VTH + some overdrive (Vov)**.
* If you keep increasing VGS for a constant VD OR if you increase VDS too much, you reach the point where you PINCH-OFF the channel.
* The **PINCH-OFF happens IF VGD VTH** (like not enough "VGD" to form a channel at the Drain edge). And that's the **start of the SATURATION REGION**. If you do a tiny bit of math you see that **the condition for Saturation VGD VTH is the same as saying that VDS >= Vov**.
* Finally, once we are in SATURATION the drain current is given by the SQUARE LAW:


<img src="https://render.githubusercontent.com/render/math?math=$I_D =\frac{\mu_n C_{\mathrm{ox}} }{2}\frac{W}{L}{\left(V_{\mathrm{GS}} -V_{\mathrm{TH}} \right)}^2 =\frac{\mu_n C_{\mathrm{ox}} }{2}\frac{W}{L}V_{\mathrm{ov}}^2$">


![image](https://user-images.githubusercontent.com/95447782/169861605-d82edce8-8922-468b-81a2-ac677d864df0.png)


But the problem with this model is that it's not very good for SHORT CHANNEL MOSFETs.

See that the SQUARE LAW fits quite well the actual characteristic for the LONG CHANNEL device (blue curve).

But the SQUARE LAW does NOT fit well the actual characteristic of the SHORT CHANNEL device (red curve).

![image](https://user-images.githubusercontent.com/95447782/169862807-c7a3cd2f-28c3-4d06-b89f-075cccb704c5.png)


