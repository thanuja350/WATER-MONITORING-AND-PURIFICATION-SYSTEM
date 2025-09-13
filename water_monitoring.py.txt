import RPi.GPIO as GPIO
import time
import Adafruit_ADS1x15

# Set up GPIO pins
GPIO.setmode(GPIO.BCM)
GPIO.setup(17, GPIO.OUT)  # Pump relay
GPIO.setup(23, GPIO.OUT)  # Filtering system relay

# Set up sensors
ADS1015 = Adafruit_ADS1x15.ADS1015()
pH_pin = 0           # Analog input pin for pH sensor
turbidity_pin = 1    # Analog input pin for turbidity sensor
temperature_pin = 2  # Analog input pin for temperature sensor
water_level_pin = 24 # Digital input pin for water level sensor

def read_water_level():
    GPIO.setup(water_level_pin, GPIO.IN)
    return GPIO.input(water_level_pin)

def read_pH():
    return ADS1015.read_adc(pH_pin, gain=1)

def read_turbidity():
    return ADS1015.read_adc(turbidity_pin, gain=1)

def read_temperature():
    return ADS1015.read_adc(temperature_pin, gain=1)

def control_pump(water_level):
    if water_level < 50:  # Adjust threshold value as needed
        GPIO.output(17, GPIO.HIGH)  # Turn on pump
    else:
        GPIO.output(17, GPIO.LOW)   # Turn off pump

def control_filtering_system(pH, turbidity):
    if pH < 6.5 or turbidity > 100:  # Adjust threshold values as needed
        GPIO.output(23, GPIO.HIGH)  # Turn on filtering system
    else:
        GPIO.output(23, GPIO.LOW)   # Turn off filtering system

try:
    while True:
        water_level = read_water_level()
        pH = read_pH()
        turbidity = read_turbidity()
        temperature = read_temperature()
        
        control_pump(water_level)
        control_filtering_system(pH, turbidity)
        
        print(f"Water Level: {water_level}%")
        print(f"pH: {pH}")
        print(f"Turbidity: {turbidity}")
        print(f"Temperature: {temperature}°C")
        
        time.sleep(1)

except KeyboardInterrupt:
    print("Program stopped by User")
    GPIO.cleanup()
