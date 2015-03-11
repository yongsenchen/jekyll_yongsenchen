---
layout: post
category : develop
tags : [dev, memleak]
---

kmemleak can be used to trace memleak in kernel space.
The memory may be allocated by kmalloc/kzalloc, vmalloc, kmem_cache_alloc or per_cpu_alloc.

# Build in kmemleak in linux kernel

Enable CONFIG_DEBUG_KMEMLEAK in kernel config, then build the kernel.
```
Kernel hacking --->
    [*] Kernel memory leak detector
```

# Enable kmemleak scan

```sh
echo scan > /sys/kernel/debug/kmemleak
```
Start application which may trigger kernel memleak issue, so kmemleak can capture it.

# Check kmemleak result

```sh
cat /sys/kernel/debug/kmemleak
```

It would show the issue points with something like bellow, which shows the leak address, size, and process name and ID.
```
unreferenced object 0xf3952000 (size 1024):
  comm "process_name", pid 245, jiffies 4529281928 (age 1245.640s)
  hex dump (first 32 bytes):
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
    00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
  backtrace:
    [<c0002354>] xxxx
```

And you can clear previous result by
```sh
echo clear > /sys/kernel/debug/kmemleak
```

# Limitations and Drawbacks

* kmemleak scan redueces performance of memory allocation and free. It even may cause application stuck for short time.
* It may report some fake memory leak report which is not real memleak. Scan again if necessary.

# Useful commands
refer to $linux/Documentation/kmemleak.txt
```
  off           - disable kmemleak (irreversible)
  stack=on      - enable the task stacks scanning (default)
  stack=off     - disable the tasks stacks scanning
  scan=on       - start the automatic memory scanning thread (default)
  scan=off      - stop the automatic memory scanning thread
  scan=<secs>   - set the automatic memory scanning period in seconds
                  (default 600, 0 to stop the automatic scanning)
  scan          - trigger a memory scan
  clear         - clear list of current memory leak suspects, done by
                  marking all current reported unreferenced objects grey
  dump=<addr>   - dump information about the object found at <addr>
```
# Reference:
* linux/ Documentation/kmemleak.txt
* http://www.360doc.com/content/13/0510/15/496343_284400027.shtml
* http://lwn.net/Articles/187979/
