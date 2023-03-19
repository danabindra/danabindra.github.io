ciscoconfparse
==============




Introduction: What is ciscoconfparse?
-------------------------------------

Short answer: ciscoconfparse is a [Python][10] library
that helps you quickly answer questions like these about your
configurations:

- What interfaces are shutdown?
- Which interfaces are in trunk mode?
- What address and subnet mask is assigned to each interface?
- Which interfaces are missing a critical command?
- Is this configuration missing a standard config line?

It can help you:

- Audit existing router / switch / firewall / wlc configurations
- Modify existing configurations
- Build new configurations

Speaking generally, the library examines an IOS-style config and breaks
it into a set of linked parent / child relationships. You can perform
complex queries about these relationships.

[![Cisco IOS config: Parent / child][11]][11]

Usage
-----

The following code will parse a configuration stored in
\'exampleswitch.conf\' and select interfaces that are shutdown.

```python
from ciscoconfparse import CiscoConfParse

parse = CiscoConfParse('exampleswitch.conf', syntax='ios')

for intf_obj in parse.find_objects_w_child('^interface', '^\s+shutdown'):
    print("Shutdown: " + intf_obj.text)
```

The next example will find the IP address assigned to interfaces.