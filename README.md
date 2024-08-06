EmailLint
=========

This is a fork of the EmailLint project: https://github.com/lukeschafer/EmailLint and is meant to bring the project up to date.

# Overview

EmailLint is a lint program ( http://en.wikipedia.org/wiki/Lint_(software) ) designed to ensure HTML emails are created using techniques that are available in all major email clients. 

# Installation on Linux

Emaillint uses a zero-build-step style of node.js.

1. Git clone this repo. 
2. If you would like to run on a different port, change the last line in src/web/index.js
3. Install Node.js
4. Run it via ```nodejs /path/to/cloned/emaillint/repo/src/web/index.js```

## Install Monit

Monit can be used to ensure the app is always running.

1. Install monit - sudo apt install monit
2. Edit /etc/monit/monitrc and make sure it has 'set http' on
     Look for the commented out line starting with "set httpd..."
     Uncomment this line and the line: allow admin:monit
     Change these credentials as desired.   
4. Create the /etc/monit/services directory if it doesn't exist.   
5. Create /etc/monit/services/emaillint and add the following contents:.
```
  check host emaillint with address 127.0.0.1
    start program = "/usr/local/bin/node /path/to/cloned/emaillint/repo/src/web/index.js"
    stop program  = "/usr/bin/pkill -f 'node /path/to/cloned/emaillint/repo/src/web/index.js'"
    if failed port [YOURPORT] protocol HTTP
        request /
        with timeout 10 seconds
        then restart
```

 [YOURPORT] is the port emaillint is listening on (8020 by default).

5. Restart monit - sudo service monit restart
   
# Contributions

You can help by submitting pull requests! Primarily looking at the following things:
* Updates to bootstrap and other client libs.
* Ensure latest node.js support.
* Updates to node.js packages (express et al).
* New rules.
* Unit tests/integration tests.

# License

GPLv2 because, well, I already host a free version for anyone to use, I would like to keep changes free and public for all. Give me a good reason to and I'll issue additional licenses or change it.
