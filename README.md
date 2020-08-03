# SMBBB
**_SMB Baddies Blocklist: a DNS blocklist of all the phishing and malware links one small company gets_**

Direct link: [https://raw.githubusercontent.com/oo12/SMBBB/master/blocklist.txt](https://raw.githubusercontent.com/oo12/SMBBB/master/blocklist.txt)

We get so many phishing and malware links at work. Mostly targeting Microsoft 365. I‘ve developed an extensive set of rules to (mostly) intercept them before they’re delivered, but still. Partly to relieve my personal frustration with this and partly in the hope that it’ll be useful to some other exasperated IT person, I’m posting the list here. At present I’m updating it daily. Feed it into your filtering DNS and flush these turds before your users click. (Though honestly, your first priority should be quarantining pesky emails before they reach your users, using mail flow rules in Exchange or whatever. DNS filtering is helpful, but you’re always a step behind.)

I use this list with [Pi-hole](https://pi-hole.net), which is totally solid for enterprise use by the way. At least running on a proper VM and for around 100 users, nary a problem.

## Block or Unblock

All of these domains were taken from actual phishing emails, by me personally. False positives should be pretty low. However, phishers like to use legitimate sites for part of the process, especially if there’s a free account available. I block or don’t block stuff based on what’s appropriate for our workplace. Is it more likely that somebody will actually need this domain, or that it‘ll be phishing?

Take a look through the rest of this document and decide what’s right for you.

### You might want to allow these

if you actually use them. They’re legitimate sites, just get abused like everything else.

* `firebasestorage.googleapis.com` — Google cloud storage. Used frequently for hosting phishing sites and for us, blocking it has had little negative effect.
* `rebrand.ly` — Another URL shortner.
* `www.notion.so` — Popular for what I call phishing lures. You know, a PDF or whatnot that says “You received secure file! Click to view” with a big button that takes you on to the actual phishing site.
* `readymag.com` — Also used to host phishing lures.

### Consider blocking

* `www.canva.com` — Online design site. There’s apparently no way to send in an abuse report without creating an account first. Zero response on Twitter. A couple people at the office actually use this mess, so I don’t block it. But I *do* quarantine any incoming email with a canva link.
* `1drv.ms` — Short link for OneDrive files. Don’t know about you, but around here they’re more likely nothin’ good.

### Regular Expressions

Some things can only be blocked with regexes. Here are a few suggestions if you’re using something like Pi-hole which accepts them.

* `\.ga$`, `\.tk$`, `\.xyz$` — and really all the other TLDs your users are unlikely to legitimately need. Take a look at the blocklist for an idea of which ones we get. It’s sorted by domain so you can easily get an idea for frequency.
* `-my\.sharepoint\.com$` — You’ll definitely have to whitelist the ones your users actually need, but having this default blocked has saved us so many times. Whenever one Microsoft 365 user gets phished, they’ll put a lure on OneNote, then blast out the link to all of their contacts. These can be convincing looking since they come from somebody you know and usually have their correct signature and all.
* `\.000webhostapp\.com$` – free web hosting. Abused as badly as you’d expect.
* `\.3utilities\.com$` — free dynamic DNS.
* `\.wze\.io$` — same
* `\.carrd\.co$` — Online design site. Unlike Canva, they’re responsive to abuse reports.
* `\.glitch\.me$` — Programming project hosting. Also good about dealing with phishers.
* `\.only2clicks\.com$` — Some junk you don’t need.
* `-dot-gl494903049\.wl\.r\.appspot\.com$` — Hosts phishing sites with unique subdomains. I wish Google—and Microsoft—were better about shutting this nonsense down.

#### One Offs

These came in for a bunch of users at once, with a unique subdomain for each email. A “one day and done” thing; haven't seen them again.

* `\.salamapetrochemical\.com$`
* `\.oragondesignstudio\.com$`
