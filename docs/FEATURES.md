# Features used by the ranking notebook

## Raw configuration

- user, current-POI, previous-POI, and candidate-POI identifiers;
- current and candidate POI categories;
- hour, weekday, weekend indicator, trail step, and time since previous visit;
- geographic distance between current and candidate POIs;
- Markov transition count and probability;
- candidate popularity calculated from training targets only;
- same-city and same-category indicators.

## Additional enriched features

### Prediction-time context

- temperature, precipitation, wind speed, conditions, and precipitation type;
- holiday name and public-holiday indicator;
- days since and until a holiday;
- opening status and visit-time bucket;
- missingness/imputation flags.

### Candidate POI context

- price, rating, rating count, tip count, and POI-metadata availability;
- nearest public-transport stop distance, feed, and transport mode;
- stop-availability flags at 250 m, 500 m, and 1,000 m;
- bus, rail, subway, metro, and total stop counts at those radii;
- missingness/imputation flags.

### Interaction features

- precipitation × geographic distance;
- weekend × candidate popularity;
- geographic distance × nearest-transit-stop distance.

No `target_next_*`, `minutes_until_next`, or other future-label columns are used as
model inputs.
