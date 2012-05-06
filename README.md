Focus is a simple DNS-based firewall for Linux that helps you stop
procrastinating.  Just give it a list of sites you spend too much time on and
enjoy not being to access them (easily :)


Starting
========

    sudo python focus.py &
    
    
Blocking Domains
================

Firewall rules involving schedules and timeframes can get complicated fast.
For this reason, the scheduling specification is pure Python, so you can make
your blacklist schedules as simple or as complex as you want.

The default scheduler is created on first startup in `/etc/focus_blacklist.py`:

```python
import re

def news_ycombinator_com(dt):
    # return dt.hour % 2 # every other hour
    return False

def reddit_com(dt):
    # return dt.hour in (12, 21, 22) # at noon, or from 9-10pm
    return False
    
def facebook_com(dt):
    return False

def default(domain, dt):
    # do something with regular expressions here?
    return True
```

The format is simple.  Just define a function named like the domain you
want to block.  Have it take a single datetime object and have it return True
or False.  In the body, you can write whatever logic makes the most sense for
you.  Maybe you want to write your own Pomodoro routine, or maybe you want to
scrape your google calendar for exam dates.

For sites without their own scheduler function, the default() function is called.

There's no need to restart Focus if you redefine your schedules.


Configuration
=============

Focus tries to start with a sensible configuration, but if you need to change
it, edit `/etc/focus.json.conf`