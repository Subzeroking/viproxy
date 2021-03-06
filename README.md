# Viproxy 1.0

Transparent intercepting proxy in Ruby for MITM attacks.

# Viproxy is forked from em-proxy
- Author: Ilya Grigorik
- Original Project: https://travis-ci.org/igrigorik/em-proxy
- EngineYard tutorial: [Load testing your environment using em-proxy](http://docs.engineyard.com/em-proxy.html)
- [Slides from RailsConf 2009](http://bit.ly/D7oWB)
- [GoGaRuCo notes & Slides](http://www.igvita.com/2009/04/20/ruby-proxies-for-scale-and-monitoring/)

## New Features
- Log file support
- SSL support
- Custom digital certificate support
- Search & Replace support for traffic manipulation

## Known bugs
- No error handling :)
- Duplex server must be SSL enabled if connection is SSL enabled
- Multithreads create some errors, they will be fixed after Blackhat/Defcon


## Getting started

    $> ruby bin/viproxy
    Usage: viproxy [options]
    -l, --listen [PORT]              Port to listen on
    -d, --duplex [host:port, ...]    List of backends to duplex data to
    -r, --relay [hostname:port]      Relay endpoint: hostname:port
    -s, --socket [filename]          Relay endpoint: unix filename
    -z, --ssl                        Run in SSL mode
    -c, --sslcert [filename]         SSL certificate file (PEM)
    -f, --logfile [filename]         Log file
    -p, --regexfile [filename]       Replacement file
    -v, --verbose                    Run in debug mode

    $> ruby bin/viproxy -l 8080 -z -c cert.crt -f /tmp/x.log -v -d 127.0.0.1:8081 -r 127.0.0.1:8083

The above will start viproxy on port 8080, relay and respond with data from port 8083, and also (optional) duplicate all traffic to ports 8081 (and discard their responses).

## Sample Search & Replace file
    #Fuzzing Demo
    REQ	rtf1	FUZZ 20000
    #XSS injection to client requests
    REQ	xsstest	<h1>Viproy Test</h1>
    #Content-Length arrangements on server responses
    RES	Content-Length: 3193	Content-Length: 25663
    #XSS injection to server responses and client requests
    BOTH	xsstest	<h1>Viproy Test</h1>



## License

The MIT License - Copyright (c) 2010 Ilya Grigorik
