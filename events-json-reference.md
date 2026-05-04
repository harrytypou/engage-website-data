# `data/events.json` — Reference

An array of event objects. Events are automatically grouped by status on the Events page (upcoming/ongoing first, past below).

```json
[
  {
    "id": "1",
    "type": "workshop",
    "status": "upcoming",
    "date": "2026-06-10",
    "time": "18:00 – 20:00",
    "icon": "🛠",
    "image": "assets/events/my-photo.jpg",
    "url": "https://example.com/register",
    "en": {
      "title": "Intro to ROS2",
      "description": "A hands-on workshop covering the basics of ROS2 for beginners.",
      "location": "Lab B2, University of Western Macedonia"
    },
    "el": {
      "title": "Εισαγωγή στο ROS2",
      "description": "Πρακτικό workshop για τα βασικά του ROS2 για αρχάριους.",
      "location": "Εργαστήριο Β2, Παν. Δυτικής Μακεδονίας"
    }
  }
]
```

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | Unique identifier |
| `type` | string | ✅ | `"workshop"` · `"talk"` · `"meetup"` · `"hackathon"` · `"other"`. Controls the type label |
| `status` | string | ✅ | `"upcoming"` · `"ongoing"` · `"past"`. Controls grouping and badge colour |
| `date` | string | ✅ | ISO date `YYYY-MM-DD`. Formatted automatically per locale |
| `time` | string | — | Free-text time string (e.g. `"18:00 – 20:00"`) |
| `icon` | string | — | Emoji shown as placeholder when no image is provided. Defaults to `📅` |
| `image` | string | — | Path or URL to a cover image. Shown at top of card |
| `url` | string | — | External link. For upcoming events shown as "Register →", for past events as "Learn more →" |
| `en` | object | ✅ | English content block |
| `en.title` | string | ✅ | Event title |
| `en.description` | string | ✅ | Short description shown on the card (1–2 sentences) |
| `en.location` | string | — | Venue or "Online". Shown with a pin icon |
| `el` | object | — | Greek content block. Same structure as `en`. Falls back to English if omitted |
