# Prayer Time App

## Overview

This is a simple, modern web-based tool that displays daily Islamic prayer times in a clean and minimal interface. It shows each prayer’s start time and its valid time window in an easy-to-read 12-hour format.

---

## What It Does

* Fetches daily prayer times based on location (currently set to Dhaka, Bangladesh)
* Displays the five daily prayers:

  * Fajr
  * Dhuhr
  * Asr
  * Maghrib
  * Isha
* Shows:

  * Start time of each prayer
  * End time (when the next prayer begins)
* Uses a clean, single-screen UI for quick viewing

---

## How It Works

1. The app sends a request to a public prayer time API.
2. The API returns daily prayer timings in JSON format.
3. The app processes the data using JavaScript.
4. Times are converted from 24-hour format to 12-hour (AM/PM).
5. Each prayer is displayed along with its valid time range.

No backend or database is required — everything runs in the browser.

---

## Why the Timing Is Accurate

* The app uses a well-established prayer time API based on astronomical calculations.
* It applies **Calculation Method 8**, which aligns with commonly used standards in Bangladesh.
* Prayer times are computed using:

  * Solar position (sunrise, sunset, angle of the sun)
  * Geographic location (latitude and longitude)
  * Timezone data

These calculations follow globally accepted Islamic prayer time methodologies.

---

## Important Note

* The displayed times represent **start times**, not mosque jamaat times.
* Local mosques may slightly adjust timings based on community practices.
* For precise jamaat times, manual configuration is recommended.

---

## Use Case

* Personal daily prayer reference
* Kiosk or display screen in homes or offices
* Lightweight integration into other web projects

---

## Tech Stack

* HTML
* CSS
* JavaScript (Vanilla)
* REST API (Prayer Times)

---
