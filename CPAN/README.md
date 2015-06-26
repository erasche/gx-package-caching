# CPAN Cache

Upstream is `mirror.uta.edu/CPAN/`

## Example

```console
hxr@leda:~/work/gx-package-caching/CPAN$ docker-compose up -d
Creating cpan_squid_1...
hxr@leda:~/work/gx-package-caching/CPAN$ # First an uncached request
hxr@leda:~/work/gx-package-caching/CPAN$ time wget --quiet http://localhost:3128/CPAN/authors/id/C/CJ/CJFIELDS/BioPerl-1.6.924.tar.gz

real    0m16.655s
user    0m0.020s
sys     0m0.252s
hxr@leda:~/work/gx-package-caching/CPAN$ # This time from squid's cache
hxr@leda:~/work/gx-package-caching/CPAN$ time wget --quiet http://localhost:3128/CPAN/authors/id/C/CJ/CJFIELDS/BioPerl-1.6.924.tar.gz

real    0m0.039s
user    0m0.000s
sys     0m0.024s
hxr@leda:~/work/gx-package-caching/CPAN$ # See the file entry in squid's cache
hxr@leda:~/work/gx-package-caching/CPAN$ sudo cat cache/store.log 
1435347377.533 SWAPOUT 00 00000000 527A8218976EF5038058FA413420B77C  200 1435347360 1405023743        -1 application/x-gzip 12623118/12623118 GET http://mirror.uta.edu/CPAN/authors/id/C/CJ/CJFIELDS/BioPerl-1.6.924.tar.gz
```
