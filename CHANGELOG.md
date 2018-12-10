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
