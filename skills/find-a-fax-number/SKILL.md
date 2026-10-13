---
name: find-a-fax-number
description: Look up the verified fax number for a US government office, such as a Social Security field office, a state Medicaid or unemployment agency, MassHealth, California EDD, the IRS for Form 2553 or FEMA, with the official source and the date it was last verified. Use when the user needs a fax number for an agency and does not have it.
---

# Find a fax number

Use the `lookup_fax_number` tool from the ProntoFax server. It returns a fax number only when ProntoFax has verified it against the agency's own published source, and returns nothing rather than a guess when it has no verified number. This skill covers lookups only. To send the fax afterward, use the `send-a-fax` skill.

## Rules

- A fax number comes only from `lookup_fax_number` or from the user, including a letter or form the user shares. Never give a number from memory, from your training data or from a web search, even when you think you know it. A wrong number sends someone's private documents to a stranger.
- Show each result as the tool returned it: the office name, the number, the official source and the date it was last verified. Do not shorten or reformat away the source and the date. They are how the user checks the number.
- When the result lists what goes to that number, such as appeals or supporting documents, show that too. An agency often has different numbers for different things, and the user should check their document belongs at this one.
- Ask the user to confirm it is the right office before anyone sends anything.

## Calling the tool

Pass the agency in the user's own words, for example "MassHealth", "Texas Workforce Commission" or "social security office in Denver". Add these when you have them:

- `state`: a two letter state code, for example `TX`. Put a state code here and not in the agency text.
- `city`: a city or town, used to pick a Social Security field office.
- `language`: `es` when the user is writing in Spanish.

The tool's own description lists the agencies it covers. It has no numbers for anything outside that list.

## Social Security and Medicaid

Social Security and Medicaid have no national fax number. Each Social Security field office has its own, and Medicaid is run by each state. So a lookup for either needs a city or a state. If the user has not given one, ask for it before calling the tool, or call it and pass on its request for a location.

Social Security offices are named after the town they sit in, not every town they serve. If the user's town has no office, the tool lists the offices in that state. Ask which one is theirs. The office named on the user's own letter from Social Security is the best guide.

## When the lookup finds nothing

Tell the user ProntoFax has no verified number for that agency. Ask them to check the letter or form they are responding to, or the agency's own website, and to give you the number from there. Do not search for one yourself.

If the tool says it cannot verify numbers right now, say so and suggest trying again in a few minutes or using the number on their letter.

## Browsing

To browse every office ProntoFax has a verified number for, point the user to the directory at https://www.prontofax.com/directory/
