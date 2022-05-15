* **2022-05-05**
    * pritunl v1.30.3157.70
---
* **2022-05-01**
    * pritunl v1.30.3153.83
---
* **2022-04-27**
    * pritunl v1.30.3149.73
---
* **2022-03-25**
    * pritunl v1.30.3116.68
---
* **2022-03-22**
    * pritunl v1.30.3113.65
---
* **2022-03-21**
    * pritunl v1.30.3112.0
    * Update Dockerfile variables to match pritunl docs
---
* **2022-03-20**
    * pritunl v1.30.3111.72
---
* **2022-03-17**
    * pritunl v1.30.3108.50
---
* **2022-03-15**
    * pritunl v1.30.3106.58
---
* **2022-03-14**
    * pritunl v1.30.3106.1
---
* **2022-03-10**
    * pritunl v1.30.3102.46
---
* **2022-03-10**
    * Fix #14, pin markupsafe and itsdangerous to 2.0.1 version
    * Rerelease image for pritunl v1.30.3098.52
    * v1.30.3101.81 released today partially fixes #14, removed markupsafe pin
    * pritunl flask is still 1.1.2, keep itsdangerous 2.0.1 manual pin
        * PR to pritunl to pin in requirements.txt or update flask
        * Closed w/o merge, see below.
    * v1.30.3101.90 released. Fully fixes #14 with no Dockerfile pin workarounds.
        * requirements.txt pins flask==2.0.3 now (was 1.1.2)
        * requirements.txt pins jinja2==3.0.3 now (was 2.11.3)
---
* **2022-03-07**
    * pritunl v1.30.3098.52
    * Update/fix GitHub archive path
---
* **2022-02-07**
    * pritunl v1.30.3070.59
---
* **2022-02-02**
    * pritunl v1.30.3065.49
---
* **2022-01-26**
    * Add ipset package (contritbution by [weekdayfabian](https://github.com/weekdayfabian))
    * pritunl v1.30.3058.49
---
* **2022-01-21**
    * pritunl v1.30.3053.58
---
* **2022-01-11**
    * pritunl v1.30.3043.48
---
* **2022-01-08**
    * pritunl v1.30.3040.44
---
* **2021-12-29**
    * pritunl v1.30.3030.85
---
* **2021-12-22**
    * pritunl v1.30.3023.56
---
* **2021-12-11**
    * pritunl v1.30.3012.75
---
* **2021-12-06**
    * pritunl v1.30.3007.74
---
* **2021-11-30**
    * pritunl v1.30.3001.35
    * pritunl v1.30.3001.87
---
* **2021-10-29**
    * pritunl v1.30.2969.92
---
* **2021-10-19**
    * pritunl v1.30.2959.58
    * pritunl v1.30.2960.4
----
* **2021-10-05**
    * pritunl v1.30.2945.60
----
* **2021-10-02**
    * pritunl v1.30.2943.13
----
* **2021-09-09**
    * pritunl v1.30.2919.89
----
* **2021-07-07**
    * pritunl v1.30.2856.5
----
* **2021-06-29**
    * Bump Pritunl release to v1.30.2847.71
---
* **2021-06-17**
    * Update GitHub actions
    * Configure multi-architecture to build for arm64
---
* **2021-06-15**
    * Update to GitHub actions for builds
    * Publish to ghcr.io in addition to Docker Hub
---
* **2021-06-14**
    * Bump Pritunl release to v1.30.2817.44
    * Update Dockerfile base back to alpine:latest
    * Update packages to python3
---
* **2020-12-28**
    * Bump Pritunl release to v1.29.2664.67
---
* **2020-10-25**
    * Bump Pritunl release to v1.29.2591.94
---
* **2020-10-14**
    * Bump Pritunl release to v1.29.2589.95
---
* **2020-09-03**
    * Bump Pritunl release to v1.29.2547.95
---
* **2020-08-17**
    * Bump Pritunl release to v1.29.2530.72
---
* **2020-08-10**
    * Bump Pritunl release to v1.29.2524.85
---
* **2020-07-07**
    * Bump Pritunl release to v1.29.2490.44
---
* **2020-06-15**
    * Update Dockerfile label schema
    * Set base to alpine:3.10, fixes bzr, python2-dev, py2-dnspython, & py2-setuptools dependencies breaking hub build
    * Update packages to specific python2 names
---
* **2020-06-15**
    * Bump Pritunl release to v1.29.2468.79
---
* **2020-05-13**
    * Bump Pritunl release to v1.29.2435.70
---
* **2020-05-05**
    * Bump Pritunl release to v1.29.2427.61
---
* **2020-05-01**
    * Bump Pritunl release to v1.29.2423.17
---
* **2020-04-04**
    * Bump Pritunl release to v1.29.2395.63
    * Add wireguard-tools package to support new wireguard option
    * Update documentation to include howto for wireguard setup
    * Add WIREGUARD environment variable - wireguard needs the pritunl https server running on 443 inside the container
    * Update documentation and examples for wireguard + reverse proxy
---
* **2020-04-02**
    * Bump Pritunl release to v1.29.2394.19
---
* **2020-03-31**
    * Bump Pritunl release to v1.29.2392.39
---
* **2020-03-27**
    * Bump Pritunl release to v1.29.2388.59
---
* **2020-03-23**
    * Bump Pritunl release to v1.29.2384.51
---
* **2019-12-06**
    * Bump Pritunl release to v1.29.2276.91
---
* **2019-10-23**
    * Bump Pritunl release to v1.29.2232.32
---
* **2019-09-30**
    * Bump Pritunl release to v1.29.2209.0
---
* **2019-09-29**
    * Bump Pritunl release to v1.29.2208.39
---
* **2019-07-27**
    * Bump Pritunl release to v1.29.2145.25
    * Add missing 'make' build dependency, fixes 'Exception: ERROR: The 'make' utility is missing from PATH' building pynacl
---
* **2019-06-28**
    * Fix GOCACHE=off deprecation introduced with Go 1.12 in updated alpine base
---
* **2019-05-02**
    * Add py-dnspython package, closes issue/enhancement #4
---
* **2019-04-25**
    * Bump Pritunl release to v1.29.2051.18
---
* **2019-03-31**
    * Bump Pritunl release to v1.29.2026.90
---
* **2019-03-15**
    * Bump Pritunl release to v1.29.2010.18
---
* **2019-03-04**
    * Bump Pritunl release to v1.29.1999.88
---
* **2019-02-26**
    * Bump Pritunl release to v1.29.1994.1
---
* **2019-02-23**
    * Bump Pritunl release to v1.29.1990.10
---
* **2019-02-12**
    * Bump Pritunl release to v1.29.1979.98
---
* **2019-01-22**
    * Bump Pritunl release to v1.29.1958.76
---
* **2019-01-21**
    * Bump Pritunl release to v1.29.1952.27
---
* **2019-01-11**
    * Bump Pritunl release to v1.29.1947.29
---
* **2018-12-24**
    * Bump Pritunl release to v1.29.1929.33
---
* **2018-12-21**
    * Bump Pritunl release to v1.29.1926.93
---
* **2018-12-20**
    * Bump Pritunl release to v1.29.1925.81
---
* **2018-12-18**
    * Bump Pritunl release to v1.29.1924.6
    * Bump Pritunl release to v1.29.1923.80
---
* **2018-12-14**
    * Bump Pritunl release to v1.29.1919.29
---
* **2018-12-12**
    * Bump Pritunl release to v1.29.1917.25
---
* **2018-12-09**
    * Bump Pritunl release to v1.29.1914.98
---
* **2018-11-27**
    * Bump Pritunl release to v1.29.1902.39
---
* **2018-09-13**
    * Bump Pritunl release to v1.29.1827.6
---
* **2018-08-24**
    * Update Dockerfile
        * Add tzdata package to container. Makes TZ= and /etc/localtime volume mapping actually work...
        * Shh, be vewy vewy quiet, I'm hunting errors in the build logs. (Add -q to Dockerfile apk commands)
    * Update build hooks script
---
* **2018-08-22:**
    * Bump Pritunl release to v1.29.1804.86
    * Update docker-entrypoint.sh version to 1.0.1
---
* **2018-08-11:**
    * Initial Dockerfile, script, etc. creation.
