Name
====


[![travis-ci](https://travis-ci.org/vislee/ngx_http_ipdb_module.svg?branch=master)](https://travis-ci.org/vislee/ngx_http_ipdb_module)
[![Coverage Status](https://coveralls.io/repos/github/vislee/ngx_http_ipdb_module/badge.svg?branch=master)](https://coveralls.io/github/vislee/ngx_http_ipdb_module?branch=master)

ngx_http_ipdb_module - creates variables with values depending on the client IP address or specifies address, using the precompiled [ipip.net](https://www.ipip.net) [ipdb](https://www.ipip.net/ipdb/test).

Table of Contents
=================
* [Name](#name)
* [Status](#status)
* [Install](#install)
* [Example Configuration](#example-configuration)
* [Directives](#directives)
    * [ipdb](#ipdb)
    * [ipdb_language](#ipdb_language)
    * [ipdb_proxy](#ipdb_proxy)
    * [ipdb_proxy_recursive](#ipdb_proxy_recursive)
    * [ipdb_specifies_addr](#ipdb_specifies_addr)
* [Variable](#variable)
    * [$ipdb_country_name](#ipdb_country_name)
    * [$ipdb_region_name](#ipdb_region_name)
    * [$ipdb_city_name](#ipdb_city_name)
    * [$ipdb_isp_domain](#ipdb_isp_domain)
* [TODO](#todo)
* [Author](#author)
* [Copyright and License](#copyright-and-license)
* [See Also](#see-also)


Status
======
The module is currently in active development.

[Back to TOC](#table-of-contents)

Install
=======

```sh
configure --prefix=/usr/local/nginx --add-module=./github.com/vislee/ngx_http_ipdb_module
# or
configure --prefix=/usr/local/nginx --add-dynamic-module=./github.com/vislee/ngx_http_ipdb_module --with-compat
```

[Back to TOC](#table-of-contents)

Example Configuration
====================

```nginx

# load_module ./modules/ngx_http_ipdb_module.so;

http {
    include       mime.types;
    default_type  application/octet-stream;

    ......

    ipdb /tmp/nginx/conf/ipiptest.ipdb;
    ipdb_language CN;
    ipdb_proxy 127.0.0.1;
    ipdb_proxy_recursive on;

    server {
        listen       8090;
        server_name  localhost;

        ......

        location / {
            # ipdb_specifies_addr $http_addr;
            # ipdb_language EN;
            return 200 $ipdb_city_name;
        }
    }
}

```

[Back to TOC](#table-of-contents)

TODO
==========

 + add variable
     * ipdb_country_code
     * ipdb_continent_code
     * ipdb_org
     * ipdb_idc
     * ipdb_latitude
     * ipdb_longitude

[Back to TOC](#table-of-contents)

Directives
==========

ipdb
----
**syntax:** *ipdb file;*

**default:** *-*

**context:** *http*

Specifies a database.

ipdb_language
-------------
**syntax:** *ipdb_language EN|CN;*

**default:** *EN*

**context:** *http,server,location*

set variable language.

ipdb_proxy
----------
**syntax:** *ipdb_proxy address|CIDR;*

**default:** *-*

**context:** *http*

Defines trusted addresses.

ipdb_proxy_recursive
--------------------
**syntax:** *ipdb_proxy_recursive on|off;*

**default:** *off*

**context:** *http*

Is recursive search.

ipdb_specifies_addr
-------------------
**syntax:** *ipdb_specifies_addr address;*

**default:** *-*

**context:** *http,server,location*

Specifies the address. The address can contain text, variables.

[Back to TOC](#table-of-contents)


Variable
========

ipdb_country_name
----------------

$ipdb_country_name - country name, for example, "中国", "China"

ipdb_region_name
----------------

$ipdb_region_name - country region name, for example, "内蒙古","Nei Mongol", "北京", "Beijing"

ipdb_city_name
--------------

$ipdb_city_name - city name, for example, "呼和浩特", "Hohhot", "北京", "Beijing"

ipdb_isp_domain
---------------

$ipdb_isp_domain - ISP name, for example, "电信", "ChinaTelecom"


[Back to TOC](#table-of-contents)

Author
======

wenqiang li(vislee)

[Back to TOC](#table-of-contents)

Copyright and License
=====================

This module is licensed under the [GPL](http://www.gnu.org/licenses/licenses.en.html) license.

Copyright (C) 2018-2019, by vislee.

All rights reserved.

[Back to TOC](#table-of-contents)


See Also
========

+ [ngx_http_geoip_module](http://nginx.org/en/docs/http/ngx_http_geoip_module.html#geoip_proxy)