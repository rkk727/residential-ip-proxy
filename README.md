# adspower proxy: How to Choose and Configure Residential IPs for Multi-Account Workflows Without "Connection Failed" Errors

AdsPower gives you isolated browser profiles with their own fingerprints, cookies and logins. What it doesn't give you is an IP address. Every profile you create still needs a working proxy behind it, and that's where most of the frustration starts.

Search around for "adspower proxy" and you'll find two very different groups of people. One group wants to know which provider to buy from. The other group already bought something, pasted host and port into the profile settings, clicked **Check Proxy**, and got a red failure message. Both problems usually trace back to the same thing: the way a proxy provider issues credentials has to match the way AdsPower connects.

This guide covers both halves — what to buy for AdsPower profiles, and how to get it configured correctly, using 9Proxy's residential network as the concrete example because it publishes an official AdsPower integration guide and its authentication model lines up cleanly with how AdsPower works.

## AdsPower doesn't sell proxies, and that changes what you're shopping for

AdsPower is an anti-detect browser. Its job is profile isolation: separate fingerprints, separate cookie jars, bulk profile creation, team access, and proxy management. It supports HTTP, HTTPS, SSH and SOCKS5 proxy types, and it will happily accept any credentials in `host:port:user:pass` form.

So AdsPower is the container. The proxy is what actually determines whether a logged-in account looks like a real person on a real home connection. Datacenter IP ranges get flagged fast on most major platforms; residential IPs come from actual ISP-assigned addresses, which is why multi-account work almost always ends up on residential proxies.

A detail worth knowing before you start: AdsPower ships preset configurations for a handful of named providers (IPFoxy, Oxylabs, Luminati, 922S5, IPHTML and others). 9Proxy isn't in that preset list — you configure it as a standard HTTP/HTTPS or SOCKS5 proxy. That's not a downgrade; the manual path is the same one you'd use for any provider outside the presets, and it gives you full visibility into what's being sent.

## Three ways to attach an IP to a profile

AdsPower handles proxy assignment in three layers, and picking the right one saves a lot of clicking later.

**The added-proxies list.** Under Proxy Management you can import proxies in bulk — up to 500 per batch, one per line, with an optional protocol prefix like `socks5://` if you're mixing types. Entries get checked for duplicates on save, so the same IP won't quietly stack up across your list. Once they're in the list, any profile can pull from it.

**Per-profile custom entry.** Standard practice for a one-off profile: New Profile → Proxy section → enter type, host, port, username, password → Check Proxy → OK.

**Excel batch creation.** For larger operations, you can export profile data, edit the spreadsheet, and re-import. The `proxyid` column binds a specific proxy from your managed list to each profile; typing `random` in that column lets AdsPower pull any available IP from the list. Other columns cover `proxytype`, `ipchecker`, and the `proxy` field itself in `host:port:user:pass` format. Two things to avoid here: don't delete the `acc_id` or `id` columns, or AdsPower can't match rows to profiles, and don't touch the `cookie` column if the exported value got truncated by Excel's cell limit.

Most people reading about "adspower proxy" setups are working in the second and third layers, and that's where credential format errors happen.

## Pick the billing model before you pick the provider

9Proxy sells residential access two ways, and the choice matters more for AdsPower work than the headline price does.

|  | Residential by IPs | Residential by GB |
| --- | --- | --- |
| Billing basis | Fixed package, by IP count | Fixed package, by data volume |
| Traffic limit | Unlimited while the IP is active | Limited to purchased GB |
| Usage period | No expiry until the IPs are used | 180 days, unlimited for Enterprise |
| IP lifetime | A few hours up to ~24 hours | Rotates per request or per session |
| Endpoints | 1 IP = 1 use when forwarded | Unlimited endpoints, only GB deducted |
| Rotation | Via Auto Rotation Proxy on selected ports | Rotating or sticky sessions |
| Authentication | Requires the 9Proxy desktop app (local port forwarding) or Proxy2Web | Username/password or IP whitelisting, straight from the dashboard |
| Setup | Desktop app required for classic IP mode | Works directly in the dashboard |

The practical translation for AdsPower users:

Go **GB-based** if you're running a moderate number of profiles, want sticky sessions that hold an IP for a set number of minutes, and want to paste credentials straight into a profile without installing anything. You buy a block of traffic, generate endpoints in the dashboard as needed, and each AdsPower profile gets its own sticky session ID.

Go **IP-based** if you have a smaller set of high-value accounts you want parked on the same IP for hours at a time, or your data usage per session is heavy and unpredictable. The catch is the workflow: 9Proxy forwards an IP to a local port, so AdsPower points at `127.0.0.1:<port>`. That works fine, since AdsPower runs on the same machine — it just means keeping the forwarding app open.

A newer option sits between the two: **Proxy2Web**, which runs the proxy on 9Proxy's infrastructure and hands you host, port, username and password without a local install. It's on the IP-based side of the product and deducts an IP resource only after a connection succeeds.

## What the whole price list actually looks like

Residential pricing moves around, and 9Proxy announced its first-ever adjustment taking effect June 1, 2026 — IP-based and bundle prices went up, GB-based prices didn't move. The tables below reflect the post-adjustment rates, and the IP tiers are the ones where unused IPs don't expire.

**IP-based packages (unlimited traffic per active IP)**

| Package | Approx. price per IP | Total | Buy |
| --- | --- | --- | --- |
| 100 IPs | $0.24 | $24 | [ Grab the 100 IP starter pack](https://bit.ly/9-Proxy) |
| 500 IPs | $0.144 | $72 | [ Order 500 residential IPs](https://bit.ly/9-Proxy) |
| 1,000 IPs + 500 bonus | $0.084 | $126 | [ Get 1,500 IPs for $126](https://bit.ly/9-Proxy) |
| 2,500 IPs | $0.084 | $210 | [ Compare the 2,500 IP tier](https://bit.ly/9-Proxy) |
| 5,000 IPs | $0.072 | $360 | [ Buy the 5,000 IP package](https://bit.ly/9-Proxy) |
| 15,000 IPs | $0.048 | $720 | [ See the 15,000 IP pricing](https://bit.ly/9-Proxy) |
| 25,000 IPs | ~$0.035 | $863 | [ Check the 25,000 IP tier](https://bit.ly/9-Proxy) |
| 50,000 IPs | ~$0.029 | $1,438 | [ View the 50,000 IP package](https://bit.ly/9-Proxy) |
| 100,000 IPs (Business) | $0.023 | $2,300 | [ Get Business IP pricing](https://bit.ly/9-Proxy) |
| 200,000 IPs (Business) | $0.021 | $4,140 | [ Request the 200,000 IP tier](https://bit.ly/9-Proxy) |
| 500,000 IPs (Business) | $0.018 | $8,625 | [ See 500,000 IP volume rates](https://bit.ly/9-Proxy) |

**GB-based packages**

| Package | Price per GB | Total | Validity | Buy |
| --- | --- | --- | --- | --- |
| 5 GB | $3.00 | $15 | 180 days | [ Try the 5 GB entry package](https://bit.ly/9-Proxy) |
| 50 GB + 5 bonus | $2.10 | $105 | 180 days | [ Buy 55 GB of residential traffic](https://bit.ly/9-Proxy) |
| 100 GB | $1.50 | $150 | 180 days | [ Compare the 100 GB package](https://bit.ly/9-Proxy) |
| 200 GB | $1.00 | $200 | 180 days | [ Order 200 GB of bandwidth](https://bit.ly/9-Proxy) |
| 1,000 GB | $0.80 | $800 | 180 days | [ See the 1,000 GB tier](https://bit.ly/9-Proxy) |
| 2,000 GB | $0.75 | $1,500 | 180 days | [ Check the 2,000 GB package](https://bit.ly/9-Proxy) |
| 3,000 GB (Enterprise) | $0.72 | $2,160 | No expiry | [ View Enterprise 3,000 GB](https://bit.ly/9-Proxy) |
| 6,000 GB (Enterprise) | $0.70 | $4,200 | No expiry | [ View Enterprise 6,000 GB](https://bit.ly/9-Proxy) |
| 10,000 GB (Enterprise) | $0.68 | $6,800 | No expiry | [ View Enterprise 10,000 GB](https://bit.ly/9-Proxy) |

**Bundle packages (IPs + bandwidth combined)**

| Bundle | Contents | Total | Buy |
| --- | --- | --- | --- |
| Starter | 100 IPs + 5 GB | $30 | [ Pick the Starter bundle](https://bit.ly/9-Proxy) |
| Popular | 1,500 IPs + 50 GB | $180 | [ Pick the Popular bundle](https://bit.ly/9-Proxy) |
| Pro | 5,000 IPs + 500 GB | $720 | [ Pick the Pro bundle](https://bit.ly/9-Proxy) |

If you're setting up a first AdsPower farm, the arithmetic is straightforward. A 100-profile setup on IP-based billing runs $24, and those IPs don't expire until used. The same 100 profiles on GB billing with a 5 GB package costs $15, but you're now managing traffic instead of IP count — which gets uncomfortable if any profile streams video, uploads files, or loads heavy pages repeatedly.

The Enterprise tier is a different animal: bandwidth never expires, and it adds a team mode with one owner plus up to five members, per-member traffic controls, and activity logs.

## Setting up 9Proxy in an AdsPower profile, step by step

9Proxy publishes an AdsPower-specific integration guide, and the sequence is short.

1. **Create the proxy session in your 9Proxy dashboard first.** Generate the endpoint you want — pick your targeting, session type, and format. You need real credentials before touching AdsPower.
2. **Open AdsPower and click New Profile**, then move to the Proxy section.
3. **Set Proxy Type to HTTPS or SOCKS5**, matching what you generated. Don't guess here; the wrong protocol type is one of the most common causes of a failed check.
4. **Paste the proxy host and port** from the dashboard.
5. **Build the username correctly.** This is the step people rush. The structured format embeds your targeting and session settings:


<subaccount>-country-<country_code>-st-<state_code>-city-<city_code>-isp-<isp_code>-ssid-<session_id>-sst-<session_time>


A working example looks like `9proxy-country-US-ssid-phTMYuotAy`. Only the parameters you need have to be present. Password is your sub-user password.

6. **Click Check Proxy.** A green pass means the environment is talking to the network. Then click OK to save.

Once the profile is built, click **Open** and confirm the exit IP is where you expect it. Checking the IP inside the browser is worth the extra ten seconds — the checker inside AdsPower and the IP that actually shows up on a target site don't always match, and AdsPower lets you switch IP query channels if a result looks off.

## Targeting and sticky sessions through the username

The username string is where 9Proxy's geo-targeting lives, and it's genuinely useful for AdsPower work rather than just a marketing feature.

- **Country:** `subaccount-country-us` — two-letter code, always the first filter.
- **State:** `st-ohio` — narrows the pool further.
- **City:** `city-newyork` — underscores for multi-word cities.
- **ISP/ASN:** `isp-as22773_Cox_Communications_Inc.` — useful when you want an ISP that matches the rest of a profile's fingerprint.
- **Sticky session:** `sst-15` holds the same IP for 15 minutes.
- **Parallel sticky:** `ssid-id1`, `ssid-id2` — each unique session ID gets its own IP even with identical settings.

That last one is the piece that matters for AdsPower. Each browser profile you want held on a stable IP needs its own `ssid`, otherwise two profiles can end up sharing an exit address — which defeats the point of separate fingerprints.

On the rotating side, if you don't specify `sst` or `ssid` you get a fresh IP per request. That's fine for scraping and price checks, and wrong for anything involving a logged-in account.

One targeting tip from the documentation that's easy to ignore: stacking state, city and ISP filters shrinks the available pool and can push up failure rates. If you're getting connection problems, strip back to country-level targeting first and add filters only when a task actually requires them.

## Batch profiles: same IP, random IP, or Excel

For anything past a few dozen profiles, use the added-proxies list rather than typing credentials into each profile.

In **batch create → quick create**, set Proxy Info to your added proxies and then choose:

- **Custom** — every profile in the batch gets the same IP. Useful when you're building a cluster that should share one exit point.
- **Random** — each new profile gets a different IP pulled from your list. This is what you want for a farm of separate accounts.

If you're driving it from a spreadsheet instead, the `proxyid` column takes either a specific proxy ID or the word `random`, and the `proxy` column accepts `host:port:user:password` — note the format is host, port, user, password in that order, and IPv6 hosts need square brackets, like `[2001:db8::1]:8000:user:password`.

## When AdsPower says "Connection test failed"

Most failures on this exact setup fall into five buckets:

**Wrong protocol type.** SOCKS5 credentials pasted into an HTTP-typed field will fail every time.

**Over-filtered targeting.** A city + ISP combination with thin coverage in that region may return nothing. Reduce to country-level and retry.

**Local network blocking the handshake.** This is the big one for users in mainland China. Local connections often can't complete a handshake with overseas proxies directly. Either run your local connection in global mode or enable AdsPower's system-proxy setting so the browser can use your local tunnel to reach the overseas IP.

**Formatting slippage.** AdsPower can auto-fill fields if you paste the full credential string into the host field, but mixed separators break it. If you're importing in bulk, the documented format uses a colon between each part.

**The IP is dead.** Residential IPs churn naturally. On 9Proxy's IP-based plans an address stays live anywhere from a few hours to roughly 24 hours, and on GB-based plans it rotates by design. A failed check on an old session just means generating a new one.

Also worth knowing: batch import caps at 500 proxies per upload, and AdsPower validates duplicates on save, so re-uploading a list won't create a mess of repeated entries.

## Payment, refunds, and the caveats worth reading first

9Proxy accepts credit and bank cards, Apple Pay, Google Pay, Alipay and crypto through CoinPayments (BTC, ETH, LTC, TRX, USDT-TRC20, USDT-ERC20, DOGE, DAI, BCH). Third-party coverage notes that crypto payments carry an automatic +5% IP bonus.

Two things a careful buyer should check before committing budget:

**The refund terms are narrow.** Independent review coverage of 9Proxy flags that published credit-refund terms essentially cover IPs that die within about 60 seconds, and there's no clearly advertised free trial. If your workflow is unusual — specific sites, specific geographies, specific automation — test with the smallest package that gives you a real answer rather than a large prepayment.

**Streaming is off the table on IP-based plans.** Review coverage reports a policy shift under which 9Proxy no longer supports media streaming such as YouTube on IP-based plans. Confirm current terms if streaming is part of your use case.

On performance, 9Proxy publishes figures of roughly 99.5% success rate, around 0.6s average response time and 99.95% uptime, and claims 20M+ residential IPs across 90+ countries. Treat those as vendor-published numbers rather than guarantees — independent reviews generally land in a similar range without lab-verifying them.

## Quick answers

**Is 9Proxy a preset inside AdsPower?** No. Configure it as a standard HTTPS or SOCKS5 proxy using the host, port, username and password from your dashboard.

**Which 9Proxy model is easier with AdsPower?** GB-based. Credentials come straight from the dashboard, no desktop app needed, and each profile can get its own sticky session.

**Can I use one IP across multiple AdsPower profiles?** Technically yes, and it usually undoes the reason you're using separate profiles. Use a distinct `ssid` per profile.

**Does the auth method matter for anything else?** With IP whitelisting, requests must originate from the whitelisted address, which generally means your own network's public IP. Since AdsPower sends traffic from your machine, username/password authentication is the more flexible choice if your connection IP changes.

If you're building out an AdsPower setup and haven't picked a provider yet, [👉 start a 9Proxy account through this invite link](https://bit.ly/9-Proxy) — the referral code is attached at sign-up, and any applicable discount shows up before you confirm payment. Buy the smallest tier that matches your profile count, get one profile working end to end, and scale the batch only after the check passes.
