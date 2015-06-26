# CRAN Cache

Upstream is `cran.revolutionanalytics.com` as they're listed as the Texas mirror for CRAN

## Example

```console
hxr@leda:~/work/gx-package-caching/CRAN$ docker-compose up -d
Creating cran_squid_1...
hxr@leda:~/work/gx-package-caching/CRAN$ # First an uncached request
hxr@leda:~/work/gx-package-caching/CRAN$ time wget --quiet http://localhost:3128/src/contrib/CommonJavaJars_1.0-5.tar.gz

real    0m1.338s
user    0m0.016s
sys     0m0.048s
hxr@leda:~/work/gx-package-caching/CRAN$ # This time from squid's cache
hxr@leda:~/work/gx-package-caching/CRAN$ time wget --quiet http://localhost:3128/src/contrib/CommonJavaJars_1.0-5.tar.gz

real    0m0.024s
user    0m0.004s
sys     0m0.008s
hxr@leda:~/work/gx-package-caching/CRAN$ # See the file entry in squid's cache
hxr@leda:~/work/gx-package-caching/CRAN$ sudo cat cache/store.log 
1435347698.238 SWAPOUT 00 00000000 A3DA8C33B65683584E634693DC721A95  200 1435347696 1408991531        -1 application/octet-stream 4635038/4635038 GET http://cran.revolutionanalytics.com/src/contrib/CommonJavaJars_1.0-5.tar.gz
```
