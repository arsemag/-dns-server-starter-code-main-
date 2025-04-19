# -dns-server-starter-code-main-


## Project 6 - DNS Server
Our DNS server takes the approach of managing DNS queries from clients through recursion. First we check if we are able to get the response ourselves because it is in our authoritative domain. If it is, then we are able to simply respond using the information in our records and send the response back to the client that sent the query. If it is not in our authoritative domain, then we forward the request out to get a response. We start and the root and recur down through NS records to finally get to a A record that contains the response we are looking for. Then we forward that response back to our client

## Challenges
We could not get our in parallel step to work. We are able to do everything one at a time but for some reason when we attempt to implement looping through our sockets, and doing things at the same time it wouldn't work. We had trouble figuring out the recursive part of the assignment as well, but eventually figured out how to properly recur through the NS records to get the right response.

## Features
Our script is able to recur through NS records to get a response starting at the root server. This way if a query is not within our authoritative zone, we are still able to respond to the client's request by contacting other DNS servers. 

## Funtions


## Testing
In order to debug our code we used the config files provided in the assignment and print statements to figure out where the code stopped working. This was we could determine if we ever got a response and were not properly sending it back to the client or if we were never getting a response in the first place. This helped us to target where we went to fix the code and what function was failing. 