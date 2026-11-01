# Yesplan Card for Home Assistant

A custom Lovelace card for displaying Yesplan events by room/location.

This repository packages the frontend card as a **standalone HACS Dashboard plugin**. It is separate from the Yesplan Home Assistant integration: keep the integration installed because the card reads the entities and event attributes it provides.

## Requirements

- Home Assistant
- HACS
- The [Yesplan Home Assistant integration](https://github.com/denieuwevorst/Yesplan-Hacs) installed and configured

## Installation with HACS

1. Publish this repository to your own GitHub account (or use the repository URL supplied by its maintainer).
2. In Home Assistant, open **HACS**.
3. Open the three-dot menu and choose **Custom repositories**.
4. Add the GitHub repository URL and select **Dashboard** as the category.
5. Add the repository, find **Yesplan Card** in HACS, and install it.
6. Refresh the browser / clear the frontend cache if the card does not appear immediately.

HACS installs the JavaScript frontend resource. You should not need to copy the file into `custom_components` or manually expose that directory.

## Add the card to a dashboard

Add a **Manual** card and use:

```yaml
type: custom:yesplan-card
title: Yesplan vandaag
range: today
```

## Configuration

| Option | Default | Description |
|---|---:|---|
| `title` | — | Card title |
| `range` | `today` | `today`, `tomorrow`, `week`, or `next7` |
| `sort` | `time` | `time` (start time) or `zalen` (room order) |
| `hide_empty` | `true` | Hide rooms without events |
| `show_profile` | `true` | Show the event profile |
| `show_schedule` | `true` | Show the schedule for today's events |
| `show_tickets` | `true` | Show ticket sales/capacity |
| `show_fields` | `true` | Show custom event fields |
| `only_ticketed` | `false` | Only show events with ticket capacity |
| `zalen` | — | Optional ordered list of room/device names |
| `fields` | — | Optional list of custom-field keywords to show |

Example:

```yaml
type: custom:yesplan-card
title: Komende voorstellingen
range: next7
sort: time
hide_empty: true
show_profile: true
show_tickets: true
only_ticketed: false
```

## Troubleshooting

- **"Custom element doesn't exist: yesplan-card"**: check that the repository was added in HACS with category **Dashboard**, that the card is installed, and that the browser has been refreshed.
- **No locations found**: check that the Yesplan integration is configured and has created its room/location devices.
- **Sensor for this period is missing**: update the Yesplan integration and restart Home Assistant. The card expects the event sensors supplied by that integration.

## Development / releases

The frontend file is `yesplan-card.js` in the repository root. For a HACS release, create a Git tag and matching GitHub release (for example `v1.0.0`) after publishing the repository.
