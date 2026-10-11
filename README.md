# My IP

A one-screen page that shows your external IP address, internet provider, hostname, Autonomous System, network type, VPN check, location, ZIP code, local time and weather. It also has a speed test, a map and an IP history. Built for iPhone and iPad, and works in any browser.

## Files

- `index.html` is the page.
- `apple-touch-icon.png` is the Home Screen icon.

## Put it on GitHub Pages

1. Sign in at github.com and create a new **public** repository, for example `my-ip`.
2. In the repository, choose **Add file → Upload files**, add `index.html` and `apple-touch-icon.png`, and click **Commit changes**.
   On iPhone, if you don't see that option, tap **aA** in Safari's address bar and choose **Request Desktop Website**.
3. Go to **Settings → Pages**. Under *Build and deployment*, set **Source** to *Deploy from a branch*, then set **Branch** to `main` and `/ (root)`, and click **Save**.
4. After a minute or two, the page is live at `https://<your-username>.github.io/my-ip/`.

## Add it to your iPhone Home Screen

Open the link in Safari, tap **Share → Add to Home Screen**, then tap **Add**.
It opens full screen like an app, and checks again each time you switch back to it.

## Where the data comes from

The page asks free lookup services directly from your phone: ipwho.is first, with ipapi.co and ipinfo.io as backups.
Location and ZIP code are based on your provider's network, so they're approximate. If you use a VPN, the page shows the VPN's details.

**VPN check:** the page asks ipapi.is (a free VPN and proxy database), then makes its own checks on your phone. It looks for provider names that belong to data centers, VPN companies or iCloud Private Relay, and compares your phone's time zone with the IP's. It shows *Not detected*, *Possible* or *Likely*. That's a best guess and can't be certain.

**Network type:** shown under the AS number as *Residential*, *Mobile network*, *Business* or *Data center*. It comes from ipapi.is's classification of the company that owns the address, or from well-known provider names when that isn't available.

**Local IP:** Safari doesn't give web pages access to your phone's local address, so on iPhone this usually shows *Hidden*, with a pointer to Settings › Wi‑Fi › ⓘ, where you can see it.

**Hostname:** the reverse-DNS name your provider gives your IP, looked up through Google's public DNS (with Cloudflare's as a backup). Shown under the provider.

**Weather:** current conditions at the IP's approximate location, from Open-Meteo. Shown in °F and mph in the US, and °C and km/h elsewhere.

**IP history:** tap the line under the IP. It lists the addresses this device has seen, with dates, and is stored only on the device (clearing Safari's website data clears it).

**Map:** the square map beside Location, ZIP code and Local IP. Tap it for a larger map. It uses OpenStreetMap and shows the approximate area of your provider's network, not your exact position.

**Speed test:** the middle button runs a quick test (about 5–7 MB of data) when the app opens, and shows download ↓ and upload ↑ speeds in Mbps. It runs again when your IP changes or the result is over 30 minutes old. Tap it for ping and jitter, and tap **Run again** there for a full test (about 10–40 MB). It uses Cloudflare's speed test servers.

## Updating

Home Screen apps keep their own cached copy of the page. The page checks `version.json` each time it opens or you switch back to it, and reloads itself when the number there differs from `APP_VERSION` in `index.html`. When you change the page, bump both numbers together. The current version is shown at the bottom of the page (for example `v7`).
