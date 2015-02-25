
d3로 행성 좌표 그리기
====

## 행성 위치 데이타 구하기

- [Astro-Phys.com](http://www.astro-phys.com/api)  
많은 도움이 되어줄... 걸로 기대하는데 coefficient는 뭐지!?!
 
[HORIZONS Web-Interface](http://ssd.jpl.nasa.gov/horizons.cgi)  
천문력을 계산해준다.

## 좌표의 영점은 어디인가
영점 위치가 궁금했는데 [Python Interface to JPL Solar System Ephemeris](http://www.cv.nrao.edu/~rfisher/Python/py_solar_system.html) 여길 보니 Green Bank가 기준인가 보다.


> barycentric_observer_track(mjd, utc, num_pts, interval)
> 
> This function returns the rectangular coordinates of the observer with respect to the solar system barycenter in the J2000 coordinate system. The observer's coordinates on the earth, in the IERS coordinate system, must first be set with the set_observer_coordinates function. The default observer position is Green Bank. A successive series of coordinates may be obtained by specifying the number of points requested and the time interval between the points.
> 
> Inputs:
> 
> Modified Julian Date (integer)
> UTC in fraction of a day for the first position
> Number of positions wanted
> Interval between positions in UTC seconds
> Output: {x:, y:, z:, x_rate:, y_rate:, z_rate:}
> 
> x component in km from the barycenter toward the vernal equinox
> y component toward the equator 90 degrees east of the vernal equinox
> z component from the equatorial plane toward the north pole.

## 이게 행성 위치다
km
```json
[{
    "name": "sun",
    "x": 445044.10500348697,
    "y": -83550.88391260746,
    "z": -59141.39245128236
}, {
    "name": "mercury",
    "x": -48036137.26913181,
    "y": 16987875.44230794,
    "z": 14086197.473754141
}, {
    "name": "mars",
    "x": 206798354.7885625,
    "y": 35705851.38452716,
    "z": 10785545.955334062
}, {
    "name": "venus",
    "x": 105567374.6815554,
    "y": 26415537.3716468,
    "z": 5212010.3520591315
}, {
    "name": "earth",
    "x": -104329603.2427341,
    "y": 95129479.68543084,
    "z": 41217720.551813304
}, {
    "name": "neptune",
    "x": 4124679581.6564865,
    "y": -1588368518.5061777,
    "z": -752816826.5495942
}, {
    "name": "uranus",
    "x": 2882659006.3073144,
    "y": 751476045.3009933,
    "z": 288355714.82770497
}, {
    "name": "pluto",
    "x": 1123282102.8247404,
    "y": -4454738996.02725,
    "z": -1728627956.924846
}, {
    "name": "jupiter",
    "x": -585204416.3030182,
    "y": 492269635.87532264,
    "z": 225235116.0371663
}]
```

> 7. The position in space
> Compute the planet's position in 3-dimensional space:
>     xh = r * ( cos(N) * cos(v+w) - sin(N) * sin(v+w) * cos(i) )
>     yh = r * ( sin(N) * cos(v+w) + cos(N) * sin(v+w) * cos(i) )
>     zh = r * ( sin(v+w) * sin(i) )
> For the Moon, this is the geocentric (Earth-centered) position in the ecliptic coordinate system. For the planets, this is the heliocentric (Sun-centered) position, also in the ecliptic coordinate system. If one wishes, one can compute the ecliptic longitude and latitude (this must be done if one wishes to correct for perturbations, or if one wants to precess the position to a standard epoch):
>     lonecl = atan2( yh, xh )
>     latecl = atan2( zh, sqrt(xh*xh+yh*yh) )
> As a check one can compute sqrt(xh*xh+yh*yh+zh*zh), which of course should equal r (except for small round-off errors).
> 
> 8. Precession
> 
> If one wishes to compute the planet's position for some standard epoch, such as 1950.0 or 2000.0 (e.g. to be able to plot the position on a star atlas), one must add the correction below to lonecl. If a planet's and not the Moon's position is computed, one must also add the same correction to lonsun, the Sun's longitude. The desired Epoch is expressed as the year, possibly with a fraction.
>     lon_corr = 3.82394E-5 * ( 365.2422 * ( Epoch - 2000.0 ) - d )
> If one wishes the position for today's epoch (useful when computing rising/setting times and the like), no corrections need to be done.
[Computing planetary positions](http://www.stjarnhimlen.se/comp/ppcomp.html#7)

## 그 외 링크들

- [Mercury Position and Finder Chart | TheSkyLive.com](http://theskylive.com/mercury-tracker)  
오 좋은데
- [Solar system dynamics on-line tools](http://ssd.jpl.nasa.gov/?tools)  
좋을것 같았는데 도움이 되지 않았다.
- [Starlit Night Project](http://www.lizard-tail.com/isana/lab/starlitnight/)  
밤하늘 별 그리는 프로젝트. 과정이 잘 나와있어 괜찮다!
- [Planetary.js: Awesome interactive globes for the web](http://planetaryjs.com/)  
지구를 그려주는 js


[Location to Information - AskGeo](https://www.askgeo.com/database/Astronomy)  
이런곳도 찾았다... 상관없어 보이지만
