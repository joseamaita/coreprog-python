# Python Application focusing Iterators and Generators

## Real-time log file monitor

### Version A

Here, we create a script that presents a generator that follows lines 
written to a real-time log file (like Unix `tail -f`). To run this 
program, you need to have a log file to work with. Also, you need to run 
the application 'simulated web-server log creator' and read the output 
file `access-log`. Leave this program running in the background to see 
how this works:

```python
#!/usr/bin/env python3
# follow.py
# Real-time log file monitor
# A generator that follows a log file like Unix 'tail -f'

# Most of the code were taken from David Beazley's web site at
# http://www.dabeaz.com/coroutines/follow.py

import time

filename = "access-log"

def monitor(f):
    f.seek(0, 2)    # Go to the end of the file (EOF)
    while True:
        line = f.readline()    # Try reading a new line of text
        if not line:    # If nothing, sleep briefly and try again
            time.sleep(0.1)
            continue
        yield line

def main():
    print('-----------------------------------')
    print('    Real-time log file monitor')
    print('-----------------------------------')
    print()
    print(f"Reading from '{filename}' ... Press [Ctrl+C] to leave\n\n")
    with open(filename,'rt') as f:
        try:
            for line in monitor(f):
                print(line, end='')
        except KeyboardInterrupt:
            print("\n\nLeaving.")
            raise SystemExit(1)

if __name__ == '__main__':
    main()
```

After running the script, the output would be something like this:

```
-----------------------------------
    Real-time log file monitor
-----------------------------------

Reading from 'access-log' ... Press [Ctrl+C] to leave


88.131.106.15 - - [24/Dec/2017:16:10:53 - 0600] "GET /cgi-bin/wiki.pl?action=change1&id=ImportDirective HTTP/1.1" 200 2741
213.41.243.144 - - [24/Dec/2017:16:10:54 - 0600] "GET /Doc/index.html HTTP/1.1" 404 133
218.94.136.173 - - [24/Dec/2017:16:10:54 - 0600] "GET /photos/wind/pages/IMG_1262.htm HTTP/1.1" 404 133
84.110.129.69 - - [24/Dec/2017:16:10:55 - 0600] "GET /04Objects.pdf HTTP/1.1" 200 502854
89.229.25.165 - - [24/Dec/2017:16:10:56 - 0600] "GET /dynamic/index.html HTTP/1.1" 200 5105
216.191.234.70 - - [24/Dec/2017:16:10:56 - 0600] "GET /dynamic/portfolio.txt HTTP/1.1" 200 100
74.6.25.125 - - [24/Dec/2017:16:10:56 - 0600] "GET /python/tutorial/beazley_advanced_python/Slides/SLIDE085.HTM HTTP/1.0" 200 1739
24.99.94.177 - - [24/Dec/2017:16:10:56 - 0600] "GET /dynamic/soln12_1.html HTTP/1.1" 404 133
99.244.205.42 - - [24/Dec/2017:16:10:57 - 0600] "GET /photos/u505/pages/IMG_1500.htm HTTP/1.0" 404 133
89.129.99.56 - - [24/Dec/2017:16:10:57 - 0600] "GET /dynamic/index.html HTTP/1.1" 304 -
212.56.88.112 - - [24/Dec/2017:16:10:57 - 0600] "GET /python/tutorial/beazley_advanced_python/Slides/SLIDE108.HTM HTTP/1.0" 200 1686
84.110.187.74 - - [24/Dec/2017:16:10:58 - 0600] "GET /ply/ply-1.1.tar.gz HTTP/1.1" 200 62496
83.238.23.214 - - [24/Dec/2017:16:10:59 - 0600] "POST /cgi-bin/wiki.pl HTTP/1.1" 200 1461
80.68.93.199 - - [24/Dec/2017:16:11:00 - 0600] "GET /about HTTP/1.1" 404 133
194.237.142.6 - - [24/Dec/2017:16:11:00 - 0600] "GET /Tcl96/tcl96.html HTTP/1.1" 404 133
199.111.167.150 - - [24/Dec/2017:16:11:01 - 0600] "GET /papers/Py97/ HTTP/1.1" 403 222
217.136.207.156 - - [24/Dec/2017:16:11:01 - 0600] "GET /python/tutorial/beazley_advanced_python/Slides/SLIDE118.HTM HTTP/1.0" 200 1437
84.110.204.246 - - [24/Dec/2017:16:11:02 - 0600] "GET /python/tutorial/beazley_advanced_python/Slides/SLIDE093.HTM HTTP/1.0" 200 1412
80.229.34.140 - - [24/Dec/2017:16:11:02 - 0600] "GET /cgi-bin/wiki.pl?SwigWikiDocs/Module HTTP/1.1" 200 9008
210.245.31.3 - - [24/Dec/2017:16:11:03 - 0600] "GET /cgi-bin/wiki.pl?SwigFaqAIXSharedLibraries HTTP/1.0" 200 3494
140.160.138.141 - - [24/Dec/2017:16:11:03 - 0600] "GET /python/tutorial/beazley_advanced_python/Slides/SLIDE055.HTM HTTP/1.0" 200 1319
91.76.66.64 - - [24/Dec/2017:16:11:03 - 0600] "GET /cgi-bin/wiki.pl?RecentChanges HTTP/1.0" 200 1775
193.252.149.16 - - [24/Dec/2017:16:11:03 - 0600] "GET /dynamic/08GeneratorNetwork.pdf HTTP/1.1" 206 339721
83.12.228.78 - - [24/Dec/2017:16:11:04 - 0600] "POST /cgi-bin/wiki.pl HTTP/1.0" 200 963
131.159.46.32 - - [24/Dec/2017:16:11:04 - 0600] "GET /dynamic/04Objects.pdf HTTP/1.1" 304 -
74.6.20.171 - - [24/Dec/2017:16:11:05 - 0600] "GET /cgi-bin/wiki.pl?SwigFaq/SharedLibraries HTTP/1.0" 200 4135
71.110.220.16 - - [24/Dec/2017:16:11:06 - 0600] "GET /dynamic/02WorkingWithData.pdf HTTP/1.1" 200 628284
221.189.180.200 - - [24/Dec/2017:16:11:07 - 0600] "GET /cgi-bin/wiki.pl?Unit_Tests_With_SWIG HTTP/1.1" 200 2103
208.80.193.48 - - [24/Dec/2017:16:11:07 - 0600] "GET /cgi-bin/wiki.pl?SwigFaq/Tcl HTTP/1.1" 200 1399
203.20.35.28 - - [24/Dec/2017:16:11:08 - 0600] "GET /photos/u505/pages/IMG_1522.htm HTTP/1.0" 404 133
203.199.177.121 - - [24/Dec/2017:16:11:08 - 0600] "GET /consulting.html HTTP/1.1" 304 -
^C

Leaving.
```

Generators are an extremely powerful way of writing programs based on 
processing pipelines, streams, or data flow. For example, this 
application mimics the behavior of the UNIX `tail -f` command that's 
commonly used to monitor log files.
