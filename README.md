# prayer-times
This is a SIMPL# Module that will allow you to display prayer times based on your location. 


#HELP_BEGIN

PRAYER TIMES SIMPL+ MODULE — HELP FILE

PURPOSE
This module calculates Islamic prayer times, Hijri date (Umm al‑Qura), Jumah Mubarak message,
tomorrow’s prayer times, Tahajjud window, and optional custom dates. It supports high‑latitude
adjustments, DST rules, custom color gradients, and licensing control.

-----------------------------------------------------------------------
INPUTS (FROM SIMPL+)
-----------------------------------------------------------------------

Latitude$
• Decimal latitude as a string (no quotes)
• Example: 40.7128

Longitude$
• Decimal longitude as a string (no quotes)
• Example: -74.0060

TimezoneOffset
• Integer offset from UTC (standard time)
• Example: -5 for EST
• DST adjustments depend on DST_Mode and DST_Region

DST_Mode (Analog Input)
0 = Disabled
    DST is ignored. TimezoneOffset is used exactly as provided.
    
1 = Auto
    Module automatically applies DST based on DST_Region.
    
2 = Force On
    DST is always applied (TimezoneOffset + 1 hour).
    
3 = Force Off
    DST is never applied.

DST_Region (Analog Input)

Selects the DST ruleset used when DST_Mode = Auto.

0 = North America (Canada / USA)
1 = Europe (EU / UK legacy rules)
2 = Middle East (Gulf regions with partial DST history)
3 = Custom (reserved for future expansion)

Notes:
• When DST_Mode = Auto, the module checks the current date against the region’s DST rules.
• When DST_Mode = Force On or Force Off, DST_Region is ignored.

Method
• Integer selecting prayer calculation method:
0 = Muslim World League
1 = ISNA
2 = Egyptian General Authority
3 = Umm al‑Qura (Saudi Arabia)
4 = University of Islamic Sciences Karachi

Asr_Method
• 1 = Shafi’i
• 2 = Hanafi

High_Latitude (Analog Input)

Selects the high‑latitude adjustment rule for Fajr and Isha.

0 = None
1 = Middle of the Night
2 = One‑Seventh of the Night
3 = Angle-Based (Angle/60)

Notes:
• Only affects Fajr and Isha.
• Only applies when twilight angles cannot be reached.
• Umm al‑Qura does not use high‑latitude adjustments.

Calculate (Digital Input)
• Pulse to calculate prayer times for a custom date.

Licensing_Enable (Digital Input)
• 0 = Demo Mode (restricted outputs)
• 1 = Full Mode (all outputs active)

License_Key$
• Serial license key string.
• Required for full-mode operation.

-----------------------------------------------------------------------
OUTPUTS
-----------------------------------------------------------------------

TODAY’S PRAYER TIMES (Serial)
Fajr$
Sunrise$
Dhuhr$
Asr$
Maghrib$
Isha$
• All formatted as HH:MM

TOMORROW’S PRAYER TIMES (Serial)
Tomorrow_Fajr$
Tomorrow_Sunrise$
Tomorrow_Dhuhr$
Tomorrow_Asr$
Tomorrow_Maghrib$
Tomorrow_Isha$

CURRENT PRAYER LOGIC
CurrentPrayer$
• Example: "Asr", "Maghrib", "Isha", "Tahajjud"

NextPrayerCountdown

• Example: "Fajr in 08:44:42"

HIJRI DATE (UMM AL-QURA)

Hijri_Date$
Hijri_Month$
Hijri_Day$
Hijri_Year$
• Example: "28 Rajab 1447"

RAMADAN STATUS

Ramadan_Info
• "X days until Ramadan"

• "Ramadan Day X"

JUMAH MUBARAK
Jumah_Mubarak
• "Jumah Mubarak" every Friday before Maghrib

Processor_ID
• Processor ID as a string (required for full license)

-----------------------------------------------------------------------
CUSTOM PRAYER COLORS
-----------------------------------------------------------------------


OVERVIEW
The PrayerTimes module supports custom color gradients for each prayer.
Each prayer uses two RGB colors:
  - Start Color: used at the beginning of the prayer window
  - End Color: used at the end of the prayer window

The module automatically interpolates between these two colors to produce
a smooth gradient effect throughout the prayer window.

By default, the module uses built-in colors. These defaults may be
overridden by creating a colors.ini file on the processor.

-----------------------------------------------------------------------

COLOR FILE LOCATION
The module looks for the following file at startup:

    /USER/colors.ini

If the file exists, the module loads the custom colors and overrides the
default palette. If the file does not exist, the module uses the built-in
colors.

-----------------------------------------------------------------------

FILE FORMAT
The file uses a simple INI-style format. Each prayer has its own section.

Example:

    [Fajr]
    Start=0,180,255
    End=0,60,120

    [Dhuhr]
    Start=255,220,0
    End=255,140,0

    [Asr]
    Start=255,165,0
    End=180,65,0

    [Maghrib]
    Start=255,80,60
    End=120,20,20

    [Isha]
    Start=140,90,255
    End=60,30,120

-----------------------------------------------------------------------

RGB VALUE FORMAT
Each color is defined using three comma-separated values:

    R,G,B

Where:
  - R = Red   (0–255)
  - G = Green (0–255)
  - B = Blue  (0–255)

Spaces are optional. Example:

    Start=255,140,0

-----------------------------------------------------------------------

HOW COLORS ARE APPLIED
1. The module loads default colors during initialization.
2. If colors.ini exists, the module overrides the defaults with values
   found in the file.
3. During runtime, the module calculates a gradient between the Start and
   End colors based on the current prayer window.
4. The resulting RGB values are output to SIMPL Windows as 16-bit analog
   values (0–65535).

-----------------------------------------------------------------------

ERROR HANDLING
- If the file is missing, default colors are used.
- If a section or key is missing, defaults for that prayer are used.
- If an RGB value is invalid, that entry is ignored and defaults remain.
- Errors are printed to the console for debugging.

-----------------------------------------------------------------------

NOTES
- The colors.ini file is optional.
- Only values present in the file are overridden.
- The format is intentionally simple for easy editing.


LICENSING

Module will operate in DEMO mode (No time limit). You will get the prayer times for today except for sunrise. If you want to unlock full functionality please email jameelm@gmail.com and send your processor ID and we will generate a license key.


