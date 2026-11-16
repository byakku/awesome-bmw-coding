<!-- markdownlint-disable-file MD013 MD033 -->
# awesome-bmw-coding

This repository is a starting point for BMW coding, ECU programming and general BMW maintenance.

> **If you find an error, a wrong date or anything else to correct, open an issue or submit a pull request.**

## Contents

- [Coding vs diagnostics](#coding-vs-diagnostics)
- [BMW ECU, TCU and infotainment list (1978-2020)](#bmw-ecu-tcu-and-infotainment-list-1978-2020)
- [ECU coding software](#ecu-coding-software)

## Coding vs diagnostics

Diagnostics reads information from the car. Coding changes how a module behaves. Programming replaces the software in a module. Each step carries more risk than the one before it.

A module is a small computer that controls one part of the car, for example the engine, the lights or the radio. Other names for a module are control unit, ECU or, in BMW documents, Steuergerät (SG). A modern BMW has dozens of modules. They talk to each other over internal networks (buses).

### Levels of access

"Risk" in this table means the risk of making a module stop working.

| Level | What it does | Does it change the module? | Risk | Example tools |
| --- | --- | --- | --- | --- |
| **Diagnostics** | Reads fault codes, live data and module information. Clears fault codes. | No. Clearing fault codes only empties the fault memory. | Low | Generic OBD-II scanner, INPA, ISTA+, BimmerLink |
| **Service functions** | Runs tests and resets, for example battery registration, service interval reset, adaptation reset and DPF regeneration. | It writes some values, but it does not change the configuration. | Low to medium | INPA, Tool32, ISTA+, BimmerLink, Carly |
| **Coding** | Changes the settings that a module stores. The software stays the same. | Yes, the coding data. | Medium | NCS Expert, E-Sys, Bimmercode, BimmerGeeks ProTool |
| **Programming** (flashing) | Replaces the software (firmware) in a module. | Yes, the software. | High | WinKFP, E-Sys, ISTA/P, ISTA+. Tuning tools such as MHD, bootmod3 and xHP also program modules. |

### Diagnostics

Diagnostics answers the question "What is wrong with the car?". A diagnostic tool asks each module for:

- stored fault codes (also called DTCs, diagnostic trouble codes)
- live data, such as sensor values, temperatures and voltages
- module information, such as the part number and the software version

Diagnostics does not change how the car behaves. If you clear a fault code and the cause is still there, the fault code comes back.

### Coding

Coding changes the settings that a module stores. The software in the module stays the same. Examples of coding changes:

- Show a digital speed value in the instrument cluster.
- Fold the mirrors when you lock the car.
- Tell the other modules that a retrofitted part is now installed.

There are two ways to code a BMW:

- **VO coding** (vehicle order coding). The vehicle order (VO, also called FA, Fahrzeugauftrag) lists the factory options of the car as option codes (SA codes). You add or remove an option code. Then you code the modules. Each module sets its own parameters to match the new vehicle order. This is the cleanest method for retrofits.
- **FDL coding** (Funktionsdatenleiste, function data list). You change single parameters in one module directly. This gives you more control. But the next VO coding, for example at a dealer, can overwrite your FDL changes.

Coding cannot add hardware. You can only turn on a feature if the car has the hardware for it. Some features on newer cars also need an FSC (Freischaltcode), which is an enable code from BMW.

### Programming

Programming, also called flashing, writes new software to a module. You need it when:

- a module needs a software update
- a retrofitted module has software that does not match the car
- you install an engine or transmission tune

If programming stops before it is complete, the module may stop working. Common causes are low battery voltage and a lost connection. On F-, G- and I-series cars, E-Sys and ISTA create a TAL (Transaktionsliste, a list of programming and coding steps) and then run it.

### How you connect to the car

The connection decides which modules you can reach and what you can do with them. BMW used three main kinds of connection over the years.

#### OBD-I and the 20-pin connector

OBD-I is the name for car diagnostics before the OBD-II standard. Each carmaker used its own connector and its own protocols. BMW used a round 20-pin connector in the engine bay. Many BMWs built before about 2001 have it, for example the E30 (later cars), E34, E36, E38, E39, early E46 and Z3.

- To use a K+DCAN cable on the 20-pin connector, you need a 20-pin to OBD-II adapter.
- Some older modules use an older protocol. They need an ADS interface instead of a K+DCAN cable. An ADS interface is a serial interface for older BMW modules.
- Some cars have both the 20-pin connector and a 16-pin OBD-II port. On these cars the 16-pin port may give only limited access. Use the 20-pin connector for full BMW diagnostics.

#### OBD-II and the 16-pin connector

OBD-II is a standard for emissions diagnostics. It defines the 16-pin connector under the dashboard and a set of standard engine data. The law requires OBD-II on:

- US cars from model year 1996
- EU petrol cars from about 2001 (the EU version is called EOBD)
- EU diesel cars from about 2004

The OBD-II port carries two kinds of diagnostics:

- **Generic OBD-II data.** Any OBD-II scanner can read it. It covers only emissions-related data from the engine and sometimes the transmission. This data includes fault codes (P-codes), readiness monitors, freeze frame data and some live values.
- **BMW-specific diagnostics.** BMW tools use the same port with BMW's own protocols. They reach all modules in the car, for example the airbag, ABS, lights, body and infotainment modules.

On E-series cars, BMW-specific diagnostics use one of two protocols:

- K-line on cars built before about March 2007.
- D-CAN (diagnostic CAN) on cars built from about March 2007.

A K+DCAN cable supports both protocols. Some cables have a switch that connects pins 7 and 8. Cars built before 2007 usually need this switch on.

#### ENET (Ethernet over OBD-II)

F-, G- and I-series cars support Ethernet through the same 16-pin OBD-II port. BMW calls this connection ENET. The first car with ENET was the F01 7 Series (2008). An ENET cable connects the Ethernet port of your laptop to the car.

- The ENET cable connects to the central gateway module. The gateway passes messages to every other module in the car.
- Ethernet is much faster than K-line or D-CAN. This makes it practical to program many modules in one session.
- E-Sys uses ENET for coding and programming. ISTA+ can use an ENET cable or an ICOM interface.
- The car only turns on the Ethernet connection when the cable has a resistor between two pins of the connector. Most ENET cables have this resistor built in. Check this before you buy a cheap cable.

F-series cars also still support D-CAN on the OBD-II port. Some tools and mobile apps use D-CAN instead of ENET.

#### Bluetooth and Wi-Fi adapters

You do not always need a laptop and a dealer-style cable. A small adapter in the OBD-II port, used with a BMW app on a phone, can do BMW-specific diagnostics and coding. The adapter only provides the connection. The app decides what you can do.

- **Adapters** connect to the phone over Bluetooth or Wi-Fi, for example the MHD Universal WiFi adapter, OBDLink MX+ or Veepeak.
- **Apps** do the work, for example Bimmercode and ProTool for coding, BimmerLink for diagnostics and MHD for tuning.

One adapter can work with several apps. For example, the MHD Universal WiFi adapter works with MHD and also with coding apps such as Bimmercode and ProTool. Check the app vendor's list of supported adapters and cars before you buy.

Cheap ELM327 clones are often too slow or unstable for coding. Use an adapter that the app vendor lists as supported.

### Which connection does my car use?

Dates vary by model and market. Check the connector on your car before you buy a cable.

| Car | Diagnostic connector | BMW protocol | Cable or interface |
| --- | --- | --- | --- |
| Cars built before about 2001 (E30, E34, E36, E38, E39, early E46, Z3) | Round 20-pin in the engine bay. US cars from 1996 also have a 16-pin OBD-II port. | Older BMW serial protocols (K-line, ADS) | K+DCAN cable with a 20-pin adapter, or an ADS interface |
| E-series built from about 2001 to March 2007 | 16-pin OBD-II | K-line | K+DCAN cable, with pins 7 and 8 connected |
| E-series built from about March 2007 | 16-pin OBD-II | D-CAN | K+DCAN cable |
| F-, G- and I-series (from 2008) | 16-pin OBD-II | ENET, and D-CAN | ENET cable. ICOM Next for dealer-level work. Bluetooth or Wi-Fi adapter for mobile apps. |

### Code reader, phone app or PC tool?

The software matters more than the plug. The same OBD-II port gives very different results depending on what you connect and which program you use.

| Setup | Example | Diagnostics | Coding |
| --- | --- | --- | --- |
| **Generic OBD-II code reader** | Any handheld OBD-II scanner | Engine and emissions faults only (generic P-codes) | No |
| **OBD adapter with a BMW app** | MHD Universal WiFi adapter, OBDLink MX+ or Veepeak with Bimmercode, BimmerLink or ProTool | All modules, with BMW fault codes | Yes. The apps offer ready-made coding options. Bimmercode Expert mode and ProTool also give access to raw parameters. |
| **Cable with PC software** | K+DCAN with INPA and NCS Expert, ENET with E-Sys, ICOM with ISTA+ | All modules, with BMW fault codes | Yes, full coding and programming |

A generic OBD-II code reader is enough to find out why the check engine light is on. It cannot see faults in other modules, for example the airbag, ABS or lights module. It cannot code. BMW modules also store their own fault codes, which are different from the generic P-codes.

For most common coding changes, an OBD adapter with a BMW app is enough. Use PC software for complex retrofits and for module software updates. See [ECU coding software](#ecu-coding-software).

### Before you code or program

> **Warning:** If the battery voltage drops during programming, the module can stop working. Always use a stable power supply.
>
> **Warning:** Some coding changes can make the car illegal on public roads in your country, for example some lighting changes. Check your local rules first.

1. Connect a battery charger or power supply that is made for vehicle programming. A trickle charger is not enough. Coding can take minutes. Programming can take an hour or more.
2. Turn the ignition on. Do not start the engine.
3. Turn off the lights, the radio and other electrical consumers.
4. Turn off sleep mode on your laptop.
5. Save a backup of the current coding before you change anything. In NCS Expert, save the `FSW_PSW.TRC` file. In E-Sys, read and save the FA and the CAFD files.
6. Change one setting at a time. Test it before you change the next one.
7. Do not disconnect the cable while coding or programming runs.

### Key terms

| Term | Meaning |
| --- | --- |
| **ECU / module / SG** | A control unit. SG stands for Steuergerät. |
| **DTC** | Diagnostic trouble code. A fault code that a module stores. |
| **VO / FA** | Vehicle order (Fahrzeugauftrag). The list of factory options of a car. |
| **SA code** | Option code (Sonderausstattung) in the vehicle order, for example a code for a specific factory option. |
| **FDL** | Funktionsdatenleiste (function data list). The single coding parameters of a module. |
| **CAFD** | The coding data file of a module on F-, G- and I-series cars. |
| **NETTODAT** | The coding data file that NCS Expert writes to an E-series module. |
| **SGBD** | The description file that EDIABAS uses to talk to a module. |
| **TAL** | Transaktionsliste. The list of programming and coding steps that E-Sys or ISTA runs. |
| **FSC** | Freischaltcode. An enable code from BMW for some features, for example navigation maps. |

## BMW ECU, TCU and infotainment list (1978-2020)

Notes on names:

- **DME** (Digital Motor Electronics) is the engine control unit for petrol engines.
- **DDE** (Digital Diesel Electronics) is the engine control unit for diesel engines.
- **EGS** (Elektronische Getriebe Steuerung) is the transmission control unit.
- Bosch Motronic (ML, M, MS, ME, MEV, MG, MD) and Siemens/VDO (MS, MSS, MSV, MSD) are the names of the supplier product lines.
- ECU names sometimes differ by market (for example SULEV versions) and by model year. DME hardware revisions are common.

### Fuel injection before Motronic (1973-1988)

| System | Years | BMW models / engines |
| --- | --- | --- |
| **Bosch K-Jetronic** (mechanical continuous injection, CIS) | 1976-1988 | E21 320i / 323i (M10/M20), E12 528i (M30, early), E24 630CSi (M30), E28 528i (early, M30), some early E30 318i |
| **Kugelfischer / Bosch + Magneti-Marelli** | 1978-1981 | E26 BMW M1 (M88/1). Mechanical injection with separate electronic ignition. |
| **Bosch L-Jetronic** (analog electronic fuel injection) | 1979-1988 | E12 528i/530i (US, M30), E23 728i / 732i / 733i (M30), E24 633CSi / 635CSi (early, M30), E28 528i / 533i / 535i (early, M30), E30 318i (early, M10) |

### Petrol engine control units (Motronic / DME)

| ECU | Years | Engines | BMW chassis / models |
| --- | --- | --- | --- |
| **Bosch Motronic ML1.1** | 1983-1987 | M20 (eta), M30 | E30 325e/325es, E28 528e, E28 533i (late), E24 633CSi (late), E23 733i (late), E32 730i/735i (early) |
| **Bosch Motronic ML1.2** | 1987-1990 | S38B36, M70 (two ECUs, one per bank) | E34 M5 (1988-1990, S38B36), E32 750i/750iL (early M70 V12), E31 850i (early M70 V12) |
| **Bosch Motronic ML1.3** | 1987-1993 | M20, M30, S14 (US, with catalytic converter) | E30 325i / 325is / 325iX, E30 M3 (US-spec S14B23), E34 525i / 535i, E32 735i / 735iL, E24 635CSi (late) |
| **Bosch Motronic ML1.7** | 1987-1994 | M40, M42, S14 (Euro/late) | E30 318i (M40), E36 318i / 318is (early, M40/M42), E30 M3 (Euro S14B23/B25 with catalytic converter) |
| **Bosch Motronic M1.7 (dual)** | 1992-1996 | M70 (later), M73 / M73N (some) | E32 750iL (late), E31 850i (late), early references to the two-bank M73 setup |
| **Bosch Motronic M3.3** | 1992-1996 | M60 (V8) | E34 540i, E32 740i / 740iL, E38 740i (1995), E31 840Ci |
| **Bosch Motronic M3.3.1 / "413" / "506"** | 1992-1995 | M50 (with VANOS) | E36 320i/325i and E34 525i/525ix with Bosch systems. Other markets used Siemens MS40 at the same time. |
| **Siemens MS40.0 / MS40.1** | 1992-1995 | M50 (24V), M50TU (with VANOS) | E36 320i / 325i / 325is / 328i (early), E34 520i / 525i (M50/M50TU), Z3 1.9 (early) |
| **Siemens MS41.0 / MS41.1 / MS41.2** | 1995-1999 | M52 (single VANOS), S52B32 (US M3) | E36 323i / 328i / Z3 2.8 (M52), E39 523i / 528i (M52), E36 M3 US (S52, MS41.2), Z3 M Coupe/Roadster US (S52) |
| **Siemens MSS50** | 1995-1999 | S50B32 (Euro M3) | E36 M3 (Euro), Z3 M Coupe/Roadster (Euro, S50B32) |
| **Bosch DME M5.2 / M5.2.1** | 1995-1998 | M62 (V8), M73 (V12, two ECUs) | E38 740i / 740iL (1996-1998, M62), E39 540i (1997-1998, M62), E31 840Ci (1996-1999, M62), E38 750i / 750iL (1995-1998, M73), E31 850Ci (1995-1999, M73) |
| **Siemens MS42** | 1998-2001 | M52TU (Double VANOS) | E46 320i / 323i / 328i (1998-2000), E39 523i / 528i (1998-2000), Z3 2.8/3.0 (M52TU) |
| **Bosch ME7.2 ("M7.2")** | 1998-2003 | M62TU (Double VANOS V8), M73N (V12 LCI, two ECUs) | E38 740i / 740iL (1998-2001), E39 540i (1999-2003), E53 X5 4.4i / 4.6is (2000-2003), E38 750i / 750iL LCI (1999-2001, M73N with two ECUs) |
| **Siemens MSS52** | 1998-2003 | S62 (V8) | E39 M5 (1998-2003), E52 Z8 (2000-2003) |
| **Siemens MS43** | 2000-2006 | M54 | E46 325i / 330i / 330Ci, E39 525i / 530i, E53 X5 3.0i, E83 X3 2.5i / 3.0i, E85/E86 Z4 2.5i / 3.0i, E60 525i / 530i (2003-2005) |
| **Siemens MSS54 / MSS54HP** | 2001-2008 | S54B32 | E46 M3 (2001-2006), E46 M3 CSL / CS (MSS54HP, 2003-2004), E85/E86 Z4 M Coupe/Roadster (2006-2008) |
| **Bosch ME9.2.x** | 2003-2010 | N62 / N62TU (V8), N73 (V12) | E60/E61 545i / 550i, E63/E64 645Ci / 650i, E65/E66 745i / 750i / 760i (N73 V12), E70 X5 4.8i / xDrive48i, E53 X5 4.4i (late, N62) |
| **Siemens MS45.0 / MS45.1** | 2004-2006 | M54 (late) | E60 525i / 530i (MS45.1 in North America, MS45.0 in other markets), E83 X3, late E46 |
| **Siemens MSV70** | 2005-2007 | N52 | E90/E91 325i / 328i / 330i, E60/E61 525i / 528i / 530i, E63 630i, E85/E86 Z4 3.0si, E83 X3 |
| **Siemens MSV80 / MSV80.1** | 2007-2013 | N52N (magnesium block), N51 (SULEV version uses MSV80.1) | E90/E92/E93 LCI 328i / 330i, E60 LCI 528i / 530i, E70 X5 3.0si / xDrive30i, E83 X3 LCI, E89 Z4 sDrive30i, E81/E82/E87/E88 128i |
| **Siemens MSS60** | 2007-2013 | S65 (V8) | E90 M3, E92 M3, E93 M3 |
| **Siemens MSS65** | 2005-2010 | S85 (V10) | E60/E61 M5, E63/E64 M6 |
| **Siemens MSD80** | 2006-2010 | N54 (twin-turbo I6) | E90/E91/E92/E93 335i / 335xi, E82/E88 135i, E60 535i / 535xi, E71 X6 xDrive35i (early), E89 Z4 sDrive35i (early) |
| **Siemens MSD81** | 2009-2013 | N54 (later) | E89 Z4 sDrive35i / 35is, E82 1M Coupe, late E92 335is, F25 X3 (early N54-based versions outside the US) |
| **Siemens MSD85 / MSD85.0 / MSD85.1 / MSD85.3** | 2008-2014 | N63, S63 (twin-turbo V8) | F01/F02 750i / 750Li (N63), F07 550i GT (N63), F10/F11 550i (N63), F12/F13 650i (N63), F06 640i (early), E70 X5 xDrive50i (N63), E71 X6 xDrive50i (N63), E70 X5 M (S63B44O0), E71 X6 M (S63B44O0) |
| **Bosch MEVD17.2.2 / 17.2.3 and others** | 2008-2014 | N63 / N63TU versions and others | F10/F11 550i (N63TU), F01/F02 750i LCI (N63TU), F15 X5 xDrive50i (N63TU). Some versions use more than one DME. |
| **Bosch MEVD17.2.4 / 17.2.5 / 17.2.6 / 17.2.8 / 17.2.K** | 2011-2018 | N20, N26, N55, N63TU | F30 328i (N20/N26), F32 428i (N20/N26), F25 X3 xDrive28i, F20 125i / 130i (N55), F30 335i (N55), F10 535i (N55), F15 X5 xDrive35i (N55), F22 M235i (N55), F87 M2 (N55, MEVD17.2.H/17.2.P) |
| **Bosch MEVD17.2.G / 17.2.9** | 2014-2020 | S55 (twin-turbo I6, M) | F80 M3, F82/F83 M4, F87 M2 Competition / CS (S55) |
| **Bosch MG1CS003 / MG1CS024 / MG1CS201 and others** | 2015-2020 | B38, B48, B46, B58, S63B44T4 | F30 LCI 340i (B58), F32 LCI 440i (B58), G20 330i (B48) / M340i (B58), G30 530i (B48) / 540i (B58), G05 X5 xDrive40i (B58), G07 X7 (B58), F90 M5 (S63B44T4, MG1CS201) |
| **Continental MD1CS006 / MD1CP002** | 2018-2020 | S58 (twin-turbo I6, M), B57 (also diesel applications) | G80 M3 / G82 M4 (production started in 2020, MD1CS006), G07 X7 50i, and some diesel models (MD1CP002) |

### Diesel engine control units (DDE)

| ECU | Years | Engines | BMW chassis / models |
| --- | --- | --- | --- |
| **Bosch DDE 2.x / 3.x** | 1991-2001 | M21, M41, M51 (early diesels) | E34 525tds, E36 325td/tds, E38 725tds, E39 525d (early M51) |
| **Bosch DDE 4.x** | 1998-2005 | M47, M57 (early) | E46 320d / 330d, E39 530d, E38 730d, E53 X5 3.0d |
| **Bosch DDE 5.x / 6.x (EDC16)** | 2002-2010 | M47TU, M57TU / M57TU2 | E46 LCI 320d, E60 525d / 530d / 535d, E70 X5 3.0d / 3.0sd / 35d, E90 320d / 330d / 335d, E83 X3 2.0d / 3.0d |
| **Bosch DDE 7.x (EDC17CP09 and others)** | 2007-2013 | M57N2, N47 (4-cyl) | E90 335d, E70 X5 xDrive35d, E60 LCI 535d, E84 X1 (N47), F25 X3 28d (N47) |
| **Bosch DDE 7.3 / 7.4 / 8.x (EDC17C50/C56/C76)** | 2010-2018 | N47, N57, N57S, N20d-class | F30 320d / 328d (N47), F10 525d / 530d / 535d (N57), F01 730d / 740d / 750d (N57/N57S), F15 X5 xDrive30d / 35d (N57), F25 X3 (N47/N57) |
| **Bosch MD1CP002 (DDE family)** | 2015-2020 | B47, B57 | F30 LCI 320d (B47), G30 520d / 530d / 540d (B47/B57), G05 X5 30d (B57), F48 X1 18d/20d/25d (B47) |

### Transmission control units (EGS)

| ECU / transmission | Years | BMW chassis / notes |
| --- | --- | --- |
| **ZF 4HP22 (EH)** with early EGS | 1983-1992 | E23 745i, E32 730i / 735i / 740i (early), E34 530i / 535i, E28 535i (late), E24 635CSi automatic |
| **ZF 5HP18** | 1991-1999 | E36 325i / 328i (automatic), E34 525i / 528i (automatic), Z3 2.8 |
| **ZF 5HP19** | 1996-2005 | E39 520i / 523i / 525i / 528i / 530i, E46 320i / 323i / 325i / 328i / 330i, E83 X3 2.5i / 3.0i (early), E60 525i / 530i (early), E85 Z4 |
| **ZF 5HP24 / 5HP30** | 1996-2003 | E38 740i (5HP24) / 750i (5HP30), E39 540i, E31 840Ci/850Ci (5HP30), E53 X5 4.4i / 4.6is (5HP24) |
| **GM 5L40-E (Steptronic)** | 1999-2006 | E46 330xi / X3 2.5i (US), some E53 X5 3.0i (US). Other markets used ZF. |
| **ZF 6HP19 / 6HP21 (GA6HP19Z, GA6HP21Z)** | 2003-2012 | E60 525i / 530i / 530xi, E90 325i / 328i / 330i / 335i, E63 630i, E83 X3 (late), E70 X5 3.0si, E71 X6 xDrive35i, E89 Z4 |
| **ZF 6HP26 / 6HP28 (GA6HP26Z, GA6HP28Z)** | 2003-2014 | E60 540i / 545i / 550i, E63 645Ci / 650i, E65 745i / 750i, E66 745Li / 750Li, E70 X5 xDrive48i / 50i, E71 X6 xDrive50i, F01 740i / 750i (early), F10 535i / 550i (early) |
| **ZF 8HP45** | 2009-present | F30 320i / 328i / 335i / 340i, F32 428i / 435i / 440i, F20/F21 125i / 135i / M135i / M140i, F10 528i / 535i, F25 X3 xDrive28i / 35i, F15 X5 xDrive35i, G20 330i, G30 530i, G29 Z4 sDrive30i, G05 X5 30i |
| **ZF 8HP70 / 8HP75** | 2009-2020 | F10 550i / M550d, F01/F02 740i / 750i, F12/F13 650i, F30 ActiveHybrid 3, F06 640i / 650i, F15 X5 xDrive50i, F16 X6 xDrive50i |
| **ZF 8HP90 / 8HP95** | 2012-2020 | F10 M5, F12/F13 M6, F90 M5 (8HP75 in some markets), F85 X5 M, F86 X6 M, F95 X5 M (G-prep), G11/G12 750i / M760Li / 760Li (8HP95), G15 M850i |
| **Getrag 7DCT (GS7D36SG / DCT)** | 2008-2019 | E90/E92/E93 M3 (Drivelogic), F10 M5 (DCT), F12/F13 M6, F80 M3, F82/F83 M4, F87 M2 / M2 Competition / CS, Z4 M (DCT in some markets) |

### Infotainment and head units

| System | Years | BMW chassis / notes |
| --- | --- | --- |
| **Bavaria / Bavaria C / Reverse / C23 / C33 / C43 (radio only)** | 1985-2000 | E30, E32, E34, E36, E38, E39. Base radios with cassette or CD, no navigation. |
| **MK1 / MK2 / MK3 / MK4 (navigation computer)** | 1995-2008 | DVD navigation unit in the trunk of the E38, E39, E46, E53, E83 and E85. Screens are 4:3, first monochrome and later color. MK4 adds DVD-based Professional Navigation. |
| **M-ASK / M-ASK2 (Audio System Controller)** | 2003-2010 | E60/E61 (pre-LCI), E63/E64, E83, E85/E86. Base radio version without full iDrive. |
| **CCC (Car Communication Computer), iDrive 1.0** | 2003-2008 | E60/E61/E63/E64 (pre-LCI), E65/E66 (LCI), E70 (pre-LCI), E90 (after 09/2008 in some markets). First iDrive generation, DVD navigation, 8.8" 16:9 screen. |
| **CIC (Car Information Computer), iDrive 2.0** | 2008-2013 | E60/E61 LCI, E63/E64 LCI, E70/E71/E72 (X5/X6), E90/E91/E92/E93 LCI, F01/F02 (early), F10/F11 (early), F25 (early). Navigation on a hard disk, 8.8" or 10.25" screen. |
| **NBT (Next Big Thing), iDrive 4.0** | 2012-2016 | F30/F31, F32/F33/F36, F10/F11 (LCI), F01/F02 (LCI), F15 X5, F16 X6, F25 X3 LCI, F26 X4, F20/F21 LCI, F22/F23. iDrive controller with touchpad from 2013. 6.5", 8.8" or 10.25" screens. |
| **Entrynav / Entrynav2** | 2013-2018 | Entry-level radios with smaller screens on F-chassis cars, often where NBT was an option. |
| **NBT Evo (ID4 / ID5 / ID6), iDrive 5/6** | 2016-2020 | G11/G12, G30/G31, G01 X3, G02 X4, F15 LCI, F16 LCI, F22 LCI, F30 LCI 2, F32 LCI, F48 X1, F39 X2, F45/F46. Touchscreen support from ID5, Apple CarPlay. |
| **HU_MGU (Media Graphics Unit), iDrive 7 ("BMW OS 7")** | 2018-2020 | G20 (3 Series, 2019+), G05 X5, G06 X6, G07 X7, G14/G15/G16 8 Series, G29 Z4. Full touchscreen, software stack derived from AAOS. |

## ECU coding software

Which tools fit which car:

- **E-series (before about 2008):** Standard Tools (INPA, NCS Expert, WinKFP) with SP-Daten, over a **K+DCAN** cable.
- **F-, G- and I-series (from about 2008):** E-Sys with PSdZData, over an **ENET** cable. Use **E-Sys Launcher PRO** to sign FDL changes.
- **All series, dealer-level diagnostics and programming:** ISTA+ (formerly ISTA/D) and ISTA/P, with **ICOM Next** hardware.
- **Mobile apps** (Bimmercode, BimmerLink, Carly, ProTool) use a Bluetooth or Wi-Fi OBD adapter. They cover the most common coding changes without a PC.

### Official BMW software (dealer and factory tools)

| Tool | Purpose | Chassis | Hardware | Notes |
| --- | --- | --- | --- | --- |
| **EDIABAS** | Low-level diagnostic runtime. INPA, NCS Expert, WinKFP and Tool32 run on top of it. You do not use it directly. | All E / F / G / I | K+DCAN, ENET, ICOM | All Standard Tools need it. |
| **INPA** (Interpreter for Test Procedures) | Live diagnostics: read and clear fault codes, view live sensor data, run service functions. Shows coding but cannot change it. | Mainly E-series (some early F-series) | K+DCAN / ICOM | Engineering tool. Parts of the interface are in German. Very flexible, but it does not stop you from making mistakes. |
| **NCS Expert** | Module coding: change the vehicle order (FA/VO), change FDL parameters, turn on hidden features. | E-series (E36 to E9x / E7x) | K+DCAN / ICOM | Needs a matching **SP-Daten** package. Wrong use can make a module unusable. |
| **NCS Dummy** | Helper program. It turns the raw NETTODAT/MAN trace files of NCS Expert into readable coding options. | E-series | None. It works offline on saved files. | Community tool. Use it with NCS Expert. |
| **WinKFP** | Programs E-series modules: firmware updates and ZUSB programming. | E-series | K+DCAN / ICOM | Use it with NCS Expert when a retrofitted module needs a firmware update. |
| **Tool32** | Runs single EDIABAS jobs (SGBD / `.prg` files) on a module, for example to reset adaptations or run service functions. | All E / F (where SGBD files exist) | K+DCAN / ICOM | A general-purpose engineering diagnostics tool. |
| **DIS / DIS+** (Diagnostic Information System) | Older guided diagnostics and programming. ISTA replaced it. | E36 / E38 / E39 / E46 / E53 / E83 / E85 (and older) | OPS / OPPS / DCAN | Mostly retired. People keep it for very old cars where ISTA support is limited. |
| **GT1 / SSS** | Dealer tester from before DIS. | E30 / E34 / E36 / E38 / E39 / E46 | OPS hardware | Obsolete. Mostly of historical interest. |
| **ISTA/D**, now **ISTA+** (Rheingold) | Current dealer diagnostics: guided test plans, wiring diagrams, fault diagnosis and basic coding. | All E / F / G / I, MINI, Rolls-Royce | ENET / ICOM Next / D-CAN | Replaced DIS. "ISTA+" has been the name since about 2017. It includes both diagnostics and coding. |
| **ISTA/P** | Dealer-level **programming**: full vehicle software updates, software integration level updates and retrofit programming. | E-series up to F/G/I. G-series moved to ISTA/P-Next / ISTA-Next inside ISTA+. | ICOM Next | On newer G/I models, ISTA+ does the programming through the **ISPI Next** backend. BMW is slowly retiring standalone ISTA/P. |
| **E-Sys** | The main coding and programming tool for F/G/I-series. Edits CAFD files (the coding data of a module), runs VO coding and runs TAL-based programming. | F-series, G-series, I-series, F-MINI / F-RR | ENET | The standard tool for any complex F/G/I retrofit or feature unlock. |
| **AOS** (Aftersales Online System) | BMW Group online portal for dealers: service information, technical bulletins and FSC (enable code) orders. | All | Browser | The official source for vehicle configuration and FSC codes. It is not a coding tool. |

### Community and third-party software

| Tool | Purpose | Chassis | Platform | Notes |
| --- | --- | --- | --- | --- |
| **E-Sys Launcher PRO** (TokenMaster) | Starts E-Sys with a "Pro" token. This allows FDL coding without an official BMW developer certificate. Includes a "Cheat Codes" library of common changes. | F / G / I | Windows | The current community standard. It replaced **E-Sys Launcher Premium**. |
| **E-Sys Launcher Premium** | Older free launcher for E-Sys. | F / G (older) | Windows | **Deprecated.** Use E-Sys Launcher PRO instead. |
| **Bimmercode** | Module coding app. FDL-level coding on F/G/I, more limited on E. | E (limited), F, G, I | iOS / Android | Works with a Bluetooth OBD-II adapter (for example Veepeak or OBDLink MX+). "Expert mode" shows raw parameters. |
| **BimmerLink** | Sister app to Bimmercode for diagnostics, live values and service functions (for example DPF regeneration or battery registration). | E (partial), F, G, I | iOS / Android | It does **not** code. Use it with Bimmercode to get both. |
| **Carly for BMW** | One app for diagnostics, coding, used-car checks and service resets. | E, F, G (limited on the newest G/I) | iOS / Android | Subscription. Offers a fixed list of coding options with less raw access than Bimmercode Expert mode. |
| **BimmerGeeks ProTool** | Coding and diagnostics app with the deepest access of the third-party apps. People often call it a "mobile E-Sys / NCS". | E, F, G, I, MINI, Rolls-Royce | Android only | One-time payment for a lifetime coding license. |
| **OBDeleven** | Module coding app. Best known for VAG (Volkswagen Group) cars, but it also supports BMW. | F, G (limited) | iOS / Android | One-click apps and Pro mode. BMW support is narrower than VAG support. |

### Tuning software (engine and transmission programming)

Tuning is close to coding, but it changes the engine or transmission software. This makes it a type of programming.

| Tool | Purpose | Chassis / engines | Notes |
| --- | --- | --- | --- |
| **MHD Flasher** | Programs the DME and switches maps on turbo BMWs (N54, N55, S55, S63, S58, B58 and others). | E / F / G turbo platforms | OBD-II adapter with Android or iOS. Stage maps and back-end flash. |
| **bootmod3** | Cloud-based programming platform. You can write custom maps. | F / G chassis (N55, S55, S63, S58, B48, B58, N63TU, S63TU4) | Browser and OBD adapter. Supports more DMEs than MHD on newer cars. |
| **xHP Flashtool** | Programs the transmission control unit (TCU): shift logic, launch control and torque limiter maps. | ZF 6HP and 8HP automatics, Getrag 7DCT on F-chassis | OBD adapter with Android or iOS. Works with any engine tune. You can use it together with MHD or bootmod3. |
| **JB4** (Burger Motorsports) | Piggyback module, not a reflash. It sits between the sensors and the DME. | Turbo BMWs (N54, N55, S55, S63, S58, B58 and others) | Not coding, but people often install it with the tools above. It does not change the DME calibration. |

### Required data packages

| Data | Used by | Series | Notes |
| --- | --- | --- | --- |
| **SP-Daten** | NCS Expert, WinKFP, INPA, Tool32 | E-series | "Spool-Daten". Coding and programming definitions. The latest widely shared version is **v74.x**. |
| **PSdZData** | E-Sys, ISTA+ programming, ISTA/P | F / G / I | "Programming System Data Zentrale". "Full" includes the SWFL/BTLD firmware files (software and bootloader). "Lite" includes only the coding data (CAFD). Version numbers follow ISTA, for example **v4.57.x / v4.58.x** in 2025-2026. |

### Interface hardware

These cables and interfaces are commonly used with the software above.

| Cable / tool | Connects | Used for |
| --- | --- | --- |
| **K+DCAN cable** (USB) | OBD-II to USB | E-series Standard Tools (INPA, NCS Expert, WinKFP). Cheap. Many clones exist. |
| **ENET cable** (Ethernet) | OBD-II to RJ45/USB | F/G/I-series E-Sys and ISTA. Carries Ethernet over pins of the OBD-II connector. |
| **ICOM A2 / ICOM Next** | OBD-II or the diagnostic connector under the hood | Official BMW dealer interface. Required for ISTA/P, advanced programming and most programming sessions on G-series cars built after 2020. |
| **MHD Universal WiFi adapter** | OBD-II to Wi-Fi | Made for MHD, but it also works with coding apps such as Bimmercode and ProTool. One adapter can cover tuning, diagnostics and coding. |
| **OBDLink MX+ / Veepeak / Vgate vLinker** | OBD-II to Bluetooth/Wi-Fi | Adapters for the mobile apps (Bimmercode, BimmerLink, Carly, ProTool, MHD, bootmod3, xHP). |
