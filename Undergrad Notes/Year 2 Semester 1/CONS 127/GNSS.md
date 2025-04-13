- First form of absolute positioning was celestial navigation
- GNSS is just an evolution of this concept, satellites are essentially just orbiting landmarks
- We know the precise position of these satellites, so GNSS calculates the distance between you and the three nearest satellites to triangulate or trilaterate your position
- The original GPS was developed by the US military and is primarily used in North America
- GPS is part of the global navigation satellite system, not the whole thing, in north america the two terms are interchangeable
- GNSS systems have a space segment (satellites), control segments (ground stations controlling satellites) and the user segment (phones)
- The ground stations communicate both ways with the satellites, and satellites only transmit information to phones, they do not receive information
- GPS has a minimum of 24 satellites on 6 orbits
- GPS is american, GLONASS is russian, GALILEO is european, and BeiDou is Chinese
- All have fairly similar specs, but BeiDou is geostationary
- New GPS technologies are constantly being updated and new satellites are being developed and launched all the time
- We're currently on generation 3 of GPS satellites
- The user segment is any GPS receiver, could be a phone or GPS devoted device
- The control segment includes antenna systems and master control systems, mainly used for monitoring satellites and maintaining their orbits
- GNSS systems use trilateration to determine your location by calculating how far you are from at least three known points
- Say a location is 175 km from Amsterdam, 185 km from Luxembourg, and 320 km from London
- To determine the point, just draw three circles around the cities and identify where they intersect
- If three satellites are above the horizon, they calculate how far you are from each one of them, and determine your position based on that
- These measurements are based on timing of signals
- Based on how long it takes for the signal from your phone to reach the satellite, you can determine the distance
- This is because radio waves always travel at the speed of light
- The more satellites you use, the more accurate your position will be

Position

- There are 5 steps to determining a position
- First the receiver downloads the satellites almanac, which provides information on the status and history of a satellite, this helps find other satellites (valid for 90 days)
- Next the receiver downloads the satellites ephemeris, which provides an accurate predicted location of the satellite and orbit path and also synchronizes the clocks of the satellite and receiver (valid for 2 hours)
- Third the satellite determines the time the signal takes to reach the satellite from the receiver
- Next the satellite calculates it's distance from at least three other satellites
- Finally it determines your position
- A receiver can work without an almanac but not without the ephemerides
- For the range calculation, the satellite just multiplies the time difference by the speed of light
- If a signal takes 0.03 seconds to transmit, then the receiver is 8994 km away
- All GPS signals have a PRN (pseudo random number/code) that essentially "timestamps" the signal
- All satellites know exactly when a certain PRN was generated
- Clocks accurate down to the billionth of a second are needed to properly calculate these distances
- Your phone is usually accurate to about 3-15 meters
- This can be influenced by the atmosphere, buildings, number of satellites, etc.
- GNSS receivers for precise surveying are accurate to about 10mm horizontally and 20 mm vertically (when using Differential GPS)
- Radio waves cannot pass through buildings, trees, or mountains
- They can also be reflected off of water or metal, causing a multipath error
- For best measurement, stand in the open with no buildings or trees, and take an average of several measurements
- Of course not all of these requirements are always possible, in enviro sci and forestry measurements are often taken in deep forest
- Number and position of satellites, atmospheric effects, receiver quality, corrections/post-processing all affect accuracy alongside obstructions

DOP

- DOP, or dilution of precision is a measure of the geometry of how satellites are distributed
- For best DOP we want satellites to be at a variety of positions, a poor one would have several grouped tightly together
- Several different kinds of DOP based on position (PDOP, most common), vertical position (VDOP), horizontal position (HDOP), and time (TDOP), meaning accuracy of satellite clocks
- A high DOP level (over 6) is bad, we want to aim for 1-3
- There are websites available to show where satellites are at different times of the day and when you will get the best accuracy
- Planning is a key part of getting good measurements
- Most advanced GPS systems can receive signals from any GNSS network
- In conclusion, errors can be due to receiver error, clock errors, ephemeris errors, ionosphere and troposphere values, and multipath errors
- Ionospheric delays create the most problems of all, this is the area between 1500 km and space
- There are often loose charged particles in the ionosphere that delays radio signals, causing significant error

Differential GNSS

- This is a technique that uses differential correction to increase accuracy
- We use a known base station that can act as another reference point that can send corrections to your GPS
- This is usually not done in real time
- There is also RTK or real time kinematic GPS which is more mobile and works faster
- Differential GNSS requires post processing, while RTK makes corrections on the spot
- This is how we get measurements accurate to the centimeter or millimeter
- The base station has a transmission antenna that also communicates with our roving GPS to communicate corrections
- Both techniques increase accuracy by using a second known landmark on earth
- Assisted GPS improves the start-up time of GPS, normally a receiver needs to gather data rom satellites before activating
- Assisted GPS uses cell towers to get this information faster
- Dead reckoning is also sometimes used to compensate for limitations of GNSS
- Google maps uses dead reckoning to estimate your position when the receiver loses communication with satellites
- More precise positioning in closed environments using wifi and bluetooth are being developed

Applications

- Besides transportation and navigation, GPS has other uses
- GPS is used for mapping and surveying, by accurately measuring points on earth we can correct and update maps
- Agriculture, aviation, environment, disaster relief, rec and wildlife all use GPS
-