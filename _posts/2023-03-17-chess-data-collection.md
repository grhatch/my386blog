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

# How to get the Data

## Endpoints

Here is a list of the endpoints that I used:

- https://api.chess.com/pub/titled/{title}
- https://api.chess.com/pub/player/{username}/games/archives
- https://api.chess.com/pub/player/{username}/games/{YYYY}/{MM}

For "title", I used "GM", "IM", "FM", and "CM".
Then for each user in each title, I got their games using their archives.

## Code

```python
#get a list of players from each title category
def TitledPlayers(title):
    url = f"https://api.chess.com/pub/titled/{title}"
    response = requests.request("GET", url)
    return response.json()
gm = TitledPlayers('GM') #Grand Master
im = TitledPlayers('IM') #International Master
fm = TitledPlayers('FM') #FIDE Master
cm = TitledPlayers('CM') #Candidate Master

#get a smaller set of data to decrease load time (but keep 200 rows)
gmSmall = random.sample(gm['players'], 50)
imSmall = random.sample(im['players'], 50)
fmSmall = random.sample(fm['players'], 50)
cmSmall = random.sample(cm['players'], 50)

#combine all names
titles = [gmSmall, imSmall, fmSmall, cmSmall]

data = []
userTitle = ''
for title in titles: #loops through each of the titles (gm, im, fm, cm)
    users = title
    # in the following code block, define which title each player has based on which part of the loop it is in
    if title == titles[0]:
        userTitle = 'gm'
    elif title == titles[1]:
        userTitle = 'im'
    elif title == titles[2]:
        userTitle = 'fm'
    elif title == titles[3]:
        userTitle = 'cm'
    for user in users: #loops through each user in the category
        #hitting chess.com API to get each month that a player has games
        url = f'https://api.chess.com/pub/player/{user}/games/archives'
        response = requests.request("GET", url)
        archives = response.json()

        #take just the first month returned so that there isn't an astronomical amount of data
        monthurls = archives['archives'][:1]

        gameslist = []
        for url in monthurls: #loop through each month
            response = requests.request("GET", url)
            gameslist.append(response.json()) #create a list of games for each player
        white = []
        black = []
        for gamelist in gameslist: #loop through each list of games
            games = gamelist['games']
            for game in games: #within each list of games, get each game
                #get wins as white and wins as black
                if game['white']['username'] == user:
                    if game['white']['result'] == 'win':
                        white.append(1)
                    else:
                        white.append(0)
                else:
                    if game['black']['result'] == 'win':
                        black.append(1)
                    else:
                        black.append(0)

        totalGames = white + black
        numGames = len(totalGames)
        winRate = np.mean(totalGames)
        numWhite = len(white)
        whiteRate = np.mean(white)
        numBlack = len(black)
        blackRate = np.mean(black)

        #create final data object from which we will create a data frame and do some analysis
        data.append([user, userTitle, numGames, winRate, numWhite, whiteRate, numBlack, blackRate])

```
