# About this document

This is draft specification for tempai.kiev.ua website.

Find the latest version and revision history at https://github.com/tempai-dev


# Scope and purpose

As the Kiev riichi mahjong club "Tempai" grows, organization of games and other club communication becomes progressively more tedious. There is an increasing need for efficient game planning tools. Club also needs a presentational webpage as its Internet “face”, a social media integration point, and a technical platform for other web services and applications.

The goal of this document is to serve as the central design authority at the time of implementation.

### A note on portability

An important consideration is that it should be possible to deploy all the services for any other club in Ukraine or abroad if they wish to (Dnipropetrovsk, Zaporizhia, Simferopol, Lviv, Minsk riichi clubs).


--------
# Design

## Landing page

Key features:

 * mobile-first (responsive layout)

 * modern (simple, plain & sequential, vertical-scrolling)

Landing page visitors are anticipated to roughly divide into these categories:

 * curios/wandering people with some knowledge about the game or the club, **seeking more information** about the game and the club — most visitors;

 * riichi players **looking specifically for a mahjong club** in Kiev — few, but important ones.

Regular club players are not expected to visit the landing page often, at least not for full reading. Landing page must have convenient navigation controls to address regular players’ needs. These include:

 * link to game planner
 * organizer contacts
 * ??? :memo:

## Member profiles

Full name, avatar, optional status/description, social profiles and contacts like phone number/email/skype/telegram/etc.

EMA ID.

### Notifications

[Game even scheduler](#game-planner) will require reminders and notifications.

Core support for RSS and iCal is mandatory.

More notification venues may be added gradually or integrated via IFTTT: [@kievtempai](https://twitter.com/kievtempai) feed, group updates in social networks, emails, messengers, perhaps even SMS.

### Statistics

It'd be good to allow opt-in stats collection for later analysis. These may include:

 * total game events visited
 * positions won (if the table wants to record this)
 * final hanchan scores
 * yakuman journal

## Game Planner

Mahjong games require 4 players per table. To ease and automate organization of games, all game arrangement scenarios must be able to happen solely via unidirectional "player-website" interaction; it should not require regular involvement of club organizers/mentors.

However, a big deal of flexibility is possible with 3 player tables (sanma, a.k.a. "hiroshima"), 5 player tables, up to 6 player tables (4+2 spectators) and 2 player bamboo/minefield sessions.

### Scenarios

 1. Club member wishes to play at any future date. He/she inspects the schedule and decides further.

 2. Club member wishes to play at a specific game already scheduled for a future date.

 3. Club member wants to schedule his own event.

 4. A guest visitor wishes to inspect the schedule.

### Privacy

A planned game session may be created publicly, or in private with a specified group of members (set either manually by the user, or through a user-group/friend-circle/forum-topic mechanism).

# Seating generator

Primarily for tournament games.

TL;DR: a reasonably fast shuffler of `[1..n]` which tries to minimize [*total overlap*](#total-table-overlap).

### Inputs

 * [mandatory] player count,

 * [mandatory] hanchan budget,

 * [optional] a whole table of player information records: {name, country/city, tournament ID number}, for better presentation,

 * [optional] number of available replacement players.

### Outputs

The primary output comprises of seatings per each hanchan, where seating is a mapping of players to pair: (gametable ID, Maybe starting wind).

The crucial feature is that the mappings must be minimized with respect to [total overlap](#total-table-overlap) between players.

There should be a warning if registered players would not be able to play because of lack of replacement players and uneven seating.

### Total table overlap
The total overlap of a seating is defined as the sum of table overlaps.

Table overlap is defined as the amount of *"already played with in the session"* players, summed relative to each player.


----------------
# Implementation

### Infrastructure

The primary domain for the club is **tempai.kiev.ua**.

Staging domain: :memo: **TODO**

GitHub org: https://github.com/tempai-dev

CI: CircleCI, TravisCI or alike

Language of development: preferably **Ruby**, but isolated components can be developed in any language of choice as soon as the functionality is exposed via HTTP APIs

Documentary collaboration <strike>at https://docs.tempai.kiev.ua (Google Apps instance)</strike> at GitHub.

Mail for notifications info@tempai.kiev.ua (Google Apps)

