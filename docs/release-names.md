# Release naming

For teams aiming to bring some extra order and flexibility to the release names that they prepare within git where normal
git-flow is not flexible enough for competing roadmaps and team size, this naming convention can be used.

* [The concept](#the-concept)
* [The structure](#the-structure)
* [Why introduce alphabetization?](#why-introduce-alphabetization)
  * [Scenario 1: Shifting priorities](#scenario-1-shifting-priorities)
  * [Scenario 2: Combined releases](#scenario-2-combined-releases)
* [Selecting thematic names](#selecting-thematic-names)
  * [Selecting names for a release](#selecting-names-for-a-release)
* [FAQ](#faq)
  * [Do the release names need to be in alphabetical order?](#do-the-release-names-need-to-be-in-alphabetical-order)
  * [Does each release need to start with a different letter?](#does-each-release-need-to-start-with-a-different-letter)
  * [Ohhhh...so we don't need to use a new letter for each month?](#ohhhhso-we-dont-need-to-use-a-new-letter-for-each-month)
  * [What do we do when a new year rolls around?](#what-do-we-do-when-a-new-year-rolls-around)
  * [My team started with a theme but we are bored of it and want to switch part way through the year. Is that okay?](#my-team-started-with-a-theme-but-we-are-bored-of-it-and-want-to-switch-part-way-through-the-year-is-that-okay)
  * [Won't this model break down a bit if a release is delayed too long?](#wont-this-model-break-down-a-bit-if-a-release-is-delayed-too-long)
  * [Wait. Which type of releases get release names?](#wait-which-type-of-releases-get-release-names) (spoiler: feature and maintenance releases, not hotfixes)
  * [How should this be organized?](#how-should-this-be-organized)
  * [My brand has multiple teams. Do we all use the same theme and list of names?](#my-brand-has-multiple-teams-do-we-all-use-the-same-theme-and-list-of-names)

## The concept

This approach stands on the shoulders of companies that have already solved this problem - like Google with Android - 
and use approachable words for release naming that will be alphabetical throughout the year.

### The structure

The anatomy of a release name is as follows:

```
release/TYY.A[.H]
```

* `T` represents the team or group name for the release. Some examples could be `L` for `LearnDash`, `B` for `Blue`, `M` for `Memberships`, etc. One letter is best for brevity, but multiple letters are viable.
* `YY` represents the current year for the release. For example, `21` for `2021`.
* `A` represents the alphabetical release name.
* `H` represents the hotfix number. Example: if `release/T23.llama` needs a hotfix, it would become `release/T23.llama.1`.

## Why introduce alphabetization?

Naming releases after the semantic version numbers can be problematic. Here are some example scenarios where
numeric release numbers break down:

### Scenario 1: Shifting priorities

> Let's say there are two teams: Team A and Team B that collaborate on a single product and repository.
> The last release was `release/4.2.1` and Team A is actively working on `release/4.3.0` - a feature release with a complicated
> feature. Something goes awry with the 4.3.0 development or QA process and Team A has to delay their release by a month.
> Team B is tapped to come in and do a quick feature release _before_ Team A's release.

In that scenario, how many possible feature version numbers are there between `4.2.0` and `4.3.0`? The answer is none. So,
that leaves the team in a bit of a predicament with their branch names. Team B's release needs to become the _new_ `4.3.0`
and Team A's release needs to become `4.4.0`.

This poses a problem with the branches themselves (all devs and any automated clones that are happening elsewhere) will
need to have the `release/4.3.0` branch deleted so that its git history is distinct from the old `4.3.0` release.

#### How alphabetization helps scenario 1

In this scenario, the previous release would have been named `release/X23.parsley` and Team A would be working on
`release/X23.potato`. When Team B needs to inject a release between parsley and potato, they can name their release
`release/X23.pea`. Team A doesn't need to change anything. The ticketing system doesn't need to change. Folks' understanding
of what the potato release is remains the same.

### Scenario 2: Combined releases

> Let's say Team A and Team B are both working on a release. Team A is working on Product 1 (version 5.1.0) and Team B is
> working on Product 2 (version 3.8.0) which involves necessary changes in Product 1 (planned version of 5.1.1).
> Team A's product was planned to be released on August 1st and Team B's product is planned for August 14th. Something
> goes awry with Team A's project and it gets delayed two weeks and now Team A and Team B will be releasing their
> products on the same day. To avoid doing two separate releases of Product 1, it is decided that Team B's work in Product 1
> will be merged into Team A's work.

In this scenario, the branch management is easy, but the narrative around what the teams call the release is complicated.
Do we say "release 5.1.0 of Product 1 and release 3.8.0 or Product 2"? That's a lot to say. What do we label the release
in our ticketing system?

This scenario is simplistic in that it involves a single product from each team. What if each team was planning their
release around multiple products at the same time? The descriptive name could get quite long.

#### How alphabetization helps scenario 2

In this scenario, Team A's release name would be `release/X23.potato` and Team B's release name would be `release/X23.radish`.
If they two releases need to be released on the same day, they could become `release/X23.potato-radish`.

## Selecting thematic names

There doesn't need to be a theme for the words that is chosen, but it could be fun for the team to rally around a particular
theme - like video game names, vegetables, things found in the kitchen, etc. The important thing is that a theme is chosen
that has enough options to last for a year!

### Selecting names for a release

When a release needs a name, it is important to select a word that has a number of options between it and the previous release,
so, if a release needs to be injected in between two releases (that isn't a hotfix), there is space to select a release
name that is alphabetically between the two releases.

A safe padding distance of ~5 between release names should accommodate most release shenanigans on large teams.

## FAQ

### Do the release names need to be in alphabetical order?

Yes! That's the point :) It allows you to look back at the year and know what order the releases were in.

### Does each release need to start with a different letter?

Nope! You could have all releases in the year start with the letter A if you wanted. Just as long as they are
alphabetical.

### Ohhhh...so we don't need to use a new letter for each month?

Exactly. That's not necessary. You can even skip letters, too!

### What do we do when a new year rolls around?

That's a great question! If you have a theme that is massive enough to continue going through multiple years, that's fine.
A new year is a great time to think of a new theme to keep stuff interesting, though! They key thing is, you need enough
potential names to get you through all of the potential releases throughout the year.

### My team started with a theme but we are bored of it and want to switch part way through the year. Is that okay?

Totally. The only requirement is that the release names continue to be alphabetical. For example, if your team was doing
releases using **Lord of the Rings** as the theme from January through March and the most recent release was `release/X23.gandalf`
and your team was switching to **Ninja Turtles**. Even though it'd be SUPER tempting to select `release/X23.april` as the
release name for April...you can't do that. You need a name that is alphabetically after `gandalf`. So `release/X23.leonardo` is
the better choice.

### Won't this model break down a bit if a release is delayed too long?

Sort of. There are sometimes releases that need to be pushed out much further than initially planned and you might run
out of words that are alphabetically between releases. In those cases, it is simple to just rename the delayed release to
new name that works for the future and ditch the user of its original name completely.

The same thing applies if a release needs to spill over to the new year. Example: if you have `release/X23.shredder` planned
for December and it gets moved to January, you'll need to rename it to `release/X24.SOMETHING` where _SOMETHING_ is a word
in your theme that is alphabetically early. (like a word that starts with A or something).

### Wait. Which type of releases get release names?

Feature releases and maintenance releases. Hotfix releases should have a `.[number]` appended to the previous named release,
incrementing that number for each hotfix. Example: `release/X23.potato` was released and a hotfix was needed. That hotfix
gets the release name `release/X23.potato.1`. If another hotfix is needed, it gets the release name `release/X23.potato.2`, etc.

Why? Because hotfixes are usually unplanned and need to be released as soon as possible. They occur so rapidly that it
is incredibly unlikely that anything will jump in front of them. Additionally, spotting problematic releases is much easier
when scanning release through the year if there are near-identical names for those hotfixes.

### How should this be organized?

It is _highly_ recommended that a brand have a master spreadsheet for its releases - regardless of whether or not releases
are named alphabetically. This allows for a single location to see what released when and with what version numbers.

### My brand has multiple teams. Do we all use the same theme and list of names?

You can, but it isn't advisable. The goal of release names is to reduce the pain of release name management and different
teams tend to have different priorities, roadmaps, and blockers. Coordinating release names between all of the potential
moving targets would be difficult. Possible? Yes. But difficult.

Instead, if each team has their own prefix and theme, they can manage their own release names without needing to coordinate.
When it comes down to it, it isn't about mapping a release name to a version number - it is about coodinating and orchestrating
releases within a team that is flexible enough to deal with the chaos of product development.

If the brand has a reasonable spreadsheet for tracking releases; the timing of those releases and what was included; and
the version numbers of the products involved, then the teams should have all the information they need to understand what
happened.
