# Wheel of Privilege

An interactive, anonymous self-positioning tool based on the Intersectionality Wheel of Privilege, adapted from James R. Vanderwoerd (Web of Oppression) and Sylvia Duckworth (Wheel of Power/Privilege).

Designed for facilitated workshops. Participants fill their profile on their own device; the facilitator sees all profiles update in real time on a dashboard screen.

---

## How it works

Two pages, one Firebase database:

- **`index.html`** — participant view. Each person opens this on their device, selects their position across 12 dimensions, and their responses sync live to Firebase.
- **`dashboard.html`** — facilitator view. Shows all participant profiles in real time as they fill in their answers. Three visualization modes: Grid, Overlay, and Aggregate.

No names or identifying information are collected. Each session is assigned a random anonymous ID stored only in the browser.

---

## The 12 dimensions

| Dimension | Privileged (center) | Middle | Marginalized (outer) |
|---|---|---|---|
| Gender | Cisgender man | Cisgender woman | Trans / nonbinary |
| Citizenship | Citizen | Documented | Undocumented |
| Skin colour | White | Lighter shades | Dark |
| Formal education | Higher education | Post-16 education | Left before 16 |
| Ability | Able-bodied | Some disability | Significant disability |
| Sexuality | Heterosexual | Gay man | Lesbian / bi / pan / asex |
| Neurodiversity | Neurotypical | Neuroatypical | Significant neurodivergence |
| Mental health | Robust | Mostly stable | Vulnerable |
| Body size | Slim | Average | Large |
| Housing | Property owner | Sheltered / renting | Homeless |
| Wealth | Comfortable | Struggling | Poverty |
| Language | Majority language | Learned language | Monolingual minority |

---

## Dashboard views

**Grid** — one radar card per participant, appears as people connect. Good for seeing individual profiles at a glance.

**Overlay** — all profiles superimposed on a single radar chart. Good for identifying patterns and starting group conversation.

**Aggregate** — horizontal bar chart per dimension showing the distribution of responses across the group. Good for discussing structural patterns without focusing on individuals.

---

## Setup

### 1. Fork or clone this repo

```bash
git clone https://github.com/seleneyang/wheel-of-privilege.git
```

### 2. Create a Firebase project

1. Go to [console.firebase.google.com](https://console.firebase.google.com)
2. Create a new project
3. Go to **Realtime Database** → Create database → choose a region → start in **test mode**
4. Go to **Project Settings** → Your apps → register a Web app → copy the `firebaseConfig` object

### 3. Add your Firebase config

In both `index.html` and `dashboard.html`, replace the `firebaseConfig` object with your own:

```javascript
const firebaseConfig = {
  apiKey: "YOUR_API_KEY",
  authDomain: "YOUR_PROJECT.firebaseapp.com",
  databaseURL: "https://YOUR_PROJECT-default-rtdb.firebaseio.com",
  projectId: "YOUR_PROJECT",
  storageBucket: "YOUR_PROJECT.firebasestorage.app",
  messagingSenderId: "YOUR_SENDER_ID",
  appId: "YOUR_APP_ID"
};
```

### 4. Enable GitHub Pages

1. Go to your repo → **Settings** → **Pages**
2. Source: **Deploy from a branch** → `main` → `/ (root)`
3. Save and wait 1-2 minutes

Your URLs will be:
- Participants: `https://YOUR_USERNAME.github.io/wheel-of-privilege/`
- Dashboard: `https://YOUR_USERNAME.github.io/wheel-of-privilege/dashboard.html`

---

## Running a workshop

1. Open `dashboard.html` on the screen you will project
2. Share the `index.html` URL with participants (QR code works well)
3. As people fill in their profiles, their radars appear on your dashboard in real time
4. Use the **Grid** view while people are filling in → switch to **Overlay** or **Aggregate** to open discussion
5. Click **Clear all** at the end of the session to remove all data from Firebase

---

## Security note

Firebase credentials are visible in the HTML source. This is acceptable for workshop use with test mode enabled (30-day open read/write window). After your event, go to **Firebase Console → Realtime Database → Rules** and lock down access:

```json
{
  "rules": {
    ".read": false,
    ".write": false
  }
}
```

Or delete the database entirely from the Firebase console.

---

## Credits

Adapted from the Wheel of Power/Privilege concept by Sylvia Duckworth and the Web of Oppression by James R. Vanderwoerd. Built with [Chart.js](https://www.chartjs.org) and [Firebase Realtime Database](https://firebase.google.com/products/realtime-database).
