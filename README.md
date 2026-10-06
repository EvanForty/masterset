# MasterSet

Finish the set. Own it as one.

MasterSet lets collectors lock Collector Crypt card NFTs into an on-chain binder. When every slot is filled, the binder mints a single **Set NFT** that represents the locked cards. The Set NFT can be traded as one asset, used as collateral, or burned to unlock and redeem the physical slabs.

This repository is the MasterSet website.

## Features

- Solana wallet connection: Phantom, Solflare, Backpack and any Wallet Standard wallet, with quiet reconnect for trusted sites.
- SOL balance lookup through `@solana/web3.js`.
- Set browser with card checklists for each binder. Card images load from the public Pokémon TCG API image CDN (`images.pokemontcg.io`). If an image can't load, the slab falls back to styled art with the card number.

## Project structure

```
index.html          The whole site: markup, styles and scripts
favicon.svg         Logo / favicon
apple-touch-icon.png
vercel.json         Static hosting config (clean URLs, security headers)
```

No build step and no dependencies to install. `@solana/web3.js` and Google Fonts load from CDNs at runtime.

## Run locally

Wallet extensions don't inject into `file://` pages, so serve the folder:

```bash
npx serve .
# or
python3 -m http.server 3000
```

Then open http://localhost:3000.

## Deploy to Vercel

1. Push this folder to a GitHub repository (the files should sit at the repo root).
2. In Vercel, choose **Add New → Project** and import the repository.
3. Leave the settings as detected:
   - Framework Preset: **Other**
   - Build Command: *(empty)*
   - Output Directory: *(empty / default)*
   - Install Command: *(empty)*
4. Click **Deploy**.

Or from the command line:

```bash
npm i -g vercel
vercel        # preview
vercel --prod # production
```

## Notes

- The public RPC endpoint (`api.mainnet-beta.solana.com`) is rate-limited. If the balance doesn't show, set `RPC_URL` near `fetchBalance()` in `index.html` to your own endpoint (Helius, QuickNode, Triton).
- Not affiliated with or endorsed by Collector Crypt. Card names are used for identification only.

## Next steps

- Anchor program for binders: create binder, deposit/withdraw card NFTs into escrow, completeness check, mint Set NFT, burn to release.
- Detect which binder cards a connected wallet holds (DAS lookups filtered to the Collector Crypt collection).
- Route missing slots through Collector Crypt marketplace and gacha APIs.
