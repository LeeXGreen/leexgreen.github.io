---
layout: post
title: "Print random line(s) from a file"
date: 2014-02-23 23:29
comments: true
categories: ["Tips"]
---

Occasionally, I have a need to pull a random line (or lines) from a file.

To make the example real, let's say we're parsing server logs, and the file contains one server name per line.
If we want to test a change to our parser, we might want to choose a random server and parse the logs for only that server.

shuf, from GNU textutils, makes this easy:

{% codeblock lang:bash %}
#!/bin/bash
source_file='our_server_list'
server=`shuf -n 1 $source_file`
echo "The server we chose is: $server"

./our_parser $server
{% endcodeblock %}

The `-n` parameter controls the number of lines returned: in this case, 1.

For more info on shuf, check [Wikipedia](http://en.wikipedia.org/wiki/Shuf) or [its man page](http://linux.die.net/man/1/shuf).
