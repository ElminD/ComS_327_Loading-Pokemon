# ComS_327_Loading-Pokemon

COM S 327, Spring 2022
Programming Project 1.07
Loading Pokemon ´
We’ve parsed in a number of data files that specify certain details about how to create pokemon. Now ´
we’re actually going to load them into our game. We’ll add the ability to encounter them, but we’ll save
battling and capturing for next week.
We’re going to simplify many of the mechanics of the pokemon main series games (MSGs) in our im- ´
plementation. The full mechanics are just too tedious, which would result in a lot of code and not much
learning. If correct (or more correct) mechanics are important to you, you’re welcome to implement something more detailed than presented here.
When walking through tall grass, each move the PC makes has a certain chance of encountering a
pokemon. In the MSGs, different areas of the world will have different kinds of pok ´ emon in the grass, as ´
well as other types of terrain (desert, caves, water) that may spawn pokemon, as well. We’ll simplify this ´
by allowing any (literally any!) pokemon to spawn in any tall grass, this includes fully evolved forms and ´
legendary and mythical pokemon. We’ve parsed in details on 1092 pok ´ emon; we’ll select from them on a ´
uniform distribution, which means that you have an equal chance of encountering a pidgey and a mewtwo.
As for the probability of encountering a pokemon in the tall grass, something like 10% seems reasonable. ´
The levels of encountered pokemon will increase with the manhatten distance from the origin. When ´
distance is less than or equal to 200, minimum level is 1 and maximum level is distance / 2 (integer division).
When distance exceeds 200, minimum level becomes (distance - 200) / 2 and maximum level is 100.
Encountered pokemon will know up to two moves. The known moves are restricted to the pok ´ emon’s ´
level-up learnset and will only be less than two if the pokemon has fewer than two moves in its level-up ´
learnset at its level.
The pokemon in our database are grouped in many ways. The ´ version group id in pokemon
moves.csv is a unique identifier of a pokemon game, and (I think) a value of 19 in the only one for ´
which all pokemon have learnsets. We’ll use that one, so that we can use all of the pok ´ emon. Again, you’re ´
welcome to do something different here, but it will increase the complication of your game somewhat.
To find the level-up moveset of a pokemon, you’ll want ´ pokemon moves.version group id
equal to 19, pokemon moves.pokemon id equal to pokemon.species id and pokemon
moves.pokemon move method id equal to 1. From these, select your two moves from a uniform
distribution.
Pokemon stats (attack, defense, etc.) are given in ´ pokemon stats.csv, which we didn’t parse last
week, so you’ll need to parse that in now. The mapping of stat numbers to names is given in stats.csv.
Each pokemon has an additive deviation from its species’ base stats, known as IVs (individual values). IVs ´
for each stat are uniformly distributed in the range [0,15]. Generate IVs for each spawned pokemon for each ´
of HP, attack, defense, speed, special attack, and special defense.
The mechanics of pokemon gender are somewhat involved (designed to reduce storage, see ´
https://bulbapedia.bulbagarden.net/wiki/Individual values). Some pokemon don’t even have genders. We’ll ´
simplify this by making all species have equal probability of being male or female. As with everything else
here, you’re welcome to implement the more complex mechanic if you like.
Pokemon have a 1/8192 chance of being shiny, based on their IVs (see the above link). Again, simplify ´
this by ignoring the IVs and simply using, e.g., rand() % 8192 == 0. Feel free to reduce that modulus to
increase your shiny rate.
In order to level up your pokemon, we’ll apply the following formulae: ´
HP = b
((base + IV ) × 2) × level
100
c + level + 10
Otherstat = b
((base + IV ) × 2) × level
100
c + 5
where base is the pokemon species’ base stat, ´ IV is its IV for the given stat and level is the pokemon’s ´
level. Again, we’re simplifying an MSG mechanic here by ignoring EVs (effort values), which normally
add an additional boost to pokemon growth. See ´
https://bulbapedia.bulbagarden.net/wiki/Stat for the deets.
When encountering pokemon, you’ll add a placeholder function for the battle and capture sequence in ´
which you’ll print the pokemon’s level, stats, and moves and pause for input (escape, any key, etc.). ´
A final note: There are probably only two of you (maybe three) who know less about pokemon than me. ´
Please let me know if I got something qualitatively wrong here, or if you think of a better simplification to
MSG mechanics than I’ve proposed.
