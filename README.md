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

**Weather:** current temperature, conditions and wind at the IP's approximate location, from Open-Meteo, with an icon for the conditions and a wind icon when it's windy (15 mph or 24 km/h and over). Shown in °F and mph in the US, and °C and km/h elsewhere. The moon picture shows tonight's phase. It's calculated on the device, and its name appears beside it on iPad. On iPhone only the picture is shown, to save space.

**IP history:** tap the line under the IP. It lists the addresses this device has seen, with dates, and is stored only on the device (clearing Safari's website data clears it).

**Map:** the map beside Location, ZIP code and Local IP. Tap it for a larger map. It uses OpenStreetMap and shows the approximate area of your provider's network, not your exact position.

**Speed test:** the middle button shows download ↓ and upload ↑ speeds in Mbps. When the app opens, it runs quick rounds until two rounds in a row agree within 15%, up to 4 rounds, then stops and shows their average. The first round picks an upload size that takes at least 0.7 seconds, so the reading isn't too low. A check usually uses about 15–50 MB. It tests again only when your IP changes or the result is over 30 minutes old. Tap the button for ping and jitter, and tap **Run again** there for a full test (about 10–40 MB). It uses Cloudflare's speed test servers.

## Updating

Home Screen apps keep their own cached copy of the page. The page checks `version.json` each time it opens or you switch back to it, and reloads itself when the number there differs from `APP_VERSION` in `index.html`. When you change the page, bump both numbers together. The current version is shown at the bottom of the page (for example `v11`).

## Privacy

The map code (Leaflet 1.9.4, BSD 2-clause license) is hosted in this repository under `vendor/leaflet`, so it loads from GitHub Pages along with the page.


The page has no accounts, cookies or analytics, and sends no names, emails or device details. Your IP history and last speed result are stored only on your device. Like any website, each service below sees your IP address when the page contacts it, plus the details listed.

| Service | What it's used for | What it receives |
|---|---|---|
| GitHub Pages | Hosts the page | Your IP |
| ipwho.is (backups: ipapi.co, ipinfo.io) | IP, provider, location | Your IP |
| api.ipapi.is | VPN check and network type | Your IP |
| api6.ipify.org | IPv6 address | Your IP |
| dns.google (backup: cloudflare-dns.com) | Hostname | Your IP, as the name being looked up |
| api.open-meteo.com | Weather | Your IP and the approximate coordinates of your IP |
| tile.openstreetmap.org | Map pictures | Your IP and which map area is shown |
| speed.cloudflare.com | Speed test | Your IP, plus blank test data |

Each service handles its records under its own privacy policy.
