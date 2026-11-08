# Linux Cloud Server Guide: What $12/Month Buys, How Much RAM You Need, and the Fees That Blow Up the Bill (Full Plan Table)

A Linux cloud server for a brochure site can cost under $4 a month. The SpinServers entry VPS costs $12.00 USD and ships with 2 vCPU, 2 GB of DDR4, a 40 GB RAID-10 SSD, 4 TB of monthly transfer, and both an IPv4 and an IPv6 address. The distance between those two price points comes from RAM and disk sizing, and from how each provider meters the things that never appear in the headline price.

Below: the current SpinServers VPS lineup, sizing rules for the four workloads people actually run, what the recurring bill contains after month one, and the CentOS 7/8 exit path if you're dragging an old stack onto new hardware.

## The quick pick

> **One site, a small API, or a handful of containers: the 2 vCPU / 2 GB plan.** $12.00 USD per month, 40 GB RAID-10 SSD, 4 TB of transfer on a 1 Gbps port, 1 IPv4 + 1 IPv6 included.
> 👉 [Check the 2 vCPU / 2 GB plan and current price](https://bit.ly/Spinservers)

You move up a tier when a database and a busy WordPress install share the box, when several Docker services need their own memory headroom, or when image and backup storage pushes past 40 GB. The full lineup is below, and two of its details matter more than the CPU count.

## SpinServers Linux VPS plans

| Plan | vCPU / RAM | Storage | Monthly transfer | Price (USD) | Order |
| --- | --- | --- | --- | --- | --- |
| KVM 2 vCPU / 2 GB | 2 vCPU (Intel) / 2 GB DDR4 | 40 GB RAID-10 SSD | 4 TB, 1 Gbps port | $12.00/mo | [View this plan](https://bit.ly/Spinservers) |
| 6 vCPU / 8 GB | 6 vCPU / 8 GB DDR4 | 120 GB RAID-10 SSD | 8 TB, 1 Gbps port | Configure at checkout | [View this plan](https://bit.ly/Spinservers) |
| KVM 12 vCPU / 12 GB | 12 vCPU / 12 GB DDR4 | 160 GB RAID-10 SSD | 10 TB, 1 Gbps port | Configure at checkout | [View this plan](https://bit.ly/Spinservers) |
| 16 vCPU / 16 GB | 16 vCPU (Intel Xeon) / 16 GB DDR4 | 320 GB RAID-10 SSD | 15 TB, 1 Gbps port | Configure at checkout | [View this plan](https://bit.ly/Spinservers) |
| 32 vCPU / 32 GB | 32 vCPU (Intel Xeon) / 32 GB | 500 GB SSD | 20 TB, 1 Gbps port | Configure at checkout | [View this plan](https://bit.ly/Spinservers) |

Every tier includes one IPv4 and one IPv6 address on a 1 Gbps port. The 2 vCPU / 2 GB configuration is the one with a published starting price of $12.00 USD per month; the four larger tiers are priced by the options you select at checkout, so the order page is the number to trust rather than any figure copied into a table.

### Read the spec sheet twice

Three things on that page change the buying decision more than clock speed does.

**Port 25 is closed by default.** SpinServers blocks SMTP on all VPS plans to limit IP abuse, and opening it requires a support ticket with a justification. They reserve the right to refuse. If you plan to run a mail server, or an app that sends its own mail instead of relaying through a transactional API, price that risk in before you order.

**Transfer is metered, not unmetered.** 4 TB on the entry plan rising to 20 TB on the 32 vCPU tier. That's generous for a web workload (a text-heavy site serving 50,000 page views a month typically uses well under 100 GB) and thin for video or large file distribution. Ask what the overage rate is past the bundle; the plan page doesn't say.

**40 GB of disk is the real ceiling on the cheap tier.** The OS and a LAMP stack eat 6–10 GB. A WordPress install with a few years of images plus local backups gets close to the limit faster than people expect, and RAID-10 SSD costs more per gigabyte than the storage on a dedicated box.

## What the monthly bill really contains

Three line items decide whether $12 stays $12.

**Powered-off hours.** Providers differ on whether idle time is free. UpCloud bills its Starter and Premium plans 24/7/365 until you delete them, while its Cloud Native plans bill only while the server is powered on, with storage and IPs billed continuously because the allocation persists. IONOS runs Cloud Cubes on per-minute billing with no minimum contract and states plainly that costs stop only when you delete the instance. Parking a server is not the same as cancelling it, and only one of those two models rewards you for shutting down over a quiet weekend.

**Outbound transfer.** UpCloud advertises zero fees on outgoing traffic. Atlantic.Net leaves inbound unmetered and charges $0.02/GB once you pass the free outbound allowance. Cloudzy bundles 1 TB to 5 TB depending on the plan. SpinServers bundles 4 TB to 20 TB. Run the same 3 TB-per-month workload through four providers and three of them bill nothing extra while one adds roughly $60 to the month. This single line item swings a bill by more than the difference between tiers.

**Extra IP addresses.** A single-IP setup costs nothing extra at SpinServers, since IPv4 and IPv6 are both included. Addresses are a paid line elsewhere: Atlantic.Net charges $3.65 per month for each additional IPv4 ($0.005431 hourly), and Cloudzy charges $2.50 per month per floating IP. If you run mail on a separate IP, or keep a failover address for blue/green deploys, that's a fixed monthly cost you should add before comparing totals.

What the SpinServers plan page doesn't answer: the overage rate past the bundled transfer, and whether the monthly fee pauses while the server is powered off. Both are one support ticket away, and both belong in the same message you send before paying.

👉 [See the full SpinServers VPS range and current pricing](https://bit.ly/Spinservers)

## How much server you actually need

Four workload bands cover almost every reader of this page, and the jump between them is usually RAM, not cores.

**Static site, reverse proxy, or one always-on bot.** 1 vCPU and 1 GB covers it. UpCloud's €3/month Starter tier ships 1 GB with 1 core and 10 GB of storage; Cloudzy's promotional $2.48 tier ships 512 MB and 20 GB of NVMe. SpinServers' smallest box is 2 vCPU / 2 GB at $12, which is more machine than a static site needs but leaves room for a database and a build step on the same host.

**WordPress, Laravel, Django, or an API with MySQL or PostgreSQL.** 2 vCPU / 2 GB is the floor and 4 GB is comfortable once caching plugins, PHP workers and the database share one kernel. Reference points for the 4 GB class: €12/month at UpCloud for 4 GB with 2 cores, $14.48 at Cloudzy's promotional rate for 4 GB with 2 vCPU and 120 GB of NVMe. The SpinServers 2 vCPU / 2 GB plan at $12 sits at the bottom of this band with twice the transfer allowance of either.

**Docker host or a Kubernetes node.** Plan for 6–8 vCPU and 8 GB minimum, because each container carries its own runtime overhead and the scheduler needs slack. The 6 vCPU / 8 GB tier with 120 GB of RAID-10 storage and 8 TB of transfer is the natural fit, and it's also the point where a single VPS starts replacing two or three smaller ones on cost.

**Database server or a high-concurrency service.** The 32 vCPU / 32 GB tier with 500 GB of SSD and 20 TB of transfer is built for this. Below that, the 16 vCPU / 16 GB tier with 320 GB of RAID-10 is the safer pick for a primary database that also serves application traffic.

One rule of thumb survives all four bands: provision for memory first, disk second, cores third. A 2-core box with 4 GB will outperform a 4-core box with 1 GB on almost any web workload, because the bottleneck is usually PHP workers or database buffers, not instruction throughput.

## Distros, root access, and the CentOS 7/8 exit

The lineup is KVM-based, which means the guest is a normal virtual machine and the operating system is yours to install and reinstall from the control panel. If you need an image that isn't in the standard list, confirm availability with support before ordering rather than after.

CentOS 7 and CentOS 8 are both past end of life, and anyone migrating an old stack has two realistic paths. The first is a drop-in rebuild: Rocky Linux and AlmaLinux are offered as one-click images across most of the market (Cloudzy lists AlmaLinux 8/9 and Rocky 8/9 alongside CentOS Stream 9/10, Debian 11–13 and Ubuntu 20.04–24.04 LTS), and existing packages generally reinstall without surprises. The second is a compatibility-focused distribution. TencentOS Server publishes an explicit mapping: Server 3 is userland-compatible with CentOS 8 and Server 2 with CentOS 7, with up to 13 years of maintenance per major version, so applications usually move without code changes. That's the vendor's own compatibility claim about its own OS, not a benchmark of your specific stack, so test the migration on a staging box either way.

Root access is standard at this level of VPS, and both IPv4 and IPv6 come with the plan, which matters if you're hardening SSH or running services that prefer a v6 path.

👉 [Open the SpinServers VPS plan list](https://bit.ly/Spinservers)

## Who should not buy this

Managed WordPress hosting, a control-panel-only experience, or someone else handling patching and backups: a KVM VPS gives you a root shell and nothing else, and that's the wrong product if you don't want one.

A hobby box that sits idle most of the month: $12/month is fine money, but Cloudzy's $2.48 tier and UpCloud's €3 tier exist for exactly that use case, and neither will notice a static page.

Per-second or request-based billing for spiky batch jobs: look at pay-as-you-go cloud rather than a monthly VPS plan.

Anything that sends mail directly from the server: the SMTP port is closed by default here, and the appeal process is discretionary.

## FAQ

**How much does a Linux cloud server cost at SpinServers?**
$12.00 USD per month for the 2 vCPU / 2 GB configuration with 40 GB RAID-10 SSD and 4 TB of transfer. Larger tiers are priced by configuration at checkout.

**Is billing monthly?**
The plan list quotes monthly pricing. Confirm the term, renewal price and cancellation process at checkout, since promotional and renewal rates are not always the same number.

**Can I get a refund if it doesn't work out?**
The plan page doesn't publish a refund window, so get the terms in writing before paying. A 14-day money-back window is common in this segment (Cloudzy advertises 14 days), which is a reasonable benchmark to ask for.

**Does the meter stop when the server is powered off?**
Not necessarily, and this varies by provider. IONOS requires you to delete the instance before charges stop; UpCloud keeps billing storage and IPs on powered-off Cloud Native servers. Ask SpinServers directly, because the answer changes what a part-time server really costs.

**Do I get a dedicated IP address?**
Yes, one IPv4 and one IPv6 with every VPS plan.

**Can I install Ubuntu, Debian or AlmaLinux?**
The plans are KVM, so the OS is yours to install. Confirm the panel's image list with support if you need a niche distribution.

## Before you order

Match the tier to the workload, not to the biggest number on the page. A single static site or a staging box belongs on the 2 vCPU / 2 GB plan at $12.00 USD. A WordPress install with a database and a couple of containers fits the 6 vCPU / 8 GB tier with 120 GB of storage. Multi-service production, or anything that holds a primary database, starts at the 12 vCPU tier and goes up to 32 vCPU / 32 GB with 500 GB of SSD and 20 TB of transfer.

Two questions to settle before paying: what the overage rate is past your bundled transfer, and what the refund and cancellation terms are in writing. Get both in a ticket reply you can keep.

👉 [Start with the SpinServers 2 vCPU / 2 GB plan at $12.00/mo](https://bit.ly/Spinservers)
