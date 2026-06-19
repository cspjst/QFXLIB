```
 ██████╗ ███████╗██╗  ██╗██╗     ██╗██████╗ 
██╔═══██╗██╔════╝╚██╗██╔╝██║     ██║██╔══██╗
██║   ██║█████╗   ╚███╔╝ ██║     ██║██████╔╝
██║▄▄ ██║██╔══╝   ██╔██╗ ██║     ██║██╔══██╗
╚██████╔╝██║     ██╔╝ ██╗███████╗██║██████╔╝
 ╚══▀▀═╝ ╚═╝     ╚═╝  ╚═╝╚══════╝╚═╝╚═════╝ 
© Jeremy Simon Thornton 2024,2025,2026 
```                                                                                                         
## Fixed point mathematics designed for DOS gaming upto and including XGA
Consider the Screen dimenisions likely in DOS games:
 + CGA4		320 x 200
 + CGA6		600 x 200 
 + HGA		720 x 348
 + VGA		640 x 480
 + SVGA		800 x 600
 + XGA		1024 x 768
   
For comparison "High Definition" HD is defined as:
 + HD720		1280 x 720
 + HD		1920 x 1080
   
Choosing fixed point layout of Q9.6 i.e. 10 bit integral and 6 bit fractional parts gives a of range (-512 < n < 511.984) and a fractional part of of 6 bits gives 1/64 resolution (approximatey). Looking at this in the context of retro graphics cards:
 
 + x range -512..511.984 or a pixel range of 0..1022.984 which would round to 0..1023 ie XGA - this library's maximum target DOS resolution
 + 0.015625 of a pixel or, to an effective 3dp, the smallest step in Q9.6 is 0.016
 + float value of PI		= 3.14159265359		Q9.6 PI	 = 3.141 (99.9% accurate)

Accuracy issues arise at the 3rd decimal place using only 6 bits for the fractional part:
 + float sin of 1 degree = 0.01745240643		Q9.6 sin(1) = 	0.016 (91.7% accurate)
 + float sin(2)			= 0.0348994967		Q9.6 sin(2) = 	0.031 (88.8% accurate) 
 + float sin(3)			= 0.05233595624		Q9.6 sin(3) = 	0.047 (89.8% accurate) 
 + float 0.023415		= 0.023415			Q9.6		 =	0.156 (66.7% accurate)
 
So the worst case scenario is the the 3dp is only 67% accurate.

NB Q9.6 fixed point math is only accurate to about 2.5 decimal places or or about 6% uncertainty at 3dp.

## Q notation
The Q notation consists of the letter Q followed by a pair of numbers m.n where m is the number of bits used for the integer part of the value, and n is the number of fraction bits.
By default, the notation describes signed binary fixed point format, with the unscaled integer being stored  in two's complement format, used in most binary processors.
The first bit always gives the sign of the value(1 = negative, 0 = non-negative), and it is not counted in the m parameter. Thus, the total number w of bits used is 1 + m + n - which is both counter-intuitive and frustrating.
