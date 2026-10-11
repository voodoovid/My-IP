# My IP

A one-screen page that shows your external IP address, internet provider, AS number, location and time zone. Built for iPhone, and works in any browser.

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
