# Cultivating Connection

A social platform for farmers — posts, comments, direct messaging, profiles and
a curated news and video feed — built as a Streamlit application over SQLite.

Agricultural knowledge travels by word of mouth and stays local. The aim here is
a space where a farmer can ask a question about a crop problem and reach
somebody two districts away who has already solved it, rather than depending on
who happens to be nearby.

---

## Features

| | |
|---|---|
| **Accounts** | Registration and login, bcrypt-hashed passwords |
| **Posts** | Text with optional image attachments, per-post comment toggle |
| **Comments** | Threaded discussion on any post that allows it |
| **Messaging** | Direct messages between users |
| **Profiles** | Per-user profile with their post history |
| **News** | Curated agricultural news feed |
| **Videos** | Embedded instructional video feed |

## Data model

```
users     (id, name, phone, password)
posts     (id, user_id, content, image, allow_comments)   → users
comments  (id, post_id, user_id, content)                 → posts, users
messages  (id, sender_id, receiver_id, message)           → users
```

Images are stored as BLOBs directly in SQLite, which keeps deployment to a
single file with no object storage to configure — a reasonable trade at this
scale, and the first thing to change if the platform grew.

## Authentication

Passwords are hashed with bcrypt and never stored in plaintext. Login selects
the user by name and verifies the supplied password against the stored hash,
rather than matching the password column in SQL. Registration enforces a
minimum length of eight characters and rejects duplicate usernames.

## Usage

```bash
pip install -r requirements.txt
streamlit run app.py
```

The SQLite database is created on first run. `farmers.db` is not committed —
it holds user accounts and message history.

## Stack

Python · Streamlit · SQLite · bcrypt · Pillow

---

## Use

© 2026 Mahesh Veeraiah R. All rights reserved.

Published for review and assessment. Not licensed for reuse, redistribution or
modification — please get in touch about any other use.
