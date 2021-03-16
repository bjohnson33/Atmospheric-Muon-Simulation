# Atmospheric-Muon-Simulation

**Abstract**

The effects of atmospheric variables in the energy flux of muons are
well known through the collection of data. However, there are not many
simulations regarding the effects of these atmospheric variables on
muons. It is known that as air pressure increases, muons lose more
energy as they travel through the atmosphere, causing there to be a
lower muon flux. It is also known that as the zenith angle increases,
muons must travel a farther path length, making it more likely for them
to decay before reaching sea level. The goal of this simulation is to
illustrate the effects of air pressure, the cosine squared law, and
particle decay on the energy of muons traveling through the atmosphere.

**Background**

Cosmic rays are charged particles that pass through the Earth's
atmosphere and originate in our galaxy. These rays are composed mostly
of protons but also helium and other heavier nuclei. When they interact
with the atmosphere, they create a shower of new particles that decay in
many ways. The interactions between the cosmic rays and the nitrogen and
oxygen nuclei in the atmosphere produce pions and kaons, that in turn
decay into muons. These are usually formed at an altitude of 15000
meters. These muons then move towards the ground at relativistic speeds.

Muons have a lifetime of 2.2 µs, and proceed to decay into an electron,
a neutrino, and an antineutrino. Normally, this would mean that we would
be unable to detect muons as at their speeds they would only be able to
travel around 660 meters before decaying, but because of special
relativity, they are subject to time dilation. As the particles also
have a relatively weak interaction with other particles, these two
factors lead to muons being able to travel far enough for us to detect
at Earth's surface. Muons are also the most prevalent particles at sea
level on account of other particles being stopped by the atmosphere. The
muon flux at sea level is approximately 1 per minute per square
centimeter per steradian.

There are many variables that can affect muon flux. The first set of
these are flux variations due to solar system properties. The earth has
a magnetic pole that acts like a dipole oriented from north to south,
which causes the magnetic field to be parallel to the surface of the
earth at the equator, and perpendicular to the surface near the poles.
This means that it takes much more energy for a cosmic ray to be able to
penetrate the magnetic field near the equator than it would to near a
pole. The muon flux is larger looking towards the west when compared to
the east due to the positively charged cosmic rays following the Earth's
magnetic field. Other solar system properties include magnetic
anomalies, solar modulation, and solar flares, but for the case of our
simulation, we assume that all solar system factors are constant and
therefore ignore them.

There are also flux variations due to atmospheric properties. The first
of these properties is the cosine squared law, that states that at
angles greater than vertical, muons must travel a much farther distance
to reach the ground and both lose much more total energy and have a
higher chance to decay. As a function of zenith angle, the muon
intensity is expected to have a cosine squared dependence. As muons
require certain amounts of energy to make it through the atmosphere, an
increase in atmospheric density will cause the particles to lose more
energy as they make their way to the surface. As atmospheric pressure
increases, the muon flux decreases. The temperature of the atmosphere
also plays a part in effecting muon flux. As temperature increases, the
atmosphere becomes less dense and allows for more particles to be
interacted with, but the increase in volume of the atmosphere also
causes the altitude of muon creation to be higher, causing an increase
and decrease in muon flux respectively. In the case of this simulation,
the temperature will only be used to calculate the density of the
atmosphere.

In this simulation, we will not model muon flux, but rather the total
energy of the muons at each altitude, which should provide a very
similar trend. In our case, we shall simulate the total muon energy at
altitudes between 0 and 20000 meters and using that simulation, show how
pressure, the cosine squared law, and particle decay effect the changes
in muon flux.

**Methods**

To study the rate of energy loss for muons passing through the
atmosphere, we must use the Bethe equation. If we apply the Bethe
equation to air, we get the equation:

<img src="https://i.imgur.com/080k0W5.png"/> 

where β = v/c, v being the speed of the particle, and c being the speed
of light; <img src="https://i.imgur.com/wQKbGqP.png"/> is the Lorenz
factor. The equation can be used to simulate the change in energy of a
muon as a function of altitude if given and initial energy and an
initial height.

Before simulating the energy loss of muons, some assumptions must be
made. The first assumption is the initial energy and height of the muon
when it is created. These factors will be variables within the function
that can be changed and in the case of simulating many muons,
randomized.

The β factor of the particle can be calculated using the relativistic
energy expression

$$E_{\text{total}} = \gamma E_{\text{rest}},
$$

$$dh\  = \ \gamma\beta cdt.
$$

$dx = dh \cdot \rho_{\text{air}}\left( h \right)$,

Where dx is now in the appropriate units and
$\rho_{\text{air}}\left( h \right)\ $is the density of air as a function
of altitude h. To determine this, the law of atmospheres must be used:

$${P\left( h \right) = P_{0}\left( \frac{1 - Lh}{T_{0}} \right)^{\frac{\text{gM}}{\text{RL}}}
}{T\left( h \right) = T_{0} - \left( \text{Lh} \right)
}{\rho_{\text{air}}\left( h \right) = \frac{\text{MP}\left( h \right)}{\text{RT}\left( h \right)},
}$$

P~0~ = 101325 Pa (standard Pressure at sea level)

T~0~ = 288.15 K (standard temperature at sea level)

L = 0.0065 K/m (temperature lapse rate)

g = 9.8 m/s^2^ (gravitational acceleration)

M = 0.0289644 kg/mol (molar mass of dry air)

R =8.31447 J/(mol\*K) (ideal gas constant)

To take into account the cosine squared dependence, the formula for dx
becomes:

$$\text{dx} = \text{dh} \cdot \rho_{\text{air}}\left( h \right) \cdot \text{co}s^{2}\left( \theta \right)$$

Once the value of dx has been obtained, the Bethe equation can be used
to find the energy loss for that increment of distance. The energy and
velocity are then updated and used in the next increment until the loop
is terminated when the muon reaches sea level, or decays.

Assuming the particle does not decay, an initial energy of 6000 MeV, an
initial altitude of 15000 m, and a zenith angle of 0° degrees, we should
obtain the follow curve:

**Figure 1** Energy vs Altitude graph for Muon with initial energy and
altitude of 6000 eV and 15000 m respectively assuming no particle decay
and a zenith angle of 0° degrees

If we assume no particles are decaying, and we set up a random
distribution of initial altitudes between 10000 m and 20000 m, of
initial energies from 2500 eV to 8000 eV, and a zenith angle of 0
degrees, we should obtain something along the following distribution:

**Figure 2** Energy vs Altitude graph for 100 Muon with pseudo-random
initial energies and altitudes assuming no particle decay and a zenith
angle of 0° degrees

To simulate particle decay, every 1000 time steps a pseudo-random number
generator is used to check if the particle has decayed. The particle has
an 80% chance to decay at every check. Under this assumption, any zenith
angle greater than 0° will result in there being a longer path length
for the muon. This means there should be a higher chance of it decaying
before reaching sea level, which should shift the total energy more
towards the higher altitudes.

To find the total energy at any altitude a function was written that
finds the closest altitude within the altitude array to the given
altitude. It then returns the energy at this timestep of the loop, which
is then added to a total energy value in order to calculate the total
energy for the given energy.

**Results and Analysis**

**The Effects of Pressure on Muon Energy**

The first factor that will be analyzed will be the effect of pressure on
the total energy of muons at different altitudes. We will first begin
with the total energy under our beginning conditions. This means that we
have standard atmospheric pressure at sea level of 101325 Pa, a zenith
angle of 0° for all muons, a pseudo-random initial altitude between
10000 m- 20000 m and a pseudo-random initial energy of 2500 eV to 8000
eV.

**Figure 3** Energy vs Altitude graph for 100 Muon with pseudo-random
initial energies and altitudes assuming a zenith angle of 0° degrees

We see that many of the particles still make it to sea level as their
path length is still short enough that there is very little chance of
decay. We expect to see less particles make it sea level if the pressure
is higher.

**Figure 4** Total Energy vs Altitude for 100 muons with a zenith angle
of 0° degrees

The rate of muons is anti-correlated with pressure, so if the standard
pressure at sea level is increased it should be expected that the total
energy should tend to be less at every altitude. To test this the
standard pressure at sea level will be increased from 101325 Pa to
161325 Pa.

**Figure 5** Energy vs Altitude graph for 100 Muon with pseudo-random
initial energies and altitudes assuming a zenith angle of 0° degrees.
Pressure at sea level of 161325 Pa

Compared to the real-life pressure at sea level, the muon energies tend
to have much steeper curves, which should correlate to a lower total
energy at most altitudes.

**Figure 6** Total Energy vs Altitude for 100 muons with a zenith angle
of 0 degrees. Pressure at sea level of 161325 Pa.

The increased level of pressure caused the total energy of the muons to
be decreased by 50000 MeV on average. This shows that as pressure
increases, the total energy of the Muons decreases.

**The Effects of Zenith Angle on Muon Energy**

The next factor that must be tested is how the change in zenith angle
effects particle decay and the total energy. It is expected that as the
zenith angle increases, the path length for each muon will be increased
which will cause them to have a higher chance of decaying before they
reach the sea level. As a result, an increase in the zenith angle should
lead to the peak in the total energies shifting towards higher
altitudes.

**Figure 7** From Left to Right: Energy vs Altitude for 100 Muons at
zenith angle of 0°, Energy vs Altitude for 100 Muons at zenith angle of
50°, Energy vs Altitude for 100 Muons at zenith angle of 80°

**Figure 8** From Left to Right: Total Energy vs Altitude for 100 muons
at zenith angle of 0°, Total Energy vs Altitude for 100 muons at zenith
angle of 50°, Total Energy vs Altitude for 100 muons at zenith angle of
80°

The difference in decayed particles between a zenith angle of 0° and 50°
is quite noticeable, with there only being 5 muons that make it to sea
level. This difference is made even more apparent at a zenith angle of
80° in that none of the muons make it anywhere close to sea level.

The effects of the increased path length are also demonstration in the
total energy graphs. The first of the total energy graphs shows that
most of the muon energy is at altitudes of 10000 meters and below. On
the second total energy graph where the zenith angle is 50°, we see that
the total energy of the muons tends to shift right towards the higher
altitudes as predicted. On the third total energy graph where the zenith
angle is 80°, we see that there is almost no energy below 10000 meters,
and that the total energy has shifted even further right, though the
total amount has decreased greatly.

**Conclusion**

It was predicted that as the pressure in the air increases, the total
energy of muons would decrease as well. In Figure 5 and Figure 6 an
increase in pressure of 60000 Pa caused the total energy at every
altitude to drop by about 50000 MeV. In Figure 5 there is a much steeper
grouping of final locations for the muons that trends towards lower
energy levels than in Figure 3. Given these results, it is reasonable to
claim that the total energy of muons is anti-correlated with air
pressure.

The zenith angle of a muon causes the path length it travels to greatly
increase, making it much more likely to decay before hitting the ground.
Figure 7 shows three different examples of 100 muons traveling towards
the surface of the planet. As the zenith angle increases, less muons
make it to the surface and by the time the zenith angle reaches 80,
there are no muons that make it close to the surface. In the Total
Energy graphs, the peaks tend to trend towards higher altitudes as
zenith angle increases. This follows the predictions laid out before
hand and shows that muons do have a cosine-squared dependence.

One problem that must be addressed with this simulation is the lack of
an accurate decay model. The simulation was built in a way that does not
include a time variable that can be tracked. Because of this, it is very
difficult to create a decay model that could be applied at every
timestep, so in order to try and emulate this, an 80% chance of decay
was applied for every 1000 iterations of the energy loss loop. In order
to properly model muon decay, a properly tracked time array would have
had to be tracked and at each timestep the probability of decay would
have had to have been calculated based on the current gamma of the muon.
The end result of such a decay model should still provide similar
conclusions to the ones found in this simulation.

