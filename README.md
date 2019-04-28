# CMOS-555

This Repository is for LibreSilicons's completely Open Source Timer IC "NE555" clone.

The Original "triple-5" chip is legendary. Once developed by the Swiss electronics engineer [Hans R. Camenzind](https://en.wikipedia.org/wiki/Hans_Camenzind "Link to Wikipedia"), working for Signetics, gets cloned by many different companies and is nowadays still in production and still a bestseller. While the first designs were build with Bipolar Junction Transistors (BJT), also a couple of clones are made in Complementary metal-oxide-semiconductor (CMOS) technologies. 

This Chip here uses the LibreSilicon 1 &micro;m CMOS-Technlogogy and contains two separted "555" on the same die - being acurate the Chip becomes functionaly similiar to the "7556".

## Requirements

### Lepton EDA

The Schematic for the CMOS-555 is done with the Schematic Entry program from Lepton-EDA - a GNU EDA tool clone with more active development than the original and the same License. On Debian-based Linux systems, you get lepton-schematic as part of the whole PCB tool suite Lepton-EDA by

```
apt-get install lepton-eda
```

as part of the whole PCB tool suite Lepton-EDA.

### Spice

A very usefull kind-of "Simulation Program with Integrated Circuit Emphasis" (SPICE), originaly from Berkley University is ngspice. Of course, this Open Source, general-purpose, analog electronic circuit simulator comes with Linux systems, e.g. on Debian-based systems with

```
apt-get install ngspice
```

Please make yourself familiar with Simulations using Spice.

### Magic

Another software tool, which should be installed before usage, is [Magic](http://opencircuitdesign.com/magic "http://opencircuitdesign.com/magic"). Magic is Open Source, but not part of all Linux distributions (lacks on OpenSuse, Arch Linux etc). On Debian-based systems

```
apt-get install magic
```
works.

## Documentation

Best Documentation about Analog Design and the "555" you'll find at Camenzind's [Book Site](http://designinganalogchips.com "Designing Analog Chips"). The Book is a great Textbook for analog Chip design; read it, study it, it is worth the time. For offline reading, you'll find the Download Link on the Book Site.

Of course, the "555" also has a [Wikipedia Page](https://en.wikipedia.org/wiki/555_timer_IC "Link to Wikipedia").

## Usage

### Schematic

```
lepton-schematic Sources/geda/555_Wikimedia-Version.sch
```

### Layout

```
magic -T scmos.tech Layout/magic/CMOS-555.mag
magic -T scmos.tech Layout/magic/CMOS-556.mag
```


