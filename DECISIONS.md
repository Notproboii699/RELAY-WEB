# Technical Decisions

A short record of the real trade-offs we made and why — judges score technical depth and trade-off understanding, not just feature count, so we're writing these down rather than leaving them implicit.

## Why WebRTC + QR instead of a server

The hackathon prompt removes internet and cell towers entirely. Any design that assumes a reachable server is disqualified by the premise itself. WebRTC lets two browsers open a direct data channel, but WebRTC normally needs a signaling server to exchange the initial connection offer/answer. We replaced that signaling server with a QR code: one device shows its offer as a QR code, the other scans it and shows its answer back. Physical proximity substitutes for a server — which is arguably a more honest fit for a "no infrastructure" scenario than pretending a lightweight server would survive when everything else didn't.

## Why store-and-forward instead of requiring both devices online at once

A direct WebRTC link only exists between two devices that are currently connected. If we required sender and recipient to be linked at the same time, the app would only work for people already standing together — which defeats the purpose. Instead, every device keeps a local copy of every message it has seen and syncs against whoever it meets next. This is delay-tolerant networking: the message physically travels through the population instead of over a continuous link.

## Why ID-diffing sync instead of full broadcast

When two devices connect, they could just dump their entire message history at each other every time. Instead, each side first sends a list of message IDs it already has, and only unseen records get transferred. This keeps repeated re-connections between the same two devices cheap (nothing new to send) and scales better as message history grows.

## Why epidemic (flood) routing, not smarter routing — for now

The simplest correct routing strategy is: forward a message to every peer you meet who doesn't already have it. This guarantees delivery (given enough peer contact over time) and was achievable in the hackathon timeframe. The known cost is redundant transfers — a message can reach the same cluster of devices multiple times through different paths. Smarter approaches (e.g., tracking which peers have already seen which messages, or vector-clock-based routing) would reduce that redundancy, and it's the first thing on our roadmap.

## Why no encryption yet — and why we're saying so

An earlier version of this concept assumed end-to-end encryption. We did not implement it in the hackathon build, and we'd rather flag that ourselves than have it discovered under questioning. The reason it's not in yet: key exchange without any trusted infrastructure adds real complexity (how do two strangers verify each other's keys without a CA or server?), and we prioritized a working, demonstrable relay mechanism first. Messages currently travel and store in plaintext.

## Why a browser app instead of native BLE/Wi-Fi Direct

An earlier concept for this idea targeted native Android with BLE for passive, always-on mesh discovery. We chose to build the browser version instead because it removes any install step for a demo audience, works across platforms without separate builds, and let us focus hackathon time on the relay logic itself rather than platform-specific Bluetooth APIs. The trade-off: BLE can discover and mesh passively in the background; our QR handshake requires an explicit, deliberate action per connection. Native BLE/Wi-Fi Direct is the natural next step and is on the roadmap.
