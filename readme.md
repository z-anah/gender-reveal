Define the mobile one page web app concept with:

Project concept & goals [gender reveal]

Core features & requirements [guess gender, statistic guessed, gender reveal, see user reaction when seeing result, recorded face and voice througth the whole the process]

Data models & relationships [to define]

Project file/folder structure [to define]

User roles & permissions [admin, user]

User flows & navigation [link for unique user → permission of recording and voice with big button → guess → result statistics → gender reveal]

UI/UX wireframes (text) [small square of recorded face and voice and the web app, big UI]

Tech stack & dependencies [HTML, vue.js CDN, Tailwind CSS CDN, Supabase, to define where to save stream video and audio]

Deployment & hosting [Github Pages]

Documentation plan [README.md]

---

## **1. Project Concept & Goals**

**Concept:**
A **mobile-first, one-page** interactive web app for gender reveal parties, where invited users guess the baby’s gender, see live statistics, then watch the reveal — while their **facial expressions and voice reactions are recorded** throughout the process.

**Goals:**

* Make gender reveals more interactive and memorable.
* Capture genuine reactions with minimal setup (just a mobile browser).
* Provide shareable statistics on guesses before the reveal.
* Allow the host (admin) to download or review the recordings afterward.

---

## **2. Core Features & Requirements**

* **Unique Access Link** (sent to each guest).
* **Permission Prompt** for camera & microphone (must be accepted).
* **Guess Gender Screen** (Boy / Girl big buttons).
* **Live Statistics** showing % guesses for each gender.
* **Gender Reveal Animation** (e.g., pink or blue confetti).
* **Reaction Capture**:

  * Record **face (webcam)** and **voice (mic)** from the moment the app loads until reveal ends.
  * Store recording securely.
* **Admin Dashboard**:

  * View/download all recordings.
  * See guess statistics.

---

## **3. Data Models & Relationships**

**Entities:**

* **User**

  * `id` (UUID)
  * `name` (optional)
  * `unique_link` (string)
  * `role` (enum: "admin" | "guest")
  * `user_name` (string - optional, for display)
  * `password` (hashed string - optional, for admin login)
* **Guess**

  * `id`
  * `user_id` (FK → User)
  * `gender_guess` (enum: "boy" | "girl")
  * `timestamp`
* **ReactionRecording**

  * `id`
  * `user_id` (FK → User)
  * `video_url` (string - Supabase storage)
  * `audio_url` (string - Supabase storage)
  * `start_time`
  * `end_time`

**Relationships:**

* One **User** → one **Guess** (1:1)
* One **User** → one **ReactionRecording** (1:1)

---

## **4. Project File/Folder Structure**

```
/gender-reveal-app
  ├── index.html
  ├── /src
  │     ├── main.js
  │     ├── components/
  │     │      ├── GuessScreen.vue
  │     │      ├── StatsScreen.vue
  │     │      ├── RevealScreen.vue
  │     │      ├── RecordingPreview.vue
  │     ├── services/
  │     │      ├── supabaseClient.js
  │     │      ├── recordingService.js
  │     │      ├── statsService.js
  ├── /assets
  │     ├── css/
  │     ├── img/
  ├── README.md
```

---

## **5. User Roles & Permissions**

* **Admin**

  * Create & manage user links.
  * View/download all reaction videos.
  * See all guess statistics.
* **Guest**

  * Access app via unique link.
  * Allow camera & microphone recording.
  * Make one gender guess.
  * See reveal & statistics.

---

## **6. User Flows & Navigation**

1. **Guest Flow**

   * Click unique link →
   * Permission screen: "We’ll record your face & voice during this fun reveal!" → **Allow**
   * Guess Screen → Select gender → Submit.
   * Statistics screen → See live percentages.
   * Reveal animation → (Reaction recorded).
   * End screen: "Thanks for joining!"

2. **Admin Flow**

   * Login → Dashboard.
   * See stats.
   * View/download videos.

---

## **7. UI/UX Wireframes (Text)**

```
[Permission Screen]
[📹 Icon] We’ll record your reaction.
[🎙 Icon] We’ll record your voice.
[Big "Allow & Continue" Button]

[Guess Screen]
[Small top-right: User camera preview]
"Guess the baby's gender!"
[Pink Button: Girl]
[Blue Button: Boy]

[Stats Screen]
[Camera preview small on top]
"Guesses so far"
Boy: 60% | Girl: 40%

[Reveal Screen]
[Small cam preview top-right]
🎉 CONFETTI Animation (Pink/Blue)
"IT'S A GIRL/BOY!"

[End Screen]
"Thanks for participating!"
```

---

## **8. Tech Stack & Dependencies**

* **Frontend:** HTML5, Vue.js (CDN), Tailwind CSS (CDN).
* **Backend / Storage:** Supabase (DB + Storage for videos & audio).
* **Video/Audio Recording:** MediaRecorder API (browser).
* **Deployment:** GitHub Pages (static front-end), Supabase for backend.
* **Other Dependencies:**

  * `@supabase/supabase-js` (Supabase client)
  * Possibly `ffmpeg.wasm` for merging video/audio if needed.

---

## **9. Deployment & Hosting**

* **Frontend:** GitHub Pages (static).
* **Backend & Storage:** Supabase (PostgreSQL + Storage bucket).
* **Custom Domain:** Optional (via GitHub Pages settings).