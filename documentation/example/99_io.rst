引脚控制
==============

数字输入
--------
gpio.digital_read(pin) 参数:引脚pin Px (P2 - P15)

例程::

    from labplus import *
    import time

    while 1:
        print(gpio.digital_read(P2))
        time.sleep(0.1)



数字输出
--------
gpio.digital_write(pin,LOW) 参数:引脚 pin: Px (P2 - P15), 输出 HIGH--1高电平/LOW--0 低电平

例程::

    from labplus import *
    import time

    while 1:
        gpio.digital_write(P13,HIGH) #设置引脚输出高电平
        time.sleep(1)
        gpio.digital_write(P13,LOW)
        time.sleep(1)




模拟输入ADC  
--------

gpio.analog_read(pin) 
参数:引脚 pin : P0/P1
返回值 范围(0-1800)

例程::

    from labplus import *
    import time

    while 1:
        adc0=gpio.analog_read(P0)
        adc1=gpio.analog_read(P1)
        print('ADC0 ====== ',adc0)
        print('ADC1 ====== ',adc1)
        time.sleep(0.1)




控制引脚pwm输出
--------

pwm.set_pin_pwm(pin,pwm) 
参数:
引脚 pin: P2/P3/P4/P5
pwm:  0 - 1024

例程::

    from labplus import *
    import time

    pwm.set_pin_pwm(P2,512)
    pwm.set_pin_pwm(P3,974) 



控制 M1、M2 pwm输出
--------
pwm.set_pwm(index,pwm) 
参数:
index：1/2 ，控制 M1、M2 pwm输出
pwm:  0 - 100


例程::

    from labplus import *
    import time

    while 1:
        pwm.set_pwm(1,10) 
        time.sleep(5)
        pwm.set_pwm(1,50) 
        time.sleep(5)
        pwm.set_pwm(1,80) 
        time.sleep(5)
        pwm.set_pwm(1,100) 
        time.sleep(5)
