---
layout: single
title: "Weather API Project Process_2"
categories: project
tags: [html, css, javaScript, weather_api]
author_profile: false
search: true
---

To use open weather api, you need to get api key from the website, and follow the step.
api key should not be exposed, so I save the keys in different file.

#### api key container

```javascript
// ./apiKey.js
const config = {
  weatherKey: "api key for weather",
  airKey: "api key for air quality",
  googleMapKey: "api key for google map",
};
```

#### variables and api stuff

Usually urls are recommended to assign a value so that your code is more readable.
Additionally, I used google map api to show where you search.

```javascript
// import api keys
const weatherKey = config.weatherKey;
const airKey = config.airKey;
const googleKey = config.googleMapKey;

// api urls
const weatherUrl =
  "https://api.openweathermap.org/data/2.5/weather?units=metric&q=";
const airUrl = "http://api.openweathermap.org/data/2.5/air_pollution?";

// get elements from html
const searchBox = document.querySelector(".search input");
const searchBtn = document.querySelector(".search button");
const weatherIcon = document.querySelector(".weatherIcon");
const airIcon = document.querySelector(".airIcon");

// google map
((g) => {
  var h,
    a,
    k,
    p = "The Google Maps JavaScript API",
    c = "google",
    l = "importLibrary",
    q = "__ib__",
    m = document,
    b = window;
  b = b[c] || (b[c] = {});
  var d = b.maps || (b.maps = {}),
    r = new Set(),
    e = new URLSearchParams(),
    u = () =>
      h ||
      (h = new Promise(async (f, n) => {
        await (a = m.createElement("script"));
        e.set("libraries", [...r] + "");
        for (k in g)
          e.set(
            k.replace(/[A-Z]/g, (t) => "_" + t[0].toLowerCase()),
            g[k]
          );
        e.set("callback", c + ".maps." + q);
        a.src = `https://maps.${c}apis.com/maps/api/js?` + e;
        d[q] = f;
        a.onerror = () => (h = n(Error(p + " could not load.")));
        a.nonce = m.querySelector("script[nonce]")?.nonce || "";
        m.head.append(a);
      }));
  d[l]
    ? console.warn(p + " only loads once. Ignoring:", g)
    : (d[l] = (f, ...n) => r.add(f) && u().then(() => d[l](f, ...n)));
})({
  key: googleKey,
  v: "weekly",
});
let map;

async function initMap(getLat, getLng) {
  const { Map } = await google.maps.importLibrary("maps");

  map = new Map(document.getElementById("map"), {
    center: { lat: getLat, lng: getLng },
    zoom: 11,
  });
}
// google map
```

#### functions

```javascript
async function checkWeather(city) {
  const responseWeather = await fetch(
    weatherUrl + city + `&appid=${weatherKey}`
  );
  var data = await responseWeather.json();

  // error handling
  if (responseWeather.status == 404) {
    document.querySelector(".error").style.display = "block";
    document.querySelector(".weather").style.display = "none";
    document.querySelector(".information").style.display = "none";
  } else {
    // to get the location
    let lat = data.coord.lat;
    let lon = data.coord.lon;

    // to get air quality api
    const responseAir = await fetch(
      airUrl + `lat=${lat}&lon=${lon}` + `&appid=${airKey}`
    );
    var airQual = await responseAir.json();

    // check sun
    let sunRise = new Date(data.sys.sunrise * 1000);
    let sunSet = new Date(data.sys.sunset * 1000);
    let currentForSun = new Date();
    let sRise;
    let sSet;
    if (sunRise < currentForSun && sunSet > currentForSun) {
      sRise = true;
      sSet = false;
      console.log("rise");
    } else {
      sRise = false;
      sSet = true;
      console.log("set");
    }

    // weather
    if (data.weather[0].main == "Clear") {
      if (sRise == true) {
        weatherIcon.src = "images/clear.png";
      } else {
        weatherIcon.src = "images/clearMoon.png";
      }
    } else if (data.weather[0].main == "Clouds") {
      weatherIcon.src = "images/clouds.png";
    } else if (data.weather[0].main == "Rain") {
      weatherIcon.src = "images/rain.png";
    } else if (data.weather[0].main == "Snow") {
      weatherIcon.src = "images/snow.png";
    } else if (data.weather[0].main == "fog") {
      weatherIcon.src = "images/fog.png";
    }

    // change background color depending on sun
    if (sRise == true) {
      document.querySelector(".card").style.background =
        "linear-gradient(135deg, #00feba, #388eb4)";
    } else if (sSet == true) {
      document.querySelector(".card").style.background =
        "linear-gradient(135deg, #070a1f, #1d4ca0)";
    }

    document.querySelector(".weather").style.display = "block";
    document.querySelector(".information").style.display = "block";
    document.querySelector(".error").style.display = "none";

    initMap(lat, lon);

    // get UTC time
    const current = new Date();
    current.setSeconds(current.getSeconds() + 8 * 3600); // convert to UTC from vancouver time
    current.setSeconds(current.getSeconds() + data.timezone);

    // date and time formatting
    let forDate;
    let hours = current.getHours();
    let minutes = current.getMinutes();
    let seconds = current.getSeconds();
    const month = [
      "January",
      "February",
      "March",
      "April",
      "May",
      "June",
      "July",
      "August",
      "September",
      "October",
      "November",
      "December",
    ];

    // time
    if (hours < 10) {
      hours = "0" + hours;
    }
    if (minutes < 10) {
      minutes = "0" + minutes;
    }
    if (seconds < 10) {
      seconds = "0" + seconds;
    }

    // date format
    if (
      current.getDate() == "1" ||
      current.getDate() == "21" ||
      current.getDate() == "31"
    ) {
      forDate = "st";
    } else if (current.getDate() == "2" || current.getDate() == "22") {
      forDate = "nd";
    } else if (current.getDate() == "3" || current.getDate() == "23") {
      forDate = "rd";
    } else {
      forDate = "th";
    }

    // get data from api
    document.querySelector(".city").innerHTML = data.name;
    document.querySelector(".temp").innerHTML =
      Math.round(data.main.temp) + "°c";
    document.querySelector(".humidity").innerHTML = data.main.humidity + "%";
    document.querySelector(".wind").innerHTML = data.wind.speed + " km/h";
    document.querySelector(".airQual").innerHTML =
      airQual.list[0].components.pm10 + " pm10";

    document.querySelector(".time").innerHTML =
      current.getDate() +
      forDate +
      "&nbsp&nbsp" +
      month[current.getMonth()] +
      ", &nbsp" +
      current.getFullYear() +
      "<br/>" +
      hours +
      " : " +
      minutes;

    console.log(data);
  }
}

// event listeners
searchBtn.addEventListener("click", () => {
  checkWeather(searchBox.value);
});
document.addEventListener("keyup", function (event) {
  if (event.keyCode === 13) {
    checkWeather(searchBox.value);
  }
});
```

[my github repo](https://github.com/HenryChung98/weatherApp)
