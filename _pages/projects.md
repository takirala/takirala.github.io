---
permalink: /projects/ 
author_profile: true
layout: single
title: Projects
modified: 2016-12-19
---
<h2> FeedMe {% include github_watch project="FeedMe" %}</h2>
A Smart Food Cluster developed using IoT and Intel Edison

- Developed a new IoT based food delivery medium using an Android application with Google App Engine as backend.
- Used Weave to communicate to a Brillo board (Intel Edison) via App Engine to control the smart cluster.



<h2> LiveEye {% include github_watch project="LiveEye" %}</h2>
Large Scale Object Recognition Using Deep Learning

- Built and trained a neural network to recognize 80+ object classes using 328,000 images with Caffe & py-faster-rcnn.



<h2> Secure Facebook {% include github_watch project="SecureFB" %}</h2>
- Designed a distributed system using spray-can framework and akka actor model that simulates Facebook server.
- Re-engineered API interfaces to be more secure using public key encryption, digital signature and AES encryption.



<h2> Chord DHT {% include github_watch project="ChordDHT" %}</h2>
- This Distributed Hash Table is implemented using akka actors.
- Along with computation of finger table entries and dynamic departures were simulated.
- Dynamic building of finger tables for 100000 node departures/joins with an overall activity of 4000+ queries/sec.



<h2> P2P Model Java Ecosystem {% include github_watch project="P2PNetwork" %}</h2>
- Implemented P2P model dynamic server client system in java.
- A client requests/sends information from/to bootstrap server to download the content or to distribute its chunks.



<h2>Information Propagation {% include github_watch project="Gossip" %}</h2>
- An akka-actor based network implementation that micmics a distributed sensor topology.
- Gossip protocol is used for information propagation. This is used for rumor propagation (E.g.: Start of a wild fire) in real life.
- Push-Sum protocol is used for aggregation analysis in a sensor network. This efficient solution was able to simulate one lakh nodes on a single quad core machine.
- Calculated convergence rates in sparse topologies like line and 2D grid and dense topologies like star and 3D grid.


<h2>Bit Coin Mining {% include github_watch project="BitMiner" %}</h2>
- A distributed multi-core implementation of mining for bitcoins using SHA-256 hash of randomly generated strings.