import requests

def get_weather_data(api_response):
    data = api_response

    date = input("Enter the date (format: YYYY-MM-DD HH:MM:SS): ")
    for entry in data["list"]:
        if entry["dt_txt"] == date:
            temp = entry["main"]["temp"]
            print(f"Temperature on {date}: {temp} K")
            break
    else:
        print("Date not found in the weather data.")


def get_wind_speed(api_response):
    data = api_response
    date = input("Enter the date (format: YYYY-MM-DD HH:MM:SS): ")
    for entry in data["list"]:
        if entry["dt_txt"] == date:
            wind_speed = entry["wind"]["speed"]
            print(f"Wind Speed on {date}: {wind_speed} m/s")
            break
    else:
        print("Date not found in the weather data.")


def get_pressure(api_response):
    data = api_response
    date = input("Enter the date (format: YYYY-MM-DD HH:MM:SS): ")
    for entry in data["list"]:
        if entry["dt_txt"] == date:
            pressure = entry["main"]["pressure"]
            print(f"Pressure on {date}: {pressure} hPa")
            break
    else:
        print("Date not found in the weather data.")


if __name__ == "_main_":
    api_url = "https://samples.openweathermap.org/data/2.5/forecast/hourly?q=London,us&appid=b6907d289e10d714a6e88b30761fae22"

    response = requests.get(api_url)

    if response.status_code == 200:
        api_response = response.json()
    else:
        print("Error fetching data from the API.")
        exit(1)

    while True:
        print("\n1. Get weather\n2. Get Wind Speed\n3. Get Pressure\n0. Exit")
        choice = input("Enter your choice: ")

        if choice == "1":
            get_weather_data(api_response)
        elif choice == "2":
            get_wind_speed(api_response)
        elif choice == "3":
            get_pressure(api_response)
        elif choice == "0":
            print("Exiting the program.")
            break
        else:
            print("Invalid choice. Please try again.")

