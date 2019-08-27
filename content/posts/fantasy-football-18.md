---
title: "Fantasy Football 18"
date: 2019-08-18T11:57:40-04:00
draft: false
tags: ["markdown", "GitHub", "website"]
---

# Fantasy Football 2018 Season
Fantasy Football statistics is getting an upgrade in 2019! I was finally
able to get my [library](https://github.com/rthallisey/espn-go-api) functional for
analyzing the ESPN Fantasy leagues after ESPN started to overhaul their API at
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

<iframe src="/html/total-bench-points.html" width="750" height="500" frameborder="0"></iframe>

Maybe it will be more interesting if we graph bench points against wins.

<iframe src="/html/total-bench-points-vs-wins.html" width="750" height="500" frameborder="0"></iframe>

Two playoff teams finished in the top 5 for total bench points. Winning teams
usually score the most, but winning teams also prevent other teams from scoring
on them by keeping a strong bench.

## Can I Buy a Win?
Wins are hard to come by in a competitive FFL, so you always need
to try and find your edge.  Like most people, I like to look back at the
previous week and think about how I could've been better. Should I have
picked up a rookie running back or a veteran wide receiver?  How can I
be more efficient using waivers? How can I better fill a gap this injury left
behind?

The best place to start looking for improvements is to understand which team
had to work harder for their wins. Working harder implies that regardless of how
you draft, you manage your team well.  Good team management leads to more wins
and more championships.  So let's see which team worked the hardest to get a win.

Working the hardest for a win means that the team had to rely on a large
number of players to get wins and was successful at it.  In other words, Todd
Gurley didn't win the owner every game -- the owner had to go out find waiver
picks, trades, and one week streamers to score points when it counted.

The stat I used to track individual players contributing to a win is called the
most valuable player (MVP). The most valuable player is a player that in a
given week scores more points than...
  - the difference of the winning team's score
  - the average player at the position

To get to which team worked the hardest, we'll first look at a team's average
most valuable players, which is the average number of MVPs a team had per win.
Think of this statistic as the number of players it took on average for a team
to get a win.

<iframe src="/html/avg-mvps.html" width="750" height="500" frameborder="0"></iframe>

Not bad! Except, this doesn't perfectly satisfy the statistic of "who worked
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

Here's a look at the number of unique MVPs per team:
<iframe src="/html/unique-mvps.html" width="750" height="500" frameborder="0"></iframe>

Now let's incorporate the MVP count into our equation:
```
(mvpSum/record.Wins)*record.Wins + MVPcount - record.Wins
```

This reduces down to:
```
mvpSum + MVPcount - record.Wins
```

OK this looks better, so let's test the corner cases...

One win with 9 MVPs:
```
9 + 9 - 1 = 17
```

Sixteen wins with 1 MVP:
```
16 + 1 - 16 = 1
```

Sixteen wins with unique players every week! (This the highest score a team can
get):
```
144 + 144 - 16 = 272
```

On a scale of 1 to 272, here's how hard it was for each team to win games:

<iframe src="/html/normalized-mvps.html" width="750" height="500" frameborder="0"></iframe>

Not surprisingly the top 4 finishers had the four highest scores.  But, what's
really interesting are the teams that had uncharacteristic scores relative to
their win totals.  Dan M (7 wins), posts a score of 4 with one less win than
Ryan (8 wins) who has a score of 36. Scrolling up to the Unique MVPs shows
Dan M with 5 and Ryan with 12.  Dan M there's some room for growth.  If you
had hit more winners in the waiver wire you probably would've 8 or 9 wins and
made the playoffs.

## Team Most Valuable Player
It's always interesting to learn what player got you the most wins and points in
a season because it's usually not who you think...

<iframe src="/html/team-mvp-points.html" width="750" height="500" frameborder="0"></iframe>

<iframe src="/html/mvps-by-wins.html" width="750" height="500" frameborder="0"></iframe>

Here are some observations:
* The top two finishers had QBs win them 6 games
* The most common position from the top MVPs were Running Backs with 9/24
* 1/24 of the top MVPs was a Kicker, Ka'imi Farbarirn
* Defense may not win you championships, but it can win you 4 games. Thanks Bears D/ST.

## On to Half Point PPR
As the sun sets on Standard Scoring in the league, let's look at each team's
average score per position.  Keep in mind that average score is
`points-scored/games-played`, so injuries don't deflate position averages.

<iframe src="/html/team-pts-per-position.html" width="750" height="500" frameborder="0"></iframe>

The 'Average' line shows the position average, so it's not surprising teams
are well over the RB and WR avg because in our league you can play 2 or 3.
* WR average points: 7.8565824848762364
* RB average points: 8.07453195497313
* QB average points: 17.73205642228142
* TE average points: 5.978830544455545
* K average points: 7.86362543012543
* DEF average points: 5.997916666666667

What's funny is Chris B is playing 2 or 3 WRs per week and actually had less
then the single WR average, 7.85, with 7.36 points per week.  Maybe you should
get to waiver wire Chris...

## Now it starts all over again in 2019
Good luck on the 2019 season!

<iframe src="https://free.timeanddate.com/countdown/i6wawlfd/n859/cf100/cm0/cu4/ct0/cs0/ca0/co1/cr0/ss0/cac000/cpc000/pc777/tc66c/fn3/fs130/szw576/szh243/tatDays%20left%20until%20Football%20starts/tac000/tpc000/iso2019-09-05T20:20:00/bo2" allowTransparency="true" frameborder="0" width="750" height="300"></iframe>
