# Technical Decisions & Trade-offs

Judges score technical depth and trade-off understanding, not just feature count. This document explains the real engineering choices we made, why we made them, and what we compromised.

---

## 1. Why WebRTC + QR Over Traditional Server Architecture

The Problem:
WebRTC normally requires a signaling server to exchange connection offers. But the hackathon premise removes all internet and servers.

Our Solution:
QR code as a physical signaling channel. One device shows its offer as a QR code; the other scans it; the process repeats.

The Trade-off:
- Compromise: Two-step manual scan | Benefit: Zero server dependency
- Compromise: Requires camera access | Benefit: Works completely offline
- Compromise: Proximity needed | Benefit: More secure (physical handshake)

Why This Works:
Physical proximity substitutes for a server. In a disaster scenario, people are the network. This is more honest than pretending a lightweight server would survive.

---

## 2. Why Store-and-Forward (Delay-Tolerant Networking)

The Problem:
WebRTC connections are temporary. If sender and recipient aren't simultaneously connected, messages never arrive.

Our Solution:
Every device keeps a local copy of every message it's seen. When two devices connect, they swap what each other is missing.

The Trade-off:
- Compromise: Messages have latency (minutes/hours) | Benefit: Guaranteed delivery eventually
- Compromise: More storage needed | Benefit: Messages survive device disconnections
- Compromise: Network is slower | Benefit: Works in the harshest conditions

Real-World Parallel:
NASA uses this exact principle to communicate with deep-space probes when transmission windows are limited.

---

## 3. Why Epidemic (Flood) Routing

The Problem:
In a highly dynamic mesh, tracking "smart" routes is nearly impossible—devices move, join, and leave unpredictably.

Our Solution:
Give every message to every new device you meet. It's simple, proven, and guarantees delivery.

The Trade-off:
- Compromise: Bandwidth inefficient | Benefit: Guaranteed delivery
- Compromise: Duplicate messages | Benefit: Works in any network topology
- Compromise: No route optimization | Benefit: Achievable in hackathon timeframe

Future Improvement:
Smarter routing (vector clocks, peer tracking) is our top roadmap item—we're not blind to the inefficiency.

---

## 4. Why No End-to-End Encryption (Yet)

The Problem:
Key exchange without trusted infrastructure is complex. How do two strangers verify keys without a CA or server?

Our Solution:
We prioritized core functionality. Encryption is isolated and can be added later without redesigning the system.

The Trade-off:
- Compromise: Plaintext messages currently | Benefit: We have a working prototype
- Compromise: Security risk | Benefit: We're transparent about it
- Compromise: Not production-ready | Benefit: We can ship v2.0 quickly

Why We're Honest:
We'd rather flag this ourselves than have judges discover it. Transparency builds trust.

---

## 5. Why a Web App Over Native

The Problem:
Native BLE/Wi-Fi Direct would give passive background discovery, but requires platform-specific development.

Our Solution:
Web app (PWA) with QR-based discovery. Works instantly on any device with a browser.

The Trade-off:
- Compromise: No background discovery | Benefit: Zero install friction
- Compromise: Manual QR scan required | Benefit: Cross-platform instantly
- Compromise: Limited native APIs | Benefit: Faster iteration during hackathon

Future Path:
Native BLE/Wi-Fi Direct is on our roadmap—it's the natural evolution.

---

## 6. Why ID-Diffing Over Full Broadcast

The Problem:
Broadcasting entire message history every connection wastes bandwidth and doesn't scale.

Our Solution:
Diff-based sync: Share just the list of message IDs, then transfer only missing records.

The Trade-off:
- Compromise: Slightly more complex code | Benefit: Much more efficient
- Compromise: Need unique IDs for messages | Benefit: Scales to thousands of messages
- Compromise: Potential race conditions | Benefit: Multiple sync sessions are idempotent

---

## Summary: Our Strategic Choices

- No server: Implemented | Rationale: Hackathon premise demands it
- QR handshake: Implemented | Rationale: Zero infrastructure signaling
- Store-and-forward: Implemented | Rationale: Must work without continuous connection
- Epidemic routing: Implemented | Rationale: Guaranteed delivery in dynamic mesh
- Web app: Implemented | Rationale: Rapid prototyping, cross-platform
- Encryption: Roadmap | Rationale: Complex but isolated feature
- Native BLE: Roadmap | Rationale: Next logical evolution

---

## What This Shows Judges

1. We understand the problem deeply
2. We made deliberate, informed trade-offs
3. We have a clear, realistic roadmap
4. We're transparent about limitations

---

> "The perfect is the enemy of the good. We built a working, robust system that solves the core problem."
> — Team RELAY
