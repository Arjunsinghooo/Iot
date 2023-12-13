Aim: Displaying different LED patterns with Raspberry Pi.

Components:

1. LED

2. 330Ω Register

3. 6 m-m jumper Wires

Connection diagram:

Code:

Centerdash-pattern.py

import RPi.GPIO as GPIO

import time

GPIO.setmode(GPIO.BCM)

GPIO.setwarnings(False)

GPIO.setup(5,GPIO.OUT)

GPIO.setup(6,GPIO.OUT)

GPIO.setup(13,GPIO.OUT)

GPIO.setup(19,GPIO.OUT)

GPIO.setup(26,GPIO.OUT)

list=[5,6,13,19,26]

 for num in range((len(list) / 2)+1):

GPIO.output(list[num],GPIO.HIGH)

GPIO.output(list[len(list)-num-1],GPIO.HIGH)

time.sleep(0.05)

GPIO.output(list[num],GPIO.LOW)

GPIO.output(list[len(list)-num-1],GPIO.LOW)

time.sleep(0.05)

GPIO.cleanup()

2b
import RPi.GPIO as GPIO
import time
import keyboard
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
GPIO.setup(5,GPIO.OUT)
GPIO.setup(6,GPIO.OUT)
GPIO.setup(13,GPIO.OUT)
GPIO.setup(19,GPIO.OUT)
GPIO.setup(26,GPIO.OUT)
list=[5,6,13,19,26]
print "Press q to Exit"
try:
 while True:
 if keyboard.is_pressed('q'):
 break;
 for num in range(len(list)):
 GPIO.output(list[num],GPIO.HIGH)
 time.sleep(0.05)
 GPIO.output(list[num],GPIO.LOW)
 time.sleep(0.05)
except KeyboardInterrupt:
 pass
GPIO.output(5,GPIO.LOW)
GPIO.output(6,GPIO.LOW)
GPIO.output(13,GPIO.LOW)
GPIO.output(19,GPIO.LOW)
GPIO.output(26,GPIO.LOW)
GPIO.cleanup()

3
import RPi.GPIO as GPIO
import time
GPIO.setmode(GPIO.BCM)
GPIO.setwarnings(False)
#GPIO.setup(4, GPIO.IN, pull_up_down=GPIO.PUD_DOWN)
segments = (17,27,22,23,24,25,5,6)
for segment in segments:
 GPIO.setup(segment, GPIO.OUT)
 GPIO.output(segment, 1)
digits = (16,20,21,12)
for digit in digits:
 GPIO.setup(digit, GPIO.OUT)
 GPIO.output(digit, 1)
num = {' ':(0,0,0,0,0,0,0),
 '0':(1,1,1,1,1,1,0),
 '1':(0,1,1,0,0,0,0),
 '2':(1,1,0,1,1,0,1),
 '3':(1,1,1,1,0,0,1),
 '4':(0,1,1,0,0,1,1),
 '5':(1,0,1,1,0,1,1),
 '6':(1,0,1,1,1,1,1),
 '7':(1,1,1,0,0,0,0),
 '8':(1,1,1,1,1,1,1),
 '9':(1,1,1,1,0,1,1)}
try:
 while True:
 n = time.ctime()[11:13]+time.ctime()[14:16]
 s = str(n).rjust(4)
 for digit in range(4):
 for loop in range(0,7):
 if num[s[digit]][loop] == 0:
 GPIO.output(segments[loop], 1)
 else:
 GPIO.output(segments[loop], 0)
 if (int(time.ctime()[18:19])%2 == 0) 
and (digit == 1):
 GPIO.output(6, 0)
 else:
 GPIO.output(6, 1)
 
 GPIO.output(digits[digit], 1)
 time.sleep(0.001)
 GPIO.output(digits[digit], 0)
except KeyboardInterrupt:
 GPIO.cleanup()

4
