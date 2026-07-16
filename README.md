# RELAY

**Offline-first, device-to-device mesh messaging — no towers, no internet, no server.**

> "When the internet disappears, communication shouldn't."

Built for **Build.IT Hackathon — Prompt 1: Software Track: First Contact**

![demo](docs/demo.gif)
*(replace this with a real screen recording before submitting — see Step 6 below)*

---

## The Problem

Modern communication depends entirely on infrastructure most people never think about — cell towers, ISPs, satellites, routers. When that infrastructure goes down, so does every messaging app, call, and social feed people rely on. This happens more often than it should:

- Natural disasters (earthquakes, floods, hurricanes)
- Remote areas with no stable connectivity
- Crowded events overloading local networks
- Total infrastructure loss — the scenario this hackathon prompt is built around

In all of these cases, conventional messaging apps become completely unusable at the exact moment people need to coordinate the most.

## Our Fix

Relay turns every device into part of the network itself. Instead of routing messages through a server, two devices connect **directly** to each other over WebRTC, using a **QR code as the handshake** — no signaling server, no internet required to establish the link. Once connected, every device keeps a local store of every message it has seen and syncs it to the next device it meets. A message doesn't need a live connection from sender to recipient — it just needs a chain of people who each spent a few seconds linked to the next.

This is called **store-and-forward / delay-tolerant networking** — the same principle NASA uses to relay data across deep space, applied here to a phone in someone's pocket.

## Key Takeaways

- ✅ Infrastructure-agnostic — no cell towers, no ISP, no server
- ✅ Zero setup cost — runs in a browser, nothing to install
- ✅ Self-healing mesh — every device that connects becomes a relay
- ✅ Store-and-forward delivery — messages can arrive hours after the sender is gone
- ✅ SOS priority channel for urgent messages
- ✅ Shared local coordination board (water points, meeting spots, hazards)
- 🔜 End-to-end encryption — see [Roadmap](#roadmap)

## How It Works

**Step 1 — Peer Discovery & Handshake**
One device generates a QR code (a compressed WebRTC connection offer). The other scans it and generates a reply QR code. The first device scans that back. No server ever brokers this — the two devices exchange everything they need to connect directly, using physical proximity as the "network."

**Step 2 — Direct Encrypted Channel**
WebRTC establishes a direct peer-to-peer data channel between the two devices over whatever local network path is available.

**Step 3 — Store-and-Forward Sync**
Every device keeps a local database (IndexedDB) of every message and board post it has ever seen, tagged with a unique ID. When two devices link up, they trade ID lists, then each sends over whatever the other is missing.

**Step 4 — Multi-Hop Delivery**
A message can travel Device A → B → C, reaching a recipient who was never in range of the original sender — carried physically as people move, not by any single radio link exceeding its normal range.

**Step 5 — Priority Handling**
Messages marked **SOS** are flagged and visually prioritized in the message thread; the board is synced the same way messages are, so coordination info (like "water at 5th & Main") spreads through the mesh automatically.

## Core Features

| Feature | What it does |
|---|---|
| Peer Discovery | QR-based WebRTC handshake, no server needed |
| Store-and-Forward Messaging | Messages persist locally and relay to every new peer |
| Hop Count | Tracks how many devices a message has passed through |
| SOS Mode | Emergency messages are visually flagged and prioritized |
| Local Coordination Board | Shared bulletin for supply points, hazards, meeting spots |
| Offline-Capable | Service worker caches the app shell for zero-network reloads |

## Tech Stack

| Layer | Technology | Why |
|---|---|---|
| Peer connection | WebRTC (RTCPeerConnection + DataChannel) | Direct device-to-device transfer, no server |
| Handshake | QR code (camera scan) | Signaling without any infrastructure |
| Local storage | IndexedDB | Persistent message/board store per device |
| Offline support | Service Worker | App still loads with zero connectivity |
| Frontend | HTML / CSS / JavaScript | No build step, runs anywhere instantly |

## Real-World Applications

- 🚨 **Emergency response** — coordination during earthquakes, floods, hurricanes
- 🏕️ **Remote expeditions** — trekking/mountaineering groups with no signal
- 🎪 **Large events** — bypassing overloaded cellular networks
- 🌍 **Rural connectivity** — regions without stable internet infrastructure

## Known Limitations

We'd rather name these ourselves than have a judge find them first:

- **QR capacity** — WebRTC offers/answers can be large. We compress them before encoding; on very noisy networks with many ICE candidates, a code can occasionally be too dense to scan reliably.
- **No encryption yet** — messages are currently unencrypted in transit and storage. This is the top item on our roadmap, not a hidden gap.
- **Two-step handshake** — connecting requires scanning twice (offer, then reply), so both devices need to be within camera range briefly. After that, no further proximity is needed for a message to keep relaying onward.
- **STUN dependency for NAT traversal** — we use a public STUN server to help discover connection candidates; on a fully offline network, ICE gathering falls back to local candidates only, which still works for devices on the same Wi-Fi/hotspot.

## Roadmap

- [ ] End-to-end encryption between original sender and recipient
- [ ] Smarter routing (currently epidemic/flood-style; could reduce redundant transfers by tracking peer knowledge)
- [ ] Delivery acknowledgements to stop unnecessary re-forwarding
- [ ] Native BLE/Wi-Fi Direct transport for always-on background meshing (no camera scan needed per link)

## Getting Started

```bash
git clone https://github.com/<your-username>/relay-web.git
cd relay-web
```

Open `index.html` with a local server — camera access for QR scanning requires a served page, not a `file://` path.

**Easiest way (VS Code):** install the **Live Server** extension → right-click `index.html` → *Open with Live Server*.

## Demo

To show multi-hop relay: open the app on 3+ devices, connect Device A ↔ B and B ↔ C via QR (keep A and C physically out of range of each other), send a message from A, and show it arriving at C through B.

## Team

- *Add your names and roles here*

## License

MIT
