---
layout: "post"
title: "Ramping Up Energy Storage: Designing a Sustainable Mechanical Battery"
author: "Avi Gulati (‘20)"
print_publication: true
tags: issue3
categories: Perspectives
related_image: 
---

*As the world population rises and a global consumer-driven culture intensifies, scientists and leaders alike must streamline energy storage practices with ethical and sustainable solutions. We propose a mechanical ramp battery that stores gravitational potential energy from input work required to push an object up an incline at a constant speed. The battery releases energy that can be measured through output work required to bring the object down an incline at a constant speed. Friction is an inherent part of this battery and is why we prioritized efficiencies, calculating energy storage efficiency to be 0.996, energy release efficiency, 0.960, and overall efficiency, 0.957. With respect to efficiency, this battery compares well to the Lithium-Ion battery and is already being tested by the US Bureau of Land Management in the Advanced Rail Energy Storage experiment (ARES). While we only assess the efficiency of this battery for one specific ramp, it is crucial to evaluate how the angle of the ramp to the horizontal, strength of the materials, and the way energy is being stored and released affects efficiency. Considering these factors, mechanical batteries can bring us one step closer to solving the global energy demand and facilitating other sustainable energy storage practices.*

<!--excerpt-->

**Introduction**

Aristotle observed, “The energy of the mind is the essence of life.” While his statement certainly rang true 2 millennia ago, now, humans must consider the concrete energy we store as an essence of life. 
	In his seminal work Energy Transitions, professor and energy historian Vaclav Smil discovered that in the 1860s, Americans used one fifteenth of the energy they use now. Through the 1900s, as global economic productivity grew by a factor of 16, energy demands rose by a similar factor of 17 (Smil). Thriving economies depend on improving energy storage capacities. Every year now, approximately 140 million impoverished individuals around the world are entering the middle class, corresponding to an ever-increasing rate of personal consumption. (Anthropocene). These new members of the middle class are ultimately spending money on energy: water heaters, air conditioners, refrigerators, cars, meat, and more (Anthropocene). The British Petroleum (BP) Statistical Review of Energy estimates that by 2100, if global energy demands rise to US middle class standards, humans will require 51.4 more Terawatts (TW) of power consumption than the current annual 18 TW. This number only factors economic growth. The United Nations Commission on Population and Development finds that global population will reach 11 billion by the end of the 21st century. Considering solely population growth, BP estimates that annual energy demands will increase anywhere from 25.0 to 28.4 TW. By the end of this century, in total, humans will annually need 74.0 TW more than our current 18.0 TW requirement. 
	Innovators are already exploring beyond present renewable energy forms. For example, Lockheed Martin is considering tidal and wave power, recently launching the Ocean Thermal Energy Conversion project (OTEC) (New York Times), and the District of Columbia is turning sewage into electricity and fertilizer (Washington Post). We can harvest more energy; however, what is most important and often least regarded is how to store this energy. 
	Right now, the US grid has an insufficient capacity for energy storage. 99% of stored energy from different sources like natural gas, coal, and renewables is based on pumped hydroelectric storage (Stanford), which is only fully effective in limited geographic regions. Even worse, grid operators curtail, or “shut down solar panels and wind turbines to reduce the production of surplus electricity” (Schwartz). If it is too windy or too sunny, the grid can overflow and blackouts become possible. As a result, many grid operators resort to curtailment. Some have tried to store surplus energy in Lithium-Ion batteries, but the substantial energy required to produce these batteries reduces the return on energy conservation by 20% (Stanford). We need a successful mechanism for storage because without one, we are losing vital energy. 
	Thus, we seek to engineer an ethical, sustainable mechanical battery: a ramp. The concept is simple. We push an object with constant force up a ramp and bring it down with a constant force such that work in each direction, W, to get the object to the top or bottom of the incline is given by 
                                                                       W=Fd,                                                             (1) where F is the constant force required to push up or bring down the object and Δd is the length of the incline. The force will be applied parallel to d so that we can easily calculate work, as we are using a spring balance to push the object. Figure 1 offers a visualization of the input force, denoted by Fp (p for push).

<!--excerpt-->

| ![](/imgs/battery1.png) | 
|:--:| 
|**Figure 1.** The free body diagram offers visualizations of all the force vectors acting on the cart during its ascent.

The energy stored in the battery is given by the gravitational potential energy, U, at the top of the ramp,                                                      U=mgh,                                                          (2) where m is mass, g is the acceleration due to gravitational force, and h is the vertical height of the center of mass of the cart above the bottom of the ramp. 
	Finally, the usable energy after storage is the output work when the object falls down the incline. To measure the output work, we let the object fall down the incline at a constant speed, preventing it from accelerating due to gravity by holding the spring balance against the direction of the cart’s descending motion. We can use equation (1) to measure this output work with output force. Figure 2 offers a visualization of the output force, denoted by Fo. 
	
<!--excerpt-->

| ![](/imgs/battery2.png) | 
|:--:| 
|**Figure 2.** The free body diagram offers visualizations of all the force vectors acting on the cart during its descent.

To assess how pragmatic our mechanical battery is, we measure and evaluate different efficiencies (Spenner). In the equations, E represents energy and W, work. 
Energy storage efficiency, energy storage, is given by 
                                                        energy storage=EstoredWInput .                                                (3)  
        
Energy release efficiency, energy release, is given by 

                                                        energy release=WOutputEstored .                                               (4)          

Overall efficiency, overall , is given by 
                                                        overall =WOutputWInput .                                                      (5)         

Engineers are already delving into the benefits of ramp batteries. The US Bureau of Land Management has allocated funds for such technologies. One of its pilot projects, the Advanced Rail Energy Storage (ARES) uses surplus energy to push 9,600 tons of rock and railcars up a 2000-foot hill (Wired). In case of an energy deficit, the rock filled railcars power down a slope, generating electricity through regenerative braking. 
For our project, the design goals we prioritize are easy maintenance, usable output, environmental protection, an ethical supply chain, and scalable technology. A ramp model should be easy to maintain because it only consists of elevating and descending mass on an incline. On the other hand, technologies like the lead-acid battery require precise, continuous watering to preserve an acid balance. Once the ramp is set-up, we estimate lubrication requirements every five years to ensure minimal friction. Such technology offers usable output as shown with ARES. The output is especially vital in the presence of an energy deficit. A chief advantage of this battery is its low impact on the environment, compared to the Lithium-Ion Battery. Mining lithium can damage air in communities and release CO2 emissions. A toxic lithium leak led to protests in Tibet last year, and mining is contaminating rivers in Chile and Bolivia (Wired UK). Not only is acquiring the metal harmful, but Lithium-Ion batteries are also not recycled effectively because the reuse process is time-consuming and expensive (Gardiner). On another hand, building our ramp requires an alloy of steel, which is not as toxic as Lithium and is also recyclable. We would also like to foster an ethical supply chain. The components of the ramp itself will be steel provided by TATA corporation which won the most ethical company award from the Ethisphere Institute (Economic Times). The final feature of this design is scalable output. To meet energy demands, we would like this ramp model to store 108 Joules, two orders of magnitude smaller than the ARES design which produces 5.2  1010 Joules. Because ramps store gravitational potential energy, modeled by equation (6), if our height is 100 meters, and g is near 10 N/kg, mass must be 105 kilograms. This is roughly 110 tons. If we implement this design to meet a 108 Joule output, we can meet our design goals. 
