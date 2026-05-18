# awesome-bmw-coding

This repository aims to be starting point for anyone interested in coding, ECU programming and general BMW maintenance parkour.

<!-- markdownlint-disable MD033 !-->
<span style="color:red">**If you see any error, wrong date or anything that needs to be corrected, create an issue or submit a PR**</span>

## BMW ECU, TCU and Infotainment List — 1978-2020

> Notes on naming: BMW DME = Digital Motor Electronics (petrol). DDE = Digital Diesel Electronics. EGS = Elektronische Getriebe Steuerung (transmission). "Bosch Motronic ML/M/MS/ME/MEV/MG/MD" and "Siemens/VDO MS/MSS/MSV/MSD" are the suppliers. ECU names sometimes differ slightly per market (e.g. SULEV variants) and per model-year (DME hardware revisions are common).

### Pre-Motronic Fuel Injection (1973-1988)

| System | Years | BMW Models / Engines |
|---|---|---|
| **Bosch K-Jetronic** (mechanical CIS) | 1976-1988 | E21 320i / 323i (M10/M20), E12 528i (M30, early), E24 630CSi (M30), E28 528i (early, M30); some early E30 318i |
| **Kugelfischer / Bosch + Magneti-Marelli** | 1978-1981 | E26 BMW M1 (M88/1) — mechanical injection, separate electronic ignition |
| **Bosch L-Jetronic** (analog EFI) | 1979-1988 | E12 528i/530i (US, M30), E23 728i / 732i / 733i (M30), E24 633CSi / 635CSi (early, M30), E28 528i / 533i / 535i (early, M30), E30 318i (early, M10) |

### Petrol Engine Management ECUs (Motronic / DME)

| ECU | Years | Engines | BMW Chassis / Models |
|---|---|---|---|
| **Bosch Motronic ML1.1** | 1983-1987 | M20 (eta), M30 | E30 325e/325es, E28 528e, E28 533i (late), E24 633CSi (late), E23 733i (late), E32 730i/735i (early) |
| **Bosch Motronic ML1.2** | 1987-1990 | S38B36, M70 (dual ECU, one per bank) | E34 M5 (1988-1990, S38B36), E32 750i/750iL (early M70 V12), E31 850i (early M70 V12) |
| **Bosch Motronic ML1.3** | 1987-1993 | M20, M30, S14 (US, catalysed) | E30 325i / 325is / 325iX, E30 M3 (US-spec S14B23), E34 525i / 535i, E32 735i / 735iL, E24 635CSi (late) |
| **Bosch Motronic ML1.7** | 1987-1994 | M40, M42, S14 (Euro/late) | E30 318i (M40), E36 318i / 318is (early, M40/M42), E30 M3 (Euro S14B23/B25 cat) |
| **Bosch Motronic M1.7 (dual)** | 1992-1996 | M70 (later), M73 / M73N (some) | E32 750iL (late), E31 850i (late), early references on M73 dual-bank setup |
| **Bosch Motronic M3.3** | 1992-1996 | M60 (V8) | E34 540i, E32 740i / 740iL, E38 740i (1995), E31 840Ci |
| **Bosch Motronic M3.3.1 / "413" / "506"** | 1992-1995 | M50 (with VANOS) | Bosch-equipped E36 320i/325i/525i/525ix variants (parallel to Siemens MS40 in other markets) |
| **Siemens MS40.0 / MS40.1** | 1992-1995 | M50 (24V), M50TU (with VANOS) | E36 320i / 325i / 325is / 328i (early), E34 520i / 525i (M50/M50TU), Z3 1.9 (early) |
| **Siemens MS41.0 / MS41.1 / MS41.2** | 1995-1999 | M52 (single VANOS), S52B32 (US M3) | E36 323i / 328i / Z3 2.8 (M52), E39 523i / 528i (M52), E36 M3 US (S52, MS41.2), Z3 M Coupe/Roadster US (S52) |
| **Siemens MSS50** | 1995-1999 | S50B32 (Euro M3) | E36 M3 (Euro), Z3 M Coupe/Roadster (Euro, S50B32) |
| **Bosch DME M5.2 / M5.2.1** | 1995-1998 | M62 (V8), M73 (V12, dual ECU) | E38 740i / 740iL (1996-1998, M62), E39 540i (1997-1998, M62), E31 840Ci (1996-1999, M62), E38 750i / 750iL (1995-1998, M73), E31 850Ci (1995-1999, M73) |
| **Siemens MS42** | 1998-2001 | M52TU (Double VANOS) | E46 320i / 323i / 328i (1998-2000), E39 523i / 528i (1998-2000), Z3 2.8/3.0 (M52TU) |
| **Bosch ME7.2 ("M7.2")** | 1998-2003 | M62TU (Double VANOS V8), M73N (V12 LCI, dual) | E38 740i / 740iL (1998-2001), E39 540i (1999-2003), E53 X5 4.4i / 4.6is (2000-2003), E38 750i / 750iL LCI (1999-2001, M73N dual ECU) |
| **Siemens MSS52** | 1998-2003 | S62 (V8) | E39 M5 (1998-2003), E52 Z8 (2000-2003) |
| **Siemens MS43** | 2000-2006 | M54 | E46 325i / 330i / 330Ci, E39 525i / 530i, E53 X5 3.0i, E83 X3 2.5i / 3.0i, E85/E86 Z4 2.5i / 3.0i, E60 525i / 530i (2003-2005) |
| **Siemens MSS54 / MSS54HP** | 2001-2008 | S54B32 | E46 M3 (2001-2006), E46 M3 CSL / CS (MSS54HP, 2003-2004), E85/E86 Z4 M Coupe/Roadster (2006-2008) |
| **Bosch ME9.2.x** | 2003-2010 | N62 / N62TU (V8), N73 (V12) | E60/E61 545i / 550i, E63/E64 645Ci / 650i, E65/E66 745i / 750i / 760i (N73 V12), E70 X5 4.8i / xDrive48i, E53 X5 4.4i (late, N62) |
| **Siemens MS45.0 / MS45.1** | 2004-2006 | M54 (late) | E60 525i / 530i (US/non-US split: MS45.1 NA, MS45.0 ROW), E83 X3, late E46 |
| **Siemens MSV70** | 2005-2007 | N52 | E90/E91 325i / 328i / 330i, E60/E61 525i / 528i / 530i, E63 630i, E85/E86 Z4 3.0si, E83 X3 |
| **Siemens MSV80 / MSV80.1** | 2007-2013 | N52N (Magnesium-block), N51 (SULEV variant uses MSV80.1) | E90/E92/E93 LCI 328i / 330i, E60 LCI 528i / 530i, E70 X5 3.0si / xDrive30i, E83 X3 LCI, E89 Z4 sDrive30i, E81/E82/E87/E88 128i |
| **Siemens MSS60** | 2007-2013 | S65 (V8) | E90 M3, E92 M3, E93 M3 |
| **Siemens MSS65** | 2005-2010 | S85 (V10) | E60/E61 M5, E63/E64 M6 |
| **Siemens MSD80** | 2006-2010 | N54 (twin-turbo I6) | E90/E91/E92/E93 335i / 335xi, E82/E88 135i, E60 535i / 535xi, E71 X6 xDrive35i (early), E89 Z4 sDrive35i (early) |
| **Siemens MSD81** | 2009-2013 | N54 (later) | E89 Z4 sDrive35i / 35is, E82 1M Coupe, late E92 335is, F25 X3 (early N54-based ROW variants) |
| **Siemens MSD85 / MSD85.0 / MSD85.1 / MSD85.3** | 2008-2014 | N63, S63 (TT V8) | F01/F02 750i / 750Li (N63), F07 550i GT (N63), F10/F11 550i (N63), F12/F13 650i (N63), F06 640i (early), E70 X5 xDrive50i (N63), E71 X6 xDrive50i (N63), E70 X5 M (S63B44O0), E71 X6 M (S63B44O0) |
| **Bosch MEVD17.2.2 / 17.2.3 (etc.)** | 2008-2014 | N63 / N63TU variants and others | F10/F11 550i (N63TU), F01/F02 750i LCI (N63TU), F15 X5 xDrive50i (N63TU) — multi-DME on some variants |
| **Bosch MEVD17.2.4 / 17.2.5 / 17.2.6 / 17.2.8 / 17.2.K** | 2011-2018 | N20, N26, N55, N63TU | F30 328i (N20/N26), F32 428i (N20/N26), F25 X3 xDrive28i, F20 125i / 130i (N55), F30 335i (N55), F10 535i (N55), F15 X5 xDrive35i (N55), F22 M235i (N55), F87 M2 (N55, MEVD17.2.H/17.2.P) |
| **Bosch MEVD17.2.G / 17.2.9** | 2014-2020 | S55 (TT I6, M-Performance) | F80 M3, F82/F83 M4, F87 M2 Competition / CS (S55) |
| **Bosch MG1CS003 / MG1CS024 / MG1CS201 / MG1CS003 etc.** | 2015-2020 | B38, B48, B46, B58, S63B44T4 | F30 LCI 340i (B58), F32 LCI 440i (B58), G20 330i (B48) / M340i (B58), G30 530i (B48) / 540i (B58), G05 X5 xDrive40i (B58), G07 X7 (B58), F90 M5 (S63B44T4, MG1CS201) |
| **Continental MD1CS006 / MD1CP002** | 2018-2020 | S58 (M-Performance TT I6), B57 (diesel applications also) | G80 M3 / G82 M4 production began 2020 (MD1CS006), G07 X7 50i, and used in some diesel chassis (MD1CP002) |

### Diesel Engine Management ECUs (DDE)

| ECU | Years | Engines | BMW Chassis / Models |
|---|---|---|---|
| **Bosch DDE 2.x / 3.x** | 1991-2001 | M21, M41, M51 (early diesels) | E34 525tds, E36 325td/tds, E38 725tds, E39 525d (early M51) |
| **Bosch DDE 4.x** | 1998-2005 | M47, M57 (early) | E46 320d / 330d, E39 530d, E38 730d, E53 X5 3.0d |
| **Bosch DDE 5.x / 6.x (EDC16)** | 2002-2010 | M47TU, M57TU / M57TU2 | E46 LCI 320d, E60 525d / 530d / 535d, E70 X5 3.0d / 3.0sd / 35d, E90 320d / 330d / 335d, E83 X3 2.0d / 3.0d |
| **Bosch DDE 7.x (EDC17CP09, etc.)** | 2007-2013 | M57N2, N47 (4-cyl) | E90 335d, E70 X5 xDrive35d, E60 LCI 535d, E84 X1 (N47), F25 X3 28d (N47) |
| **Bosch DDE 7.3 / 7.4 / 8.x (EDC17C50/C56/C76)** | 2010-2018 | N47, N57, N57S, N20d-class | F30 320d / 328d (N47), F10 525d / 530d / 535d (N57), F01 730d / 740d / 750d (N57/N57S), F15 X5 xDrive30d / 35d (N57), F25 X3 (N47/N57) |
| **Bosch MD1CP002 (DDE family)** | 2015-2020 | B47, B57 | F30 LCI 320d (B47), G30 520d / 530d / 540d (B47/B57), G05 X5 30d (B57), F48 X1 18d/20d/25d (B47) |

### Transmission Control Units (EGS)

| ECU / Transmission | Years | BMW Chassis / Notes |
|---|---|---|
| **ZF 4HP22 (EH)** w/ early EGS | 1983-1992 | E23 745i, E32 730i / 735i / 740i (early), E34 530i / 535i, E28 535i (late), E24 635CSi auto |
| **ZF 5HP18** | 1991-1999 | E36 325i / 328i (auto), E34 525i / 528i (auto), Z3 2.8 |
| **ZF 5HP19** | 1996-2005 | E39 520i / 523i / 525i / 528i / 530i, E46 320i / 323i / 325i / 328i / 330i, E83 X3 2.5i / 3.0i (early), E60 525i / 530i (early), E85 Z4 |
| **ZF 5HP24 / 5HP30** | 1996-2003 | E38 740i (5HP24) / 750i (5HP30), E39 540i, E31 840Ci/850Ci (5HP30), E53 X5 4.4i / 4.6is (5HP24) |
| **GM 5L40-E (Steptronic)** | 1999-2006 | E46 330xi / X3 2.5i (US), some E53 X5 3.0i (US, ROW used ZF) |
| **ZF 6HP19 / 6HP21 (GA6HP19Z, GA6HP21Z)** | 2003-2012 | E60 525i / 530i / 530xi, E90 325i / 328i / 330i / 335i, E63 630i, E83 X3 (late), E70 X5 3.0si, E71 X6 xDrive35i, E89 Z4 |
| **ZF 6HP26 / 6HP28 (GA6HP26Z, GA6HP28Z)** | 2003-2014 | E60 540i / 545i / 550i, E63 645Ci / 650i, E65 745i / 750i, E66 745Li / 750Li, E70 X5 xDrive48i / 50i, E71 X6 xDrive50i, F01 740i / 750i (early), F10 535i / 550i (early) |
| **ZF 8HP45** | 2009-Present | F30 320i / 328i / 335i / 340i, F32 428i / 435i / 440i, F20/F21 125i / 135i / M135i / M140i, F10 528i / 535i, F25 X3 xDrive28i / 35i, F15 X5 xDrive35i, G20 330i, G30 530i, G29 Z4 sDrive30i, G05 X5 30i |
| **ZF 8HP70 / 8HP75** | 2009-2020 | F10 550i / M550d, F01/F02 740i / 750i, F12/F13 650i, F30 ActiveHybrid 3, F06 640i / 650i, F15 X5 xDrive50i, F16 X6 xDrive50i |
| **ZF 8HP90 / 8HP95** | 2012-2020 | F10 M5, F12/F13 M6, F90 M5 (8HP75 in some markets), F85 X5 M, F86 X6 M, F95 X5 M (G-prep), G11/G12 750i / M760Li / 760Li (8HP95), G15 M850i |
| **Getrag 7DCT (GS7D36SG / DCT)** | 2008-2019 | E90/E92/E93 M3 (Drivelogic), F10 M5 (DCT), F12/F13 M6, F80 M3, F82/F83 M4, F87 M2 / M2 Competition / CS, Z4 M (DCT in some markets) |

### Infotainment / Head Units

| System | Years | BMW Chassis / Notes |
|---|---|---|
| **Bavaria / Bavaria C / Reverse / C23 / C33 / C43 (radio-only)** | 1985-2000 | E30, E32, E34, E36, E38, E39 (base radios — cassette / CD, no nav) |
| **MK1 / MK2 / MK3 / MK4 (Navigation Computer)** | 1995-2008 | Trunk-mounted DVD-nav unit on E38, E39, E46, E53, E83, E85 (4:3 monochrome → color screens). MK4 with DVD-based Professional Navigation |
| **M-ASK / M-ASK2 (Audio System Controller)** | 2003-2010 | E60/E61 (pre-LCI), E63/E64, E83, E85/E86 — base radio variant, no full iDrive |
| **CCC (Car Communication Computer) — iDrive 1.0** | 2003-2008 | E60/E61/E63/E64 (pre-LCI), E65/E66 (LCI), E70 (pre-LCI), E90 (post-09/2008 in some markets) — first iDrive generation; DVD nav, 8.8" 16:9 screen |
| **CIC (Car Information Computer) — iDrive 2.0** | 2008-2013 | E60/E61 LCI, E63/E64 LCI, E70/E71/E72 (X5/X6), E90/E91/E92/E93 LCI, F01/F02 (early), F10/F11 (early), F25 (early) — HDD-based, 8.8" / 10.25" screen |
| **NBT (Next Big Thing) — iDrive 4.0** | 2012-2016 | F30/F31, F32/F33/F36, F10/F11 (LCI), F01/F02 (LCI), F15 X5, F16 X6, F25 X3 LCI, F26 X4, F20/F21 LCI, F22/F23 — Touchpad iDrive controller from 2013, 6.5" / 8.8" / 10.25" screens |
| **Entrynav / Entrynav2** | 2013-2018 | Entry-level radios with smaller screens on F-chassis (often where NBT was an option) |
| **NBT Evo (ID4 / ID5 / ID6) — iDrive 5/6** | 2016-2020 | G11/G12, G30/G31, G01 X3, G02 X4, F15 LCI, F16 LCI, F22 LCI, F30 LCI 2, F32 LCI, F48 X1, F39 X2, F45/F46 — touchscreen support (ID5+), Apple CarPlay |
| **HU_MGU (Media Graphics Unit) — iDrive 7 ("BMW OS 7")** | 2018-2020 | G20 (3-Series, 2019+), G05 X5, G06 X6, G07 X7, G14/G15/G16 8-Series, G29 Z4 — fully touchscreen, AAOS-derived stack |

## ECU Coding software

