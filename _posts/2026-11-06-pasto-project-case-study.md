---
layout: post
title: "How I built Pasto, a temporary bridge between devices"
date: 2026-11-06
categories: [projects]
tags: [project, React, TypeScript, Supabase]
description: "The implementation story behind Pasto, a browser-based tool for moving text and files between devices without accounts."
---

## Why I built it

I kept running into the same small problem: something was on my phone, but I needed it on my laptop. The usual options were opening a chat with myself, sending an email, or signing into another service. All of them worked, but they were too much ceremony for a five-second transfer.

Pasto started as a simpler idea: open one page, connect another device, move the data, and let the session disappear.

[Try Pasto](https://usepasto.vercel.app/) · [Read the source](https://github.com/kakarotsec/pasto)

This is not a vulnerability writeup. It is a project article, so there is no severity rating. The useful labels here are `project`, `React`, `TypeScript`, and `Supabase`.

## The flow I wanted

The first device creates a temporary link. Pasto puts the session code in the URL, displays a QR code, and lets the second device join by scanning or entering the code. Once both devices are connected, text is synchronized live and files can be uploaded into the same session.

The URL detail matters. If the second device opens a link such as `/?session=...`, the app reads the query parameter on startup and attempts to join that session. It means the QR code is not a separate invitation system; it is just a convenient way to carry the same session link.

The main screen supports:

- live text editing;
- file uploads;
- QR pairing and PIN entry;
- copying the session code;
- closing a session manually;
- reconnecting and detecting an expired session.

The current upload limits are five files at a time and 50 MB per file. Those limits keep Pasto focused on moving useful snippets and files, rather than turning it into general-purpose storage.

## The frontend is deliberately small

The application is a React and TypeScript app built with Vite. `src/pages/Index.tsx` contains the main session flow, while React Router leaves room for the home and admin routes.

The page keeps a small amount of state:

- the session ID and public session code;
- the current text draft;
- items already loaded for the session;
- whether the session is idle, active, or closed;
- realtime connection status;
- upload and QR-scanner state.

The URL is updated with `history.replaceState` when a session is created or joined. That avoids a full navigation while still making the session link shareable and restorable.

For the QR scanner, the app uses `html5-qrcode`. The generated code uses `react-qr-code`. This is a practical split: one component displays a pairing code and the other opens the camera when someone chooses to scan.

## Creating and joining a session

Creating a session goes through the `clipbeam-create-session` Edge Function. The client receives a session ID and a short session code, stores them in React state, updates the URL, and starts the realtime subscription.

Joining follows the same shape. The entered code is sent to `clipbeam-join-session`; if the session is valid, the client stores the returned identifiers, updates the URL, loads existing items, and subscribes to the session channel.

Keeping creation and joining behind server functions was important. The browser should not decide whether a code exists, whether it has expired, or whether the session can be used. It asks the backend, then renders the result.

## Why Supabase Broadcasts handle the live text

Pasto subscribes to a channel named after the session:

```text
clipbeam-session-{sessionId}
```

The client listens for two broadcast events:

- `live_text` updates the shared draft;
- `session_closed` tells connected clients to leave the active state.

When a user types, the current text is sent as a broadcast instead of creating a database row for every keystroke. That keeps the live path fast and avoids filling the database with a history Pasto never promised to keep.

There is still a small amount of polling. After connecting, the client fetches existing items through `clipbeam-get-items`, and it changes polling phases depending on how recently the connection was established. Broadcasts handle the immediate experience; fetching items handles state that may have existed before a device joined or may have been missed during reconnect.

That combination is more useful than pretending realtime delivery is perfect. A live channel is great for changes, but a reload still needs a way to rebuild the current session state.

## Files take a different path

Text is broadcast. Files are not.

For an upload, the client first checks the number of files and each file's size. It uploads accepted files to the `clipbeam-items` Supabase Storage bucket, then calls `clipbeam-send-item` with the session code and file metadata. Other clients fetch the item list and build a download URL from the stored path.

The flow is therefore:

1. reject files over the client-side limits;
2. upload the file to storage;
3. register the item for the current session;
4. refresh the session items for connected clients;
5. remove the storage object when the session is cleaned up.

The last step is the one that is easy to miss. Deleting a database record while leaving the file in storage would not be ephemeral sharing. Pasto's cleanup function collects the file paths, removes the storage objects, deletes the item rows, and then deletes the session row.

## The 15-minute cleanup job

Pasto uses a fixed 15-minute inactivity window. The Supabase Edge Function `clipbeam-expire-sessions` runs on a schedule and processes up to 200 sessions per invocation.

It removes sessions that were explicitly ended or have been inactive past the cutoff. For each one it:

1. loads the associated items;
2. removes their paths from the `clipbeam-items` bucket in chunks;
3. deletes the item rows;
4. deletes the session row;
5. records aggregate cleanup statistics.

The function also checks a dedicated cleanup secret before doing any work. That is a small but important operational boundary: a public endpoint should not be able to trigger privileged deletion with no scheduler authentication.

Cleanup errors are logged and the function continues processing other sessions where possible. That makes the job observable without allowing one stale file to stop cleanup for every other expired session.

## Closing a session early

Expiration is the safety net, not the only control. Pasto also has a manual end-session path through `clipbeam-end-session`.

When the session is ended, the client broadcasts `session_closed`. Connected browsers transition out of the active state, clear their local items, and keep enough of the code to show that the link has closed. The backend cleanup then removes the associated data.

This two-part behavior is intentional. The broadcast makes the UI respond immediately; the cleanup job provides eventual deletion if a client disappears or the manual request is never made.

## What the repository taught me

The project changed how I think about “temporary” features. The difficult part was not generating a QR code. It was making every path agree about the lifecycle:

- a new session must be created server-side;
- a joining device must be checked server-side;
- text updates should not become permanent history;
- files need both metadata cleanup and storage cleanup;
- an ended session must stop looking active in connected browsers;
- a scheduled job must finish cleanup even when individual operations fail.

Those details are the actual product. The UI only makes them visible.

## Current state

Pasto is a public MIT-licensed repository with a live deployment. It currently focuses on one job: moving text and files between devices quickly without accounts or long-lived history.

The next improvements I would make are better reconnect feedback, stronger automated tests around session expiry and partial cleanup, and clearer operational metrics for failed storage deletions. I would not add accounts or permanent history unless the product goal changed; both would weaken the reason Pasto exists.

