<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link rel="stylesheet" href="styles.css">
  <title>Прогноз погоди</title>
</head>

<body>
  <div class="weather-container">
    <h1>Прогноз погоди</h1>
    <table id="weather-table">
      <thead>
        <tr style="text-align: center">
          <th>День</th>
          <th>Час</th>
          <th>Дата</th>
          <th>Температура (°K)</th>
          <th>Опис</th>
        </tr>
      </thead>
      <tbody id="weather-data"></tbody>
    </table>
  </div>
  <script src="script.js"></script>
</body>

</html>
document.addEventListener("DOMContentLoaded", function () {
    const apiKey = "e6e1f5ef68aa4a1fb47214526232012";
    const city = "Dnipro";


    fetch(apiUrl)
        .then(response => response.json())
        .then(data => {
            const weatherData = document.getElementById("weather-data");
            weatherData.innerHTML = ""; 

            
            data.list.forEach(item => {
                const date = new Date(item.dt * 1000);
                const day = date.toLocaleDateString("en-US", { weekday: "long" });
                const time = date.toLocaleTimeString("en-US", { hour: "numeric", minute: "numeric" });
                const formattedDate = date.toLocaleDateString();
                const temperature = item.main.temp.toFixed(1);
                const description = item.weather[0].description;

                
                const tableRow = document.createElement("tr");
                tableRow.innerHTML = <td style = "border: 1px solid black; text-align: center">${day}</td>;
                <td style = "border: 1px solid black; text-align: center">${time}</td>;
                <td style = "bordeer: 1px solid black; text-align: center">${formattedDate}</td>;
                <td style = "border: 1px solid black; text-align: center">${temperature}</td>;
                <td style = "border: 1px solid black; text-align: center">${description}</td>;

                weatherData.appendChild(tableRow);
            });
        })
        .catch(error => {
            console.error("Error fetching weather data:", error);
        });
});
html {
  height: 100%;
  width: 100%;
}
body {
    font-family: Arial, sans-serif;
    background-color: #f4f4f4;
    margin: 0;
    padding: 0;
}

.weather-container {
    max-width: 600px;
    margin: 50px auto;
    background-color: #fff;
    padding: 20px;
    border-radius: 8px;
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
}

h1 {
    text-align: center;
    color: #333;
}

#weather-data {
    margin-top: 20px;
}
