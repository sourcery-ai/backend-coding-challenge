# Sourcery Backend Coding Challenge

(inspired by https://github.com/busbud/coding-challenge-backend-c)

## Requirements

Design a REST API endpoint that provides auto-complete suggestions for large
cities.

- The endpoint is exposed at `/suggestions`
- The partial (or complete) search term is passed as a querystring parameter `q`
- The caller's location can optionally be supplied via querystring parameters
  `latitude` and `longitude` to help improve relative scores
- The endpoint returns a JSON response with an array of scored suggested matches
  - The suggestions are sorted by descending score
  - Each suggestion has a score between 0 and 1 (inclusive) indicating
    confidence in the suggestion (1 is most confident)
  - Each suggestion has a name which can be used to disambiguate between
    similarly named locations
  - Each suggestion has a latitude and longitude

## Advice

- **Try to design and implement your solution as you would do for real
  production code**. Show us how you create clean, maintainable code that does
  awesome stuff. Build something that we'd be happy to contribute to. This is
  not a programming contest where dirty hacks win the game.
- Documentation and maintainability are a plus, and don't you forget those unit
  tests.
- We don’t want to know if you can do exactly as asked (or everybody would have
  the same result). We want to know what **you** bring to the table when working
  on a project, what is your secret sauce. More features? Best solution?
  Thinking outside the box?

## Data

Use the cities in the tab separated file `data/cities_canada-usa.tsv`. You'll
need the name, latitude and longitude fields which are indices 1, 4, 5 below:

- geonameid : integer id of record in geonames database
- name : name of geographical point (utf8) varchar(200)
- asciiname : name of geographical point in plain ascii characters, varchar(200)
- alternatenames : alternatenames, comma separated varchar(5000)
- latitude : latitude in decimal degrees (wgs84)
- longitude : longitude in decimal degrees (wgs84)

## Sample responses

These responses are meant to provide guidance. The exact values can vary based
on the data source and scoring algorithm

**Near match**

```
GET /suggestions?q=Londo&latitude=43.70011&longitude=-79.4163
```

```json
{
  "suggestions": [
    {
      "name": "London, ON, Canada",
      "latitude": "42.98339",
      "longitude": "-81.23304",
      "score": 0.9
    },
    {
      "name": "London, OH, USA",
      "latitude": "39.88645",
      "longitude": "-83.44825",
      "score": 0.5
    },
    {
      "name": "London, KY, USA",
      "latitude": "37.12898",
      "longitude": "-84.08326",
      "score": 0.5
    },
    {
      "name": "Londontowne, MD, USA",
      "latitude": "38.93345",
      "longitude": "-76.54941",
      "score": 0.3
    }
  ]
}
```

**No match**

```
GET /suggestions?q=SomeRandomCityInTheMiddleOfNowhere
```

```json
{
  "suggestions": []
}
```

## References

- Geonames provides city lists Canada and the USA
  http://download.geonames.org/export/dump/readme.txt

## Getting Started

Begin by cloning this repo.
