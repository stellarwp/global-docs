# Sensitive Information Best Practices

It's important to take extra care when dealing with sensitive information in engineering. This includes Personally Identifiable Information (PII),
security-related information, etc. This document walks through best practices expected of each team when dealing with sensitive information. It's
written in the form of commandments both to make this more fun to read, and also to make it clear that these are expectations.

## The 5 Commandments

### 1. Thou shalt include sensitive data indepdendently and intentionally, NOT as a side-effect

When doing things likes embedding sensitive information — for example to use subsequently in JS — it is critical that the manner in which the data
is handled is clear and indepdendent. DO NOT use functions such as `wp_localize_script()` which introduces it as a side-effect.

"Side-effect" here means that the data is introduced as a result of another action taking place. For example, `wp_localize_script()` embeds the data
on the page when a script is enqueued to the page. That sounds fine, but what if someone decides to enqueue that script in another, less secure
location? They may not realize this data is automatically introduced, resulting in unintended senstive data being in the wrong place.

Instead, use a Controller or something that handles the retrieving of the data, the conditions of when and where to embed the data, and which data
should be included. Keep it in one, clear location to make it self-evident for review.

### 2. Thou shalt have limits on queries containing sensitive data

Having a LIMIT on queries should really be an always thing, but when handling sensitive data it's especially important. At the very least, we always
want to reduce the amount of data being leaked. Simply making sure that queries have _sensible_ limits helps contain this.

### 3. Thou shalt increase sensitive data used iteratively, but AVOID decreasing it

Often times we like to work iteratively on things, at times over a few PRs. That's great! But a common mistake is to do something like grab _all_ user
data — e.g. `SELECT * FROM ...` — for quick building, with the intention to reduce the data needed later. Do not do that!

Instead, grab only the minimum amount of data needed to do the iterative piece of work. Subsequently, grab more data as necessary over time. Avoid the
situation where work gets released that was meant to be reduced and forgotten or missed. That's bad news bears.

### 4. Thou shalt use mock data until safe data is ready for use

Let's say you are making a dropdown menu with a first name, last name, and email. It's a great idea to use mock data — Darth Vader, vader@deathstar.com
— while building things out. Later, once a repository, endpoint, or whatever has been introduced that provides a safe way of gathering the data, then
plug it in!

### 5. Thou shalt mark work as containing or affecting sensitive information

Whether it's a ticket in Jira or a PR in Github, it's important to mark work that includes or affects sensitive information. This informs others, such as
the reviewer or the QA analyst to take further steps in inspecting and testing the work.
