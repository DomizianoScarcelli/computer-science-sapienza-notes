---
Exam:
  - Distributed Systems
---
If there is a CDS (Content Delivery Service) like "CNN" and users that want to get the service, there is the problem of overload, since a lot of users want to access to the CDS.

A better way to do this is having many servers around the world, and the user will somehow connect to the nearest ones. This can be achieved with an ad hoc solution, but Akamai found a generalized solution.

The problem with Internet protocols is that once the protocol is deployed, it’s very hard to change it in the future.

The idea is to use DNS, and whenever an user asks for the CDS server, the IP given to them is the IP of another copy server. This is done without ever changing the DNS domain mapping, otherwise there will be problems with caching.

Every time there is a link to a picture or a video or something like that in the HTML file in the CDN, the link it's akamaized, this means that they add `akamai.com` before the link. (www.cnn.com → akamai.com/www/cnn/com)

The Akamai DNS server, it can see your IP and estimate the location, and so give the IP of one of the nearest Akamai server that contains the content. Akamai copy the content from CNN to their servers.

Akamai is a type of Content Delivery Network (CDN).