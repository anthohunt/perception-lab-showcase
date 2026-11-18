**English** · [Français](README.fr.md)

# Perception Lab

**A Meta Quest headset used as a sensor: its camera, microphone and body tracking are recorded on a server and replayed in a dashboard, to give an AI agent's memory real data.**

![The XR Agent dashboard replaying a Quest 3 session: the passthrough camera shows the wearer's hands, then the page scrolls to the face and hand-joint panels](docs/demo.gif)

<details><summary>French version</summary>

![Le tableau de bord XR Agent relit une session Quest 3 : la caméra passthrough montre les mains de la personne qui porte le casque, puis la page descend vers les panneaux du visage et des articulations des mains](docs/demo.fr.gif)

</details>

*Recorded on a Quest 3 on 24 September 2026; dashboard in French.*

## Using it

- **Capture.** The XR Agent module, inside a Unity VR app, sends the headset's outward camera (passthrough, Quest 3) or its screen (Quest Pro), the microphone, head, hands and body; gaze and face on Quest Pro, face expressions inferred from the voice on Quest 3.
- **Live view.** The dashboard follows a headset at the headset's rate (72 per second on a Quest 3), with the video about 1.9 s behind.
- **Recording.** Started and stopped from the dashboard; the server keeps 1 to 30 samples and video frames per second, while the live view stays complete.
- **Replay.** Play, frame-by-frame steps, scrubbing and speed; each session exports as an archive described by its README, and an API serves the raw data chunks.
- **In other apps.** The school's HITeC VR training app carries the module in its test builds since November 2026, video off: recordings started remotely and a feedback button. The dashboard also opens per headset inside the QuestFleet headset manager.
- **Memory (not wired yet).** A separate service has a vision model describe one frame every 2 s and adds it to a time-stamped knowledge graph.

## Architecture

![Architecture: the researcher's browser starts, stops and sets the rate on the capture server, which exchanges data chunks and commands with the Unity app on the Meta Quest and sends back live view and replay; Meta HMS installs the app and its config; a memory service (Graphiti, Groq vision) is meant to receive frames from the headset, not wired yet](docs/architecture.svg)

<details><summary>French version</summary>

![Architecture : le navigateur du chercheur lance, arrête et règle la fréquence sur le serveur de capture, qui échange blocs de données et commandes avec l'appli Unity du Meta Quest et renvoie le direct et la relecture ; Meta HMS installe l'appli et sa configuration ; un service de mémoire (Graphiti, vision Groq) doit recevoir les images du casque, pas encore câblé](docs/architecture.fr.svg)

</details>

## Status

- **Running** on the school's server since September 2026; data on a volume capped at 25 GB.
- **Measured in September 2026.** First Quest 3 recording: 30 s, 592 chunks, no loss. Lossless compression of the tracking data: 4.6 GB down to 0.73 GB.
- **Headsets.** The app went to nine test headsets through Meta's headset console (HMS), installation confirmed on three.
- **Memory service** deployed in July 2026, 7 out of 7 tests passing.
- **Stack.** Unity 6, Meta XR Core SDK, OpenXR; Android module in Java (Camera2, MediaProjection); Node.js, WebSocket, ffmpeg, brotli; FastAPI, Graphiti, FalkorDB, Groq; Docker.

---

**Anthony Hunt** · [ingevision.cloud](https://ingevision.cloud/?lang=en&p=xr-agent) · [LinkedIn](https://www.linkedin.com/in/anthony-hunt-3948a9196) · [GitHub](https://github.com/anthohunt)

The code is private.
