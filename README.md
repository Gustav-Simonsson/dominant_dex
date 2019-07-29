## Dominant DEX

Dominant DEX is an extension to the classical order book model for decentralized exchanges.  It increases the incentive to provide liquidity on the book and introduces hard time guarantees to make liquidity more reliable and transparent.

Dominant DEX also mitigates spoofing and some other challenges with current DEX / order book models.

## Description

This is a quick, informal description which assumes a regular order book and matching engine.

1. Add / configure the following on top of a regular order book based DEX:
1. All order fees are sent to a “Fee Pool”.  There is one Fee Pool per order book.
1. Limit orders can optionally include a timestamp denoting a future time instant.  If set, the order cannot be cancelled until this future time.
1. Maker fees are defined by a continuous function which is not only proportional to the order amount, but also inversely proportional to:
   1. How far in the future the order is locked.
   1. How close the order is to the bid-ask spread.
1. Maker orders locked far enough into the future and close enough to the bid-ask spread will get a negative fee, which transforms into a claim on the Fee Pool.
1. Taker fees must be positive and should generally be higher than the highest maker fee.

Essentially, this adds an optional incentive for makers to not only get a lower or zero fee - but even get paid for locking their liquidity.  Makers can very granulary configure their liquidity cost vs potential fee revenue.

Long term hodlers can safely earn funds by locking their tokens at their long-term target price.  Short-term speculators/traders can earn a significant percentage on liquidity they would anyway place in limit orders, and be more incentivized to make liquidity than take it.

Takers - while required to pay a positive fee - gain not only from the increased amount of liquidity on the book, but also from the hard time guarantees.  A taker can filter the order book to only see liquidity locked within the time frame they care about.

Time locked liquidity cannot be spoofed.

This could create a market that both makers and takers prefer over a zero-fee regular DEX.  A key assumption is that liquidity is often the most important factor for market participants - especially larger ones - often triumphing centralized counterparty risk and considerable trade fees (e.g. 0.3%).  Takers that are currently accepting industry standard fees would presumably do so in a Dominant DEX that gives them access to more reliable and predictable liquidity.

Open questions include:
1. Should the inverse proportional factors in the maker fee function (duration of time locks and proximity to bid-ask spread) be linear, quadratic, etc?
1. What is a meaningful maximum time lock period?  True hodlers would surely prefer infinite lockup, but that would also give a negligible fee decrease compared to e.g.  1y lockup.
1. What is the best way to compute a new order’s proximity to the bid-ask spread?
   1. To avoid (extremely) short term manipulation, it could make sense to use a time and/or volume based average of the spread.
   1. As the spread moves while the order is locked, how/would the proximity factor be updated?
1. How exactly is the negative maker fee == claim on Fee Pool modeled?  E.g. a time locked order could continuously earn fees as long as it is not (fully) crossed.


## License

The Dominant DEX repo is licensed under the
[GNUBL License](https://github.com/Gustav-Simonsson/GNUBL/blob/master/LICENSE),
also included in this repository in the `LICENSE` file.