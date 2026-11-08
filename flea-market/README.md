# Tarkov Flea Market Price Calculator

A single-page, no-dependency calculator for pricing Escape from Tarkov flea market listings.
Open `index.html` in any browser. Inputs are remembered in your browser's local storage.

## Inputs
- **Current minimum list price** (per item)
- **Quantity**
- **Qty buffer % per doubling / max**: extra undercut for larger stacks, which stay listed longer and are more likely to be undercut (default 1% per doubling, capped at 10%)
- **Item base price**: drives the listing fee. A helper converts a trader's buy price to base price (trader price ÷ trader multiplier).
- **Fee reductions**: Intelligence Center level 3 (−30%) plus Hideout Management (+0.3%/level, up to 45%)
- **Advanced**: cost per item, target margin %, undercut amount, Ti/Tr tax constants

## Outputs
- **Optimal list price**: current min minus the quantity buffer and undercut, never below the price that meets the target margin
- **Margin peak price**: the price where the fee takes the smallest share (about 1.6× base price with no cost), compared against the optimal price
- **Profit at current minimum**
- **Listing fee at optimal**: total, per item, and as a % of revenue
- **Price scale**: ±50% of the optimal price in 10% steps, plus margin-peak and current-min rows, with fee, profit and margin at each price

## Fee formula
```
Fee = (VO·Ti·4^PO + VR·Tr·4^PR) · Q · (1 − discount)
VO = base price, VR = list price, Ti = Tr = 0.03
PO = log10(VO/VR), PR = log10(VR/VO); whichever is positive is raised to the 1.08 power
```
Source: [Escape from Tarkov Wiki – Flea market](https://escapefromtarkov.gamepedia.com/Flea_market).
Always compare the calculated fee at the current min with the in-game fee. A mismatch usually means the base price is off.
