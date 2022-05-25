# [What does it all mean: Net-zero, carbon neutral, climate positive, carbon negative?](https://www.devoxx.co.uk/talk/?id=11217)
Asim Hussain from Microsoft and [the Green Software Foundation](https://greensoftware.foundation/)

[Video on YouTube](https://www.youtube.com/watch?v=HXEnbi64TdQ)

There are a number of different climate commitments out there: it can be a bit confusing.
Some mean something official, and some are just nice words.

The unit of measurement is CO2eq (carbon dioxide _equivalent_) e.g. Methane is about 40x more warming

## There are various ways of reducing emissions:
* abatement/elimination = not emitting carbon, like not taking a flight
* offsets
  * compensation/avoidance = paying someone not to emit carbon (paying them not to take a flight?)
  * neutralisation/removal = taking carbon out of the atmosphere (e.g. planting trees, etc)

## There are many paths to zero and total elimination is hard/impossible. 
Commitments include:
* 'carbon neutral' is the bare minimum: if you just offset it all, you have met this level of commitment, even if it's all by compensation/avoidance and no removal or abatement
* 'net zero' = 90% eliminated, 10% neutralised permanently (no compensations -- you have to pay to remove the carbon, not just pay someone else not to emit it)
* 'carbon negative' = net zero and then a bit more neutralisation (there's no real definition, but it is further than net zero)
* 'climate positive' has no real meaning at all

## What you cannot measure you cannot improve
Measurement methods include:
* [Greenhouse Gas Protocol](https://ghgprotocol.org/)
* [Software Carbon Intensity Specification](https://greensoftware.foundation/projects/software-carbon-intensity-sci-specification)

### Greenhouse gas protocol (GHG)
Three levels or 'scopes'
1. direct emissions
2. indirect emissions -- heat and electricity which are produced by someone else burning stuff
3. other indirect emissions -- all the other stuff like travel, supply chain, hardware creation etc

#### Software in the public cloud:
This is all GHG scope 3 (as is front end).

Makes it confusing and hard to work out.

* do you know everywhere your software is run? 
* can you track where it's run? 
* do you have the rights to track the usage?

maybe carbon emissions should be per user or some such qualification

### Software Carbon Intensity

SCI = ((energy consumer by software in KWh * carbon emitted per kWH) + carbon of hardware) * R

where R is your unit, like maybe you measure per user

This will be launching at COP 27

It only allows eliminations -- you can only engineer your way to a better score, not pay

For more see [the Green Software Foundation](https://greensoftware.foundation/) and maybe [join us](https://greensoftware.foundation/join-us/ )