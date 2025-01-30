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


# Git
