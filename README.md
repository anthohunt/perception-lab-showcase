**English** · [Français](README.fr.md)

> Showcase repository: the code and data of this project are private; this README describes it.

# Perception Lab

A test bench that records what a Meta Quest headset sees, hears and measures, and passes it to an agent with a temporal memory.

## The problem

Work on agent memory in virtual reality often starts from hand-written data, for lack of real capture. This bench provides real data, taken from the headset, to research teams at an engineering school. The goal is to learn what a headset actually delivers, stream by stream. It is a tool for knowledge, not a product.

## How it works

- The headset acts as a sensor: a Unity module, which can be embedded in a VR application, sends the passthrough camera video, microphone audio, head, hands, body, gaze and face.
- The server receives the data in chunks over HTTPS and relays it live over WebSocket.
- A web dashboard starts and stops recordings, sets the rate and replays sessions.
- The live view stays at the headset's rate; when recording, the server keeps only the chosen rate (1 to 30 per second).
- On the memory side, one frame every 2 seconds is described by a vision model, then added to a time-stamped knowledge graph.

## What is built

In progress, exploration phase.

- Capture service running; application distributed to nine test headsets, installation confirmed on three.
- Live view measured at 72 samples per second, displayed video delay of about 1.9 s.
- First recording on Quest 3: 30 s, 592 chunks, no loss.
- Lossless compressed storage: 4.6 GB reduced to 0.73 GB; disk space capped at 25 GB.
- Memory service deployed, 7 out of 7 tests passing.
- Still to do: wire continuous capture between the VR application and the memory service, and test on a headset the module's integration into a training application.

## What is public

This showcase is public; the code, the server and the recorded data remain private.

## Tech stack

- Unity 6, Meta XR Core SDK, OpenXR
- Android module in Java (Camera2, MediaProjection), H.264 video
- Node.js server, WebSocket, ffmpeg, gzip and brotli compression
- Memory service in Python: FastAPI, Graphiti, FalkorDB
- Groq (qwen3.6-27b vision model)
- Local sentence-transformers embeddings (all-MiniLM-L6-v2)
- Docker; distribution to headsets through Meta Horizon Managed Services
