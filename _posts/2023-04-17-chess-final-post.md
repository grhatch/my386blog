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

This analysis is based on chess data that was collected through the [chess.com](https://www.chess.com) [API](https://www.chess.com/news/view/published-data-api). The data contains usernames, titles, number of games, and win rates for white and black. For more information, reference [this earlier blog post](https://grhatch.github.io/my386blog/2023/03/17/chess-data-collection.html).

The question we wanted to answer was whether color (or anything else) has an affect on win rate, but during the analysis some new interesting points popped up.

As you can see, most of the data is clustered around .5, or 50%, win rate. However, I find it interesting that there are is a curiously large amount of dots between .7 and .9 win rates. This means that these players consistenly win almost every time. What concerns me is that this is the case even for players who have played over 200 games. The [chess.com algorithm](https://support.chess.com/article/369-how-does-matching-work-in-live-chess) always matches you with someone that has a similar ELO rating to make each match balanced. If someone plays someone else around their skill level, the chances of winning should be equal (I suspect the expected value of wins would be around 50%). If a player is consistently winning 70%, 80%, or even 90% of the time, it would not be out of the question that cheating is present. Cheating can take place if a player inputs each move into a separate game against a computer analysis system that calculates the best possible move for the player. To learn more about this and look deeper into possible cheating, I want to gather the accuracy score, or how perfectly the player moved his or her pieces compared to what the computer suggests in each position.

# Conclusion

Check out my repository to view my code by clicking [here](https://github.com/grhatch/chess-grhatch)!
