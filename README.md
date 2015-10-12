# git-fantasy
Ever wanted to play Fantasy Football with your development team?

# Business Logic

## Classes

### League

A `League` is associated with a GitHub organization in a one-to-one relationship. Only one league can exist for an organization. A league is the top of the parent-child hierarchy. It contains a collection of `Seasons` and a pool of `Players`. Leagues will only allow `Players` that are authorized to access a GitHub organization.

### Season

A `Season` is a duration of time that points are accumulated consisting of weekly matchups. Most seasons will last between 8-12 weeks. A season has an individual pool of `Players` as well as a group of consistent `Managers`. Each `Season` is independent from other `Seasons` i.e. the results & `Players` exist in a vacuum within each individual `Season`. At the end of a `Season's` duration, a "winner" will be declared based on the best record of `Matchups` (decided by _least number of losses -> total points for ->total points against -> alphabetical_). The __league manager__ will need to manually create a new `Season` as desired, as they will not be created automatically at the end of the season to allow teams to operate in the best way that matches their development cycle. A `League` is only allowed to have one current `Season` at a time (_current_ meaning that the current datetime is inbetween a `Season's` begin time and end time).

### Matchup

A `Matchup` is a head-to-head period of point accumulation between two `Players` within a `Season`. Every week for the duration of a `Season`, a `Manager` will be placed in a competition against another `Manager`. Each `Manager` will attempt to accumulate the highest total number of points possible from their drafted `Players`. At the end of the week, the `Manager` with the highest point total will win the `Matchup`.

At the beginning of each `Matchup`, a `Manager` will need to select double the amount of available `Player` slots (typically 3-5 slots, requiring 6-8 `Players` chosen) in order of preference. Each `Manager` will have a list of preferred `Players` ranked by preference, and at draft time the `Manager` to pick first will be randomly decided. Each `Manager` will have an automated alternating turns to pick their highest preferred `Player` to be on their team each week. This implies that every `Player` in the `Players` pools for the current `Season` is available to be part of a `Managers` weekly team except for the `Managers` themselves (i.e., for a 10 `Manager` `Season`, each `Matchup` will have 8 available `Players` as the `Managers` participating in the `Matchup` will not be allowed to choose themself or the opponent as a `Player`). Each week in a `Season` will include `Matchups` for every `Manager` unless the number of `Managers` is odd, in which one `Manager` will receive a bye for the week.


## Positions

### Manager

A `Manager` is a `Player` that wishes to manage a team. He/she will own a team for the `Duration` of a `Season` and will compete for the best record in a collection of `Matchups` during the course of a `Season`. A `Manager` will select `Players` on a weekly basis to comprise his/her team. A `Manager` is also a `Player` but will not be allowed to place themselves in his/her `Matchup` roster. A `Manager` must commit to be a `Manager` before a `Season` begins as they are active participants during the course of the `Season`. A `Manager's` position is not carried over `Season` to `Season`, but must be re-upped each `Season`.

### League Managers

A `League Manager` operates as an administrator for the `League`. Their duty is to create new `Seasons` at the end of another `Season` and to invite `Players` to the `League`. They can also remove `Players` from the `League` and delete the `League` as a whole.

### Player

A `Player` is a human with a GitHub account that has access to the organization that is associated with a `League`. A `Player` exists in the `Player` pool for each `Matchup` in any season. A `Player` is a passive role and requires no participation beyond signing up for Git Fantasy. A `Player` can become a `Manager` as well by creating a team for a `Specific` season. A `Player` accumulates points throughout the `Season` according to the __Scoring__ rules listed below.

## Scoring

| Actions | Number |
| :------------- | :------------- |
| Commit  | 10  |
| Pull Request | 12  |
| Merged Pull Request  | 25  |
| Denied Pull Request  | -10  |

| Additions | Multiplier per Commit |
| :--- | :--- |
| 0-200  | 1.0x  |
| 201-400  | 1.3x  |
| 401-600  | 1.6x  |
| 601-800  | 1.9x  |
| 801-1200  | 2.3x  |
| 1201+  | 2.5x  |

| Deletions | Multiplier per Commit |
| :------------- | :------------- |
| 0-400  | 1.0x  |
| 401-800  | 1.3x  |
| 801-1200  | 1.6x  |
| 1201-1600  | 1.9x  |
| 1601-2000  | 2.3x  |
| 2001+  | 2.5x  |

## Actions

### Removing Players

In some cases, a `Player` might need to leave a `League`. A `Player` cannot be deleted from a `Season`, but after being removed, a `Player` will earn 0 points each `Matchup` and will not be able to accumulate any points for the remainder of the `Season`. The `Player`, once removed, will not be able to sign into Git Fantasy for the organization they were removed from, be available to become a `Manager` for future seasons, or be selected as a `Player` for any `Matchup` in future `Seasons`.

### Draft during weekly Matchup

Each week, every `Manager` will be involved in a `Matchup`. For a 24-hour duration a `Manager` has the option to choose and order a list of `Players` double the roster size from the available `Player` pool for a `League`. If a `Manager` does not choose a complete lineup of ordered `Players` before the draft period ends for each matchup, a roster of `Players` will be randomly assigned to the `Manager`. A `Manager` will need to choose an amount of `Players` double the amount of available slots for each `Matchup`.

