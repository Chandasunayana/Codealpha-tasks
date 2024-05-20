import React, { useEffect } from 'react';

const WeatherMap = ({ location }) => {
  useEffect(() => {
    // Initialize map and add weather layer
    const map = new google.maps.Map(document.getElementById('map'), {
      zoom: 10,
      center: { lat: 40.7128, lng: -74.0060 }, // Default to New York
    });

    const weatherLayer = new google.maps.weather.WeatherLayer({
      temperatureUnits: google.maps.weather.TemperatureUnit.CELSIUS,
    });
    weatherLayer.setMap(map);

    // Update map center based on location
    const geocoder = new google.maps.Geocoder();
    geocoder.geocode({ address: location }, (results, status) => {
      if (status === 'OK') {
        map.setCenter(results[0].geometry.location);
      }
    });
  }, [location]);

  return <div id="map" style={{ height: '400px', width: '100%' }}></div>;
};

export default WeatherMap;


