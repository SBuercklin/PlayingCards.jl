# PlayingCards.jl

|||
|---------------------:|:----------------------------------------------|
| **Docs Build**       | [![docs build][docs-bld-img]][docs-bld-url]   |
| **Documentation**    | [![dev][docs-dev-img]][docs-dev-url]          |
| **GHA CI**           | [![gha ci][gha-ci-img]][gha-ci-url]           |
| **Code Coverage**    | [![codecov][codecov-img]][codecov-url]        |
| **Bors enabled**     | [![bors][bors-img]][bors-url]                 |

[docs-bld-img]: https://github.com/charleskawczynski/PlayingCards.jl/workflows/Documentation/badge.svg
[docs-bld-url]: https://github.com/charleskawczynski/PlayingCards.jl/actions?query=workflow%3ADocumentation

[docs-dev-img]: https://img.shields.io/badge/docs-dev-blue.svg
[docs-dev-url]: https://charleskawczynski.github.io/PlayingCards.jl/dev/

[gha-ci-img]: https://github.com/charleskawczynski/PlayingCards.jl/workflows/ci/badge.svg
[gha-ci-url]: https://github.com/charleskawczynski/PlayingCards.jl/actions?query=workflow%3Aci

[codecov-img]: https://codecov.io/gh/charleskawczynski/PlayingCards.jl/branch/main/graph/badge.svg
[codecov-url]: https://codecov.io/gh/charleskawczynski/PlayingCards.jl

[bors-img]: https://bors.tech/images/badge_small.svg
[bors-url]: https://app.bors.tech/repositories/32815

A package for representing playing cards for card games (for a standard deck of fifty two).

## Cards

A playing `Card` is consists of a suit (`♣`,`♠`,`♡`,`♢`) and a rank:

 - `Rank(N::Int)` where `1 ≤ N ≤ 13` where
 - `N = 1` represents an Ace (which can have high or low values via `high_value` and `low_value`)
 - `N = 11` represents a Jack
 - `N = 12` represents a Queen
 - `N = 13` represents a King

The value of the rank can be retrieved from `high_value` and `low_value`:

 - `high_value(c::Card) == low_value(c::Card) == c.rank`
 - `high_value(::Card) = 14` for Ace
 - `low_value(::Card) = 1` for Ace

`Card`s have convenience constructors and methods for extracting information about them:

```julia
julia> using PlayingCards

julia> card = A♡
A♡

julia> string(card)
"A♡"

julia> suit(A♡)
Heart()

julia> rank(A♠)
Ace()

julia> high_value(A♢)
14

julia> high_value(J♣)
11

julia> low_value(A♡)
1
```

## Decks

A `Deck` is a struct with a `Vector` of `Card`s, which has a few convenience methods:

```julia
julia> using PlayingCards

julia> deck = ordered_deck()
A♣ 2♣  3♣  4♣  5♣  6♣  7♣  8♣  9♣  T♣  J♣  Q♣  K♣
A♠ 2♠  3♠  4♠  5♠  6♠  7♠  8♠  9♠  T♠  J♠  Q♠  K♠
A♡ 2♡  3♡  4♡  5♡  6♡  7♡  8♡  9♡  T♡  J♡  Q♡  K♡
A♢ 2♢  3♢  4♢  5♢  6♢  7♢  8♢  9♢  T♢  J♢  Q♢  K♢


julia> shuffle!(deck)

julia> hand = pop!(deck, 2)
(5♣, 8♢)

julia> deck
Q♣  T♣  5♢  K♠  J♢  4♢  T♡  K♢  2♠  5♠  2♡  8♣  8♠
K♣  T♠  A♣  Q♠  Q♢  2♢  7♣  6♣  J♡  9♠  6♢  A♢  7♠
A♡  7♡  3♢  3♣  7♢  J♠  5♡  4♡  9♢  4♣  3♠  J♣  6♡
9♡  6♠  T♢  3♡  A♠  8♡  K♡  2♣  4♠  Q♡  9♣
```

## Acknowledgements

Some ideas used here were inspired by
 - [@StefanKarpinski](https://github.com/StefanKarpinski)'s [Cards.jl](https://github.com/StefanKarpinski/Cards.jl)
 - [@scheinerman](https://github.com/scheinerman)'s [PlayingCards52.jl](https://github.com/scheinerman/PlayingCards52.jl)

