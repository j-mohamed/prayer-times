# prayer-times
This is a SIMPL# Module that will allow you to display prayer times based on your location. 


#HELP_BEGIN

GETPRAYERTIMES SIMPL+ MODULE — HELP FILE

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

NextPrayerCountdown$
• Example: "Fajr in 08:44:42"

HIJRI DATE (UMM AL-QURA)
Hijri_Date$
Hijri_Month$
Hijri_Day$
Hijri_Year$
• Example: "28 Rajab 1447"

RAMADAN STATUS
Ramadan_Status$
• "X days until Ramadan"
• "Ramadan has begun"
• "Ramadan Day X"

JUMAH MUBARAK
Jumah_Mubarak$
• "Jumah Mubarak" every Friday before Maghrib

LICENSING OUTPUTS
License_Status$
• "Licensed" or "Demo Mode"

Processor_ID$
• Processor ID as a string (gated in demo mode)

-----------------------------------------------------------------------
CUSTOM PRAYER COLORS
-----------------------------------------------------------------------
The module supports custom color gradients for each prayer using /USER/colors.ini.
(Full documentation unchanged for clarity.)

#HELP_END
