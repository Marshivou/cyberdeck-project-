# Future Upgrades

A running list of improvements and additions being considered for future revisions. 
Not a strict roadmap — more of a wishlist with reasoning behind each item.

---

## Ethernet Passthrough

The current setup relies entirely on WiFi, 
which works fine for most use cases but becomes a liability when doing wired network assessments or 
working in RF-noisy environments. 
The plan is to add a dedicated RJ45 port routed through a USB 3.0 to 2.5GbE adapter, 
with the jack flush-mounted on the chassis side panel. 
The main challenge is finding a clean way to do the cutout without weakening the case wall — 
might require a small reinforcement plate behind the panel. 
Once it's in, it also opens up the possibility of using the deck as a portable tap point with a network tap inline.

---

## External Antenna Connector

The internal WiFi adapter works well at close range but signal degrades quickly through walls or at distance. 
Adding an RP-SMA bulkhead connector to the chassis would allow swapping between a low-profile stubby antenna for 
everyday use and a high-gain directional antenna when range matters. 
e Alfa card already supports an external antenna — it just needs a pigtail routed to the chassis port. 
Low effort, high payoff. This one is probably the next thing to actually get done.

---

## Internal Storage Expansion

Right now there's a single SSD handling everything — OS, 
tools, and capture storage. That's fine day-to-day but gets uncomfortable fast when doing large packet captures or storing disk images.
The goal is to add a secondary drive, either a second USB-attached SSD or an NVMe via a PCIe adapter if the SBC supports it, 
mounted in a dedicated bay in the lower chassis. Captured data and case files would live on the secondary drive, 
keeping the OS drive clean and making it easier to pull just the data drive if needed.

---

## Improved Cable Routing

Covered in lessons learned, but worth having here as a proper upgrade target. 
The next chassis revision will treat cable routing as a first-class design constraint rather than something figured out after the fact.
Specific plans include integrated cable channels molded into the chassis walls, right-angle connectors throughout, 
velcro tie points at regular intervals, and a dedicated passthrough panel on the internal wall separating the compute bay from the battery bay. 
The goal is for any component to be reachable and swappable in under five minutes without disturbing anything else.

---

## GPS Module

Adding a GPS receiver would let the deck log location alongside packet captures and scan results — 
useful for wardriving, site surveys, or any fieldwork where knowing where data was collected matters. 
small USB GPS dongle would work, but a cleaner option is a UART-connected module mounted internally with a small patch antenna on the lid.
`gpsd` handles the daemon side on Linux with decent tool support. Not urgent, but a natural fit for the use case.

---

## E-Paper Status Display

A small e-paper panel on the outside of the lid — showing battery percentage, IP addresses, and active interface status — 
would mean not having to open the deck just to check basic system state. E-paper is ideal here because it holds the last image without drawing power, 
so it updates periodically and stays readable without any battery drain between refreshes. A 2.9" or 4.2" panel driven over SPI is the likely approach.
More of a polish item than a functional upgrade, but it would make the deck feel genuinely finished.

---

## Dedicated SDR Integration

A software-defined radio would round out the RF capability significantly — passive spectrum monitoring, 
ADS-B aircraft tracking, trunked radio scanning, and general signal analysis are all on the table. 
An RTL-SDR v4 would cover most use cases cheaply, but a HackRF One would open up transmit capability as well (within legal limits). 
Either way, the chassis would need a dedicated mount point and an antenna port separate from the WiFi antenna. 
This one is further out, but it's been in the back of the plan since the start.

---

*Last updated: June 2026*
