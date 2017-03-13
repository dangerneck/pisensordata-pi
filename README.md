# Raspberry Pi Sensor data project

 

## Requirements:

1. Python program to sample Sense HAT data and submit to an API
2. API for receiving data
3. DB to store data
4. Web application to provide views of data including:
   - Graph view of data points over time
   - Raw data
   - Whatever else is cool

 

## Tasks satisfying requirements:

1. **Python program**

   1. Using the [http://pythonhosted.org/sense-hat/](http://pythonhosted.org/sense-hat/) library sample available data from sensors:
      1.  Gyroscope
      2. Accelerometer
      3. Magnetometer
      4. Temperature
      5. Humidity
      6. Barometric pressure


   2. Submit sampled data at a decided interval to an API

   ​

2. **API**

   1. Receive JSON data from the python program
   2. Possibly bother with oauth

3. **CouchDB db storing all received data by date and type**

4. **Vue.js + D3(probably) for graphs**

     1. All data points over time graphs
     2. I dunno what else?

     ​

## Data structures

### Sensor data (JSON)

```json
{
  "humidity": 0.00, // percentage humidity (float)
  "temperature": 0.00, // degrees Celsius (float)
  "pressure": 0.00, // pressure in Millibars (float)
  "orientation": {
    "pitch": 0.00, // degrees (float)
  	"roll": 0.00, // degrees (float)
  	"yaw": 0.00 // degrees (float)
  },
  "directionNorth": 0.00, // direction north from the magnetometer in degrees (float)
  "magnetometerRaw": {
    "x": 0.00, // magnetic intensity of axis in microteslas (float)
    "y": 0.00, // magnetic intensity of axis in microteslas (float)
    "z": 0.00 // magnetic intensity of axis in microteslas (float)
  },
  "accelerometerRaw":{
    "x": 0.00, // acceleration intensity of the axis in Gs (float)
    "y": 0.00, // acceleration intensity of the axis in Gs (float)
    "z": 0.00 // acceleration intensity of the axis in Gs (float)
  },
  "captureTime": 1424233311.771502, // unix epoch  at capture moment (float)
  "capturePeriodStart": 1424233311.771502, //unix epoch at capture period start (float)
  "capturePeriodEnd": 1424233311.771502 //unix epoch at capture period end (float)
}
```

 This could represent the data captured at a single instant or over a period. 
If it is over a period we could either:

1. Submit the average over the period in the format above, or
2. Submit to the API an array of the above for each moment captured

If we went with the second one the structure should be:

```json
{
  "data": [
    // the entire JSON object as above excluding capturePeriodStart and capturePeriodEnd
    // ... 
    "captureTime": 1424233311.771502,
  ],
  "capturePeriodStart": 1424233311.771502, 
  "capturePeriodEnd": 1424233311.771502
}
```

 

 