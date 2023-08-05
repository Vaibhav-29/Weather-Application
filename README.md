# Weather-Application

# HTML Structure
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather Application</title>
  <link rel="stylesheet" href="styles.css">
</head>
<body>
  <div class="container">
    <input type="text" id="locationInput" placeholder="Enter location (e.g., city name or zip code)">
    <button id="searchButton">Search</button>
    <div id="weatherInfo"></div>
  </div>
  <script src="app.js"></script>
</body>
</html>

#CSS Styling
body {
  font-family: Arial, sans-serif;
  margin: 0;
  padding: 0;
}

.container {
  max-width: 400px;
  margin: 50px auto;
  padding: 20px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

input {
  width: 100%;
  padding: 10px;
  font-size: 16px;
  margin-bottom: 10px;
}

button {
  background-color: #007bff;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
}

#weatherInfo {
  margin-top: 20px;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 8px;
}

#JavaScript logic
const API_KEY = 'YOUR_API_KEY';
const searchButton = document.getElementById('searchButton');
const locationInput = document.getElementById('locationInput');
const weatherInfo = document.getElementById('weatherInfo');

searchButton.addEventListener('click', fetchWeatherData);

async function fetchWeatherData() {
  const location = locationInput.value;
  if (!location) return;

  try {
    const response = await fetch(`https://api.openweathermap.org/data/2.5/weather?q=${location}&appid=${API_KEY}&units=metric`);
    if (!response.ok) {
      throw new Error('Weather data not found');
    }
    const data = await response.json();
    displayWeather(data);
  } catch (error) {
    displayError(error.message);
  }
}

function displayWeather(data) {
  const weather = data.weather[0];
  const temperature = data.main.temp;
  const windSpeed = data.wind.speed;
  const humidity = data.main.humidity;
  const cityName = data.name;

  weatherInfo.innerHTML = `
    <h2>${cityName}</h2>
    <p>${weather.description}</p>
    <p>Temperature: ${temperature}°C</p>
    <p>Wind Speed: ${windSpeed} m/s</p>
    <p>Humidity: ${humidity}%</p>
    <p>${new Date().toLocaleString()}</p>
  `;
}

function displayError(errorMessage) {
  weatherInfo.innerHTML = `<p>Error: ${errorMessage}</p>`;
}

#J
