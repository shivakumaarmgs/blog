+++
title = '1 Series Introduction'
date = 2024-06-20T22:37:09+05:30
draft = true
+++

### Background

I've a total of 11 years of experience and started my career a Full-Stack Ruby on Rails developer. In the last 2 years I'm working as Backend Ruby developer building micro-services to tackle the AFC topics for a German based BaaS company. Now I've started learning Go.

In our organisation we have monolith that has grown big in the last 8-9 years, in terms of code and the number of teams supporting it. Hence any change to the monolith is becoming a big task that needs lot of co-ordination and support from various teams. The decision is to split the monolith by cutting out features to its own micro-services and writing them primarily in Go.

### Motive

I've been reading a lot of tutorials, watching videos and practicing few exercise to get myself familiar with Go. It has helped a little. I'm able to browse source code of other projects in my organisation written in Go and I now understand the keywords, statements. But still can't form an end-to-end understanding of how things work and why is something built the way it is.

I want to accelerate my learning so that I can build projects from scratch, learn best practices, review code written by others, deploy projects to production. What is the best way other than learning by doing? 

### The Plan: Creating a Tic-Tac-Toe API in Go

I've decided to create a simple API-based Tic-Tac-Toe application in Go, where two players can create a game, take turns playing, and continue until the game results in a win or a draw.

On a high level, this is what the API will need to do:

- **Game Initialisation**: Each new game will be assigned a unique game ID to track the game instance.
- **Two Players**: The API will support two players—x_team and o_team—who will take turns making moves.
- **Turn-Based Gameplay**: Players must take turns, and the same player cannot send consecutive moves. The API will ensure that moves are made in the correct order.
- **Move Validation**: The API will prevent invalid moves, such as marking an already occupied tile. If a player tries to make an invalid move, the API will return an appropriate error response.
- **Game State and Persistence**: After each move, the API will return the current game state and, once completed, store the final result (win, draw, or ongoing) for future retrieval.

Implementing this from scratch to a full featured application with database to store all the games and results should give a good solid foundation in backend development with Go Lang - atleast I believe. I will build this step by step in smaller increments, trying different libraries along the way.

This blog series is mainly to log and share my learning as I build in increments. Also I believe this will help anyone who is starting with Web development in Go. First post in the series, setting up the Tic-Tac-Toe Project.
