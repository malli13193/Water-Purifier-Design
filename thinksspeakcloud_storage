import requests
import time

# ThingSpeak credentials
THINGSPEAK_API_KEY = 'YOUR_THINGSPEAK_WRITE_API_KEY'
THINGSPEAK_URL = "https://api.thingspeak.com/update"

# Simulate sensor data
def get_purification_data():
    return {
        'field1': 98,  # Water purity
        'field2': 0.5,  # Flow rate (L/min)
        'field3': 25   # Temperature (Celsius)
    }

while True:
    data = get_purification_data()
    response = requests.get(THINGSPEAK_URL, params={'api_key': THINGSPEAK_API_KEY, **data})
    if response.status_code == 200:
        print("Data sent to ThingSpeak:", data)
    else:
        print("Error:", response.status_code)
    time.sleep(60)  # Send data every 60 seconds
