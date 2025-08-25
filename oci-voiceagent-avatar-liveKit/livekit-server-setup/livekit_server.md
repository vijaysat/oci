# Lab : Setting up Livekit server on local

## Introduction

LiveKit is an open source platform for developers building realtime media applications. It makes it easy to integrate audio, video, text, data, and AI models while offering scalable realtime infrastructure built on top of WebRTC.

### Installation
Self-hosted: Run the open source LiveKit server on your own infrastructure for maximum control and customization.

#### MacOS
```
brew install livekit

OR

pip install livekit-api     # server API
```
#### Linux
```
curl -sSL https://get.livekit.io | bash

OR

pip install livekit-api     # server API
```

### Getting Started
#### Starting LiveKit
Start LiveKit in development mode by running livekit-server --dev. It'll use a placeholder API key/secret pair.

```commandline
API Key: devkey
API Secret: secret
```

### Generating an access token using Livekit Pyhton SDK

```
from livekit import api
import os

# will automatically use the LIVEKIT_API_KEY and LIVEKIT_API_SECRET env vars
token = api.AccessToken() \
    .with_identity("python-bot") \
    .with_name("Python Bot") \
    .with_grants(api.VideoGrants(
        room_join=True,
        room="my-room",
    )).to_jwt()
```

### Creating a room
RoomService uses asyncio and aiohttp to make API calls. It needs to be used with an event loop.

```
from livekit import api
import asyncio

async def main():
    lkapi = api.LiveKitAPI("https://my-project.livekit.cloud")
    room_info = await lkapi.room.create_room(
        api.CreateRoomRequest(name="my-room"),
    )
    print(room_info)
    results = await lkapi.room.list_rooms(api.ListRoomsRequest())
    print(results)
    await lkapi.aclose()

asyncio.run(main())
```

### Connecting Livekit with OCI Agent


