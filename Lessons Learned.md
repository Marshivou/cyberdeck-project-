# Lessons Learned

A running log of problems hit during the build, what caused them, and how they got resolved. 
Kept loose — this is more of a build journal than a formal doc.

---

## Display Mounting

Getting the display seated correctly took way more iterations than expected. 
The first attempt used M3 standoffs straight off the mounting holes on the display PBC, 
but the angle ended up slightly off once the chassis lid was closed — 
there was just enough flex in the 3D printed frame to push the panel out of true. 
Shimming with a thin piece of foam tape helped, but it introduced a small gap on one edge. 
The eventual fix was redesigning the mount bracket in CAD to account for the panel's actual thickness 
(which was 0.5mm thicker than the datasheet listed) and adding two additional contact points to distribute pressure evenly. 
Lesson: always measure the physical unit, don't trust the spec sheet for fit-critical dimensions.

---

## Cooling

Thermals weren't a concern during short bench tests, 
but after running a network scan and a parallel compile job for about 40 minutes, 
the SBC started throttling. 
Turns out the case design had the single exhaust vent positioned directly behind a standoff column,
which was partially blocking airflow. 
Repositioned the vent cutout and added a small 30mm intake fan on the opposite side to create a proper cross-flow path. 
Temperatures under sustained load dropped significantly and throttling hasn't recurred. 
Going forward, any enclosed compute component gets a thermal stress test before the chassis design is finalized.

---

## Cable Management

The inside of the first prototype looked like a bird's nest by the time all the connections were in — power rails, 
USB, HDMI, and GPIO ribbon cables all fighting for the same space. 
It wasn't just ugly; it made accessing the SD card slot a 10-minute job involving tweezers. 
For the next revision, the plan is to route power along the bottom of the chassis with adhesive cable clips, 
keep data cables on the left spine, and leave a clear vertical lane down the center for any components that need to be swapped out. 
Also switching to right-angle connectors wherever possible to reclaim headroom. 
Serviceability should have been a design constraint from the start, not an afterthought.

---

## Power Management

The initial power setup was a simple USB power bank feeding the SBC directly. 
It worked fine on the bench but the bank kept entering sleep mode during low-draw idle periods, 
utting power mid-session. Switched to a UPS HAT with a dedicated LiPo cell, 
which solved the sleep issue and added the bonus of a clean shutdown on battery disconnect. 
The HAT also exposes battery percentage over I2C, 
which opened the door to a simple status script showing charge level in the terminal prompt. 
Worth the extra complexity.

---

## SD Card Reliability

Early on, the OS SD card corrupted twice in two weeks — both times after an unclean shutdown from pulling power. 
Moved the root filesystem to a USB-attached SSD and now use the SD card only for the bootloader. 
No corruption issues since. For any future builds, booting from SSD should be the default from day one; 
SD cards are fine for experimentation but not a reliable long-term root device under real workloads.

---

## WiFi Adapter Driver Conflicts

The USB WiFi adapter (Alfa AWUS036ACH) wasn't recognized out of the box on the chosen distro. 
The in-kernel driver existed but was an older version that didn't support monitor mode reliably.
Had to pull the `rtl88xxau` driver from GitHub and build it against the current kernel headers. 
Not difficult, but it needs to be redone after every kernel update, which gets old fast. 
Added a small shell script to automate the rebuild — it lives in `scripts/rebuild-wifi-driver.sh`. 
Next time, check driver support and monitor mode compatibility *before* buying the adapter.

---

*Last updated: June 2026*
