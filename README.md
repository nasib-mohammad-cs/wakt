# WAKT - Prayer Time App (Vanilla JS)

Minimal, dependency-free prayer time UI built with HTML, CSS, and JavaScript. Designed for easy embedding into web apps, kiosks, or dashboards.

---

## Features

* Fetches daily prayer times via REST API
* Uses **Calculation Method 8 (Bangladesh standard)**
* Displays:

  * Prayer start times
  * Prayer validity window (start → next prayer)
* 12-hour (AM/PM) format
* Single-screen, responsive UI
* No build tools, no dependencies

---

## API Integration

### Endpoint

```
GET https://api.aladhan.com/v1/timingsByCity
```

### Query Params

| Param   | Value      | Description                                        |
| ------- | ---------- | -------------------------------------------------- |
| city    | Dhaka      | Target city                                        |
| country | Bangladesh | Country name                                       |
| method  | 8          | Calculation method (Bangladesh Islamic Foundation) |

### Example Request

```
https://api.aladhan.com/v1/timingsByCity?city=Dhaka&country=Bangladesh&method=8
```

### Response Shape (trimmed)

```json
{
  "data": {
    "timings": {
      "Fajr": "04:45",
      "Sunrise": "06:00",
      "Dhuhr": "12:05",
      "Asr": "15:30",
      "Maghrib": "18:20",
      "Isha": "19:35"
    }
  }
}
```

---

## Time Window Logic

Prayer windows are derived client-side:

| Prayer  | Start   | End     |
| ------- | ------- | ------- |
| Fajr    | Fajr    | Sunrise |
| Dhuhr   | Dhuhr   | Asr     |
| Asr     | Asr     | Maghrib |
| Maghrib | Maghrib | Isha    |
| Isha    | Isha    | —       |

---

## Core Implementation

### Fetch + Render

```js
const apiUrl = \"https://api.aladhan.com/v1/timingsByCity?city=Dhaka&country=Bangladesh&method=8\";

const res = await fetch(apiUrl);
const data = await res.json();
const t = data.data.timings;
```

### 24h → 12h Conversion

```js
function to12Hour(time) {
  let [h, m] = time.split(\":\");
  h = parseInt(h);
  const ampm = h >= 12 ? \"PM\" : \"AM\";
  h = h % 12 || 12;
  return `${h}:${m} ${ampm}`;
}
```

---

## Usage

### 1. Drop-in

* Copy the HTML file
* Open in browser

### 2. Embed in Existing App

* Extract the `fetchPrayerTimes()` logic
* Mount into your UI layer (React/Vue/etc.)

### 3. Change Location

Replace query params:

```
city=YourCity&country=YourCountry
```

Or switch to lat/lng endpoint:

```
/timings?latitude=XX&longitude=YY&method=8
```

---

## Accuracy Notes

* Times are computed using astronomical calculations:

  * Solar angles (Fajr/Isha)
  * Solar noon (Dhuhr)
  * Shadow length (Asr)
* Method 8 aligns with Bangladesh standards
* Accuracy depends on:

  * Correct location input
  * Selected calculation method

---

## Limitations

* No jamaat timing (not provided by API)
* No timezone override handling
* Requires internet connection

---

## Extending

### Add Jamaat Times

Apply offsets:

```js
const offsets = {
  Fajr: 20,
  Dhuhr: 15,
  Asr: 15,
  Maghrib: 5,
  Isha: 20
};
```

### Add Auto Refresh

```js
setInterval(fetchPrayerTimes, 60 * 60 * 1000);
```

### Add Current Prayer Detection

Compare current time against prayer ranges.

---

## License

Free to use and modify.
