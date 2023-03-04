from motorcontroller import *
from machine import Pin, ADC
import time
import math

import sc

# Declare I/O pins for light sensor and potentiometer
pot0InputPin = machine.Pin(26) #Pin A2
pot1InputPin = machine.Pin(27) #Pin A3
pot2InputPin = machine.Pin(28) #Pin A2
pot3InputPin = machine.Pin(29) #Pin A2
#pot4InputPin = machine.Pin(12) #Pin A2

pot0 = machine.ADC(pot0InputPin)
pot1 = machine.ADC(pot1InputPin)
pot2 = machine.ADC(pot2InputPin)
pot3 = machine.ADC(pot3InputPin)
#pot4 = machine.ADC(pot4InputPin)

print(pot0.read_u16())
print(pot1.read_u16())
print(pot2.read_u16())
print(pot3.read_u16())
#print(pot4.read_u16())

sendnumeros = 12

MySerial = sc.serial_comm(115200)
MySerial.abort()

while True:
    sendnumeros = 12
    #print('0:',pot0.read_u16())
    if pot0.read_u16() > 20000:

        print('-------0-------')
        sendnumeros = 0
    #print('1:',pot1.read_u16())
    if pot1.read_u16() > 20000:
        print('-------1-------')
        sendnumeros = 1
    #print('2:',pot2.read_u16())
    if pot2.read_u16() > 20000:
        print('------2------')
        sendnumeros = 2
    #print('3:',pot3.read_u16())
    if pot3.read_u16() > 20000:
        print('------3------')
        sendnumeros = 3
    
    code ='''
import time
import machine
from secrets import Tufts_Wireless as wifi
import mqtt_CBR
    
mqtt_broker = '10.245.145.47' 
topic_sub = 'Two/listen'
topic_pub = 'Two/listen'
client_id = 'Marc&Fo'

mqtt_CBR.connect_wifi(wifi)
led = machine.Pin(2, machine.Pin.OUT)  # 6 for 2040

def blink(delay = 0.1):
    led.off()
    time.sleep(delay)
    led.on()
    
def whenCalled(topic, msg):
    print((topic.decode(), msg.decode()))
    blink()
    time.sleep(0.5)
    blink()
        
def main():
    fred = mqtt_CBR.mqtt_client(client_id, mqtt_broker, whenCalled)
    fred.subscribe(topic_sub)

    old = 0
    i = 0
    

    try:
        fred.check()
        msg = 'iteration %d' % i
        fred.publish(topic_pub, '{0}')
        time.sleep(1)
        i += 1
        blink()
    except OSError as e:
        print(e)
        fred.connect()
    except KeyboardInterrupt as e:
        fred.disconnect()
        print('done')
main()
    '''.format(sendnumeros)
    
    print(sendnumeros)
    time.sleep(1)
    
    MySerial.send_code(code)
    
    while MySerial.any():
        if MySerial.any():
            text = MySerial.readln();
            print(text, end = "")
        time.s.
