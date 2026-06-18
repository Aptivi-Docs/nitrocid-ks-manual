---
description: This is today's weather forecast.
icon: sun-cloud
metaLinks:
  alternates:
    - >-
      https://app.gitbook.com/s/yhORwVwuIgJMLsQRqN3S/fundamentals/simulated-kernel-features/extra-features/common-programs/weather
---

# Weather

<figure><img src="../../../../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>

The weather kernel addon allows you to check your city's weather forecast using either the Weather.com API (`weather`) or the OpenWeatherMap forecast API (`weather-old`). You can check the information about the current weather condition in your city, such as the state of the forecast, the wind speed, the humidity, and so on.

***

## <mark style="color:$primary;">Usage</mark>

You can use either the newer `weather` command or the older `weather-old` command.

In addition to that, you can consult the weather in an interactive TUI by calling the `weather` command with just the `-tui` switch.

{% hint style="info" %}
`weather`: You'll need to consult [this page](https://www.ibm.com/products/environmental-intelligence-suite) to learn how to get a 15 Day weather forecast API key from Weather.com.

`weather-old`: You can get the free weather forecast API key by going to [this page](https://home.openweathermap.org/api_keys). You'll need an OpenWeatherMap account.
{% endhint %}

{% hint style="info" %}
We recommend the Weather.com implementation using the `weather` command. The syntax is a bit different, because it requires that you know the latitude and the longitude of your area. If you want to get this information, you can use the `-list` switch, providing it your city name and your API key.
{% endhint %}

{% hint style="info" %}
Please note that the interactive TUI is not supported for the OpenWeatherMap version of the `weather` command.
{% endhint %}

***

## <mark style="color:$primary;">Supported properties</mark>

The weather kernel addon provides the following properties:

<table><thead><tr><th width="150">Property</th><th>Description</th></tr></thead><tbody><tr><td>Weather</td><td>The state of the weather forecast in your city (Clear, smoke, cloudy, raining, etc.)</td></tr><tr><td>Temperature</td><td>The temperature of the outside environment either in Celsius, in Kelvin, or in Fahrenheit</td></tr><tr><td>Feels like</td><td>The temperature that makes you feel like it either in Celsius, in Kelvin, or in Fahrenheit</td></tr><tr><td>Wind speed</td><td>The wind speed in the outside environment in meters per second</td></tr><tr><td>Wind direction</td><td>The direction of the wind in degrees</td></tr><tr><td>Pressure</td><td>The pressure in Hectopascals</td></tr><tr><td>Humidity</td><td>The weather humidity in percentage</td></tr></tbody></table>
