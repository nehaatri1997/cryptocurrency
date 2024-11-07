# cryptocurrency tracker

# Overview
This Python script fetches and tracks the real-time price of a specified cryptocurrency using the CoinGecko API. Users can customize the cryptocurrency, target currency, and update interval to receive regular updates on the price.

# Requirements
Python 3.x: Make sure you have Python 3 installed.
Requests Library: Install it by running the following command:

pip install requests

# How It Works
Fetch Price: The get_crypto_price function makes a request to the CoinGecko API to retrieve the current price of the specified cryptocurrency in the chosen currency.
Track Price in Loop: The track_price function continuously checks the cryptocurrency price at specified intervals, displaying the updated price in the console.

# Code Structure
get_crypto_price Function
Fetches the current price of a cryptocurrency in a specified currency.

1. Parameters:
crypto_id (str): The cryptocurrency’s ID on CoinGecko (e.g., bitcoin, ethereum).
currency (str): The currency code in which to display the price (e.g., usd, eur).
2. Returns: The price of the cryptocurrency in the specified currency if the request is successful; otherwise, it returns None and prints an error message.

# track_price Function
Tracks the cryptocurrency price in a loop at a given interval.

1. Parameters:
crypto_id (str): Cryptocurrency ID to track.
currency (str): Target currency for the price display.
interval (int): Time in seconds between each price update.

Example Code

import requests
import time

def get_crypto_price(crypto_id="bitcoin", currency="usd"):
    url = f"https://api.coingecko.com/api/v3/simple/price?ids={crypto_id}&vs_currencies={currency}"
    response = requests.get(url)

    if response.status_code == 200:
        data = response.json()
        return data[crypto_id][currency]
    else:
        print("Error fetching data from CoinGecko API.")
        return None

def track_price(crypto_id="bitcoin", currency="usd", interval=60):
    while True:
        price = get_crypto_price(crypto_id, currency)
        if price is not None:
            print(f"The current price of {crypto_id.capitalize()} in {currency.upper()} is: {price}")
        else:
            print("Failed to retrieve price.")
        time.sleep(interval)
        
crypto_id = input("Enter cryptocurrency ID (e.g., bitcoin, ethereum): ").strip().lower()
currency = input("Enter target currency (e.g., usd, eur): ").strip().lower()
interval = int(input("Enter update interval in seconds (e.g., 60): "))

track_price(crypto_id, currency, interval)

# Usage Instructions
1. Run the script.
2. Enter the cryptocurrency ID, the target currency, and the interval in seconds when prompted.
3. The script will continuously print the latest price at the specified interval.

# Notes
1. Ensure a stable internet connection for consistent data retrieval.
2. The CoinGecko API allows free access, but rate limits apply for excessive requests. Adjust the interval as needed.

# Sample Output

Enter cryptocurrency ID (e.g., bitcoin, ethereum): bitcoin
Enter target currency (e.g., usd, eur): usd
Enter update interval in seconds (e.g., 60): 10
The current price of Bitcoin in USD is: 40000.0


This script provides a simple way to monitor cryptocurrency prices in real time.
