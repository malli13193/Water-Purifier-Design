import time
import requests

# Constants
THINGSPEAK_READ_API_KEY = 'YOUR_THINGSPEAK_READ_API_KEY'
THINGSPEAK_CHANNEL_ID = 'YOUR_THINGSPEAK_CHANNEL_ID'
SOLAR_PANEL_PIN = 17  # GPIO pin for controlling solar panel
MAX_CAPACITY = 100  # Max storage capacity in liters

# Initialize GPIO (assuming Raspberry Pi)
import RPi.GPIO as GPIO
GPIO.setmode(GPIO.BCM)
GPIO.setup(SOLAR_PANEL_PIN, GPIO.OUT)

# Function to get consumption data from ThingSpeak
def get_consumption_rate():
    url = f'https://api.thingspeak.com/channels/{THINGSPEAK_CHANNEL_ID}/fields/2.json?api_key={THINGSPEAK_READ_API_KEY}&results=1'
    response = requests.get(url)
    data = response.json()
    consumption_rate = float(data['feeds'][0]['field2'])
    return consumption_rate

# Function to control solar panel based on storage and consumption
def control_solar_panel(current_storage, consumption_rate):
    if current_storage >= MAX_CAPACITY:
        print("Max storage reached, turning off solar panel.")
        GPIO.output(SOLAR_PANEL_PIN, GPIO.LOW)  # Turn off solar panel
    elif consumption_rate > 0:  # Consumption has increased
        print("Consumption detected, turning on solar panel.")
        GPIO.output(SOLAR_PANEL_PIN, GPIO.HIGH)  # Turn on solar panel
    else:
        print("No consumption, keeping solar panel off.")
        GPIO.output(SOLAR_PANEL_PIN, GPIO.LOW)  # Keep off

# Simulate water storage and monitor consumption rate
current_storage = 0

while True:
    consumption_rate = get_consumption_rate()
    
    if GPIO.input(SOLAR_PANEL_PIN) == GPIO.HIGH:
        # Solar panel is running, increment storage
        current_storage += 1  # Simulating 1L added every iteration (adjust as needed)
    
    control_solar_panel(current_storage, consumption_rate)
    
    # Reset storage when consumption increases
    if consumption_rate > 0:
        current_storage -= consumption_rate  # Adjust storage based on consumption
    
    time.sleep(60)  # Check every 60 seconds
