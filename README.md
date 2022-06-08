# Gm over Id methodology
An overview of Gm over Id methodology.

## Motivation for a gm/Id methodology

First, let's define the concept of Transistor Efficiency, TE, as the ratio between gm and the bias current that we need to burn in order to get that gm.

![image](https://user-images.githubusercontent.com/95447782/169858303-a97b762e-cda7-4eb5-bb05-5dca062a0964.png)

The transistor efficiency, defined as the ratio between gm and Id of a transistor at a specific bias point,

* ![equation](https://latex.codecogs.com/svg.image?TE=%20%5Cfrac%7Bg_m%7D%7BI_D%7D)

not only is a good representation of the trade-off between transconductance and quiescent current, but also serves as a valuable indicator for further design decisions.

The motivation for a gm/Id methodology stems from the fact that:
* in deep submicron nodes the **square law description of Id fails to describe device behaviour accurately**
* especially **for short channel devices in strong inversion**
* and also **for both long and short channel devices operating in weak inversion**

In addition to this, gm is one of the most important parameters that determine device performance in terms of speed and noise.


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

If we look at the gm, again we see the gm predicted by the SQUARE LAW fits (relatively) well the LONG CHANNEL device but it does NOT fit well the actual gm of a SHORT CHANNEL device.

Notice how gm is supposed to grow linearly with VGS-VTH which is the Vov. In the LONG CHANNEL device that's a good approximation, more overdrive gives more gm, approximately linearly. **But not in the SHORT CHANNEL one, there as you increase the overdrive the gm flattens off, it stops growing linearly so you can't get more gm by just overdriving it more.**

Notice that **the "PROBLEM" is at high Overdrive (STRONG INVERSION).** At the beginning (low Overdrive, WEAK INVERSION) the Square Law works more or less, **it's at STRONG INVERSION where it starts to fail for the SHORT CHANNEL one.**


![image](https://user-images.githubusercontent.com/95447782/169866635-2a16c1d3-9a80-45ba-981a-ee66136a897b.png)

The causes for this are:

* Short channel effects (velocity saturation, mobility degradation, etc)
* In strong inversion, short channel, Id is no longer quadratic with V overdrive, but it's more like linear (gm saturates at large Vov)

Overall, we have that:
* **SQUARE LAW FAILS TO DESCRIBE THE SHORT CHANNEL DEVICE IN STRONG INVERSION **


So:

* In the **SHORT CHANNEL MOSFET**, due to short channel effects, the **SQUARE LAW stops working at STRONG INVERSION**.
* For the SHORT CHANNEL, in STRONG INVERSION, the CURRENT is NO LONGER SQUARE, IT BECOMES MORE LIKE LINEAR GROWTH WITH Vov.
* Since gm is just the slope:
* For the **SHORT CHANNEL MOSFET in STRONG INVERSION, the GM is NO LONGER GROWING LINEARLY, IT BECOMES FLAT, CONSTANT OR SATURATED AT LARGE Vov**.

Now, what happens with gm/Id ratio for the SHORT CHANNEL device?

And by what happens we mean, does the SQUARE LAW PREDICT a dependency of gm/Id versus VGS that really matches the actual characteristic of the device in real life?

Starting from the SQUARE LAW expression of Id, we are "supposed" to get a gm/Id dependency of VGS that is INVERSE function of gm/Id versus VGS.

![image](https://user-images.githubusercontent.com/95447782/169869264-9a1e5eec-d40a-46ff-a32f-90d7d3f8eb36.png)


Now let's look at model versus reality:

![image](https://user-images.githubusercontent.com/95447782/169870245-ac68170d-7a52-4878-b9cc-0a9159174a05.png)


Notice how the gm/Id expression that results from the SQUARE LAW

<img src="https://render.githubusercontent.com/render/math?math=$\frac{g_m }{I_D }=\frac{2}{V_{\textrm{ov}} }$">

**predicts that at very low overdrive (weak inversion) we should get HUGE gm/Id values** (HUGE TRANSISTOR EFFICIENCY, nearly infinite) but that's **not the case in reality**.

So, **the SQUARE LAW fails to describe weak-inversion COMPLETELY**, for both LONG and SHORT channel devices.

Remember that for the BJT we got that TE (transistor efficiency, gm/Ic) was CONSTANT no matter what VBE?

For the MOSFET, the TE (transistor efficiency, gm/Id) is NOT constant, it actually DEPENDS ON THE BIAS POINT:

![image](https://user-images.githubusercontent.com/95447782/169871545-55a71119-a7aa-4511-927c-41253a4604b0.png)


Boundary between WI, MI and SI:

* There is no real boundary but just rough values:
* If you have:
* **gm/Id > 20 ==> You are in WI**
* **gm/Id ~ 10 to 20 ==> You are in MI**
* **gm/Id < 10 ==> You are in SI**

![image](https://user-images.githubusercontent.com/95447782/169871770-6489081a-ca58-421d-948d-7f1ff13bcfa3.png)


Actually the value of the **gm/Id TELLS YOU what kind of inversion you have** and what region you are in.



## Should we stop using the Square Law?

The Square Law has its limitations.

* **In STRONG inversion, it's INACCURATE for SHORT CHANNEL** due to short channel effects
* **In WEAK inversion it FAILS COMPLETELY (BOTH FOR LONG AND SHORT CHANNEL devices)**


Does this all mean that the SQUARE LAW has reached its end of life? Is it useless? Should we forget it?

No.

It's still an IMPORTANT asset because:
* In Analog design we use relatively long L and relatively low Vov. Hence short channel effects are less pronounced.
* It's still a simple yet POWERFUL model that provides a GREAT DEAL OF INTUITION as to in what direction are things going to move.
* Just don't use SQUARE LAW for SIZING. But use it for INTUITION, to understand TRENDS, understand rough direction of things.


## What happens in Sub-Threshold?

**Sub-threshold is simply Weak Inversion**. VGS is smaller than VTH, that's all. There is still a bit of current building up and it builds up exponentially, going from nothing to something.

The question is, what is the value of gm/Id in Sub-Threshold (synonym for Weak Inversion), is it BIG or SMALL, does it keep increasing as we keep reducing VGS to almost zero, or does it grow but saturates at some value?

We just look at the curves.

* Look at Id versus VGS curve. The slope of that is gm.
* Look at log (decimal) of Id versus VGS. The slope of that is the TE (a "proxy" for gm/Id, as in it's proportional to it).
* Look at the actual gm/Id characteristic (measured/simulated). See if it stacks up with what we predict from the log plot of the current.

And what we see is:

* Looking at Id curve versus VGS: at high VGS, big slope so big gm. At very low VGS, flattened slope so tiny gm.
* Looking at log(Id) versus VGS: at high VGS, small slope so small efficiency TE, small gm/Id. As we decrease VGS going from SI to MI to WI, slope of log(Id) increases so efficiency TE and gm/Id increases, until at very low VGS (WI is the same as sub-threshold) the slope is large but it stops growing, so gm/Id will saturate, flatten out.
* Looking at actual gm/Id plots, we see the gm/Id values stack up with the log(Id) slope.

But the IMPORTANT point is not just that: the IMPORTANT point here is that at low VGS, look at the log(Id) plot, slope flattens out to a constant, meaning that log(Id) is linear w.r.t. VGS, and **that must necessarily imply that Id is EXPONENTIAL with respect to VGS in the very low VGS region (WI to sub-threshold).**

And that exponential behaviour of Id versus VGS is similar to the BJT.

![image](https://user-images.githubusercontent.com/95447782/169980549-98abb7ba-f457-44ee-ac81-c921ccca1117.png)


That's the empyrical observation, we just looked at real measured curves of gm/Id and plotted log(Id) versus VGS and saw that slope flattening at low VGS and hence we DEDUCTED that Id must be exponential w.r.t. VGS in that region.

But let's derive the equation for that, as in, let's model it, see if we can model where that exponential behaviour is coming from.

This is what happens:

Subthreshold is synonym for WEAK INVERSION.

* In Weak Inversion, the channel has not formed yet. There is no INVERSION LAYER YET, we haven't created the CHANNEL yet. All we have done is we have got rid of the HOLES of the p-sub, we have pushed them away, we have emptied the area under the Gate Oxide, but we haven't attracted electrons yet. Hence **IN WEAK INVERSION WE DON'T HAVE AN INVERSION LAYER YET, ALL WE HAVE IS A DEPLETION REGION WHICH IS SIMPLY AN AREA EMPTY OF CARRIERS** (HOLES HAVE BEEN PUSHED AWAY, ELECTRONS NOT ATTRACTED IN YET).
* **That empty depletion region is a CAP. Depletion capacitor, Cdep**. Conductor layer on top (the Gate), conductor layer below (the substrate electrons waiting on the substrate outside the depletion region) and no charge carriers in the middle.
* Here we still don't have a MOSFET, we have an NPN junction (D-Psub-S) which is a BJT. The Collector is the Drain, the Base is "the sheet of Psub material that lies just underneat the gate oxide, the would-be channel", and the Emitter is the Source. Notice that the Base is not the GATE of the transistor, the Base is "the sheet of Psub material that is right underneath the oxide, where the channel will eventually form but it hasn't formed yet".
* The Base of such BJT is connected to the Gate of the NMOS via a capacitive divider (Cox + Cdep). Cox cap has one plate on the Gate and one plate on "the sheet of Psub material that lies just underneath the oxide". Cdep has one plate on "the sheet of Psub material that lies just underneath the oxide" and the other plate on the rest of the Psub which is connected to Ground, at the bottom.
* Hence the Base voltage is a the Gate voltage divided by the (capacitive) voltage divider formed by Cox and Cdep. Since Ve=Vs,

![equation](https://latex.codecogs.com/svg.image?V_%7B%5Cmathrm%7BBE%7D%7D=V_%7B%5Cmathrm%7BGS%7D%7D%5Cfrac%7BC_%7B%5Cmathrm%7Box%7D%7D%7D%7BC_%7B%5Cmathrm%7Box%7D%7D&plus;C_%7B%5Cmathrm%7Bdep%7D%7D%7D=%5Cfrac%7BV_%7B%5Cmathrm%7BGS%7D%7D%7D%7Bn%7D)

where 

![equation](https://latex.codecogs.com/svg.image?n=%5Cfrac%7BC_%7B%5Ctextrm%7Box%7D%7D%20&plus;C_%7B%5Ctextrm%7Bdep%7D%7D%20%7D%7BC_%7B%5Ctextrm%7Box%7D%7D%20%7D)

* With that VBE, the BJT current in this situation is 

![equation](https://latex.codecogs.com/svg.image?I_c%20=I_%7B%5Ctextrm%7Bss%7D%7D%20e%5E%7B%5Cfrac%7BV_%7B%5Ctextrm%7BBE%7D%7D%20%7D%7BV_T%20%7D%7D%20=I_%7B%5Ctextrm%7Boff%7D%7D%20e%5E%7B%5Cfrac%7BV_%7B%5Ctextrm%7BGS%7D%7D%20%7D%7BnV_T%20%7D%7D)
          
Notice that n is always > 1.

* For Bulk MOSFET,  ![equation](https://latex.codecogs.com/svg.image?n%5Capprox%201%5Cldotp%202%5Cto%201%5Cldotp%205)
* For SOI or FinFET, ![equation](https://latex.codecogs.com/svg.image?n%5Capprox%201%5Cldotp%201) (because in these techs you have a very small Cdep). 


![image](https://user-images.githubusercontent.com/95447782/169987120-c8924cf6-4071-41f3-bd4b-093543ce4bf8.png)


How does that translate to specific values of gm/Id in WI region?

* From the exponential equation of Id in subthreshold, we just differentiate that w.r.t. VGS and we get gm. Then we divide that by Id and we get gm/Id.
* And again we get a CONSTANT value of gm/Id for the MOSFET in Weak Inversion (subthreshold), like we did for the BJT, but this time the constant value is the BJT value divided by the n factor. The BJT value was constant at 1/Vt, where Vt is the thermal voltage kT/q=26mV hence the BJT constant gm/Id value was 38.5 S/A.
* So **for the MOSFET in WI the constant gm/Id value with 38.5 divided by n, so overall it's a number between 25 and 35 for bulk CMOS depending on whether n is closer to 1.5 (bulk CMOS) or closer to 1.1 (SOI or FinFet)**.

![image](https://user-images.githubusercontent.com/95447782/169995901-f97d365a-829d-4169-a62c-257a05ec89d8.png)

Ok so it's quite clear that the region with highest gm/Id (highest TE or Transistor Efficiency) is Weak Inversion.

Should we then be putting all our transistors in Weak Inversion because that's the most efficient region?

The anwer is No.

Why not?

* One of the false conclusions that people get is that in Weak Inversion since you have highest gm/Id then you will get highest intrinsic gain (Av=gm * ro), since ro=VA/Id, then Av=gm * ro=(gm/Id) * VA so clearly we will get largest Av when gm/Id is largest and that's Weak Inversion. Correct?
* Well no. Remember what matters for speed is not just high intrinsic gain (Av) but high Gain-Bandwidth-Product (GBW=Av * BW) and we saw  so what matters for speed is gm.
* And **in Weak Inversion we may get higher Av but more importantly we get really tiny gm, remember how once you are in Weak Inversion gm decreases EXPONENTIALLY as we reduce VGS**, as in Subthreshold ID is exponential with VGS.
* Since gm will decrease exponentially also speed will decrease exponentially.
* So if you put all your transistors  in Weak Inversion (subthreshold) you will end up with very slow circuits. This can be ok for some applications, low power etc but not ok whenever speed matters.
* Some people may say ok in Weak Inversion we get a very small ID which causes a really low gm (correct, since remember the expression of gm in subthreshold, Id is the exponential, differentiate that to get gm, you get ![equation](https://latex.codecogs.com/svg.image?g_m%20=%5Cfrac%7BI_%7B%5Cmathrm%7Boff%7D%7D%20%20e%5E%7B%5Cfrac%7BV_%7B%5Cmathrm%7BGS%7D%7D%20%7D%7B%7B%5Cmathrm%7BnV%7D%7D_T%20%7D%7D%20%7D%7B%7B%5Cmathrm%7BnV%7D%7D_T%20%7D=%5Cfrac%7BI_d%20%7D%7B%7B%5Cmathrm%7BnV%7D%7D_T%20%7D) so yes gm is proportional to the absolute value of the (tiny) Id). So people may say ok so let's keep it in Weak Inversion, but with higher ID, but still in Weak Inversion, as in, a device that with the same small VGS as before (a VGS that's less that VTH) conducts a higher ID. How do you do this? Well just make W larger, so it's more sensitive (use the square law intuition, larger W is more ID for same VGS). So yes, why don't we do that? That would be good, because we get a device that is still in Weak Inversion hence we get the benefit of high gm/Id but since we have made the absolute value of ID larger we will also get gm larger and hence speed won't go down as much. Would this reasoning work?
* The answer is that won't take you very far because in order to compensate the loss of gm you have already incurred in (gm has gone down exponentially) you would have to increase W also exponentially. And of course you can't usually increase W exponentially because your device will become huge and occupy a large area, but even if you said ok I have the area I can do it, you still don't fix the speed problem with this approach because by making W larger you increase the capacitance exponentially which makes it exponentially slow so that's really not going to solve the low speed in weak inversion issue. I mean you could make your device a bit larger W and get a bit more gm in weak inversion but you won't compensate the full loss, just a bit.


So what's the solution?

## Moderate inversion

* **Just operate in Moderate Inversion (MI).**

That's becoming really popular with lower supply voltages.

**Moderate Inversion is a pretty good trade off because**:

* You have decent gm/Id, I mean much better than Strong Inversion
* You have decent gm/gds (when we talk about gm/gds basically it's like saying gds=1/ro, so gm/gds is gm * ro=Av, so we are talking about the intrinsic gain, gm/gds is a measure of the intrinsic gain).
* Some degradation in speed (from Strong Inversion) is OK, as SHORT channel MOSFETs are already very fast.


![image](https://user-images.githubusercontent.com/95447782/170001602-c9bbbf45-9296-465e-a299-9874a8f490a1.png)


The problem with Moderate Inversion?

* No simple model exists for Moderate Inversion.
* We have a good model for Strong Inversion (the SQUARE LAW)
* And a good model for Weak Inversion (the subthreshold EXPONENTIAL)
* But not for Moderate Inversion.

But we ask the question, DO WE REALLY NEED ACCURATE MODELS?

Maybe not, because:

* SIMPLE models like SQUARE LAW are necessary for intuition ("roughly" understand trends) BUT ARE NOT ACCURATE
* ACURRATE models provide NO INTUITION and are INTRACTABLE when you want to do some analysis with them

At this step, it's worth noting that ACCURATE MODELS ARE:

* The simulator type models like BSIM etc, they are ACCURATE but can't use for analysis just simulation.
* The EKV model, yes this model is ACCURATE and works in all regions of operation, so it is valid for Moderate Inversion BUT IN REAL LIFE AS A DESIGNER WHEN YOU HAVE TO DO SOME REAL ANALYSIS OR SOME REAL DEVICE SIZING THIS MODEL BECOMES INTRACTABLE AND IS NOT RELATED TO CIRCUIT SPECS, LIKE DO THIS TO GET MORE GM AND MORE SPEED ETC SO CIRCUIT DESIGNERS DON'T LIKE THIS MODEL VERY MUCH.

So the proposed methodology is:

* Maybe we don't need ACCURATE models for Moderate Inversion.
* Just **use SIMPLE MODELS FOR INTUITION AND TRENDS** (LIKE THE SQUARE LAW)
* and **then for CIRCUIT SIZING** (CALCULATE THE NUMBERS FOR YOUR CIRCUIT) **USE LUTs**.

But before we talk about what are LUTs and how to use them, let's look at the MOSFET design problem.


## Design variables in the MOSFET design problem

The MOSFET design is a function of 5 variables (5 degrees of freedom).

Three voltages:
* VGS
* VDS
* VSB

And two sizing parameters:
* W
* L

From least important to most important, these are:

Least important, VSB.

* VSB causes Body effect, if Body is biased higher than Source then it increases VTH.
* But it's not an important degree of freedom.
* If you have a dedicated well (Deep NWELL) then you can tie Body to Source so no problem there.
* In some circuits you may not have Deep NWELL and you just can't tie Body to Source, like in a 5T-OTA where you have a floating Source BUT that is a necessity to provide the circuit's Common Mode, so you can't do anything about it, just live with it.
* Overall, **VSB is not an important degree of freedom, you just tie Body to Source if you can and if not you just live with it.**

Then, VDS.

* Ideally from simple SQUARE LAW VDS should not affect ID but in reality it does due to Early Voltage (VA), that happens due to Channel Length Modulation and DIBL.
* The VDS effect is modelled by ro, remember ro=VA/ID so more VA is better for larger ro.
* A point that is not often discussed much is that VA is not constant or fixed, it actually varies depending on VDS. VA increases as we increase VDS. Hence to get good ro you can't have your device oeprating at the edge of saturation (VDsat) you must place it deep into saturation (use a higher VDsat_margin).
* VA also increases as we increase L, longer devices have more VA hence more ro BUT to get the extra VA which is what you want in order to increase your ro you can't just increase L and keep operating your device at the edge of saturation, to get the higher VA from your Longer device you need to place it deeper into saturation again.
* But again, even if we know how to make VA larger in order to get higher ro, in many cases we can't just increase our VDS as much as we want, because we run out of headroom specially at low supply voltages.
* The reason why we say all this is that, at the end of the day, **VDS is not a variable that we have a lot of freedom to play with, it is not a very flexible degree of freedom for the designer, a lot of the time it's imposed by circuit circumstances like headroom crushing etc**.

Now **VGS, THIS IS THE MOST IMPORTANT VOLTAGE OF THE 3**.

* VGS is the primary voltage that really controls device behaviour.
* VSB and VDS were WEAK variables but VGS is a STRONG VARIABLE in our circuit design.
* However in reality, we almost never set a specific VGS value, what we do is that we set a specific ID value, then we mirror it up and down and the ID is what sets the VGS.
* Therefore **in reality we should replace VGS by ID in the Degrees Of Freedom list**.

Now the 2 sizing Degrees of Freedom.

First, Length.
* The following is a good summary of how you choose L in analog design most of the time.
* Use SHORTER L if you want smaller area, smaller capacitance, HIGH SPEED (since transit time ft = gm/(2pi * Cgate) ).
* Use LONGER L if you want high gain (as long L produces high VA), less random mismatch (longer L implies more area which reduces mismatch), lower flicker noise (longer L is more area).

Finally, the Width.
* This is one of the most difficult problems for the designer.
* Choice of W is affected by the other things that you want to get out of your device (what gm/Id you want, i.e. what inversion level) also how much L you chose before, how much ID etc.
* **Search range of W can go from sub-1um to 1000um.**
* **Once you selected a specific W, then if you change something else like L or ID, that will change your gm/ID**.

So **you end up "chasing the right W"** which is a tricky problem not straight-forward to pinpoint.

How to fix this?

In the good old days: **the OLD FIX was to replace W by Vov**, like choose a Vov that gets you the desired ID and TE (gm/Id) and from there compute W.

* This worked ok in the good old days WITH THE SQUARE LAW.
* Because:
* From the square law, ID proportional to Vov^2. And gm (derivative) proportional to Vov. And gm/Id was also proportional to Vov.
* So choose a Vov and that gives you desired gm (or at least an indication thereof) and gm/Id (Vov is a DOF).
* You also try to choose an ID (ID chosen as a DOF).
* Once you have Vov and ID, from those 2 DOFs, from the square law you computed back W.

But this relationship (SQUARE LAW) is not valid any more (just as an intuition is ok but not for sizing, not for getting W values), because:
* Square law not accurate in Strong Inversion for short channel (gm predicted by Square Law in strong inversion nowhere near reality FOR SHORT CHANNEL, LONG channel is ok but SHORT CHANNEL not at all)
* In MI and WI, square law completely fails both for SHORT and LONG channels, it predicts huge or infinite TE (gm/Id) which is far from reality.
* Vov not related to circuit specs any more, you can't get any idea about speed, gain or noise just by looking at how much is Vov.

**The new fix: the new fix is just use gm/Id methodology!**

gm/Id is the parameter we care about MOST. Because it's the TE (Transistor Efficiency).

It captures the most basic function of the transistor (gm, transconductance, voltage controlled current) and the most valuable resource (power consumption).

**So, replace W by gm/Id in the list of DOFs!**

That means, forget about W and just find gm/Id. Don't deal with W any more. And don't deal with Vov any more either. Don't try to guess W any more, stop trying to guess the best W that will give your circuit the best specs, stop "chasing W"... instead design for a certain gm/Id and then once you got the correct gm/Id for your device, just go to the LUT and get the W from there.

**gm/Id is the main design "knob"**.

**Your SIZING PARAMETERS ARE gm/Id AND L. Not W and L any more!**

Why? Because gm/Id controls, sets, defines the TE for a device **“ORTHOGONALLY”**.

**What does “orthogonal” control of TE mean?** It means you set gm/Id and you get a TE, period, and that won't change even if you change Id afterwards, as long as you keep the same gm/Id. If ID changes, TE is kept unchanged. If L changes, TE is kept unchanged. How is it possible that with different ID you get the same TE? Because **we simply lookup the new W to guarantee the same gm/Id that we have decided to stick with**.

An important point is also that **THE SEARCH RANGE FOR gm/Id IS LIMITED, TYPICALLY IN THE RANGE OF 5 TO 25.**
* The range of gm/Id doesn't differ much from one device type to another
* And from one technology to another

So now we need to know the trade-offs of gm/Id, that means when should we use LARGE gm/Id and when to set SMALL gm/Id.

Use SMALL gm/Id if we want:
* Strong Inversion biasing
* Small gm for a given ID (devices whose gm does not contribute to gain, or whose gm we prefer to keep low in order to keep other things low like noise or offset, such as for example active loads in a 5T opamp)
* Small area
* Small capacitance
* **HIGH SPEED**
* Large VA (large ro) since at lower gm/Id, strong inversion, the gate has more control over the channel, meaning that the effect of VDS on the channel is less, which means large ro.

Use LARGE gm/Id if we want:
* Moderate or Weak Inversion biasing
* Large gm for a given ID (devices whose gm contributes to gain, such as input pair devices and cascodes)
* **High efficiency (LOW POWER)** i.e. low ID for a given spec of noise and speed (that's to say a given spec on gm, since gm controls speed and noise)
* Less random mismatch. This is because large gm/Id implies large W (larger area)
* Low flicker noise. Again, because large gm/Id implies large W (larger area)
* Large input range and/our output swing. Because large gm/Id implies low Vdsat as Vdsat ~ 2/(gm/Id).

The BEST COMPROMISE is usually in MODERATE INVERSION (gm/Id between 10 and 20).

## How to get device dimensions from gm/Id

All we have said so far sounds promising but our simulator doesn’t understand gm/Id, it understands W/L. We can’t tell our simulator please give me a device with gm/Id of X, we need to tell it this is a device with such W and such L.

**How do we get W from gm/Id?**

Here is how:

### Reference plots extraction:

* First of all, assume (imagine) we have a “reference device” with width W or “some (known) W”.
* **We simulate this device, sweeping VGS over a range of voltages**. For that step, we give it also “some (known) L”.
* From that simulation **we plot ID versus VGS** and we take note of the fact that, for a given L (we have set L to “some L”) there is one-to-one correspondence between VGS and ID. That means, **given “some W and L”, VGS determines ID completely.**
* At this step we don't think about VDS explicitly but again we saw before that VDS is a WEAK variable and it has LITTLE impact on ID. So for this step we may just set VDS to something reasonable like some intermediate Vdsat_margin, maybe not tie the Drain all the way up to supply but something intermediate. Or maybe put a diode on top like VDD minus one VTH or something like that, in any case it's just a case of **setting VDS to some voltage**.
* Once the previous sweep is done (ID vs VGS) we have our 1st reference curve, which is ID vs VGS curve for our “reference device”.
* Next, **we also plot gm/Id versus VGS for this device**. And again we take note of the fact that we have one-to-one correspondence between gm/Id and VGS, that simply means that for any value of gm/Id (whether it’s in WI, MI or SI) there is only one VGS that produces it so we can calculate VGS from gm/Id and vice-versa.
* By the way, plotting gm/Id at this step can be done from the simulation data from the previous sweep, where we swept VGS and at each point we recorded ID and we would also record gm for each point.
* Next we notice the following fact: if gm/Id gives me VGS as a one-to-one correspondence, and VGS gives me ID as a one-to-one also, then that means that gm/Id gives me ID as a one-to-one correspondence also.
* **At this point, why not plot everything versus gm/Id?** If anything can be plotted versus VGS then it can also be plotted against gm/Id, since there is a one-to-one relationship between VGS and gm/Id.
* Also, **any other parameter that comes out of the VGS sweep can also be plotted against gm/Id**.
* So **we combine the previous 2 plots into a new plot which plots ID versus gm/Id**. Now the X axis, independent variable or DOF or “knob” is gm/Id. Choose a gm/Id value and that tells me straight away exactly what ID corresponds to it, for this “reference device” with “some (known) W and L” (these are values we know and are associated with the plots we have just generated for the “reference device” which we will call “reference plots”).


### Sizing devices with the help of reference plot data
Ok we have finalized the process of generating “reference plots” for our “reference device” with “some (known) W and L”.

Now we are going to see **how do we use this information to design any device, that is to solve a new design problem**. What does that mean? It means that now **we are going to take ANY gm/Id that we want AND ANY ID that we want, and we are going to find out exactly how much W and L produce it.**

For this step it’s crucial to simply notice the fact that ID is ALWAYS proportional to W, as a general rule.

![equation](https://latex.codecogs.com/svg.image?I_D%20%5C;%20%5Calpha%20%5C;%20W)

And by ALWAYS we mean in all regions, this is true in WI, MI and SI. And of course for all processes, this as true in 130nm as it is in 22nm.

Why? Because regardless of the region, if you stick 2 devices in parallel you get 2x the current, or if you take a device and you make it 2 fingers of the same width, you get a device with 2x W and 2x the current flows.

From this insight, we SIMPLY apply **cross-multiplication**.

We know:

* For the “reference device” of “some (known) W and L” we have its ID versus gm/Id plot, or equivalently its ID versus VGS plot.
* For a new device or “design problem”, we are given a target ID, let’s call it IDx, this is defined in the problem DOFs. More than saying “we are given a target ID” we should say we have given it to ourselves, because we MUST have actually reached to the conclusion (somehow) that for this certain device in our circuit in order to achieve a certain functionality and parametric performance it has to have a certain ID. ID is one of our DOFs (knobs) so we are the ones who choose ID.
* Once we have the new IDx, we need to find out which width Wx will produce it. We simply calculate Wx proportionally (cross-multiplication) like Wx = W * IDx/ID.
* The resulting device will have the same L as the reference device, the same VGS (corresponding to the 

This summarizes cross-multiplication.

An example of cross-multiplication:

![image](https://user-images.githubusercontent.com/95447782/170090178-5f7934e4-4b97-47c8-85f2-742af7adad41.png)

Another example:

![image](https://user-images.githubusercontent.com/95447782/170090274-cd9a4646-bf84-401c-a9a5-f117eb8120ed.png)


A recap of the 5 DOFs:

* Old-school (SQUARE LAW): W, L, VGS, VDS, VSB.
* New paradigm (gm/Id): gm/Id, L, ID, VDS, VSB.


### Generating the LUTs

Now more specifically, how do we generate these LUTs?

First of all recognize the implications of ID being proportional to W. Due to this property, our life is easier!

**Key point 1:**
* If ID is proportional to W, anything proportional to ID is ALSO proportional to W.
* gm, gds, cgb, csb, cdb are ALL proportional to W.
* Also NOISE is proportional to the W: thermal noise and flicker noise.

**Key point 2:**
* The ratios of these parameters, they all must be INDEPENDENT of the W.
* gm/Id, gm * ro, VA, etc these are all INDEPENDENT of the W.

For this reason, **when we simulate our reference device, WE STORE THESE PARAMETERS for the reference device**. Not only we store the plots, we also store these parameters. Just so that afterwards we can calculate these parameters for our new design problem via cross-multiplication.

**THIS IS WHY WE ONLY NEED TO CHARACTERIZE ONE REFERENCE WIDTH DEVICE.** We can characterize various Lengths, but just one width is enough for each Length.

How do we build the design charts? (the LUTs)

Just a simple testbench like this, do our sweeps, store all the data.

![image](https://user-images.githubusercontent.com/95447782/170103763-c83c1dfe-54fe-4853-9a4a-47783c237bf0.png)


If you want ACCURATE results, you need to take into account the VDS and VSB dependence.

So you sweep them also!

And hence you have a 4D array.

But that’s ok! Don’t worry! You just have to do it once.

![image](https://user-images.githubusercontent.com/95447782/170245768-abd302d3-b8e4-4d13-8a21-860bfa6b58de.png)


### References
[[1](https://www.youtube.com/watch?v=dzz4z3ijVts&t=932s)] The gm/ID Design Methodology Demystified, Dr. Hesham Omran, Master-Micro

[[2](https://web.stanford.edu/~murmann/gmid)] Gm/ID Starter Kit, Dr. Boris Murmann, Stanford University.

[[3](https://www.cambridge.org/jespers)] P.G.A. Jespers and B. Murmann, Systematic Design of Analog CMOS Circuits: Using Pre-Computed Lookup Tables, Cambridge University Press, 2017.


### Next steps

Next step is run LUT generation in Skywater 130nm PDK.

Either using [ADT](https://www.mos-ak.org/spring_2022/presentations/Omran_Spring_MOS-AK_2022.pdf) or using [pyMOSChar](https://github.com/ashwith/pyMOSChar).

* [ADT for LUT generation and systematic design](https://www.mos-ak.org/spring_2022/presentations/Omran_Spring_MOS-AK_2022.pdf)
* [pyMOSChar for LUT generation compatible with ngspice](https://github.com/ashwith/pyMOSChar)
* [gmIdNeoKit GUI for visualizing charts from LUTs and design data](https://github.com/fengqzHD/gmIdNeoKit)

Do systematic circuit sizing using Matlab code from:

* Systematic Design of Analog CMOS Circuits : Using Pre-Computed Lookup Tables, Paul G A Jespers; Boris Murmann, Cambridge : Cambridge University Press, 2017.

![image](https://user-images.githubusercontent.com/95447782/170247188-0b15dbd0-9768-411f-916e-34534b5d3a98.png)


* Link to Matlab code by Prof. B. Murmann: https://web.stanford.edu/~murmann/gmid (plan to use this, or [pyMOSChar](https://github.com/ashwith/pyMOSChar) repo above)



