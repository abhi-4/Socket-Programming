                        Point-of-Sale Terminal using socket programming

Use socket programming to implement a simple client and server that communicate over the network and
implement a simple application involving Cash Registers. The client implements a simple cash register
that opens a session with the server and then supplies a sequence of codes (refer request-response
messages format) for some products. The server returns the price of each one, if the product is available,
and also keeps a running total of purchases for each clients transactions. When the client closes the
session, the server returns the total cost. This is how the point-of-sale terminals should work. You can use
a TXT file as a database to store the UPC code and item description at the server end.
You also require implementing a "Concurrent Server", i.e., a server that accepts connections from
multiple clients and serves all of them concurrently.

Request-response messages format

    Request_ Type | UPC-Code | Number

Where
• Request_Type is either 0 for item or 1 for close.
• UPC-code is a 3-digit unique product code; this field is meaningful only if the Request_Type is 0.
• Number is the number of items being purchased; this field is meaningful only if the Request_Type is 0.
For the Close command, the server returns a number, which is the total cost of all the transactions done by
the client. For the item command, the server returns:
Response_ Type
Response
Where:
 <Response_type> is 0 for OK and 1 for error
 If OK, then <Response> is as follows:
o if client command was "close", then <response> contains the total amount
o if client command was "item", then <response> is of the form <price><name>
  
where
<price> is the price of the requested item
<name> is the name of the requested item
 If error, then <Response> is as follows: a null terminated string containing the error; the only
possible errors are "Protocol Error" or "UPC is not found in database".
You should accept the IP Address and Port number from the command line (Don't use a hard-coded port
number). Prototype for command line is as follows:
Prototypes for Client and Server
Client: <executable code><Server IP Address><Server Port number>
Server: <executable code><Server Port number>
The connection to the server should be gracefully terminated. When the server is terminated by pressing
control C, the server should also gracefully release the open socket (Hint: requires use of a signal
handler). *Please make necessary and valid assumptions whenever required
