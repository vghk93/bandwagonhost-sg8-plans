# singapore vps: BandwagonHost SG_8 plans, CN2 GIA routing, and how to pick the right config

When you type "singapore vps" into a search box, you're usually after one of three things: a low-latency box for Chinese visitors, a Southeast Asia hub that doesn't fall over during evening peak hours, or just a clean Singapore IP for services that geo-fence by region. BandwagonHost's SG_8 line — launched in 2026 and sitting inside Equinix SG1 — is the option most people land on once they realize the cheapest SG VPS rarely comes with usable China routing. This guide walks through what SG_8 actually is, how the six plans differ, where the real discounts are, and how it compares against the older SG_1 and BandwagonHost's other Asian CN2 GIA locations.

## Why "singapore vps" usually means CN2 GIA or nothing

Most Singapore VPS listings you'll find on LowEndTalk or HostAdvice are fine for serving Southeast Asia — Malaysia, Indonesia, Vietnam, Thailand — but they hit a wall the moment traffic has to come back into mainland China. The default route is AS4134 (ChinaNet/163), and during peak hours that network runs 30%+ packet loss. BandwagonHost spells this out on their own CN2 GIA explainer page: at that loss rate you can't reliably serve web content, hold a video call, or keep a game session alive.

SG_8's selling point isn't the hardware, it's the routing. Return traffic to mainland China rides:

- **China Telecom** via CN2 GIA (AS4809)
- **China Mobile** via CMI / CMIN2 (AS58807)
- **China Unicom** via the premium AS10099 / AS4837 path

That "triple-network" return is what separates SG_8 from random Singapore boxes. If your visitors are all in China, the routing matters more than the CPU model. If your visitors are all in ASEAN, you're paying for routing you don't need — and a cheaper SG provider would do the job.

## BandwagonHost SG_8 datacenter: what you're actually getting

SG_8 is BandwagonHost's second-generation Singapore location, distinct from the older SG_1.

| Spec | SG_8 | SG_1 (older) |
| --- | --- | --- |
| Datacenter | Equinix SG1 | Singapore (non-Equinix) |
| CPU | AMD EPYC Genoa | AMD EPYC (older Gen) |
| Storage | NVMe SSD | SSD / NVMe mix |
| Return routing | Triple-network CN2 GIA | Triple-network CN2 GIA |
| Entry price | $49.99/mo | $89.99/mo (via HK migration) |
| How to get it | Direct purchase | Migration from HK CN2 GIA plans |

Equinix SG1 is one of the bigger internet exchange hubs in Southeast Asia — Google, Cloudflare, NTT and a pile of carriers have nodes in or around it. That matters less for China routing (which is handled by the CN2 GIA transit) and more for peering to the rest of the region. If part of your traffic is going to Malaysian or Indonesian eyeballs, SG_8 has shorter paths to those networks than a random SG DC.

The AMD EPYC Genoa platform is the same family BandwagonHost rolled out across HK3/HK8, LA DC9, and New York in 2025–2026. On the 2GB plan you get 2 cores, on 64GB you get 12. Storage is NVMe across the board — no RAID-10 SAS leftover from the old days.

## Full SG_8 plan lineup and pricing

SG_8 is sold as its own product line, not as a config-option on the generic KVM plans. Here are all six currently listed plans, with monthly and annual pricing straight from the SG_8 order page.

| Plan | RAM | vCPU | NVMe | Monthly traffic | Port | Monthly | Annual | Order |
| --- | --- | --- | --- | --- | --- | --- | --- | --- |
| Singapore 2GB | 2 GB | 2 | 40 GB | 0.5 TB | 1.5 Gbps | $49.99 | $499.99 | [Order SG_8 2GB](https://bwh81.net/aff.php?aff=77528&pid=173) |
| Singapore 4GB | 4 GB | 4 | 80 GB | 1 TB | 1.5 Gbps | $86.99 | $869.99 | [Order SG_8 4GB](https://bwh81.net/aff.php?aff=77528&pid=174) |
| Singapore 8GB | 8 GB | 6 | 160 GB | 2 TB | 2.5 Gbps | $165.99 | $1,665.99 | [Order SG_8 8GB](https://bwh81.net/aff.php?aff=77528&pid=175) |
| Singapore 16GB | 16 GB | 8 | 320 GB | 4 TB | 2.5 Gbps | $329.99 | $3,199.00 | [Order SG_8 16GB](https://bwh81.net/aff.php?aff=77528&pid=176) |
| Singapore 32GB | 32 GB | 10 | 640 GB | 6 TB | 5 Gbps | $549.99 | $5,549.99 | [Order SG_8 32GB](https://bwh81.net/aff.php?aff=77528&pid=177) |
| Singapore 64GB | 64 GB | 12 | 1,280 GB | 8 TB | 5 Gbps | $1,059.99 | $10,559.99 | [Order SG_8 64GB](https://bwh81.net/aff.php?aff=77528&pid=178) |

A few things worth noting before you click anything:

**Annual billing is roughly "pay 10, get 12."** On the 2GB plan, $49.99 × 12 = $599.88 vs. $499.99 yearly — about $100 saved, or two months free. The savings scale roughly proportionally up the lineup. If you've already decided SG_8 fits your use case, annual is the obvious call.

**Bandwidth is tied to plan size, not a free choice.** 2GB and 4GB sit on 1.5 Gbps, 8GB and 16GB on 2.5 Gbps, and only the 32GB/64GB plans get the full 5 Gbps port. You can't pay extra to bump the 2GB plan to 5 Gbps — you have to go up a tier.

**Traffic caps are real.** 0.5 TB on the 2GB plan is fine for a blog or business site, but if you're proxying media or running a CDN origin, you'll eat through it. Overages aren't billable at a flat rate — BandwagonHost will throttle or suspend once you blow past the quota, depending on plan. Pick the plan by traffic first, then by RAM.

**Singapore is geographically far from China.** Even with CN2 GIA on the return path, latency to mainland China sits in the 60–125 ms range depending on city and carrier. Hong Kong (HKHK_8) is closer and usually 30–60 ms lower. You're choosing SG_8 when you need balanced three-carrier routing and Southeast Asia reach, not when you need the absolute lowest ping to Beijing.

## Which SG_8 plan actually fits what you're doing

The temptation is to grab the 2GB plan because it's the cheapest. Sometimes that's right, sometimes it's a false economy.

**2GB — $49.99/mo.** Fine for a single WordPress site, a static company page, a small Ghost blog, or a tunnel endpoint that doesn't do much local work. 0.5 TB is the real constraint, not the RAM. If your site gets featured anywhere with Chinese traffic, you'll hit the cap inside a week.

**4GB — $86.99/mo.** The sweet spot for e-commerce (WooCommerce, Shopify-style self-hosted), small business sites with a real database, and the cheapest plan where 1 TB traffic gives you headroom. Also the minimum I'd consider for running n8n, Dify, or Open WebUI — those AI workflow tools will OOM on 2GB the moment you load a real model.

**8GB — $165.99/mo.** Multiple websites, CI/CD runners, lightweight AI inference (small LLMs, embeddings), or a shared dev box for a small team. This is also where you jump to 2.5 Gbps port speed, which matters if you're pushing builds or large containers.

**16GB — $329.99/mo.** Production apps with real concurrency, mid-size teams, local model hosting that actually stays responsive. Still 2.5 Gbps.

**32GB / 64GB — $549.99 / $1,059.99/mo.** 5 Gbps port, 6–8 TB traffic. These are enterprise-tier and priced accordingly. You buy them when you have a specific workload — high-traffic CDN origin, multi-user proxy with media, large model hosting — not "just in case."

If you're uncertain, the 4GB plan is the safest middle. The 2GB exists for tight budgets, the 8GB is where the port speed and traffic both step up meaningfully.

## SG_8 vs SG_1: which Singapore location to pick

BandwagonHost has two Singapore locations and they're not interchangeable.

SG_1 launched in 2024 and is the older Singapore DC. It runs triple-network CN2 GIA routing just like SG_8, but on an older AMD EPYC generation, and — critically — **you cannot buy SG_1 directly**. The only way onto SG_1 is to purchase a Hong Kong CN2 GIA plan and migrate it via KiwiVM, and migration slots aren't always available.

SG_8 (2026) is the one you can buy off the shelf. Newer Genoa CPUs, NVMe across the board, hosted in Equinix SG1, and roughly 44% cheaper at entry level ($49.99 vs. $89.99 for the comparable SG_1 plan after migration).

For new customers, the answer is almost always SG_8. The only reason to chase SG_1 is if you already own a Hong Kong CN2 GIA VPS and want a second Asia location without buying a new product.

## SG_8 vs Hong Kong, Tokyo, Osaka CN2 GIA

BandwagonHost runs four Asian CN2 GIA locations. Picking between them comes down to geography and price.

| Location | Code | Entry price | Entry port | Return routing | Best for |
| --- | --- | --- | --- | --- | --- |
| Singapore | SG_8 | $49.99/mo | 1.5 Gbps | Triple-network CN2 GIA | ASEAN reach + balanced China carriers |
| Hong Kong | HKHK_8 | $89.99/mo | 1 Gbps | China Telecom CN2 GIA | Lowest latency to mainland China |
| Tokyo | JPTYO_8 | $89.99/mo | 1.2 Gbps | China Telecom CN2 GIA | Japan IP / Japan-focused services |
| Osaka | JPOS_6 | $49.99/mo | 1.5 Gbps | China Telecom CN2 GIA | Value pick, lower latency than SG |

A few practical takeaways from this table:

**Hong Kong wins on latency, loses on price.** If your entire audience is in mainland China and you want the lowest possible ping, HKHK_8 is the right answer. You pay $40/month more for the privilege and give up half a Gbps of port speed at entry level.

**Osaka is the value alternative to SG_8.** Same $49.99 entry price, same 1.5 Gbps port, usually lower latency to China because Japan is closer. The trade-off: Osaka runs China Telecom CN2 GIA only, not the triple-network routing. China Unicom and China Mobile users see less consistent performance than on SG_8.

**SG_8 is the pick when China Unicom and China Mobile matter.** Most CN2 GIA locations optimize hard for China Telecom and treat the other two carriers as an afterthought. SG_8's triple-network return is the differentiator — if your users are split across all three carriers, SG_8 gives the most consistent experience across the board.

**SG_8 is the only one that's also a real ASEAN hub.** Equinix SG1 has direct peering to Malaysian, Indonesian, Vietnamese, and Thai networks. If you're serving a regional audience and China is part of it but not all of it, SG_8 covers both sides.

## How to actually order an SG_8 plan

The flow is straightforward but the promo code step is easy to miss.

1. **Pick a plan** from the SG_8 lineup above and click through to the order page.
2. **Choose billing cycle** — monthly or annually. Annual unlocks the ~2-months-free discount automatically.
3. **Configure location.** For SG_8 plans the location is fixed to Singapore; you don't need to pick a DC.
4. **Enter the promo code** in the "Promo Code" field on the checkout page. Apply it before proceeding to payment — the discount recalculates the cart total inline.
5. **Pay via PayPal or account balance.** Provisioning is usually instant; you'll get KiwiVM login credentials by email.

If you already have a BandwagonHost account, the new SG_8 VPS shows up alongside your existing services in the client area. If you're brand new, the account is created during checkout.

## Current promo codes and how much they actually save

BandwagonHost runs a recurring-discount promo code system. The codes below are the ones currently in circulation, sourced from BandwagonHost's own coupon listings and third-party trackers that mirror them.

| Code | Discount | Applies to | Notes |
| --- | --- | --- | --- |
| **BWHCGLUKKB** | 6.78% recurring | All VPS plans, including SG_8 | Highest discount currently active; applies every billing cycle, not just first |
| BWH1ZBPVK | 6.00% recurring | Most VPS plans | Slightly below the top code |
| BWH1XZOBK | 5.50% recurring | Most VPS plans | — |
| ireallyreadtheterms8 | 5.50% recurring | Most VPS plans | Older long-running code |
| BWH1NJJHL | 4.50% recurring | Most VPS plans | — |

**BWHCGLUKKB is the one to use.** The 6.78% is recurring, meaning it shaves the same percentage off every renewal, not just the first invoice. On the SG_8 2GB annual plan that's $499.99 → roughly $466.10, saving about $33.89/year. On the 8GB monthly plan it's $165.99 → $154.74, about $11.25/month back in your pocket. The savings scale with the plan you pick.

The other codes exist mostly for cases where the top code has been pulled or restricted on a specific product. As of right now, BWHCGLUKKB works on SG_8 — use it.

To apply: paste the code into the "Promo Code" field at checkout and click Apply. The cart total updates immediately. If it doesn't, the code may have been deactivated for that product — try the next one down the list.

## KiwiVM: what you actually get after purchase

Every BandwagonHost VPS is managed through KiwiVM, their in-house control panel. You don't need to install anything — it's web-based and tied to your account.

The relevant features for SG_8 specifically:

- **Start/stop and OS reinstall.** Over 20 OS templates including AlmaLinux, RockyLinux, CentOS, Debian, Ubuntu (26.04 is now supported), CentOS Stream, and Fedora. 32-bit and 64-bit both available.
- **Datacenter migration.** This is how you'd move a CN2 GIA-E plan into Singapore if you wanted SG_1 (not SG_8). SG_8 itself is purchased directly, not migrated into.
- **Snapshots.** Manual point-in-time backups. Useful before OS upgrades or risky config changes.
- **rDNS (PTR) management.** Set the reverse DNS for your IP without a support ticket.
- **Emergency console.** Out-of-band access when SSH is broken.
- **API.** Programmable control for automation.

KiwiVM is self-managed by design — BandwagonHost keeps prices down by not bundling managed support. If you need someone to fix your nginx config for you, this isn't the provider. If you can run your own box, you get a clean panel and don't pay for hand-holding you won't use.

## Network performance and China latency: what to realistically expect

BandwagonHost publishes latency numbers for SG_8 that line up with third-party testing. Real-world RTT to major Chinese cities sits roughly in these ranges under normal conditions:

- **Beijing (China Telecom)**: ~125 ms
- **Shanghai (China Telecom)**: ~70 ms
- **Guangzhou (China Telecom)**: ~46 ms
- **Beijing (China Unicom)**: ~108 ms
- **Shanghai (China Unicom)**: ~67 ms
- **Guangzhou (China Unicom)**: ~74 ms

These are routing-optimized numbers — without CN2 GIA, the same paths run 200+ ms with 20–30% peak-hour loss. The CN2 GIA backbone is what makes the difference, and it's why BandwagonHost charges what they charge.

A few honest caveats:

- **Latency is distance-limited.** No routing trick makes Singapore physically closer to Beijing. If you need <30 ms to China, you need Hong Kong.
- **Peak-hour stability is the real win.** The 30% packet loss on regular AS4134 transit during evening rush is what CN2 GIA eliminates. On SG_8, peak-hour loss is effectively zero under normal conditions.
- **CN2 GIA has limited DDoS tolerance.** BandwagonHost explicitly notes this on their CN2 GIA page: under attack, they null-route the affected IP rather than absorbing the flood. If you're running something attack-prone, plan for that.
- **Port speed is uplink, not throughput guarantee.** The 1.5–5 Gbps figure is the link speed to the upstream. Real-world throughput depends on the remote end, the path, and congestion. The 5 Gbps plans can actually push close to line rate to well-peered destinations; the 1.5 Gbps plans typically sustain 1–1.4 Gbps in practice.

## Use cases where SG_8 is the right call

Based on the routing, pricing, and specs above, SG_8 fits a specific set of workloads better than the alternatives.

**Sites serving a mix of China and ASEAN traffic.** If your audience spans Guangzhou, Kuala Lumpur, and Jakarta, SG_8 is the single location that handles both without compromise. Hong Kong is great for China but worse for ASEAN; Tokyo is fine for China but adds latency to Southeast Asia.

**Teams with users across all three Chinese carriers.** Most CN2 GIA providers over-optimize for China Telecom. SG_8's triple-network return means China Unicom and China Mobile users get a comparable experience, not the afterthought path they usually get.

**AI workflow hosting on a budget.** The 4GB and 8GB plans are priced low enough to run Dify, n8n, Open WebUI, or Langflow without renting a GPU box. The Singapore location gives acceptable latency to Chinese operators who need to interact with the tools, and NVMe storage handles the model files without dragging.

**Proxy or tunnel endpoints for China users who need a stable Asia IP.** The triple-network routing keeps the connection stable during peak hours when cheaper SG VPS options start dropping packets. Singapore also has fewer geopolitical IP-reputation issues than some HK ranges.

**CDN origin or file distribution with China-facing audience.** The 32GB and 64GB plans with 5 Gbps ports and 6–8 TB traffic are built for this. Pair with a China CDN for the actual edge delivery; use SG_8 as the origin.

## When SG_8 is the wrong pick

Equally important — SG_8 isn't always the answer.

**If your audience is purely mainland China and you want lowest ping.** Hong Kong HKHK_8 is the right choice. You'll pay $40/month more at entry level and get less port speed, but latency is meaningfully lower and China Telecom performance is unbeatable.

**If you need a Japan IP for licensing or service requirements.** Tokyo JPTYO_8 is what you want. Same CN2 GIA routing quality, Japan IP, similar pricing.

**If you're purely serving ASEAN and don't care about China.** A cheaper non-CN2 Singapore VPS will do the same job for less. You're paying a premium for routing you won't use.

**If you need managed support.** BandwagonHost is self-managed. The KiwiVM panel is clean, the network is solid, but nobody is going to debug your config files for you. Look elsewhere if you need a managed tier.

**If you expect to absorb DDoS attacks.** CN2 GIA's limited capacity means BandwagonHost null-routes under attack rather than mitigating. For attack-prone workloads, look at AS4134-based providers that can tank floods.

## Bottom line on singapore vps and BandwagonHost SG_8

If you got here by searching "singapore vps," the question you're really asking is probably "which SG VPS won't fall apart when my Chinese users hit it at 9 PM." SG_8 is the most coherent answer in BandwagonHost's lineup for that specific problem. It's not the cheapest Singapore VPS on the market, and it's not the lowest-latency option for China — but it's the one that combines real CN2 GIA routing across all three Chinese carriers, modern EPYC Genoa hardware, NVMe storage, and a $49.99 entry price that undercuts Hong Kong and Tokyo by $40/month.

For most readers, the **4GB plan at $86.99/month with promo code BWHCGLUKKB** is the practical pick — enough RAM for real workloads, 1 TB of traffic for headroom, and the same 1.5 Gbps port as the 2GB plan. Step up to 8GB ($165.99) when you need the 2.5 Gbps port or you're running AI tools. Step down to 2GB ($49.99) only if the budget is hard-capped and traffic will stay light.

Whatever you pick, use the recurring promo code at checkout — there's no reason to pay full price when the discount applies to every renewal.

👉 [View all SG_8 plans and order](https://bit.ly/BandWaGon)
