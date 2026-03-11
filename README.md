# Cville Trees Live — Workshop Deploy

## How It Works

This repo has ONE file: `index.html`. It's deployed to Vercel. During the
workshop, you swap the placeholder HTML with the Claude-generated prototype
and it goes live instantly.

## Setup (Tonight)

1. Create repo on GitHub: `uva-medical-design/cville-trees-live`
2. Push this folder to it
3. Connect to Vercel:
   - Go to vercel.com → New Project → Import this repo
   - Framework: None (Other)
   - Deploy
4. Note the URL (e.g., `cville-trees-live.vercel.app`)
5. Open the URL — you should see the "Building..." placeholder page

## During the Workshop (The Swap)

When Claude generates the prototype artifact in Phase 6:

**Option A — GitHub push (cleanest, ~30 seconds)**
1. Copy the artifact HTML from Claude
2. In terminal: open the repo folder
3. Paste into `index.html` (replacing the placeholder)
4. `git add . && git commit -m "live build" && git push`
5. Vercel auto-deploys in ~10 seconds
6. Refresh the URL on the projector → students see the real tool
7. Share the URL with the class

**Option B — Vercel dashboard (no terminal needed)**
1. Copy the artifact HTML from Claude
2. Go to Vercel dashboard → your project → Settings → edit
3. Or just redeploy from the Vercel CLI: `vercel --prod`

**Option C — Just share the artifact (simplest fallback)**
If deploy is fiddly during class, skip it. The artifact renders in Claude
Chat already. Deploy after class and share the URL via Carmen.

## The Reveal (Slide 17)

Show the URL on the projector. Students open on their phones.
The placeholder page says "Refresh in a few minutes" — so if anyone
visits early, it looks intentional, not broken.

## After the Workshop

The URL stays live. Students can share it, revisit it, show friends.
It becomes a proof point for the methodology.
