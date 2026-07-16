# 📡 RELAY
## When the internet disappears, communication shouldn't.

**Built for Build.IT '26 Hackathon — Prompt 1: Software Track: First Contact**

---

## The Problem

You're at a music festival with 50,000 people. Your friend is 100 meters away, but your phone shows "No Service." The network is overloaded. Now imagine an earthquake hits and all cell towers go down. Your messaging apps? Completely useless.

This happens more often than we realize:
- Natural disasters knocking out infrastructure
- Remote areas with zero connectivity  
- Crowded events overwhelming networks
- Complete internet blackouts

In these moments, traditional communication fails exactly when we need it most.

---

## The Solution: RELAY

Relay turns every smartphone into a walking postal service.

Instead of relying on cell towers or internet, Relay lets phones talk directly to each other. When you send a message, it hops from phone to phone like a game of telephone—until it reaches your friend. Even if it takes 30 minutes and passes through 5 strangers' phones, the message gets through.

**How It Works**

Step 1: "Hello!"
Your phone shows a magical QR code. Your friend scans it with their camera. Poof! You're connected.

Step 2: "Here's a message!"
You type "Meet me at the big tree." Your phone sends it directly to your friend's phone.

Step 3: "Pass it on!"
Your friend walks away. Their phone meets another person's phone and automatically shares your message with them.

Step 4: "Mission complete!"
The message keeps hopping from phone to phone until it reaches your best friend who's across the festival. Everyone becomes a messenger!

---

## Key Features

What's Working Now:
- QR Handshake: Scan a code to connect—no typing, no servers
- Instant Messages: Send text back and forth directly
- Store & Forward: Messages auto-sync when phones meet
- Community Board: Share public updates everyone can see
- SOS Mode: Emergency messages get priority delivery
- Works Offline: Opens without internet, remembers everything

Coming Soon:
- End-to-end encryption (top priority!)
- Native app with Bluetooth background mode
- Smarter routing for faster delivery
- Photo and file sharing

---

## Technical Architecture

Tech Stack:
- Connection: WebRTC — Direct device-to-device, no server
- Handshake: QR Code — Zero infrastructure signaling
- Storage: IndexedDB — Persistent local message database
- Offline: Service Worker — App works with zero internet
- Frontend: HTML/CSS/JS — No build step, works everywhere

Why RELAY Wins:
- Truly Decentralized — No servers, no single point of failure
- Instant Access — Opens in browser, no app store needed
- Realistic — Based on NASA's deep-space communication principles
- Practical — Works with today's smartphones, no special hardware

---

## Real-World Applications

Emergency Response: Coordinate rescue during earthquakes, floods, hurricanes
Remote Expeditions: Trekking groups stay connected with no signal
Large Events: Bypass overloaded cellular networks at concerts, festivals
Rural Areas: Connect communities without stable internet

---

## Known Limitations

We're honest about where we stand:
1. Two-step scan — Both phones need to scan QR codes (takes 10 seconds)
2. No encryption yet — On our roadmap, not a hidden flaw
3. Manual connection — Requires deliberate action (not passive like Bluetooth)
4. WebRTC limits — Works best on same Wi-Fi/hotspot

---

## Getting Started

Clone the repository:
git clone https://github.com/Notproboii699/relay-web.git
cd relay-web

Run with Live Server (VS Code):
Install Live Server extension → right-click index.html → Open with Live Server

Or use Python:
python -m http.server 8000
Visit http://localhost:8000

For Demo:
1. Open the app on 2+ devices
2. On Device A: Click "Create Connection" → Show QR code
3. On Device B: Click "Scan QR" → Scan Device A's code
4. Device B shows their own QR code → Device A scans it back
5. Start messaging! Messages auto-sync between connected devices

---

## Hackathon Submission

Judging Criteria Alignment:
- Creativity: Novel QR handshake replacing server signaling
- Innovation: Store-and-forward messaging in a browser
- Prototype: Fully working web app with real-time relay
- Originality: Unique approach to offline communication

Submission Checklist:
- Project Title: RELAY
- Demo Video: https://youtu.be/your-demo-link
- Repository: https://github.com/Notproboii699/relay-web
- Team Registration Complete
- All team members registered individually

---

## The Team

Advitya Walia — Lead Developer
Akshaj Gulati — System Architect
Aadi Bansal — UI/UX & Testing

---

## License

MIT License — Free for anyone to use, modify, and share.

---

> "When the internet disappears, communication shouldn't."
> — Team RELAY, Build.IT '26
