Transformers

### Core type
- Coil heats up and natural cooling occurs.
- Current passes through coil.
- Core is built of laminations to form a rectangular frame and it provides a single magnetic circuit.
- Windings are normally cylindrical in form and concentric, low voltage windings being placed near the core.
- Both the windings are uniformly distributed over the two limbs of the core.
- These windings surround a considerable portion of the core.
- Since the windings are distrubuted on 2 limbs, natural cooling is more effective.
- The coil can be withdrawn just by dismantlinbg laminations of the top yoke (L-Shaped).

### Shell type
- The core of this type of transformer provides a double magnetic circuit.
- The windings are normally sandwiched, always placed on the central limb of the core. H.V. and L.V. coils which are wound in the form of pancakes are interleaved. The top and bottom coils which are closer to the yoke are L.V.
- The core nearly surrounds the windings placed on its central limb. This feature is useful from the point of view of providing mechanical protection to the windings.
- Natural cooling is poor.
- When the coils are to be withdrawn for repairs, a large number of laminations are to be dismantled.

### Berry type
- This type of transformer has a distributed magnetic circuit, i.e. the number of independent magnetic circuits is more than 2.
- The core is constructed in such a fashion that its yoke radiates out from the center just like the spokes of a wheel.
- Rest of the features are similar to that off a shell type transformer.

Differences between core and shell type

|Core type|Shell type|
|---------|----------|
|Winding encircles the core|Core encircles most of the winding|
|Cylindrical type|Multilayer type or sandwiched|
|Natural cooling is provided|Natural cooling is not possible so cooling fans have to be used|
|Coils can be easily removed for maintenance|Removing the coils for maintenance work is not easy|
|Generally low voltage transformers|Generally high voltage transformers|

In one 2 pi cycle, phi is max at pi/2 (1/4th of a cycle).

Therefore average rate of change of flux = phi(max)/t = 4 phi(max) f Wb/sec.

Average emf produced in each turn = Average rate of change of flux = 4 phi(max) f.

Form factor = RMS Value/Average value = 1.11.
Therefore RMS value of EMF induced every turn = 4*1.11=4.44 phi(max) f.

E1 = 4.44 phi(max) N1 f Volts.
E2 = 4.44 phi(max) N2 f Volts.
Dividing
E1/E2=N1/N2.

At no load V2=E2, V1~=E1.
Therefore V1/V2=E1/E2=N1/N2.

V1/V2 = voltage ratio of transformer, N1/N2 = turns ratio of transformer.

V2/V1 = E2/E1 = N2/N1 = K <-- Transformation ratio.

If K>1, then V2>V1, Step up transformer.

If K<1, then V2<V1, Step down transformer.

If K=1, then V2=V1, one to one transformer.

Power input = Power output

### Kilowatt-Ampere rating of a transformer (KVA) :-
Coil -> Current

Core -> Voltage

In the case of current loss, the coil will heat, and in the case of voltage losses, the core will heat.

Since the losses depend upon the current and the voltage, we can simplify the rating of the transformer as the product of these 2 parameters, i.e. the transformer rating.
It is specified as the product of volate and current, and is called KVA rating.

KVA rating of a transformer = V1 I1/1000 = V2 I2/1000.

I1 full load current = KVA * 1000 / V1.

I2 full load current = KVA * 1000 / V2.

### Ideal transformer :-
Permeability of core should be high so that less current is required to magnetise the it.
There should be no magnetic leak, i.e. all the flux should be confined to the iron core.
The windings should have no ohmic resistance.
There should be no losses.


### Transformer losses :-
Copper losses = I<sub>1</sub><sup>2</sup>R<sub>1</sub>+I<sub>2</sub><sup>2</sup>R<sub>2</sub>.
Iron/cose losses :-
 -Hysteresis losses -> P<sub>h</sub> = K<sub>h</sub>B<sub>m</sub>fV.
 -Eddy current losses -> P<sub>e</sub> = K<sub>e</sub>B<sub>m</sub><sup>2</sup>f<sup>2</sup>t<sup>2</sup>V.
 Where K<sub>h</sub> and K<sub>e</sub> are constants, B<sub>m</sub> is the max flux density, V the volume, and t the thickness of the core.

Regulation of transformer is defined as the change in secondary terminal voltage from no load to full load with primary impressed voltage V<sub>1</sub>, and the temperature of the transformer is maintained at some constant value.

% Regulation = E<sub>2</sub> - V<sub>2</sub>/E<sub>2</sub> * 100%.

### Efficiency of transformer

Output power = Input power - losses

V<sub>2</sub>I<sub>2</sub> cos phi<sub>2</sub> = V<sub>1</sub>I<sub>1</sub> cos phi<sub>1</sub> - (P<sub>Cu</sub>+P<sub>n</sub>+P<sub>e</sub>). [P<sub>n</sub>+P<sub>e</sub>=P<sub>i</sub>]

% efficiency = (Output power/input power) * 100 = (V<sub>2</sub>I<sub>2</sub> cos phi<sub>2</sub>.V<sub>2</sub>I<sub>2</sub> cos phi<sub>2</sub>+P<sub>i</sub>+P<sub>Cu</sub>) * 100.

Full load efficiency = (Full load output power / Full load output power + losses) * 100 = (Full load KVA * PF/Full load KVA * PF + P<sub>i</sub>+P<sub>Cu</sub>) * 100

= (V<sub>2</sub>I<sub>2</sub> cos phi<sub>2</sub>/V<sub>2</sub>I<sub>2</sub> cos phi<sub>2</sub> + (P<sub>Cu</sub>+P<sub>n</sub>+P<sub>e</sub>)) * 100.

I2 Full load = KVA*1000/V2.