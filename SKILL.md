---
name: searchapi-travel-planning
description: Use live SearchApi results to compare hotels by stay cost and door-to-door transit, or shortlist flights by full itinerary and fare terms. Use for date-specific travel research and venue or airport trips with concrete constraints.
---

# Plan a trip with SearchApi

Start with exact local dates, traveler counts, currency, and requirements that could rule out an otherwise cheap option. For a venue trip, get the destination and the local arrival deadline or commute limit. For flights, get acceptable airports, date flexibility, bags, and tolerance for self-transfers. Ask for missing details when they would change the shortlist. Label any other assumptions.

Use the connected SearchApi tools for live results. If they are unavailable and the environment already has `SEARCHAPI_API_KEY`, use the REST examples in [Request examples](references/requests.md). If neither is available, explain what could be checked and identify any estimates. Keep credentials out of URLs, files, and output.

## Hotels and transit

- Search Booking.com or Google Hotels for the same dates and occupancy across neighborhoods. Consider well-connected areas as candidates. Keep the room type, taxes and fees, cancellation terms, and hard requirements such as pet policy or a heated pool with each quote. Confirm details that materially affect the choice on the property or seller page.
- For the best few options, get transit directions from the exact property address, place ID, or coordinates to the venue entrance. Route to the same arrival time in the destination's timezone. Compare total door-to-door time, walking, transfers, and expected arrival. Check the evening return separately when late service matters.
- Report a compact shortlist with total stay price and currency, rate conditions, transit time, walking and transfers, and seller and route links where available. Call out why a cheap option failed a constraint. Show a station-to-station time separately if it helps explain the route.

## Flights

- For flexible trips, use the Google Flights Calendar tool to find promising dates. Then use the flight search for exact dates and airports. Compare equivalent cabin, traveler count, baggage, layover duration, and connection type. Flag separate tickets and self-transfers.
- Fetch booking options for the selected itinerary when available. Keep the search quote and the seller's total separate. Capture the seller, currency, baggage terms, and when each quote was checked. If the fare changes or the booking link fails, report the discrepancy and which details still need checking.

Finish with the best options for the user's constraints and the specific checks that could change the decision. Label prices as quotes unless the user has a confirmed booking. If an amount is missing or incomparable, leave it unknown. Leave purchases and reservations to the user's explicit direction.
