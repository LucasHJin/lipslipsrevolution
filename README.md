# LipsLips Revolution
> [!NOTE]  
> This was a group project for Hack the North 2024. This fork has an updated description adapted from our [Devpost listing](https://devpost.com/software/lipslips-revolution). 

The demo link is currently broken as dependencies have changed since the event (i.e. the event QR codes), but this demo video demonstrates it really well!
**→[Demo Video](https://youtu.be/C_vZ8xYM-pw)←**

## Description
Like singing? LLR is for you! Don’t like singing? LLR IS STILL FOR YOU! Fight for the top position in a Hack The North lip-syncing challenge. How does it work? Very simple, very demure:

1. Choose a song. Harder songs = more points.
2. Lip sync to a 10-15 second clip of the song. (Don’t mumble!)
3. LLR reads your lips to determine your skill of lip-syncing to popular songs!
4. Scan your HTN QR code to submit your score and watch as you rise in ranking.

## Inspiration
Why not? We wanted to try something new. The Symphonic Labs API allows us to transcribe lip movements into text, without any audio. Lip reading and the Symphonic Labs API was something we hadn't seen before. **We wanted to see how far we could push it!**

## Tech Stack
LLR is a web app built with Next.js, enabling the rapid development of reactive apps with backend capability. The Symphonic API is at the core of LLR, powering the translation from lip movement to text. We’re using OpenAI’s embedding models to determine the lip sync’s accuracy/similarity and MongoDB as the database for score data.

## *Note - Reverse engineering the APIs*
While the Symphonic API is super cool, we found it slow sometimes. We found that a 10-second video took around 5 seconds to upload and 30 seconds to translate. This just wasn’t fast enough for users to get immediate feedback. We looked at Symphonic Lab’s demo of Mamo, a macOS app, and it was much faster. Since it was not browser based, we had to decrypting its network traffic through a proxy to dig deeper. We found that it used a much faster internal web socket API. After a bunch of tinkering with a combination of base64 encoding and other shenanagins. We figured out how this newfound API worked, and lowered our latency from 30 seconds to 7 seconds with the same 10-second clip.

We wanted an easy to use leaderboard that didn't require a complicated login process. The Hack The North hacker badges were the obvious choice, but provided no public API to fetch data as the participant's name. We found that the Hack The North site used a GraphQL API internally, which we used to get the participants name for the leaderboard.

## Installation
1. Clone the repo
```bash
git clone https://github.com/yourusername/lips-lips-revolution.git
cd lips-lips-revolution
```
2. Install dependencies
```bash
npm install
```
3. Create `.env` file with the following values (you may or may not need a HTN badge for this...)
```bash
MONGODB_URI=your_mongodb_connection_string
NODE_ENV=development_or_production
HTN_TOKEN=your_htn_token_here
```

## What's next?
We hope to integrate with the Spotify API or other music services to offer a larger variety of songs. We also wish to add a penalty system based on the amount of noise made. It is, after all, lip-syncing and not just singing. We do hope to turn this into a mobile app! It’ll be the next TikTok, trust…
