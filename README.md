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

**Network type:** the tag under the Autonomous System number. It shows *Residential*, *Mobile network* or *Satellite* in green; *Data center* or *Relay / CDN* (for example iCloud Private Relay) in amber; *VPN*, *Proxy* or *Tor* in red; and *Business*, *Education*, *Government*, *Banking* or *Unknown type* in grey. It uses ipapi.is's classification of the company that owns the address when that service answers. It also checks the IP's hostname for words providers use for mobile service (for example TELUS's `…wireless.telus.com`) or wired home service (for example `…hsia.telus.net`, `…hsd1…comcast.net`), which tells mobile from home when one company runs both under the same Autonomous System number. Otherwise it uses well-known provider names and words. A few home internet providers that lookup services sometimes list as data centers, currently Atlas Networks, always count as residential unless the address is flagged as a VPN, proxy or Tor.

**Local IP:** Safari doesn't give web pages access to your phone's local address, so on iPhone this usually shows *Hidden*, with a pointer to Settings › Wi‑Fi › ⓘ, where you can see it.

**Hostname:** the reverse-DNS name your provider gives your IP, looked up through Google's public DNS (with Cloudflare's as a backup). Shown under the provider.

**Weather:** current temperature, conditions and wind at the IP's approximate location, from Open-Meteo, with an icon for the conditions and a wind icon when it's windy (15 mph or 24 km/h and over). Shown in °F and mph in the US, and °C and km/h elsewhere. The moon picture shows tonight's phase. It's calculated on the device, and its name appears beside it on iPad. On iPhone only the picture is shown, to save space.

**IP history:** tap the line under the IP. It lists the addresses this device has seen, with dates, and is stored only on the device (clearing Safari's website data clears it).

**Map:** the map beside Location, ZIP code and Local IP. Tap it for a larger map. It uses OpenStreetMap and shows the approximate area of your provider's network, not your exact position.

**Speed test:** the middle button shows download ↓ and upload ↑ speeds in Mbps, and ping (the delay, in milliseconds). The measuring is done by Cloudflare's own speed test engine ([@cloudflare/speedtest](https://github.com/cloudflare/speedtest) 1.14.1, MIT license), the code behind speed.cloudflare.com, hosted here under `vendor/cloudflare-speedtest`. Its reporting of results back to Cloudflare is switched off, and the packet loss test is left out. When the app opens, a short rough check runs (a few seconds, at most about 20 MB each way). The full test only runs when you ask for it. When your IP changes, the speed numbers are cleared straight away, because they belonged to the old connection. If your IP changes during the rough check (switching between Wi‑Fi and cellular, or turning a VPN on or off), it stops and checks the new connection. It gives up after 5 seconds without progress or 15 seconds in total, so connections left hanging by a network switch can't hold it up. It tests again only when your IP changes or the result is over 30 minutes old. Tap the button for download, upload, ping, jitter, and ping while downloading and uploading. Tap **Run again** there for the full test, the same sequence speed.cloudflare.com runs. It can use over 1 GB on a gigabit line. Treat the numbers as an in-browser estimate. Testing showed that a page hosted on another site (here github.io) reads noticeably lower than Cloudflare's own site in Safari, even with the same engine. That was about half the download and twice the ping on a gigabit line. The panel has buttons for an accurate test on **speed.cloudflare.com** or in the **Speedtest app** (`speedtest://`, which only works if the Ookla app is installed). If a request stalls, the test stops after 20 seconds without progress and shows what it measured so far.

## Updating

Home Screen apps keep their own cached copy of the page. The page checks `version.json` each time it opens or you switch back to it, and reloads itself when the number there differs from `APP_VERSION` in `index.html`. When you change the page, bump both numbers together. The current version is shown at the bottom of the page (for example `v26`).

## Privacy

The map code (Leaflet 1.9.4, BSD 2-clause license) and the speed test engine (Cloudflare speedtest 1.14.1, MIT license) are hosted in this repository under `vendor/`, so they load from GitHub Pages along with the page. The speed test engine's reporting of results to Cloudflare is switched off.


The page has no accounts, cookies or analytics, and sends no names, emails or device details. Your IP history and last speed result are stored only on your device. Like any website, each service below sees your IP address when the page contacts it, plus the details listed.

| Service | What it's used for | What it receives |
|---|---|---|
| GitHub Pages | Hosts the page | Your IP |
| ipwho.is (backups: ipapi.co, ipinfo.io) | IP, provider, location | Your IP |
| api.ipapi.is | VPN check and network type | Your IP |
| api6.ipify.org / api4.ipify.org | Your other address (IPv6, or IPv4 when IPv6 is your main one) | Your IP |
| dns.google (backup: cloudflare-dns.com) | Hostname | Your IP, as the name being looked up |
| api.open-meteo.com | Weather | Your IP and the approximate coordinates of your IP |
| tile.openstreetmap.org | Map pictures | Your IP and which map area is shown |
| speed.cloudflare.com | Speed test | Your IP, plus blank test data (results aren't sent back) |

Each service handles its records under its own privacy policy.
