---
layout: single
title: "Weather API Project_1"
categories: project
tags: [weather-api]
author_profile: false
search: true
---

[my github repo](https://github.com/HenryChung98/weatherApp)

### Programming languages used

- html
- css
- javaScript

### Introduction

We will make simple weather app using [Open Weather API](https://openweathermap.org/api).
First we need to prepare assets for search button, weather icons, wind speed, air quality, and humidity.

I assume you all set and move to code work.

### code

#### frame

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Weather App</title>
</head>
<body>
  <div class="card">
    <div class="search">
      <input type="text" placeholder="enter city name" spellcheck="false">
      <button><img src="images/search.png"></button>
    </div>
    <div class="error">
      <img src="images/error.png" alt="">
      <p>WRONG CITY NAME!</p>
    </div>
    <div class="container">
    <div class="weather">
      <img src="images/rain.png" class="weatherIcon">
      <h1 class="temp">0°c</h1>
      <h2 class="city">city</h2>
      <div class="details">
        <div class="col">
          <img src="images/humidity.png">
          <div>
            <p class="humidity">50%</p>
            <p>Humidity</p>
          </div>
        </div>
          <div class="col">
            <img src="images/windsock.png">
            <div>
              <p class="wind">15 km/h</p>
              <p>Wind Speed</p>
            </div>
          </div>
            <div class="col">
              <img src="images/dust.png" class="airIcon">
              <div>
                <p class="airQual">1</p>
                <p>Air Quality</p>
              </div>
              </div>
        </div>
        </div>
        <div class="information">
          <h1 class="time">00:00:00</h1>
          <div id="map"></div>
        </div>
      </div>
      </div>

    </div>
</body>
<link rel="stylesheet" href="style.css">
<script type = "text/javascript" src="apiKey.js"></script>
<script src="main.js"></script>
</html>
```

#### css

css code

```css
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  background-color: #222;
}

.card {
  width: 90%;
  background: #887d6b;
  color: #fff;
  margin: 100px auto 0;
  border-radius: 20px;
  padding: 40px 35px;
  text-align: center;
}

.search {
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.search input {
  border: 0;
  outline: 0;
  background: #ebfffc;
  color: #555;
  padding: 10px 25px;
  height: 60px;
  border-radius: 30px;
  flex: 1;
  margin-right: 16px;
  font-size: 18px;
}

.search button {
  border: 0;
  outline: 0;
  background: #ebfffc;
  border-radius: 50%;
  width: 60px;
  height: 60px;
  cursor: pointer;
}

.search button img {
  width: 16px;
}

.weatherIcon {
  width: 170px;
  margin-top: 30px;
}

.weather h1 {
  font-size: 80px;
  font-weight: 500;
}
.weather h2 {
  font-size: 45px;
  font-weight: 400;
  margin-top: -10px;
}

.details {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0, 20px;
  margin-top: 70px;
}

.col {
  display: flex;
  align-items: center;
  text-align: left;
}

.col img {
  width: 40px;
  margin-right: 10px;
}

.weather,
.information {
  display: none;
  min-width: 400px;
}

.error {
  text-align: center;
  margin-top: 10px;
  font-size: 30px;
  color: #f16051;
  display: none;
}

.time {
  text-align: center;
  margin-top: 10px;
}
.container {
  display: flex;
  justify-content: space-around;
}

#map {
  border: solid black;
  border-radius: 10px;
  width: 95%;
  min-height: 350px;
  margin: 20px;
}
@media screen and (max-width: 768px) {
  .card {
    max-width: 470px;
  }
  .container {
    flex-direction: column;
  }
}
@media screen and (min-width: 769px) {
  .card {
    min-width: 850px;
  }
}
```
