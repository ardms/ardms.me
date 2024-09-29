---
title: "uk electricity market"
date: 2023-06-23
modified: 2024-09-29
draft: false 
tags: ['notes','work']
---

# Basic principals 

Electricity generators enter into contracts to sell electricity to retailers
(who expect to use that electricity for their residential and commercial
customers). These can be traded several years ahead, right through to the hour
in question. In fact, it is not just generators selling to retailers: other
participants enter into these forward contracts to buy and sell electricity,
including on exchanges.

If we got to the period in question, and the amount of electricity generators
supplied and retailers received, matched their contracts, all would be nice.
The grid would be in balance (ignoring factors like congestion and transmission
losses). The retailers would pay the generators the price they had agreed.

In practice, customers are likely to consume more or less electricity than the
retailers predicted, and generators may choose (or be forced by outages) to
produce less than they’ve sold in their forward contracts. When this happens,
National Grid’s balancing mechanism kicks in, and they buy or sell electricity
to ensure a balance. Then, another organisation, Elexon, are responsible for
calculating an imbalance price for each half hour. Any participants that have
used more than they had bought (or generated less than they had sold) have to
pay the imbalance price for the amount they are short. Any participants that
have used less than they had bought (or generated more than they had sold)
receive the imbalance price for the amount they are long (have excess).

The imbalance price can be very volatile because it is expensive to store
electricity. In 2018 it ranged from £-150/MWh (ie you had to pay if you
produced too much electricity) to £990/MWh, so participants have a strong
incentive to minimise their imbalances.

# How is Electricity Traded on the Wholesale Market?

## Bilateral trading

Bilateral electricity trading refers to contracts between generators and
suppliers for the purchase of electricity. Usually, bilateral trading of
electricity is framed by some sort of master contract for a set period that
establishes overarching trading conditions. Individual trading contracts then
set the amounts of electricity to be traded and the trading price.

To avoid market imbalances, generators inform the system operator (National
Grid) of the volume of electricity traded before delivery.

## Market trading

Electricity supply and demand is mostly matched on two exchanges when it comes
to electricity delivered on the same day or the next day (the spot market): APX
and N2EX. In this case, an auction process matches offers from generators
(certain quantities of electricity at a certain price) and bids from suppliers
or large consumers (expected consumption).

Once more, avoiding market imbalances and grid capacity requires the network
operator (National Grid) to be aware of traded volumes of electricity.

## Long-term trading

Long-term trading of electricity mostly happens through electricity brokers.
There are nine members of the London Energy Brokers’ Association: BGC Partners,
Evolution Markets Ltd, GFI Group Inc, ICAP plc, Marex Spectron Group Ltd, PVM
Oil Associates, Tradition Financial Services Ltd, Tullett Prebon Inc, Griffin
Markets Limited).

Long-term electricity trading prices are established less according to supply
and demand than forecast market development: availability and cost of supply,
forecast demand, etc.

# Data streams and resources

Main data portal is [ELEXON BSC](https://developer.data.elexon.co.uk/api-details#api=prod-insol-insights-api&operation=get-generation-actual-per-type-from-from-to-to)




# Resources

[Guy Lipman](https://guylipman.medium.com/analysing-uk-electricity-prices-part-1-62890ea17713)
[Good Energy blog post](https://www.goodenergy.co.uk/blog/why-does-the-price-of-gas-drive-electricity-prices-including-renewables/)

