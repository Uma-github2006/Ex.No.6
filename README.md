# Ex.No.6 Development of Python Code Compatible with Multiple AI Tools

## Date: 30-10-2025
## Register no : 212223060293
## Aim: 
Write and implement Python code that integrates with multiple AI tools to automate the task of interacting with APIs, comparing outputs, and generating actionable insights with Multiple AI Tools

## AI Tools Required:
- Gemini
- Chatgpt 
## Explanation:
- Experiment the persona pattern as a programmer for any specific applications related with your interesting area. 
- Generate the outoput using more than one AI tool and based on the code generation analyse and discussing that.
  
## Prompt : “Write a Python program for my IoT-based smart environment project that fetches temperature and humidity data from an IoT sensor API and the OpenWeatherMap API, then displays both values side by side in a Pandas table.”
## Step 1:Generate Python code for interacting with multiple APIs

<img width="919" height="565" alt="image" src="https://github.com/user-attachments/assets/b3318451-6919-46e3-9011-9d069808f818" />

###  Project Code
```
import requests
import pandas as pd

# IoT Sensor API (Indoor Data)
iot_url = "https://api.thingspeak.com/channels/123456/feeds/last.json?api_key=YOUR_API_KEY"

# OpenWeatherMap API (Outdoor Data)
weather_url = "https://api.openweathermap.org/data/2.5/weather?q=Chennai&appid=YOUR_WEATHER_API_KEY&units=metric"

# Fetch data from IoT API
iot_response = requests.get(iot_url)
iot_data = iot_response.json()

# Fetch data from OpenWeatherMap API
weather_response = requests.get(weather_url)
weather_data = weather_response.json()

# Extract values
indoor_temp = float(iot_data.get("field1", 0))   # assuming field1 = temperature
indoor_humidity = float(iot_data.get("field2", 0))  # assuming field2 = humidity

outdoor_temp = weather_data["main"]["temp"]
outdoor_humidity = weather_data["main"]["humidity"]

# Display both data side by side
data = {
    "Source": ["Indoor (IoT Sensor)", "Outdoor (OpenWeatherMap)"],
    "Temperature (°C)": [indoor_temp, outdoor_temp],
    "Humidity (%)": [indoor_humidity, outdoor_humidity]
}

df = pd.DataFrame(data)
print(df)

```
## Explanation
The code directly requests JSON data from both the IoT sensor API and the OpenWeatherMap API, extracts the temperature and humidity values, and displays them side by side in a Pandas table. It’s simple, efficient, and clearly shows the difference between indoor and outdoor readings. However, it does not include exception handling or validation for missing data.
### Functional Python script that:
- Fetches weather data using the requests module from both APIs.
- Extracts key parameters — temperature and humidity.
- Displays the results clearly in a Pandas table for easy comparison.

## Gemini Output
```
import pandas as pd
import requests

# --- Configuration & Mock Keys ---
MOCK_IOT_ENDPOINT = "http://192.168.1.100/data" # Placeholder for local sensor API
OPENWEATHERMAP_API_KEY = "YOUR_OWM_API_KEY_HERE"
TARGET_CITY = "New Delhi" 
LATITUDE, LONGITUDE = 28.7041, 77.1025

def fetch_iot_data():
    """
    Simulates fetching real-time temperature and humidity from a local IoT sensor.
    In a real project, this would be an actual HTTP GET request to the sensor's IP.
    """
    try:
        # response = requests.get(MOCK_IOT_ENDPOINT, timeout=5)
        # response.raise_for_status() # Raise exception for bad status codes
        
        # --- MOCK DATA SIMULATION ---
        data = {
            'temperature_c': 26.5,  # IoT Sensor Reading (e.g., in the corner of the room)
            'humidity_perc': 62.0
        }
        return data
    except Exception as e:
        print(f"Error fetching IoT data: {e}")
        return None

def fetch_owm_data(city):
    """
    Simulates fetching temperature and humidity from OpenWeatherMap.
    """
    # Note: Using mock data to avoid needing a real API key for execution.
    # The actual OWM API returns data in Kelvin (needs conversion) or Celsius (if 'units=metric').
    
    # --- MOCK DATA SIMULATION ---
    mock_owm_response = {
        'main': {
            'temp': 29.8,      # OWM Temperature
            'humidity': 55     # OWM Humidity
        }
    }
    
    if 'main' in mock_owm_response:
        return {
            'temperature_c': mock_owm_response['main']['temp'],
            'humidity_perc': mock_owm_response['main']['humidity']
        }
    else:
        return None

def generate_comparison_table():
    """Fetches, combines, and displays data in a Pandas DataFrame."""
    
    # 1. Fetch Data
    iot_results = fetch_iot_data()
    owm_results = fetch_owm_data(TARGET_CITY)

    if not iot_results or not owm_results:
        print("Failed to retrieve data from one or both sources. Cannot generate table.")
        return

    # 2. Combine Data into a structured format for Pandas
    comparison_data = {
        'IoT Sensor': [iot_results['temperature_c'], iot_results['humidity_perc']],
        'OpenWeatherMap': [owm_results['temperature_c'], owm_results['humidity_perc']]
    }

    # 3. Create Pandas DataFrame
    index_labels = ['Temperature (°C)', 'Humidity (%)']
    df = pd.DataFrame(comparison_data, index=index_labels)

    # Display the result
    print(f"--- Comparison for {TARGET_CITY} ---")
    print(df)
    
    return df

if __name__ == '__main__':
    comparison_df = generate_comparison_table()
    # Now, comparison_df holds the table for the next prompt stage.
```
## Gemini Explanation
The code uses Python functions to simulate fetching temperature and humidity data from a local IoT sensor API and the OpenWeatherMap API, then extracts these values and displays them side by side in a clean Pandas table. It's a clear, modular way to juxtapose indoor and outdoor environmental readings. The structure includes basic error handling by checking if fetched results are valid (if not iot_results or not owm_results:), which prevents the DataFrame from being created with bad data.

### The preceding prompt successfully guided the AI to produce a modular and structured Python script that:
- Fetches environmental data using dedicated functions (fetch_iot_data and fetch_owm_data) for both the simulated local sensor and the public API, using mock data placeholders.
- Extracts both temperature and humidity data points (temperature_c and humidity_perc).
- Clearly displays the combined results in a Pandas DataFrame (generate_comparison_table) for immediate visual comparison.
  
## Step 2 : Compare outputs from different APIs and highlight differences.

| Criteria                 | **My Project Code (Manual)**                              | **AI-Generated Code (Gemini)**                                                                                 |
| ------------------------ | --------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Code Structure**       | Straightforward and linear — all logic in a single block. | Modular — separated into reusable functions (`fetch_iot_data`, `fetch_owm_data`, `generate_comparison_table`). |
| **Data Source Handling** | Directly fetches live JSON data from actual APIs.         | Uses mock/simulated data to represent API calls (for demo or testing).                                         |
| **Error Handling**       | No error handling or validation.                          | Includes `try–except` and result checks (`if not iot_results or not owm_results`).                             |
| **Output Format**        | Simple Pandas table printed directly.                     | Nicely formatted comparison table with city name and labeled indexes.                                          |
| **Execution Simplicity** | Quick and easy to test for real IoT data.                 | Safer, structured, and more maintainable for future expansion.                                                 |

### Analysis
- My project code focuses on real API interaction, making it closer to an actual IoT setup.
- The AI-generated version is more structured and includes extra features like modular design, error handling, and mock testing.
- Gemini’s output would be more suitable for presentation and scalable projects, while my version is good for quick validation and prototyping.

## Step 3: Suggest Meaningful Insights or Next Steps Based on the Results
### Insights from the Comparison
- The indoor IoT data helps monitor local room or lab conditions in real time.
- The outdoor OpenWeatherMap data provides environmental reference values for comparison.
- The difference between indoor and outdoor readings can show how effectively the room or building maintains temperature and humidity stability.
- For example: if the indoor temperature is consistently higher than outdoor, it may indicate poor ventilation or heat accumulation.

### Next Steps for Improvement
- Add Exception Handling : Include try–except blocks to handle missing or incorrect API data safely.
- Store and Analyze Trends : Save data into a database (like ThingSpeak or Azure IoT) to study long-term temperature/humidity variations.
- Data Visualization : Use graphs in Matplotlib or Excel to visualize daily or weekly environmental changes.
- Automation : Use the comparison data to trigger alerts (like turning on a fan or humidifier) when indoor readings exceed limits.
- Improve Prompting : In the next AI prompt, specifically ask: “Add error handling, data visualization, and control actions based on comparison results.”

## Reflection Note
This stage helped me understand how AI-generated insights can guide improvements in real IoT-based projects. I learned that comparing both API results not only checks accuracy but also helps design smart control systems for maintaining an ideal indoor environment.

## Conclusion:
Through this exercise, I learned how to use AI tools effectively to assist in project coding. By designing proper prompts, I was able to generate working Python code that connects to multiple APIs, compares their outputs, and provides useful insights. Comparing my own code with the AI-generated version helped me understand the importance of structured programming, error handling, and modular design. This activity also showed how AI can act as a helpful partner in developing and improving IoT-based smart environment projects.


## Result: 
The corresponding Prompt is executed successfully.
