# Documentatie BGT LD

Zie welke types ondersteund worden door naar de GraphQL editor te gaan: <https://labs.kadaster.nl/gateway/>

In onderstaande stappen noemen we zo'n type bijvoorbeeld `NAAM = bak`.

We bouwen een GraphQL query in een file `NAAM.graphql`, op basis van wat we in de GraphQL editor zien.  Kijk naar het bestand `bak.graphql` voor een voorbeeld.

We halen de resultaten op van de GraphQL endpoint in reguliere JSON:

```sh
curl -X POST -H "Content-Type: application/json" -H "Accept: application/json" --data-binary @NAAM.graphql https://labs.kadaster.nl/gateway/graphql > NAAM.json
```

We kunnen dezelfde resultaten ophalen bij het Enhancer endpoint in JSON-LD:

```sh
curl -X POST -H "Content-Type: application/json" -H "Accept: application/ld+json" --data-binary @NAAM.graphql https://labs.kadaster.nl/enhancer > NAAM.jsonld
```

Volg de installatie instructies op [JSON-LD CLI](https://github.com/digitalbazaar/jsonld-cli).

Van die JSON-LD kan automatisch N-Quads (een RDF formaat) gemaakt worden:

```sh
jsonld format -q NAAM.jsonld > NAAM.nq
```

Het N-Quads bestand (`NAAM.nq`) kan worden geupload in de triple store: <https://data.labs.kadaster.nl/bgt-test-omgeving>

Het BGT vocabulaire daar daar worden bijgeladen middels de import functionaliteit: (1) Ga naar "Graphs", (2) Klik op "Import a new graph", (3) Selecteer `kadaster/bgt` in het veld "Add data from an existing dataset".
