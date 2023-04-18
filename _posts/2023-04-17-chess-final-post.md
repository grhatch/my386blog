---
layout: post
title: 'Checkmate - Final Chess Data Analysis'
author: Gavin Hatch
description: Results of my analysis of all the chess data!
image: /assets/images/checkmate.avif
---

# Final Analysis

<img 
    src="https://github.com/grhatch/my386blog/blob/main/assets/images/handshake.avif?raw=true" alt="handshake" style="display: block;
            margin-left: auto;
            margin-right: auto; width:400px;"
/>

This analysis is based on chess data that was collected through the [chess.com](https://www.chess.com) [API](https://www.chess.com/news/view/published-data-api). All data is public and availble for analysis. The data contains usernames, titles, number of games, accuracies, and win rates for white and black. For more information, reference [this earlier blog post](https://grhatch.github.io/my386blog/2023/03/17/chess-data-collection.html).

Our question at the beginning was whether color of pieces affected win rate. After collecting the data, an exploratory analysis was conducted. It was clear from the data that playing as white had a slight advantage by producing higher win rates on average. However, we noticed a large spread of win rates. In the upper quadrant of win rates, some eerily high win rates were had, and a new story emerged.

Several players had hundreds of games played, but their win rate was well over 50%. This is interesting because it means they win almost every time. The [chess.com algorithm](https://support.chess.com/article/369-how-does-matching-work-in-live-chess) always matches you with someone that has a similar ELO rating to make each match balanced. If someone plays someone else around their skill level, the chances of winning should be equal (I suspect the expected value of wins would be around 50%). If a player is consistently winning 70%, 80%, or even 90% of the time, it would not be out of the question that cheating is present. Cheating can take place if a player inputs each move into a separate game against a computer analysis system that calculates the best possible move for the player. To learn more about this and look deeper into possible cheating, I collected data on accuracy score, or how perfectly a player moves compared to what the computer suggests in each position.

Here is an intuitive look at the spread of accuracy based on color and title:

<img 
    src="https://github.com/grhatch/my386blog/blob/main/assets/images/accuracy.png?raw=true" alt="accuracy" style="display: block;
            margin-left: auto;
            margin-right: auto; width:400px;"
/>

As expected based on previous analysis of win rates, accuracy for white has a higher mean and/or median for each of the titles. Amazingly, (confirmed by looking at the raw data) not a single player has an accuracy of 100. The averages and upper quartiles match what one might expect for each of the titled players. This tells the story that no cheaters are present within the professional ranks (at least not cheaters using bots that tell them the best move). This means that those high win rates were achieved fairly and that those players are just purly talented! It also shows that increased win rates are correctly predicted by color. However, one more point must be considered.

Magnus Carlsen is considered by many to be the greatest chess player alive today (and possibly of all time). His win rate is [42.34%](https://www.365chess.com/players/Magnus_Carlsen). How can the greatest chess player with one of the highest average accuracy scores have a less than 50% win rate while countless other players are riding high in the 70's, 80's or even 90's?

The answer: unfair matchups.

Becase masters of chess are so highly rated and so few of them exist, there is often not a player playing at the same time with a close enough rating for the match to be considered fair. Although most likely not their fault, win rate at such a high level of play is not a good indicator of how good a player is. Magnus Carlsen has many official matches set up for him with other players of his caliber which makes his win rate so low comparitively.

# Conclusion

Players not only win more as white, but they also play more accurately after making the first move. At first, I suspected cheating to play a role, but it turns out that the data is pure! When playing against your friends, try to take white! It will put you on the top!

Regarding unfair matchups, chess.com may not be the best place to break into the master circuit. As you increase in skill, your opnonents will be left behind. To play the best of the best, look for tournaments and sign up to play the greats.

Check out my repository to view my code by clicking [here](https://github.com/grhatch/chess-grhatch)!
