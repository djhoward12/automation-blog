---
layout: post
title:  "Json Exercise"
date:   2021-01-15 08:36:34 -0400
categories: jekyll update
---

I've been in a beginner python class this week and one of the exercises required the importing of a json file into python as a dictionary and pulling out specific information. The below code and output were my attempt at this exercise:

*With the attached JSON of device configs, do the following: Load and convert the json to a python dictionary, with the json.load function. Hint: You’ll need to open it, with something like: f = open ‘devices.json’, ‘r’ Programmatically list the devices with interfaces that are active, like: Devicename – make – model – interface Add an ipv4 address if it’s present, like: no address Devicename – make – model – interface with address Devicename – make – model – interface – ipaddr*

{% highlight python %}
import json
from pprint import pprint

with open("python\Programs\devices.json", "r") as f:
    data = f.read()
    obj = json.loads(data)
    test_list = []

    for key in obj:
        interfaces = key["interfaces"]
        for interface, settings in interfaces.items():
            if settings["is_active"] == True:
                device = (key["name"], key["make"], key["model"], interface)
                test_list.append(device)
            if "ip4" in settings:
                device = (
                    key["name"],
                    key["make"],
                    key["model"],
                    interface,
                    settings["ip4"],
                )
                test_list.append(device)
            if "is_trunk" in settings:
                device = (
                    key["name"],
                    key["make"],
                    key["model"],
                    interface,
                    "Trunk",
                )
                test_list.append(device)

    # my_dict = {item[0] : [item[1:]] for item in test_list}
    # pprint(my_dict)
    pprint(test_list)

    # print (key['interfaces'])

{% endhighlight %}

*Output*
('B-R-1', 'Cisco', 'CSR1000V', 'gi0/1'),
 ('B-R-1', 'Cisco', 'CSR1000V', 'gi0/5'),
 ('B-R-1', 'Cisco', 'CSR1000V', 'gi0/9'),
 ('B-R-1', 'Cisco', 'CSR1000V', 'gi0/9', 'Trunk'),
 ('B-R-2', 'Cisco', 'CSR1000V', 'gi0/1'),
 ('B-R-2', 'Cisco', 'CSR1000V', 'gi0/5'),
 ('B-R-2', 'Cisco', 'CSR1000V', 'gi0/8', '169.192.172.13'),
 ('B-R-3', 'Juniper', 'KRS-1', 'gi0/0', 'Trunk'),
 ('B-R-3', 'Juniper', 'KRS-1', 'gi0/1', '192.168.0.13'),
 ('B-R-3', 'Juniper', 'KRS-1', 'gi0/2')]
