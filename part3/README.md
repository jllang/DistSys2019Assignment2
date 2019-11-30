# Part 3

We tried to model the Kumpula intersection with two Petri nets; One for
synchronisation between traffic lights and one for enforcing capacity
constraints on the roads.

## Synchronisation Model
For synchronisation, we started by adding five sets of traffic ligts. We
employed the following naming convention for the traffic lights: The lights have
three-letter identifiers:
- The fist letter denoties the colour of the light
  - `R` stand for red,
  - `G` stands for green, and
  - `O` stands for orange.
- The second letter denotes the location of the light
  - `N` stands for the part of the main road to the north of the intersection,
  - `S` stands for the part of the main road to the south of the intersection, and
  - `E` stands for the side road.
- The third letter denoting the direction of the light
  - `F` for forward;
  - `L` for left; and
  - `R` for right.

The traffic lights should turn in the following cycle of *configurations*:
- `A`: All the lights are red, except for `GNF` and `GSF`.
- `B`: All the lights are red, except for `GSR` and `GEL`.
- `C`: All the lights are red, except for `GNF` and `GNL`.

For orchestrating the cycle, we added seven synchronisation places, also named 
with three letters: The first letter denotes the source configuration, the and
the third letter denotes the target configuration. There are also primed
versions of these places for controlling the second set of lights, which can
turn to green.

Our synchronisation pattern seems to allow correct firing sequence at least for
the `A2B` transition.

## Capacity Model

Modeling the capacity constraints for different road seemed very challenging as
to our knowledge standard Petri nets are incapable of performing arithmetics. We
tried adding places to count the number of cars moving through different lanes.
These places follow the naming convention `<direction>2<direction>`, where
direction is one of `N`, `S`, or `E` as in the synchronisation model. The places
`F,F+R,_`, `_,R,L`, and `F+L,_,_` correspond with the configurations `A`, `B`,
and `C` respectively in the synchronisation model.
