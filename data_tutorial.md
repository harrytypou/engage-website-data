# EVCLUB — Data File Reference

All content files live in your GitHub content repo under `data/`. The site fetches them via the raw GitHub URL. To update content, edit the JSON files and commit — no code deploy needed.

---

## `data/projects.json`

An array of project objects. All fields except `name` and `description` are optional.

```json
[
  {
    "name": "Autonomous rover prototype",
    "description": "GPS-guided outdoor rover with obstacle avoidance using LIDAR and ROS2.",
    "icon": "⚙",
    "tags": ["Robotics", "ROS2", "C++", "LIDAR"],
    "status": "active",
    "featured": true,
    "members": 5,
    "github": "https://github.com/your-org/rover"
  }
]
```

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✅ | Project display name |
| `description` | string | ✅ | Short one-line description shown on the card |
| `icon` | string | — | An emoji displayed as the project icon. Defaults to `⚙` |
| `tags` | string[] | — | Tech/topic tags shown as pills (e.g. `["Python", "ROS2"]`) |
| `status` | string | — | `"active"` · `"completed"` · `"paused"`. Defaults to `"active"` |
| `featured` | boolean | — | If `true`, the project appears on the homepage preview. At most 4 featured projects are shown |
| `members` | number | — | Number of members working on this project |
| `github` | string | — | Full URL to the GitHub repo. If omitted, the "View on GitHub" link is hidden |

---

## `data/competitions.json`

An array of competition objects. Grouped automatically on the Competitions page by `status`.

```json
[
  {
    "name": "IEEEXtreme 19.0",
    "date": "October 2025",
    "scope": "International",
    "status": "past",
    "result": "2nd place",
    "url": "https://ieeextreme.org"
  }
]
```

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✅ | Competition display name |
| `date` | string | — | Free-text date string (e.g. `"April 20, 2026"`, `"Ongoing"`) |
| `scope` | string | — | Geographic scope shown as a subtitle (e.g. `"International"`, `"National"`) |
| `status` | string | ✅ | `"upcoming"` · `"active"` · `"past"`. Controls grouping and badge colour |
| `result` | string | — | Result string shown in accent colour (e.g. `"1st place"`, `"Finalists"`). Leave empty or omit if not applicable |
| `url` | string | — | External link to the competition website. Shown as a `→` arrow link |

---

## `data/team.json`

An array of team member objects. Members are grouped by their `category` field on the Team page.

```json
[
  {
    "name": "Alexis Kostopoulos",
    "role": "President",
    "category": "Board",
    "photo": "https://your-cdn.com/alexis.jpg",
    "linkedin": "https://linkedin.com/in/alexis",
    "github": "https://github.com/alexis"
  }
]
```

| Field | Type | Required | Description |
|---|---|---|---|
| `name` | string | ✅ | Full name. Also used to generate initials for the avatar fallback |
| `role` | string | ✅ | Role or title shown under the name (e.g. `"President"`, `"Software Engineer"`) |
| `category` | string | — | Group heading on the Team page (e.g. `"Board"`, `"Members"`, `"Alumni"`). Members with the same category are grouped together. Defaults to `"Board"` if omitted |
| `photo` | string | — | URL to a profile photo (square recommended). If omitted, an avatar is generated from the member's initials |
| `linkedin` | string | — | Full LinkedIn profile URL. If omitted, the LinkedIn icon is hidden |
| `github` | string | — | Full GitHub profile URL. If omitted, the GitHub icon is hidden |

---

## News — GitHub Issues

News is not a JSON file. It is pulled live from **GitHub Issues** on your content repo.

### How to post news

1. Open a new Issue on the content repo.
2. Add one of these labels to control the news type badge:
   - `announcement` → shown as "Announcement"
   - `event` → shown as "Event"
   - `achievement` → shown as "Achievement"
   - (no label) → defaults to "Announcement"
3. The Issue **title** becomes the news card headline.
4. The Issue **body** (up to 160 characters) becomes the excerpt.
5. **Publish** = Issue is open. **Unpublish** = close the Issue.

### Tips

- The homepage preview shows the 3 most recent open issues.
- The News page shows all open issues (up to 50).
- The "Read more on GitHub →" link points to the Issue page — useful for longer announcements.
- You can add multiple labels; only the first recognised one is used for the badge type.

---

## Adding or removing fields

All fields not listed above are silently ignored by the renderer. You can add any extra fields (e.g. `"notes"`, `"year"`) for your own bookkeeping — they won't break anything.

If you want to add new fields that are actually *rendered*, you'll need to update the corresponding `*CardHTML` function in `js/content.js`.

---

## `data/news.json` *(replaces GitHub Issues)*

An array of news article objects. Supports bilingual content, an optional hero image, optional related links, and a full article body.

```json
[
  {
    "id": "1",
    "type": "achievement",
    "date": "2026-03-15",
    "image": "assets/news/my-photo.jpg",
    "links": [
      { "label": "Official results", "url": "https://example.com" }
    ],
    "en": {
      "title": "2nd place at IEEEXtreme",
      "excerpt": "Short summary shown on the card.",
      "body": "Full article text here.\n\nNew paragraph after a blank line.\n\n- Bullet item one\n- Bullet item two"
    },
    "el": {
      "title": "2η θέση στο IEEEXtreme",
      "excerpt": "Σύντομη περίληψη για την κάρτα.",
      "body": "Πλήρες κείμενο άρθρου εδώ."
    }
  }
]
```

| Field | Type | Required | Description |
|---|---|---|---|
| `id` | string | ✅ | Unique identifier for the article. Used internally to open the correct overlay |
| `type` | string | ✅ | `"announcement"` · `"event"` · `"achievement"`. Controls the badge label and colour |
| `date` | string | ✅ | ISO date string `YYYY-MM-DD`. Formatted automatically per locale |
| `image` | string | — | Path or URL to a hero image. If omitted, no image is shown. Relative paths (e.g. `assets/news/photo.jpg`) or full URLs both work |
| `links` | array | — | Array of `{ "label": "...", "url": "..." }` objects. Shown at the bottom of the full article as "Related links". Can be empty `[]` |
| `en` | object | ✅ | English content block |
| `en.title` | string | ✅ | Article title |
| `en.excerpt` | string | ✅ | Short summary shown on the news card (1–2 sentences) |
| `en.body` | string | ✅ | Full article text. Use `\n\n` (blank line) to separate paragraphs. Lines starting with `- ` become bullet list items |
| `el` | object | — | Greek content block. Same structure as `en`. If omitted, falls back to English |

### Body formatting

The `body` field is plain text with two conventions:
- **Paragraphs**: separate with a blank line (`\n\n`)
- **Bullet lists**: start lines with `- ` (hyphen-space). A block of `- ` lines becomes a `<ul>` list

Example:
```
"body": "First paragraph here.\n\nSecond paragraph here.\n\nWhat we offer:\n- Item one\n- Item two\n- Item three"
```
