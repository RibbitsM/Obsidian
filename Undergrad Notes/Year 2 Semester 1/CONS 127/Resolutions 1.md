- Spatial resolution is defined as the smallest possible feature that can be detected
- This is usually the area depicted by each pixel
- Satellite resolution is fixed because they maintain the same altitude, but planes and drones have a variable resolution depending on how close they are
- Each pixel represents a different reflectance value
- If a satellite has a resolution of 30 meters, then each pixel is 30 meters by 30 meters
- Spatial resolution is determined by platform, sensor, and geometry
- Platform means what the sensor is mounted on, what kind of sensor it is, and what kind of geometry it's observing
- MODIS is one of our most commonly used spatial sensing technologies
- Terra, Aqua, and Landsat all use MODIS and provide publicly available data
- IKONOS was a high resolution satellite that was used for urban planning, road mapping etc
- Had a spatial resolution of about 4 meters and was privately owned
- For extremely high spatial resolution, drones and airplanes equipped with digital cameras are used
- The main advantage is to make out individual features, in our context individual trees
- Instead of a single image, you work off of a collage of several
- Definitely not free, can either be government owned or private

Spectral Resolution

- Sensors measure the EMS in bands
- Say a satellite has 5 bands
- Generally the more bands, the finer the spectral resolution
- Each band has a certain size, say 700 nm to 850 nm
- Satellites don't measure the whole EMS, just portions of it
- Each band represents a different part of the spectrum, for example red, or ultraviolet
- Depending on which band is activated, the satellite knows what it's seeing
- To get a visual image, a satellite just needs red green and blue bands to create color composite

Temporal Resolution

- Measured by how long it takes for a satellite to return to a point on earth
- Basically, how long it takes for a satellite to orbit the earth once
- A coarse time scale would be monthly or annually, getting a picture every month isn't going to give us fine temporal detail
- A satellite with a faster orbit will give us a much better temporal resolution
- This depends on the kind of orbit, and also the swath width
- Swath width is basically the field of view of the satellite, it doesn't have to orbit until it's above the same spot, just until it can see the area in question
- The bigger the swath width, the better the temporal resolution
- Most satellites are either in close elliptical orbit (700-2000), or geostationary orbit (36000)
- Because geostationary orbits image the same spot constantly, they have unlimited temporal resolution only limited by how fast it can take images
- A close elliptical orbit will have a much lower temporal resolution