# Build.IT '26 Submission 

## Quick Reference

- Project Title: RELAY - Offline-First Mesh Messaging
- Track: Software Track - Prompt 1: First Contact
- Team Name: STRAWHATS
- Members: Advitya Walia, Akshaj Gulati, Aadi Bansal
- Submission Date: July 17, 2026
- Video Link: [Insert YouTube URL here]

---

## What We Built

Relay is an offline-first messaging system that works without any internet or cellular infrastructure. It uses WebRTC for direct device-to-device connections and a QR code for the initial handshake. Messages are stored on each device and forwarded to new devices they meet, creating a self-healing mesh network.

The core innovation: Replacing the signaling server with a QR code handshake, making truly serverless communication possible.
--

## Project Structure
relay/
├── README.md           # Main project documentation
├── DECISIONS.md        # Technical trade-off explanations
├── SUBMISSION.md       # This file - submission details
├── LICENSE             # MIT License
├── .gitignore          # Git ignore rules
└── index.html          # The web app (main entry point)

---

## How We Meet Judging Criteria

Creativity:

- QR code as signaling server replacement is novel
- Applying space communication principles to smartphones
- No other hackathon project uses this approach

Innovation:

- WebRTC without signaling server
- Store-and-forward in a web app
- Browser-based mesh networking

Prototype:

- Fully working web app
- Real-time communication between devices
- Syncs messages automatically

Originality:

- Unique approach to offline messaging
- Not just another "chat app"
- Solves a genuine problem
