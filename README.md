import requests

def get_weather_data(city, api_key):
    url = f"https://api.openweathermap.org/data/2.5/forecast/hourly?q={city}&appid={api_key}"
    response = requests.get(url)
    return response.json()

def get_weather_by_date(weather_data, date):
    for item in weather_data['list']:
        if date in item['dt_txt']:
            return item['main']['temp']
    return None

def get_wind_speed_by_date(weather_data, date):
    for item in weather_data['list']:
        if date in item['dt_txt']:
            return item['wind']['speed']
    return None

def get_pressure_by_date(weather_data, date):
    for item in weather_data['list']:
        if date in item['dt_txt']:
            return item['main']['pressure']
    return None

def main():
    city = input("Enter the city name: ")
    api_key = "YOUR_API_KEY"  # Replace this with your actual OpenWeatherMap API key

    weather_data = get_weather_data(city, api_key)

    while True:
        print("\nChoose an option:")
        print("1. Get weather")
        print("2. Get Wind Speed")
        print("3. Get Pressure")
        print("0. Exit")

        choice = input("Enter your choice: ")

        if choice == '1':
            date = input("Enter the date (YYYY-MM-DD HH:mm:ss format): ")
            temperature = get_weather_by_date(weather_data, date)
            if temperature is not None:
                print(f"The temperature at {date} is {temperature} Kelvin.")
            else:
                print("No weather data available for the given date.")

        elif choice == '2':
            date = input("Enter the date (YYYY-MM-DD HH:mm:ss format): ")
            wind_speed = get_wind_speed_by_date(weather_data, date)
            if wind_speed is not None:
                print(f"The wind speed at {date} is {wind_speed} m/s.")
            else:
                print("No weather data available for the given date.")

        elif choice == '3':
            date = input("Enter the date (YYYY-MM-DD HH:mm:ss format): ")
            pressure = get_pressure_by_date(weather_data, date)
            if pressure is not None:
                print(f"The pressure at {date} is {pressure} hPa.")
            else:
                print("No weather data available for the given date.")

        elif choice == '0':
            print("Exiting the program.")
            break

        else:
            print("Invalid choice. Please try again.")

if __name__ == "__main__":
    main()
