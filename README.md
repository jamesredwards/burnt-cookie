# Burnt Cookie
Horrorho's Burnt Cookie.

##What is it?
Parses Apple binary cookie file/s into their Netscape equivalent/s. These Netscape cookie files are easily imported into web browsers or can be used with compatible tools like [curl](https://curl.haxx.se/).

Illustrative example:
```
$ burntcookie Cookies.binarycookies > cookies.txt
```
```
$ cat cookies.txt
# Netscape HTTP Cookie File
# This file was generated by Horrorho's Burnt Cookie.
# http://github.com/horrorho/burnt-cookie
.example.com	TRUE	/	FALSE	1482374690	MOOMOO	2534780572345.54354351154
.example.com	TRUE	/	FALSE	1482374690	__woof	434543.435434
.example.com	TRUE	/	FALSE	1482374690	__meow	423e5ab398aa342f
.example.com	TRUE	/	FALSE	1482374690	__oink	1
```
```
$ curl -v -b cookies.txt http://www.example.com > response.txt
* Rebuilt URL to: http://www.example.com/
* Hostname was NOT found in DNS cache
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0     0    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0*   Trying 93.184.216.34...
* Connected to www.example.com (93.184.216.34) port 80 (#0)
> GET / HTTP/1.1
> User-Agent: curl/7.35.0
> Host: www.example.com
> Accept: */*
> Cookie: MOOMOO=2534780572345.54354351154; __meow=423e5ab398aa342f; __oink=1; __woof=434543.435434
```

##Build
Requires [Rust](https://www.rust-lang.org).

[Download](https://github.com/horrorho/burnt-cookie/archive/master.zip), extract and navigate to the burnt-cookie-master folder:
```
~/burnt-cookie-master $ cargo build --release
```

The executable is located at: `/target/release/`
```
~/burnt-cookie-master $ ./target/release/burntcookie --help
Usage: burntcookie [OPTION]... [FILE]...
Parses Apple binary cookie file/s into their Netscape equivalent/s.
With no FILE, read standard input.

Options:
        --help          display this help and exit
    -h, --http_only     use #HttpOnly_ prefix

Examples:
burntcookie Cookies.binarycookies > cookies.txt		Parse into cookies.txt
RUST_LOG=WARN burntcookie Cookies.binarycookies		With warnings

Project home: http://github.com/horrorho/burnt-cookie
```

##Usage

Convert a Cookies.binarycookies file:
```
burntcookie Cookies.binarycookies
```
Pipe to cookies.txt:
```
burntcookie Cookies.binarycookies > cookies.txt
```
\#HttpOnly\_ prefixes are not prepended by default. Use the -h/ --http-only switch:
```
burntcookie -h Cookies.binarycookies > cookies.txt
```
Temporary .dat files are also parseable although they may generate warnings (supressed by default):
```
burntcookie Cookies.binarycookies_tmp_1234_0.dat > cookies.txt
```
Enable warning output.
```
RUST_LOG=WARN burntcookie Cookies.binarycookies_tmp_1234_0.dat > cookies.txt
```

##Why Rust?
This project is largely an exercise in Rust programming. It's a conversion of a private tool I created a while back.

##Useful links
HTTP cookie: https://en.wikipedia.org/wiki/HTTP_cookie

Safari/iOS - Cookies.binarycookies reader: http://www.securitylearn.net/2012/10/27/cookies-binarycookies-reader/

PHP reading a cookie file: http://stackoverflow.com/questions/410109/php-reading-a-cookie-file

Netscape HTTP Cooke File Parser in PHP: http://www.hashbangcode.com/blog/netscape-http-cooke-file-parser-php




