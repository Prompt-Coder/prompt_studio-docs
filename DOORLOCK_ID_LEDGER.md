# Doorlock ID Ledger

> Historical record of `ox_doorlock` id allocation across Prompt Studio products.

## Rule for new products

**Ship `(DEFAULT, 'name', 'data')` — never hardcode ids.** As of 2026-07-21 every product's doorlock SQL uses `DEFAULT` for the `id` column, so MySQL's AUTO_INCREMENT assigns a free id on import. A product can no longer collide with another product's doors, or with doors the buyer already has — no manual id allocation is needed.

The table below records the fixed ids products used **before** the DEFAULT migration. It is kept for reference only and no longer governs new work.

## Historical allocations (pre-DEFAULT)

| Doorlock IDs | Doors | Product |
| --- | ---: | --- |
| 9-30, 32-96 | 87 | `civilian-maps/opened-city-project.md` |
| 97-114 | 18 | `sandy-maps/sandy-city-hall.md` |
| 116-138 | 23 | `sandy-maps/sandy-hospital.md` |
| 140-158 | 19 | `sandy-maps/sandy-fire-department.md` |
| 159-199 | 41 | `sandy-maps/sandy-sheriff.md` |
| 200-202 | 3 | `sandy-maps/sandy-train-station.md` |
| 203-205, 207-215 | 12 | `sandy-maps/boat-house.md` |
| 216-218, 471-475 | 8 | `sandy-maps/sandy-marina.md` |
| 219-220 | 2 | `subscription-exclusives/gas-station.md` |
| 221-247, 249-252 | 31 | `sandy-maps/sandy-airport.md` |
| 253-258 | 6 | `subscription-exclusives/sandy-lost-mc.md` |
| 259-291 | 33 | `government-maps/blaine-county-cityhall.md` |
| 292-316 | 25 | `government-maps/paleto-fire-department.md` |
| 317-364 | 48 | `government-maps/vespucci-fire-department.md` |
| 365-370 | 6 | `government-maps/pillbox-fire-department.md` |
| 371-379, 381-402 | 31 | `government-maps/rockford-fire-department.md` |
| 403-445 | 43 | `government-maps/rockford-police-department.md` |
| 446-470 | 25 | `government-maps/noose-department.md` |
| 476-477, 479-501 | 25 | `subscription-exclusives/vespucci-cityhall.md` |
| 502-509 | 8 | `subscription-exclusives/rockford-dealership.md` |
| 514-517 | 4 | `subscription-exclusives/mosley-dealership.md` |
| 532 | 1 | `civilian-maps/reds-auto-parts.md` |
| 533-548 | 16 | `subscription-exclusives/japanese-restaurant.md` |
| 549-553 | 5 | `subscription-exclusives/dynasty-8.md` |
| 554-569 | 16 | `crime-maps/abandoned-theater.md` |
| 570-572 | 3 | `subscription-exclusives/paleto-hunting-store.md` |
| 573-599 | 27 | `civilian-maps/truck-you-repairs.md` |
| 600-609 | 10 | `civilian-maps/bus-station.md` |
| 610, 612-617 | 7 | `crime-maps/secret-underground-plantation.md` |
| 618-625 | 8 | `civilian-maps/wiwang-pc-club.md` |
| 626-633 | 8 | `crime-maps/gang-hideout-el-burro.md` |
| 634-644 | 11 | `crime-maps/gang-hideout-groove.md` |
| 645-652 | 8 | `crime-maps/gang-hideout-davis.md` |
| 653 | 1 | `subscription-exclusives/watch-store.md` |
| 654-682 | 29 | `subscription-exclusives/paleto-sheriff.md` |
| 1026-1031 | 6 | `subscription-exclusives/vinewood-fire-station.md` |
| 1032-1037 | 6 | `subscription-exclusives/legion-fire-station.md` |
| 1044-1050 | 7 | `sandy-maps/sandy-car-dealership.md` |
| 1051-1055 | 5 | `sandy-maps/sandy-church.md` |
| 1056-1065 | 10 | `sandy-maps/sandy-illegal-garage-and-gas-station-with-carwash.md` |
| 1066-1081 | 16 | `sandy-maps/sandy-mechanic.md` |
| 1082-1116 | 35 | `civilian-maps/repair-garages-5-locations.md` |
| 1117-1156 | 40 | `sandy-maps/sandy-motel.md` |
| 1157-1226 | 70 | `government-maps/san-andreas-highway-patrol-2-locations.md` |
| 1600-1712 | 113 | `sandy-maps/sandy-houses.md` |
| 1900-1919, 3007 | 21 | `sandy-maps/sandy-bank.md` |
| 1920-1964 | 45 | `civilian-maps/gym-5-locations.md` |
| 1965-1980, 1982-1985 | 20 | `civilian-maps/hornys-burgers-4-locations.md` |
| 1986-2524 | 539 | `government-maps/bolingbroke-prison.md` |
| 2525-2716 | 192 | `sandy-maps/sandy-apartments.md` |
| 2717-2753 | 37 | `sandy-maps/sandy-hospital-v2.md` |
| 2754-2770 | 17 | `sandy-maps/sandy-fire-station-v2.md` |
| 2771-2792 | 22 | `sandy-maps/university.md` |
| 2793-2851 | 59 | `civilian-maps/bilgeco-hq-and-warehouse.md` |
| 2852-2911 | 60 | `civilian-maps/4-dragons-casino-and-triad-hq.md` |
| 2912-2996 | 85 | `government-maps/mission-row-police-department.md` |
| 2997-3006 | 10 | `subscription-exclusives/motorcycle-paradise.md` |

> Note: `sandy-bank` door **G-3** was relocated to 3007 (out of the gym 1920 collision); the rest of the bank stays 1900-1919.
