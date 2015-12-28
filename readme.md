# Drinkspec

This is an attempt to enumerate what Drinkspec is and how we should attempt to build it.

Author: [@gooley](https://github.com/gooley)

## Mission

**"Github for cocktails"**

Build an open ecosystem for creating, perfecting, and sharing cocktails by leveraging the power of version control and borrowing collaborative editing ideas such as forking and discussions.

## Project Goals

1. Create open repository of cocktails which can be used and augmented by the community.
2. Include non-technical users.
3. Embrace normalization of data and domain knowledge to make a specific cocktail platform. This is not a general purpose system.

## Key Concepts

* open data
  * strong public API
  * permissive licensing by default
* text-based
  * easily diffable
  * portable, editable anywhere
  * convertable from primary spec to alternate formats (e.g. into Markdown/HTML)
* discoverable
  * search for cocktails by name
  * search by ingredients
  * search by similarity
  * "editorial" component (highlight new/interesting drinks)
  * embeddable (like twitter cards or gists)
* powerful
  * embrace power users
  * make it easy to connect to other services (e.g. Amazon Echo)
  * CLI tools
  * open-source API libraries
* collaborative
  * discussions
  * voting (or some way to indicate quality/popularity)
  * forkable (let me create variations while tracking provenance)
  
## Management

TBD

## Data Structure [draft]

In order to generalize the data, certain formal data structures will be necessary. We should make an effort to have a very minimal number of required fields in order to ease data entry and import. Augmenting and normalizing data after-the-fact should be made easy and batchable.

When possible, references (like [**Ingredients**](#ingredient)) should be referenced by a human-readable name. Naming variations of identical Ingredients should be fuzzy-matched or human-aliased after-the-fact.

#### Drink

The **Drink** is our primary object and should be able to be completely specified in a single text document with implicit references to additional objects (e.g. [**measures**](#measure) may be an array of hashes)

* name: String
* measures: Set[[**Measure**](#measure)]
* steps: Seq[String]
* tags: Set[**Tag**]
* history: String
* refs: Set[**Ref**]
* images: Seq[Image]
* credits: Set[**Credit**]

#### Measure

The **Measure** object aims to normalize unit-based measures of ingredients to enable changes of units (fluid ounces into milliliters) as well as multiplication of quantities (make 2 of this drink).

The reference to [**Ingredient**](#ingredient) may be specified by a string name.

* quantity: Decimal
* unit: Enum (oz, splash, dashes, peel)
* ingredient: [**Ingredient**](#ingredient)
* note: String
* optional: Bool
* garnish: Bool

#### Ingredient

The **Ingredient** object aims to normalize the components of a cocktail in order to aid in reverse-cocktail searches (e.g. "what can I make with these three ingredients?") as well as to assist with categorizing drinks and identifying similar cocktails.

* name: String
* categories: Set[**Category**]
* aliases: Set[String]
