# Number-Engraver

This is a small programming project just for fun You may freely use and modify this code, NO WARRANTY, blah blah blah, as long as you give proper credit to the original and subsequent authors.

Date: Author: 2021-12-23 Marcos Valter Vidal Russo Alegre m.valter@ua.pt

Abstract:
Engraving a number with a CNC machine can be very usefull for serial procuction. Serial numbers and time/date stamps can be automatically generated for identification purpose.
It will work with any controller that works with ISO format, ex: FANUC or MAZAK.

Important: This macros should be protected with a 8000's or 9000's numbers. Please change the program number.

How to use this macro:

G65 P0100 X Y Z W F E Q R S V H
where:
X - X AXIS POSITION
Y - Y AXIS POSITION
Z - Z AXIS FEED PLANE
W - Z AXIS RETRACT
F - FEED PLANE X,Y
E - FEED Z AXIS
Q - NUMBER
R - NUMBER LENGH
S - SCALE
V - SPACING(positive-space between number/negative-box lenght)
H - HELP CONTENTS

Tips:
Some controllers demand a H number for a tool lenght offset, you may need to define it before you call the macro.

T1 M6;
H1;
G65 P0100 X* Y* Z* W* F* E* Q* R* S* V*;

For a serial number you need to create a counter

G65 P0100 X* Y* Z* W* F* E* Q#100 R* S* V* H*;

#100=#100+1;

For a time stamp you need the value stored in variable #3011 (HHMMSS format)
For a time stamp you need the value stored in variable #3012 (YYYYMMDD format)

You can use this to isolate the values:

DAY DD #3011-[FIX[#3011/100]*100]

MONTH MM FIX[#3011/100]-[FIX[#3011/10000]*100]

YEAR YYYY FIX[#3011/10000]

YEAR YY FIX[#3011/10000]-[FIX[#3011/1000000]*100]

SECONDS SS #3012-[FIX[#3012/100]*100]

MINUTES MM FIX[#3012/100]-[FIX[#3012/10000]*100]

HOURS HH FIX[#3012/10000]-[FIX[#3012/1000000]*100]
