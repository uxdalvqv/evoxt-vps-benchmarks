# Evoxt VPS Benchmark Deep Dive: Does the 6.0 GHz CPU Claim Hold Up Under Independent Testing? VM-1 to VM-16 Performance Showdown Across Web, CPU, Disk I/O & Network — Plus the 40% Recurring Discount You Shouldn't Miss

There's something quietly satisfying about running a benchmark on a VPS you paid less than six bucks for and watching it punch above its weight. I've been there — refreshing the sysbench output at 1 a.m., half-expecting the numbers to collapse the moment the test gets serious, and instead seeing the CPU hold steady at 4.5 GHz while the disk churns through random writes like it actually means it.

That's the corner of the internet Evoxt has been quietly carving out since 2020. Headquartered in Malaysia, this provider built its entire pitch around one stubborn idea: most cloud companies are running CPUs at 2.3–2.4 GHz and hoping nobody notices, so why not do the opposite? Throw fast silicon at the problem, keep the prices boring, and let the benchmarks speak for themselves.

So let's actually look at what the benchmarks say — not the marketing copy, the independent third-party numbers from VPSBenchmarks, which has been buying and testing Evoxt servers for years. That's the whole point of searching "evoxt vps benchmark" in the first place: you want the unvarnished version.

## Why a Benchmark Matters More Than a Spec Sheet

Anyone can write "up to 6.0 GHz" on a pricing page. The question is what happens when an independent lab rents the server, installs Ubuntu, and runs Geekbench, fio, iperf3, sysbench, and a 24-hour endurance test against it. VPSBenchmarks has done exactly this across multiple Evoxt plans — VM-1, VM-2, VM-4, and VM-8 — and the results tell a more nuanced story than the headline frequency suggests.

Here's the part worth understanding before we get into the numbers: a "grade" from VPSBenchmarks isn't a pass/fail. It's a relative ranking. A VM-2 scoring a D in raw CPU power might still outperform another provider's VM-2 in the same price band — the grade reflects performance against the entire field, not against some absolute ceiling. That distinction matters a lot when you're reading Evoxt's results, because the pricing is aggressive enough that even middling grades often represent excellent value per dollar.

## The CPU Story: Single-Core Speed Is the Whole Point

Across every Evoxt trial VPSBenchmarks has published, the CPU story is consistent. The VM-1 trial in February 2026 ran on an AMD EPYC-Genoa processor in Paris, France, with an observed starting frequency of 4.5 GHz. The VM-8 trial in May 2026, deployed in Frankfurt, Germany, started at 4.3 GHz on the same EPYC-Genoa family. The VM-2 trial in September 2025, deployed in Malaysia, ran on an EPYC-Milan processor at 4.2 GHz.

| Plan | Trial Date | Location | CPU Family | Starting Frequency | Overall Score |
| --- | --- | --- | --- | --- | --- |
| VM-1 | Feb 25, 2026 | Paris, France | AMD EPYC-Genoa | 4.5 GHz | 53 |
| VM-2 | Sep 03, 2025 | Malaysia | AMD EPYC-Milan | 4.2 GHz | 34 |
| VM-4 | Nov 30, 2025 | — | — | — | 60 |
| VM-8 | May 24, 2026 | Frankfurt, Germany | AMD EPYC-Genoa | 4.3 GHz | 62 |

These are price-weighted scores out of 100, so they already account for what you're paying. A VM-8 at $47.99/month scoring 62 isn't shabby. A VM-1 at $5.99/month scoring 53 is genuinely impressive for the price.

The VM-8 trial is the one that really shows the upside. It pulled an **A grade in both web performance and raw CPU power** — 17.00/20 and 18.09/20 respectively. That's the kind of result you'd expect from a much more expensive box. Web performance on an 8-core/16GB NVMe server responding to locally generated HTTP requests, scoring an A, translates into a server that can genuinely absorb traffic without breaking a sweat.

But the same VM-8 trial scored a **D in performance stability and an E in network performance**. That's the honest caveat: raw compute is excellent, but sustained 24-hour CPU endurance and outbound network throughput aren't where Evoxt wins. If your workload is bursty single-threaded stuff — WordPress, a Discord bot, a small game server, a dev compile loop — the VM-8 is a monster. If you're saturating a 1 Gbps port 24/7 shifting large files to distant endpoints, you'll feel the network grade.

## Disk I/O: Solid, Not Spectacular

The disk I/O picture is more mixed than the CPU picture. The VM-1 trial scored a **B in disk IO performance** (14.53/20) — solid for a $5.99 server with a 20 GB NVMe drive. The VM-8 trial dropped to a **C** (10.89/20), and the VM-2 trial managed only a D (9.62/20).

What this means in practice: for the typical web/database workload with mixed random reads and writes, Evoxt's NVMe storage is more than adequate. The Reddit user who benchmarked a South Korea deployment and reported I/O speeds up to 1900 MB/s on AMD EPYC 9004 nodes wasn't exaggerating — sequential throughput is genuinely fast. The weaker grade is in the mixed random I/O workload that VPSBenchmarks uses, which is a tougher, more realistic test than a pure sequential read.

If you're running a database with a hot working set, you'll be fine. If you're trying to push the absolute limits of random 4K write IOPS against a saturated queue, you'll find the ceiling faster than you would on a higher-end provider charging three times the price.

## Network Performance: The Honest Weakness

Let's be straight about this: network performance is Evoxt's weakest dimension across the trials. The VM-2 trial scored an **F in network performance** (3.08/20). The VM-8 trial scored an E (6.37/20). The VM-1 trial scored a D (7.66/20).

This isn't because Evoxt's network is broken — it's because VPSBenchmarks measures outbound transfer speed to nearby servers, and Evoxt's 1 Gbps ports, while adequate, don't have the kind of multi-gigabit bursting that higher-end providers offer. For most users, 1 Gbps is plenty. For users who specifically need to push a lot of bandwidth out — large CDN origin serving, heavy video transcoding output, big dataset replication — this is where you'll feel the limit.

The Reddit complaints about packet loss from mainland China to certain Evoxt IPv4 addresses are also worth noting if your audience is in China. The premium Asian regions (Hong Kong, Osaka) exist precisely to address this, with direct routing to regional ISPs, but the standard regions can have uneven reachability from the Chinese mainland. If China access matters to you, pick the Hong Kong or Osaka premium region and test before committing.

## The Full Plan Lineup: All 11 Tiers, Three Network Tiers

Evoxt's pricing structure is unusually transparent. There are three network tiers — Standard, Premium, and Premium Plus — and within each tier the same 11 plans run from VM-0.5 (the $2.99 entry point) up to VM-16 (the $95.99 16-core/32GB flagship). The plan names and base prices are identical across tiers; only the monthly bandwidth allocation changes.

### Standard Network Regions

Coverage: United States, United Kingdom, Canada, Germany, Poland, Amsterdam, Japan (Tokyo), Malaysia, Australia.

| Plan | CPU | RAM | Storage | Transfer | Backup | Price | Deploy |
| --- | --- | --- | --- | --- | --- | --- | --- |
| VM-0.5 | 1 core (up to 6.0 GHz) | 512 MB | 5 GB NVMe | 500 GB | Weekly | $2.99/mo |  [Deploy VM-0.5](https://bit.ly/EvoXt) |
| VM-0.75 | 1 core (up to 6.0 GHz) | 1 GB | 10 GB NVMe | 750 GB | Weekly | $4.99/mo |  [Deploy VM-0.75](https://bit.ly/EvoXt) |
| VM-1 | 1 core (up to 6.0 GHz) | 2 GB | 20 GB NVMe | 1,000 GB | Weekly | $5.99/mo |  [Deploy VM-1](https://bit.ly/EvoXt) |
| VM-1.5 | 2 cores (up to 6.0 GHz) | 2 GB | 20 GB NVMe | 1,500 GB | Weekly | $6.95/mo |  [Deploy VM-1.5](https://bit.ly/EvoXt) |
| VM-2 | 2 cores (up to 6.0 GHz) | 4 GB | 30 GB NVMe | 2,000 GB | Weekly | $11.99/mo |  [Deploy VM-2](https://bit.ly/EvoXt) |
| VM-3 | 4 cores (up to 6.0 GHz) | 4 GB | 30 GB NVMe | 3,000 GB | Weekly | $14.99/mo |  [Deploy VM-3](https://bit.ly/EvoXt) |
| VM-4 | 4 cores (up to 6.0 GHz) | 8 GB | 60 GB NVMe | 4,000 GB | Weekly | $23.99/mo |  [Deploy VM-4](https://bit.ly/EvoXt) |
| VM-6 | 8 cores (up to 6.0 GHz) | 8 GB | 60 GB NVMe | 5,000 GB | Weekly | $29.99/mo |  [Deploy VM-6](https://bit.ly/EvoXt) |
| VM-8 | 8 cores (up to 6.0 GHz) | 16 GB | 80 GB NVMe | 6,000 GB | Weekly | $47.99/mo |  [Deploy VM-8](https://bit.ly/EvoXt) |
| VM-12 | 16 cores (up to 6.0 GHz) | 16 GB | 80 GB NVMe | 8,000 GB | Weekly | $60.95/mo |  [Deploy VM-12](https://bit.ly/EvoXt) |
| VM-16 | 16 cores (up to 6.0 GHz) | 32 GB | 100 GB NVMe | 10 TB | Weekly | $95.99/mo |  [Deploy VM-16](https://bit.ly/EvoXt) |

### Premium Network Regions

Coverage: Hong Kong, Japan (Osaka). Same plan names and prices; transfer allocations roughly halved to reflect the more expensive Asian transit. Useful when latency to East Asian audiences is the priority.

### Premium Plus Network Region

Coverage: Malaysia (Premium). Same plan names; VM-0.5 starts at $3.49/mo (a 50¢ premium over Standard) and transfer allocations are the smallest of the three tiers. Pick this only if you specifically need the premium Malaysian routing.

## The 40% Recurring Discount: Not a Gimmick

This is the part that genuinely changes the math. Evoxt runs a **40% recurring discount** applicable to VM-1 and all higher plans. The word "recurring" is doing the heavy lifting here — this isn't a first-month tease that reverts to full price on renewal. The discount sticks every billing cycle.

The codes currently circulating for 2026:

- **`EVOXT595`** — 40% off recurring on Cloud VMs (VM-1 and above)
- **`BHW595`** — similar recurring structure, community-sourced
- **`AFF1129-hostspot`** — 40% recurring discount for Cloud Virtual Machines

Apply `EVOXT595` to the VM-1 plan and the $5.99/month drops to roughly **$3.59/month, permanently**. One core up to 6.0 GHz, 2 GB RAM, 20 GB NVMe, 1 TB transfer, weekly offsite backups — for less than the price of a fancy coffee. The VM-0.5 entry plan at $2.99 isn't eligible for the percentage discount, but at that price point it's already the cheapest ticket in.

👉 [Apply the recurring discount and deploy your Evoxt VM](https://bit.ly/EvoXt)

## What the Benchmarks Mean for Each Plan Tier

### VM-0.5 and VM-0.75: The Entry Tier

At $2.99 and $4.99, these are explicitly starter machines — 512 MB and 1 GB of RAM respectively, with 5–10 GB of storage. They haven't been independently benchmarked by VPSBenchmarks (the lab tends to test the mid-tier and upper-tier plans where the performance story is more interesting), but the same EPYC-Genoa / EPYC-Milan CPUs run across the entire fleet. For a personal VPN, a tiny monitoring agent, or a DNS resolver, these are genuinely usable. Don't expect to host a WordPress site on 512 MB in 2026.

### VM-1: The Sweet Spot for Single-Threaded Workloads

The Feb 2026 trial is the headline result here. Overall score of 53 (price-weighted), with a **B in web performance and a B in disk I/O**. The E grade in raw CPU power looks alarming until you remember: this is a 1-core VM being graded against the entire VPS field including 16-core boxes. Per-core, the 4.5 GHz EPYC-Genoa is genuinely fast. The 2 minutes 20 seconds provisioning time is also worth noting — that's quick.

For a single WordPress site, a Discord bot, a small Nextcloud instance, or a dev environment, VM-1 with the 40% recurring discount applied (so ~$3.59/month) is the value play. This is the plan I'd reach for first.

### VM-2: The Honest Caveat

The Sep 2025 trial of VM-2 is the weakest result in Evoxt's recent benchmark history. Overall score of 34, with grades of D, D, E, D, F across the five categories. The 10-minute provisioning time was also the slowest in the recent trials.

This is the part where I have to be straight: if you're choosing between VM-1 and VM-2 based on benchmarks alone, VM-1 looks like the better value. VM-2 doubles the cores and RAM but the benchmark scores don't scale proportionally, and the network F grade is a real concern if outbound throughput matters to you. That said, the Malaysia deployment in this trial may not represent the performance you'd see in Frankfurt or Paris — VPSBenchmarks runs each trial in a single location, and regional variation is real. The VM-2 plan itself isn't broken; this specific trial was unlucky.

### VM-4 and VM-8: Where the High-Frequency CPU Shines

The VM-4 trial in November 2025 scored 60 overall, and the VM-8 trial in May 2026 scored 62 with those A grades in web performance and raw CPU power. This is where Evoxt's whole thesis pays off. When you have 8 fast cores running at 4.3+ GHz, single-threaded workloads fly and multi-threaded workloads have enough headroom to breathe.

For a small-to-mid production web app, a medium-traffic database, or a build server for a development team, VM-4 ($23.99) or VM-8 ($47.99) is where the benchmarks actually justify the spend. With the 40% recurring discount, VM-4 drops to around $14.39/month and VM-8 to roughly $28.79/month — at which point the price-to-performance ratio gets hard to argue with.

### VM-12 and VM-16: The Flagship Tier

These haven't been independently benchmarked by VPSBenchmarks, but they share the same EPYC-Genoa infrastructure as the VM-8 trial. VM-16 at $95.99/month (or ~$57.59 with the recurring discount) gets you 16 cores, 32 GB RAM, 100 GB NVMe, and 10 TB of transfer. That's not enterprise-grade, but it's a serious mid-tier server at a price point where most competitors are offering half the RAM.

## Data Center Footprint: 13 Countries, 17 Locations

Evoxt operates data centers across 13 countries, with 17 total locations:

- **North America**: Los Angeles, New York, Montreal
- **Europe**: London, Paris, Amsterdam, Frankfurt, Warsaw, Zurich
- **Asia-Pacific**: Tokyo, Osaka, Hong Kong, Malaysia (standard and premium), Indonesia, South Korea, Australia

The Los Angeles location has direct links to China Unicom and multiple APAC ISPs — useful if you're serving traffic that crosses the Pacific. The South Korea location runs on the KT backbone, which Reddit users have noted provides solid direct routes to Chinese ISPs. The Asian premium regions (Hong Kong, Osaka) trade roughly half the bandwidth allocation for better routing to East Asian end-users.

## What's Included Beyond the Specs

A few things that don't show up in the benchmark numbers but matter in practice:

- **Weekly automatic offsite backups** are included on every plan — not snapshots on the same physical disk, actual offsite backups restorable from the control panel. This is genuinely unusual at this price point.
- **Windows VPS at Linux prices** — no licensing surcharge. If you've priced Windows Server hosting elsewhere, you know this is a real differentiator.
- **KVM virtualization** with dedicated CPU and RAM allocation — your neighbors' workloads don't eat into your resources.
- **IPv4 and IPv6 both included** on every deployment. Some providers still charge extra for IPv6.
- **Cryptocurrency payments** accepted (Bitcoin, Litecoin, Ethereum, USDt Tron) alongside credit cards, debit cards, and PayPal.
- **Layer 3 firewall** configurable from the control panel, no SSH required.
- **24-hour refund policy** — effectively a risk-free trial if you deploy and dislike it.

👉 [See all included features and deploy your VM](https://bit.ly/EvoXt)

## Who Should Actually Use Evoxt Based on the Benchmarks

For **developers and side projects**, the VM-1 plan with the 40% recurring discount is the obvious entry point. The benchmark scores are good for the price, the 4.5 GHz single-core speed makes dev environments feel responsive, and the weekly offsite backups mean you won't lose your work to a bad config change.

For **small-to-mid production web apps**, VM-4 or VM-8 is where the benchmarks justify themselves. The A grades in web performance and raw CPU power on the VM-8 trial are the real deal — that's a server that can absorb traffic without you nervously watching the load average.

For **game servers** (Minecraft, Valheim, small multiplayer), the high single-core frequency is exactly what you want. Game server tick rates live and die on single-thread performance.

For **Asia-Pacific-focused projects**, the premium Hong Kong and Osaka regions are worth the reduced bandwidth allocation. The standard regions can have uneven reachability from mainland China.

For **Windows-specific workloads**, the zero licensing surcharge is the headline. You're paying Linux prices for a Windows VPS.

## The Honest Downsides

This isn't a perfect product, and pretending otherwise doesn't help anyone.

**Network performance is the weakest dimension.** The F grade on the VM-2 trial and the E grade on the VM-8 trial are real. If your workload is bandwidth-heavy — large CDN origin serving, constant large file replication, video transcoding output — you'll hit the ceiling faster than you would on a higher-end provider.

**Support can be slow during peak times.** Ticket response times occasionally stretch to 48 hours. Discord and Telegram channels tend to move faster if you're already in those communities.

**Dedicated servers are currently only available in Malaysia**, with expansion in progress. If you need dedicated hardware outside Malaysia right now, you're waiting.

**The company is young.** Founded in 2020 means less than six years of track record. The benchmarks and reviews are good, but Evoxt hasn't been through multiple economic cycles the way the established names have.

**China reachability from standard regions is inconsistent.** If your audience is in mainland China, pick Hong Kong or Osaka premium regions and test before committing — the standard-region IPv4 addresses can have packet loss issues from Chinese networks.

## The Short Version

If you've been searching "evoxt vps benchmark" because you're trying to figure out whether the 6.0 GHz CPU claim is real or marketing fluff — the independent testing says it's real. The EPYC-Genoa processors in the recent trials ran at 4.3–4.5 GHz observed, the single-core performance is genuinely strong, and the price-weighted scores from VPSBenchmarks consistently place Evoxt in the top tier of budget VPS providers.

The CPU and web performance are the upside. The network performance and long-term stability are the honest weaknesses. The 40% recurring discount on VM-1 and above — codes `EVOXT595`, `BHW595`, or `AFF1129-hostspot` — is the cherry on top, dropping the VM-1 plan to roughly $3.59/month permanently.

For the right workload — single-threaded apps, dev environments, game servers, small-to-mid web apps, Windows-specific workloads — the benchmarks justify the spend. For bandwidth-saturated or China-mainland-facing workloads, look carefully at the premium Asian regions and test before you commit.

Start with VM-1 at the discounted rate, run your own yabs.sh test, and see how the numbers look for your specific location. The 24-hour refund policy means the downside is genuinely small.

👉 [Deploy an Evoxt VPS and benchmark it yourself](https://bit.ly/EvoXt)
