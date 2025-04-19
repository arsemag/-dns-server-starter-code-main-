## DNS Server
Project 6 - DNS Server
This project involves creating a DNS server that handles DNS queries through recursion. When the server receives a DNS query, it first checks if the query is in its authoritative domain. If it is, the server responds using the local DNS records. If the query is not in the authoritative domain, the server forwards the request to the root server and recursively follows NS records until it finds the correct A record with the response. The response is then forwarded back to the client.

Challenges
During development, we encountered issues with parallel processing, particularly with looping through multiple sockets to handle DNS queries simultaneously. We were able to process DNS requests one at a time, but struggled with implementing parallelism. Additionally, understanding and implementing recursion with NS records was a challenge, but we ultimately figured out how to recurse properly and get the right response.

**** Features ****
Recursive Query Handling: The server can forward requests to external DNS servers if the query is outside its authoritative domain.

Support for NS Records: The server can resolve NS records by recursively querying through name servers, starting from the root and progressing down the DNS hierarchy.

Efficient Query Resolution: Once the query is resolved, the server responds with the appropriate A record, or an NXDOMAIN if the record is not found.

*** Functions **** 


__init__(self, root_ip, domain, port)
Purpose: Initializes the server, binds the socket, parses the zone file, and prepares the server to receive DNS queries.

log(self, message): Logs messages to the standard error output for debugging and tracking purposes.

send(self, addr, message): Sends the DNS response back to the client.

parse_zone_file(self, file_path): Reads and parses the zone file to store DNS records for authoritative responses.


create_forward_socket(self): Creates a UDP socket for forwarding DNS queries to other DNS servers.

forward_helper(self, client_request, ip, forward_sock): Forwards a client DNS query to a given IP address (typically to another DNS server).

forward_request(self, client_request, ip, client_addr, depth=0): Recursively forwards a DNS query to other DNS servers, starting with the root server.

handle_pending_responses(self): Handles pending responses from forwarded DNS queries, managing timeouts and processing responses when they arrive.

recv(self, socket): Receives DNS queries from the client and processes them, either resolving them locally or forwarding them if necessary.


ns_case(self, record, response): Handles NS records by adding them to the authority section of the response and resolving any additional A records.


cname_case(self, record, response): Handles CNAME records by adding them to the response and resolving any additional A records.

send_outside_zone(self, request, addr, response): Forwards a DNS query to a root DNS server or external DNS server when the query is not within the authoritative zone.

run(self): Runs the DNS server, listening for incoming DNS queries and processing them as they arrive.

Testing
To test and debug the server, we used the configuration files provided in the assignment and incorporated print statements to track the flow of the code. This allowed us to identify whether the server was receiving and processing responses correctly, or if it was failing to obtain responses. By tracking where the failure occurred, we were able to target specific functions and address issues such as socket management and recursion. This iterative process helped us refine our solution and ensure that the server was handling DNS queries properly.