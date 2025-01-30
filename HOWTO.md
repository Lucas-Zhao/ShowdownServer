# Overview
The purpose of this document is to be a general how-to on managing a pokemon showdown server from start to finish.

# Administration
Pokemon showdown consists of two services, the "server" and "client". The server piece handles actual battle simulation and logic, while the client bridges between players and the server and displays animations, chat rooms, etc to end users. Both of these services are servers that need to be hosted at a shared location, for instance AWS.

The client piece is hosted as a web server, and will need HTTPS SSL Certificate configuration to work on a public domain. Users connect with the client by websockets, which can require an additional configuration piece.
	The client repository that pokemon showdown provides is not "batteries included" primarily, it does not come with user authentication out of the gate. Elite Redux uses an OAuth client provided by pokemon showdown in order to authenticate existing pokemon showdown users with our server. They have a form to request oauth credentials for a website: https://forms.gle/VAoSjqHn4zwem7tp9
The server piece is hosted as a TCP server and should not be publicly available, it only needs to be communicated with by the web server.

I recommend starting with the latest pokemon showdown repository code, since you were wanting to make sure you get newest updates for ZA, etc. 
It's important to know that code we worked on for Elite Redux was already out of date with the latest showdown, since it was from a forked repository that they had worked on in the past.
The only caveat there is some of the snippets/solutions we created for Elite Redux "may" not be perfectly plug and play with the latest codebase, but probably will.

Sprites are not included with any repository, we wrote a script to download them from pokemon showdown live. This is a client side change.

# Adding a pokemon

Updates to these files are required to add a new pokemon:
- data/formats-data.ts - This file controls the format restrictions for gen 9. All pokemon are listed here and can be given a tier for singles, double and national dex play. "Illegal" will make the pokemon not eligible for that format.
- data/items.ts - This file controls the items available for gen 9. All items are listed here and can be given a gen which is used to control what gens/formats the item is legal in.
- data/learnsets.ts - This file controls the moves a given pokemon can learn legally. See #learnset-codes below for more details.
- data/moves.ts - This file controls move definitions. Add new moves here.
- data/pokedex.ts - This file defines all pokemon available.
- data/rulesets.ts - This file contains the rulesets for the different formats. Rulesets specify things like species clause and also implement the logic to handle validating teams to fit those rules.
- texts/* These files contain descriptive texts for the different dex definition files that will be shown on screen.

# Git



# Learnset codes
This table indicates the codes used for learnsets. A learnset code is specified as {gen}{code}{level}.
For instance, 9L1 means [generation 9][Level-up][level 1].
```
 * - M = TM/HM
 * - T = tutor
 * - L = start or level-up, 3rd char+ is the level
 * - R = restricted (special moves like Rotom moves)
 * - E = egg
 * - D = Dream World, only 5D is valid
 * - S = event, 3rd char+ is the index in .eventData
 * - V = Virtual Console or Let's Go transfer, only 7V/8V is valid
 * - C = NOT A REAL SOURCE, see note, only 3C/4C is valid
```