# geoaccess
Generates a map of the accesses to a website

First extract the ip addresses from the log file:

```bash
awk '{ print $1 } ' access.log | sort | uniq > locs.txt
```

Then convert the IP addresses to coordinates:

```python
from geoip import geolite2

with open('locs.txt','r') as f:
        for line in f:
                with open('locs.txt.geo','a') as g:
                        g.write(str(geolite2.lookup(line.strip()).location))
                        g.write('\n')
```

Then convert the coordinates to a map?
