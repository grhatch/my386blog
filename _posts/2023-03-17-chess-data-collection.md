---
layout: post
title: 'Chess Data Collection'
author: Gavin Hatch
description: The process of collecting data for my chess data analysis project
image: /assets/images/black-and-white-chess.avif
---

# Chess Data Collection

<img 
    src="https://github.com/grhatch/my386blog/blob/main/assets/images/knights.avif?raw=true" alt="knights" style="display: block;
            margin-left: auto;
            margin-right: auto; width:400px;"
/>

White moves first. This rule is well known by almost everyone - even if they don't know how to play. Is this an advantage? Does the first move have an effect on the outcome of the game? Or does black's response to white's opening take control of the match's direction?

I have spent quite some time playing and learning about chess in the past few months, and this question has come up often as I look at stats of top players and explore new openings. To find out, I went to [chess.com](https://www.chess.com) to look for an API.

Every game of chess on chess.com is well documented. It has everything from the players' moves to the type of game played (e.g. blitz, rapid, daily). Gratefully, chess.com has a committed community that put together a public API with the ability to access all of this data.

As no API key is required, all the information is publicly available, and nobody's private data is up for grabs, no ethical problems were had in gathering this data.

The [API's documentation](https://www.chess.com/news/view/published-data-api) comments on the subject:

"Our goal is to re-package all currently public data from the website and make it available via the PubAPI. "Public Data" is information available to people who are not logged in, such as player data, game data, and club/tournament information. This excludes private information that is restricted to the logged in user, such as game chat and conditional moves."

Using this public API, I collected a list of users and their games to look for trends in win rates vs color played. Additionally, I was curious to see if diffently titled players (i.e. Grand Master, International Master, etc.) have different outcomes based on the color they played.

With thousands of records of players and even more games, the potential of the data is immense. Here's to improving at one of the oldest and most popular games in the world. Stay tuned to find out how the color you play will affect your game!

Check out my repository by clicking [here](https://github.com/grhatch/chess-grhatch)!
