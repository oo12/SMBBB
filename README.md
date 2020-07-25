# SMBBB
**_SMB Baddies Blocklist: a DNS blocklist of all the phishing and malware links one small company gets_**

Direct link: [https://raw.githubusercontent.com/oo12/SMBBB/master/blocklist.txt](https://raw.githubusercontent.com/oo12/SMBBB/master/blocklist.txt)

We get so many phishing and malware links at work. Mostly targeting Microsoft 365. I‘ve developed an extensive set of rules to (mostly) intercept them before they’re delivered, but still. Partly to relieve my personal frustration with this and partly in the hope that it’ll be useful to some other exasperated IT person, I’m posting the list here. At present I’m updating it daily. Feed it into your filtering DNS and flush these turds before your users click.

I use this list with [Pi-hole](https://pi-hole.net), which is totally solid for enterprise use by the way. At least running on a proper VM and for around 100 users, nary a problem.

## You might want to allow these

if you actually use them. They're legitimate sites, just get abused like everything else.

* `rebrand.ly` — Another URL shortner.
* `www.canva.com` — Hosts phishing lures. You know, a PDF or whatnot that says “You received secure file! Click to view” with a big button that takes you on to the actual phishing site.
* `www.notion.so` — Really popular for phishing lures.

## Consider blocking

these domains. I have them listed here as regular expressions; useful if you’re using something like Pi-hole which allows regexes.

* `-my\.sharepoint\.com$` — You’ll definitely have to whitelist the ones your users actually need, but having this default blocked has saved us so many times. Whenever one Microsoft 365 user gets phished, they’ll put a PDF lure on OneNote, then blast out the link to all of their contacts. These can be convincing looking since they come from somebody you know and usually have their correct signature and all.
* `\.000webhostapp\.com$` – free web hosting. Abused as badly as you’d expect.
* `\.3utilities\.com$` — free dynamic DNS.
* `\.ga$`, `\.tk$`, `\.xyz$` — and really all the other TLDs your users are unlikely to legitimately need. The list is sorted by domain, so simply by looking at it you‘ll get an idea for frequency.