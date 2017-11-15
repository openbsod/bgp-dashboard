BGP Dashboard-  fork of Richard Hicks repo ( without Docker addiction )
=============

A "realtime" web view of your BGP network

- Who do I peer with?
- How many routes do I receive from my peers?
- Who do I use for tranist?
- What AS path does a prefix take out of my network?
- How many routes and autonomous systems do I see?
- BGP Looking Glass (IPv4/IPv6/ASN)


How it works
---------

- BGP peering session using GoBGP
- GoBGP pipes BGP information into MongoDB
- Flask App queries MongoDB to build website and JSON API

###### Dependencies
- GoBGP [osrg/gobgp](https://github.com/osrg/gobgp)
- MongoDB [mongo](https://www.mongodb.com)
- Flask ([flask](http://flask.pocoo.org)

###### GoBGP
The GoBGP container serves two functions:
- Peer with the "real" network
  - Configure [gobgpd.conf](https://github.com/openbsod/bgp-dashboard/blob/master/gobgp/gobgpd.conf) to peer with the real network.
  - Only IPv4-Unicast and IPv6-Unicast supported at this time.
- Pass BGP updates into BGP
  - The [bgp-mongo-bulk-load.py](https://github.com/openbsod/bgp-dashboard/blob/master/bgp-mongo-bulk-load.py) script pipes the JSON updates from GoBGP into the MongoDB

###### MongoDB
- Mongo receives JSON updates from the GoBGP
- The Flask App queries Mongo for relevant information

###### Flask
- Flask presents a Dashboard for realtime BGP updates
- A JSON API is used on the backend to support the frontend and display Looking Glass queries


Screenshot
---------
![screenshot](bgp-dashboard.png)


Install
---------
```
$ git clone https://github.com/openbsod/bgp-dashboard.git
$ cd bgp-dashboard
$ # modify /etc/gobgp/gobgpd.conf to peer with your network
$ # modify ./flask/app/hello.py globals to support your network BGP communities
```


