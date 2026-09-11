# Screens

A variant of the "multimedia urban furniture" devices.

Variations:

- Orientation
- Size (pixels, width x height)
- Display technology
  - Dot-matrix
  - LCD
  - eInk

## Stop Screens

Example information architecture from MBTA's [Bus E-Ink](https://raw.githubusercontent.com/mbta/screens/refs/heads/main/docs/assets/sample_app_screenshots/bus_eink.png) screen:

- StopScreenHeader
  - StopName
    - `stops.stop_name`
  - LiveDateTime
    - `datetime`
  - StatusInfo
    - `status_info.is_connected`
    - `status_info.message`
  - TransitSystemLogo
    - `transit_system.logo`
- ScreenNextTripsBoard
  - ScreenNextTripRow
    - `routes.route_short_name`
    - `routes.route_long_name`
    - `trips.trip_headsign`
    - `stop_times.arrival_time`
    - `stop_times.departure_time`
    - `vehicle.occupancy_status`
    - `trip_update.stop_time_update.arrival.time`
- MessageBoardCarousel
  - MessageBoardItem
    - `item`
- MessageCard
  - MessageCardContent
    - `content`
- StopScreenFooter
  - StopScreenFooterMessage
    - `message`

```js
from "@infobus/vue" import { StopName, LiveDateTime, StatusInfo, TransitSystemLogo }
```

## Station Screens

## Kiosk Screens

## Vehicle Screens

## Operations Screens

Example: a one-pixel screen that blinks when the vehicle is incoming at the stop, steady-on when stopped at, and off otherwise.
