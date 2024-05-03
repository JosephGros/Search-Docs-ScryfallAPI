# MTG Vault Search


### Main URL for scryfall API - https://api.scryfall.com/

**How the url could look**

https://api.scryfall.com/cards/search?include_extras=true&include_variations=true&order=set&q=e%3Aotc&unique=prints

### Breakdown of the url

***&*** - Between every parameter except after search becuase then you need '?' after search.

***include_extras=true*** - if extras cards should be included or not.

***include_variations=true*** - if different variations of each card should be included.

***order=set*** - In what order you want the cards to be sorted. Read more [here](#order).

***q=e%3Aotc*** - This is the search query and is built in a sertain way. See more detailed info [here](#Search-query).
 
***unique=prints*** - Returns all prints that exist for each card. Read more [here](#unique).

<br><br><br>

## Explainations from scryfall API docs

- ***q*** | String | A fulltext search query. Make sure that your parameter is properly encoded. Maximum length: 1000 Unicode characters.

- ***unique*** | String | The strategy for omitting similar cards. [See below](#unique).

- ***order*** | String | The method to sort returned cards. [See below](#order).

- ***dir*** | String | The direction to sort cards. [See below](#dir).

- ***include_extras*** | Boolean | If true, extra cards (tokens, planes, etc) will be included. Equivalent to adding include:extras to the fulltext search. Defaults to false.

- ***include_multilingual*** | Boolean | If true, cards in every language supported by Scryfall will be included. Defaults to false.

- ***include_variations*** | Boolean | If true, rare care variants will be included, like the Hairy Runesword. Defaults to false.

- ***page*** | Integer | The page number to return, default 1.

- ***format*** | String | The data format to return: json or csv. Defaults to json.
pretty

<br><br>

## Unique

- ***cards*** | Removes duplicate gameplay objects (cards that share a name and have the same functionality). For example, if your search matches more than one print of Pacifism, only one copy of Pacifism will be returned.

- ***art*** | Returns only one copy of each unique artwork for matching cards. For example, if your search matches more than one print of Pacifism, one card with each different illustration for Pacifism will be returned, but any cards that duplicate artwork already in the results will be omitted.

- ***prints*** - Returns all prints for all cards matched (disables rollup). For example, if your search matches more than one print of Pacifism, all matching prints will be returned.

<br><br>

## Order

So for example ***&order=set*** as in the url above its going to sort the cards by their set and then collector number.

- ***name*** | Sort cards by name, A → Z

- ***set*** | Sort cards by their set and collector number: AAA/#1 → ZZZ/#999

- ***released*** | Sort cards by their release date: Newest → Oldest

- ***rarity*** | Sort cards by their rarity: Common → Mythic

- ***color*** | Sort cards by their color and color identity: WUBRG → multicolor → colorless

- ***usd*** | Sort cards by their lowest known U.S. Dollar price: 0.01 → highest, null last

- ***tix*** | Sort cards by their lowest known TIX price: 0.01 → highest, null last

- ***eur*** | Sort cards by their lowest known Euro price: 0.01 → highest, null last

- ***cmc*** | Sort cards by their mana value: 0 → highest

- ***power*** | Sort cards by their power: null → highest

- ***toughness*** | Sort cards by their toughness: null → highest

- ***edhrec*** | Sort cards by their EDHREC ranking: lowest → highest

- ***penny*** | Sort cards by their Penny Dreadful ranking: lowest → highest

- ***artist*** | Sort cards by their front-side artist name: A → Z

- ***review*** | Sort cards how podcasts review sets, usually color & CMC, lowest → highest, with Booster Fun cards at the end

<br><br>

## Dir

- ***auto*** | Scryfall will automatically choose the most inuitive direction to sort

- ***asc*** | Sort ascending (the direction of the arrows in the previous table)

- ***desc*** | Sort descending (flip the direction of the arrows in the previous table)

<br><br>

## Search query


Here comes the tricky part. The search query is built in the way that you need to use [percent encoding](https://en.wikipedia.org/wiki/Percent-encoding). That means that for characters like **: ; | < >** and so on have an encoding that looks like this:

<img src="./images/image.png">
<br>
<img src="./images/image-1.png">

<br>

So every character has its encoding underneath. This means that if we want to write a ":" in the search query, we need to write "%3A". And this is important because the API expects certain ":" and so on in the search query. 

**From scryfall** - Use ***s:, e:, set:, or edition:*** to find cards using their Magic set code.

So this means that for it to be a ***e:*** we need to wright ***e%3A*** instead for the search to be accepted. 

Here's an example:

Set name OTC (Outlaws of Thunder Junction).
The search query would be ***e%3Aotc*** like this ***&q=e%3Aotc***. So its important to check the [scryfall docs](https://scryfall.com/docs/syntax) for knowing what they want for edition, cards, sets and so on. That way whe can get the wright information. 