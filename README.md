# Weather-App
My first HTML , CSS and Javascript Project
<script>
    // Define API key and API URL for fetching weather data
    const apiKey = "958b619c9ff67d354d9cc0b802db67b6";
    const apiUrl = "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";

    // Select necessary elements from the HTML document
    const searchBox = document.querySelector(".search input");
    const searchBtn = document.querySelector(".search button");
    const weatherIcon = document.querySelector(".weather-icon");

    // Define an asynchronous function to fetch weather data from the API
    async function checkWeather(city) {
        // Fetch weather data from the API using the provided city name and API key
        const response = await fetch(apiUrl + city + `&appid=${apiKey}`);

        // Check if the response status is 404 (city not found)
        if (response.status == 404) {
            // If city not found, display error message and hide weather details
            document.querySelector(".error").style.display = "block";
            document.querySelector(".weather").style.display = "none";
        } else {
            // If city found, parse the JSON data
            const data = await response.json();
            
            // Update weather information in the HTML document
            document.querySelector(".city").innerHTML = data.name;
            document.querySelector(".temp").innerHTML = Math.round(data.main.temp) + "°C";
            document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
            document.querySelector(".wind").innerHTML = data.wind.speed + "km/h";

            // Set appropriate weather icon based on weather condition
            if (data.weather[0].main == "Clouds") {
                weatherIcon.src = "images/clouds.png";
            } else if (data.weather[0].main == "Clear") {
                weatherIcon.src = "images/clear.png";
            } else if (data.weather[0].main == "Rain") {
                weatherIcon.src = "images/rain.png";
            } else if (data.weather[0].main == "Drizzle") {
                weatherIcon.src = "images/drizzle.png";
            } else if (data.weather[0].main == "Mist") {
                weatherIcon.src = "images/mist.png";
            }

            // Display weather details and hide error message
            document.querySelector(".weather").style.display = "block";
            document.querySelector(".error").style.display = "none";
        }
    }

    // Event listener for search button click
    searchBtn.addEventListener("click", () => {
        // Call checkWeather function with the value entered in the search input
        checkWeather(searchBox.value);
    });
</script>

