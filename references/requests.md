# SearchApi request examples

With a SearchApi connector, select the corresponding Booking.com, Google Hotels, Google Maps Directions Transit, or Google Flights tool and use its declared parameter schema. The REST interface uses the engine names below.

## Compare hotel prices and commutes

For the REST examples, use a POSIX shell with curl and an existing `SEARCHAPI_API_KEY` environment variable. Set `destination`, `check_in` and `check_out` (YYYY-MM-DD), `adults`, and `currency` (ISO currency code) from the trip.

```sh
curl --silent --show-error --fail --get 'https://www.searchapi.io/api/v1/search' \
  --header "Authorization: Bearer ${SEARCHAPI_API_KEY:?Set SEARCHAPI_API_KEY}" \
  --data-urlencode 'engine=booking' \
  --data-urlencode "q=${destination}" \
  --data-urlencode "check_in_date=${check_in}" \
  --data-urlencode "check_out_date=${check_out}" \
  --data-urlencode "adults=${adults}" \
  --data-urlencode "currency=${currency}"
```

Inspect `properties` for each room type, stay `price`, `taxes_and_charges`, and `gps_coordinates` when present. Check whether taxes and charges are already included before calculating a total. Use the seller link to verify the room conditions. See the [Booking.com API](https://www.searchapi.io/docs/booking-api). The [Google Hotels API](https://www.searchapi.io/docs/google-hotels-api) is another source and returns separate `price_per_night` and `total_price` objects when available.

For each finalist, set `hotel_address` and `venue_address` to precise locations. Set `arrival_epoch` to the Unix timestamp corresponding to the desired local arrival date and time at the venue. Keep it the same across hotels.

```sh
curl --silent --show-error --fail --get 'https://www.searchapi.io/api/v1/search' \
  --header "Authorization: Bearer ${SEARCHAPI_API_KEY:?Set SEARCHAPI_API_KEY}" \
  --data-urlencode 'engine=google_maps_directions' \
  --data-urlencode "from=${hotel_address}" \
  --data-urlencode "to=${venue_address}" \
  --data-urlencode 'travel_mode=transit' \
  --data-urlencode "time=arrive_by:${arrival_epoch}"
```

Read the route's `formatted_duration`, `time_window`, and `instructions` in `directions`. The instructions show individual legs. Use the route duration for the comparison, including the walks to and from stations. See the [Google Maps Directions API](https://www.searchapi.io/docs/google-maps-directions-api).

## Shortlist and verify fares

- Use [Google Flights Calendar](https://www.searchapi.io/docs/google-flights-calendar-api) to find dates. For round trips, constrain date windows to the documented combination limit and compare the same traveler count and currency.
- Use [Google Flights](https://www.searchapi.io/docs/google-flights-api) with exact dates to inspect route and fare details. For a round trip, select the outbound with the returned `departure_token`, then use the final itinerary's `booking_token` to fetch seller options. Keep date, passenger, and cabin parameters consistent between calls. If the seller requires a form submission, use the provider's documented handoff or direct the user to the seller with the itinerary details.
