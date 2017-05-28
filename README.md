# Integrating with Epicor ERP 10 #
Epicor ERP has had a variety of code-based integration scenarios described and commented over the years. If you cannot use a higher-level tool such as Service Connect, the Import functionality, BPM, etc and you need to use code here are examples and tradeoffs for each approach.
## Prerequisites ##
### Existing Help ###
I routinely install the Erp 10 Help doc on my dev box. You can for your customers on a local server or use the ‘Epicor.com’ help.
### Network Protocol Bindings ###
Before getting started with code level approaches, make sure you understand the different deployment models and the different Networking options available to you. This should give you an understanding of how options will affect your performance.
## Leveraging Client Assemblies ##
This is the first approach ever discussed and still is probably the fastest due to the serialization approach used in the Epicor binary serialization. When we have a Contract assembly on the client and server, columns and table order can be ensured. This allows for fast and dense packing of values into the payloads sent across the wire.

**Pro**

Speed. Models the client approach

**Con**

Have to manually deploy dlls to the client, have a partial client in stall (a sysconfig). 
## Use SOAP ##
SOAP is the open standard from communicating across multiple OS and languages. It has advanced communication options available (See ws-*). No Epicor client files are required since this approach needs to support any OS or language.

**Pro**

Supports every advanced integration scenario
No Epicor dlls needed on client

**Con**

Only talks over BasicHttp and SOAPHttp bindings. No binary serialization so duration of calls can be longer than other options.
## New approach – REST ##
REST is the approach new to 10.1.500 preview and released in 10.1.600 so it is the newest approach. REST leverages a URL address to make calls into the server and passes data as http Request and Response objects. It requires nothing from Epicor on the client as it is normally running within OS and languages that are not dotnet and Windows. 
It has a distinct advantage over other Integration approaches as it can query from just it’s columns of interest so the wire serialization time can be tuned.

**Pro**

Works EVERYWHERE
No Epicor dlls needed on client
Tunable payload on client

**Con**

Least mature for Epicor.
Not always an exact mapping to legacy approaches



