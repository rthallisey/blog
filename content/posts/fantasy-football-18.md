---
title: "Fantasy Football 18"
date: 2019-08-18T11:57:40-04:00
draft: true
---

# Fantasy Football 2018 Season
Fantasy Football statistics is getting an upgrade in 2019 as I was finally
able to my [library](https://github.com/rthallisey/espn-go-api) functional for
anazlying the ESPN Fantasy leagues after ESPN started to overhaul their API at
the end of 2018.

## Summary of 2018
2018 was another great FF season as the League saw it's second two time winner,
David H, blow everyone away in the regular season with exceptional drafting.
Here are some records David set in 2018 in the modern era of scoring (2015-2018):
  * Most points 1547.2 - that's an average of 110.5 points per game.
  * 3rd regular season title, winning the title in 2011, 2015, and now 2018
  * Most wins in a season with 12.

## Total Bench Points
Total bench points seems like a pointful statistic because it can be interpreted
as "the amount of points I didn't take advantage of" or "I could've won that game
if I only had 10 more points week 3".  Hindsight is 20/20.

<iframe src="http://localhost:1313/html/total-bench-points.html" width="750" height="500" frameborder="0"></iframe>

The most interesting thing about total bench points is when it's graphed against
total wins.

<iframe src="http://localhost:1313/html/total-bench-points-vs-wins.html" width="750" height="500" frameborder="0"></iframe>

Interesting, winning teams usually score the most, but winning teams also prevent
other teams from scoring on them by keeping a strong bench.

## Can I Buy a Win?
Wins are hard to come by in a competitive FFL, so you always need
to try and find your edge.  Like most people, I like to look back at the
previous week and think about how I could've been better. Should I have
picked up a rookie running back or a veteran wide receiver?  How can I
be more efficient using waivers? With the 2018 seaosn in the past, I want to do
the same retrospective analysis over a full season to see if it can bring a
different perspective.  I want to find which owner worked to the hardest to get
a win and maybe I can learn something.

Working the hardest for a win means that the team had to rely on a large
number of players to get wins and was successful at it.  In otherwords, Todd
Gurley didn't win the owner every game -- the owner had to go out find waiver
picks, trades, and one week streamers to score points when it counted and won
a lot.

The stat I use to track individual players contributing to a win I called the
most valueable player (MVP). The most valuable player is a player that in a
given week scores more points than...
  - the difference of the winning team's score
  - the average player at the position

We'll first look at a team's average most valuable players, which is the average
number of MVPs a team had per win.  Think of this statistic as the number of
players it took on average for a team to get a win.

<iframe src="http://localhost:1313/html/avg-mvps.html" width="750" height="500" frameborder="0"></iframe>

Not bad!  Except, this doesn't perfectly satisfy the statistic of "who worked
the hardest for a win".  To prove this let's look at a corner case.  If a team
wins 1 game and every player on their team contributed to the win, then that
team would have an average of 12 MVPs per win.  12 MVPs for one win is impressive,
however I'm more interested in wins.

Let's include wins into the equation because the weight of each win makes
it harder to have more MVPs. Here's the resulting equation:

```
(mvpSum/record.Wins)*record.Wins
```

A little better, but record.Wins has a lot of weight and this doesn't take into
account the amount of unique players a team had to use to win.  For example, I
could get 8 wins with Todd Gurley, Tyreek Hill, and Pat Malholmes winning me
every game.  But that shouldn't count more than a team with 8 wins having to use
Randall Cobb, Josh Allen, Jordan Howard to win one week and Russel Wilson,
David Johnson, and Zay Jones the next.

Here's a look at MVP count.
<iframe src="http://localhost:1313/html/unique-mvps.html" width="750" height="500" frameborder="0"></iframe>

Now let's incororate MVP count into our equation:
```
(mvpSum/record.Wins)*record.Wins + count - record.Wins
```

This reduces down to:
```
mvpSum + count - record.Wins
```

OK this looks better, so let's test the corner cases...

One win with 9 MVPs:
9 + 9 - 1 = 17

Sixteen wins with 1 MVP:
16 + 1 - 16 = 1

Sixteen wins with unqiue players every week!:
144 + 144 - 16 = 272

And here's the final graph:

<iframe src="http://localhost:1313/html/normalized-mvps.html" width="750" height="500" frameborder="0"></iframe>

Not surprisingly the top 4 finishers had the four highest score.  What's
interesting is the teams that jumped rank.  Me (Ryan) finished 4th and had
the highest score.  John had the second highest score and finished 3rd.

Math's the math.  Don't hate the player hate the numbers.

## Team Most Valuable Player
It's always interesting to learn what player got you the most wins in a season
because it's usually not who you think...

<iframe src="http://localhost:1313/html/team-mvp.html" width="750" height="500" frameborder="0"></iframe>

Da Bears!

## On to Half Point PPR
As the sun sets on Standard Scoring in my league, let's look at how each team's
average score per position matched up agaist the overall average score per
position.  Keep in mind that average score is points-scored/games-played so
injuries don't deflate position averages.

<iframe src="http://localhost:1313/html/avg-pts-per-position.html" width="750" height="500" frameborder="0"></iframe>

## Now it starts all over again in 2019
Good luck on the 2019 season!

<iframe src="https://free.timeanddate.com/countdown/i6wawlfd/n859/cf100/cm0/cu4/ct0/cs0/ca0/co1/cr0/ss0/cac000/cpc000/pc777/tc66c/fn3/fs130/szw576/szh243/tatDays%20left%20until%20Football%20starts/tac000/tpc000/iso2019-09-05T20:20:00/bo2" allowTransparency="true" frameborder="0" width="750" height="300"></iframe>
