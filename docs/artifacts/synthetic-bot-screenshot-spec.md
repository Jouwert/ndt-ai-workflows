# Synthetic bot screenshot spec

## Purpose
This artifact shows the interaction shape of the NDT assistant without exposing real operational content.

It is a synthetic public-facing visual derived from the real workflow pattern:
- a user asks a practical scheduling question
- the bot acknowledges the request
- the bot returns a structured operational answer

## Why this artifact exists
This repository already explains the workflow in text.

This image adds one thing that the text does not show as quickly:
- the chat-based interaction surface of the assistant

The image should support the repository, not dominate it.

## Format
- smartphone chat screenshot style
- Telegram-like interface
- portrait orientation
- readable at GitHub README or docs size
- clean enough to work as a repo illustration

## Keep
- the general Telegram-like visual structure
- a two-party chat with a bot and a user
- a believable operational question-and-answer flow
- Dutch interface text, because that matches the real working context
- a practical, non-marketing tone

## Remove or generalise
- real dates
- real room names
- real activity names
- real customer names
- real contact names
- real booking details
- anything that looks like raw internal operational data
- any wording that implies this is a literal production screenshot

## Content shape
The image should show:
1. a short user question about an activity or planning item
2. a short acknowledgement from the bot
3. a structured bot answer with generic but plausible fields
4. a short follow-up question about contact or context
5. a bounded reply that stays practical

## Suggested visible labels
- group name: `NDT Assistant Demo`
- bot label: `NDT Assistant`
- two participants is fine

## Example synthetic message flow
User:
- `Welke activiteit staat gepland voor dinsdagochtend?`

Bot:
- `Ontvangen — ik ga dit na.`

Bot:
- `Ik zie één activiteit in de ochtend.`
- `Tijd: 10:00–12:00`
- `Type: workshopruimte`
- `Status: concept`
- `Locatie: gedeelde ruimte`
- `Notitie: voorbereiding nodig, begeleider gewenst`

User:
- `Is er al een contactpersoon gekoppeld?`

Bot:
- `Er is nog geen contactpersoon ingevuld in deze boeking.`

## Visual style requirements
- realistic smartphone screenshot look
- soft green Telegram-like background
- white bot bubbles and green user bubbles
- simple round bot avatar with initials
- clear timestamps, but generic and not narratively important
- no watermarks
- no extra branding outside the demo context

## Generation strategy
Use the real screenshot only as a visual layout reference.

Replace the actual conversation with synthetic Dutch content.
Do not preserve literal operational details from the source image.

## Generation brief for GPT image model
Create a realistic smartphone screenshot of a Telegram-like chat conversation in Dutch.

The chat is a demo assistant conversation, not a real leaked screenshot.
Use a clean green Telegram-style background with subtle doodles.
Show a group chat titled "NDT Assistant Demo" with 2 members.
Use a simple circular bot avatar with the initials "NA".

The visible conversation should be:
- User: "Welke activiteit staat gepland voor dinsdagochtend?"
- Bot: "Ontvangen — ik ga dit na."
- Bot: "Ik zie één activiteit in de ochtend.\nTijd: 10:00–12:00\nType: workshopruimte\nStatus: concept\nLocatie: gedeelde ruimte\nNotitie: voorbereiding nodig, begeleider gewenst"
- User: "Is er al een contactpersoon gekoppeld?"
- Bot: "Er is nog geen contactpersoon ingevuld in deze boeking."

Make it look like a believable real chat screenshot on a phone, with green user bubbles and white bot bubbles.
Keep the typography readable and natural.
Do not include any real names, exact real locations, client details, or sensitive operational data.
Do not make it flashy or promotional.

## Acceptance criteria
The image is good enough for the repo if:
- it looks like a believable chat interface
- the text is readable
- the content is clearly synthetic and generic
- no sensitive details from the real screenshot remain
- it supports the repo as documentary evidence rather than marketing art
