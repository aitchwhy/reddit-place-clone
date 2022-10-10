# reddit-place-clone
Personal implementation of Reddit's r/place

## Design

TODO: Lucidchart diagram here

* Dataflow
  * client side publishes image edits via REST call to server
  * server edits publishes to kafka topic (which are ordered)
  * server consumes from kafka (via websocket endpoint)
    * this is directly called from client only to replay 

* Django server
* Kafka topic (1 is enough) - this imposes global ordering + storage for replay
* nginx webserver 


## Roadmap

* [x] Come up with rough overall design
  * [x] diagram of dataflow - https://lucid.app/documents/view/5ad2f8b0-f60e-41dd-9ed2-05fe2f6686c9
  * [x] capacity planning (reqs / second load)
  * [x] API endpoints design
* [ ] backend server + Kafka
  * [ ] 1 - install + start kafka local instance with 1 topic
  * [ ] 2 - create skeleton django server
  * [ ] 3 - server APIs impl
    * [ ] 3.1 - `/api/edit` along with JSON payload
```
POST /api/edit

{
    ???

}
```
    * [ ] 3.2 - `/api/fetchBoard` - this is called by NGINX to refresh board state periodically (not by client directly)
    * [ ] 3.3 - `some websocket for client<>server` - fetch edits in kafka following version of fetched board state (nginx will have slightly stale state)
  * [ ] 4 - setup nginx to periodically fetch board state and serve clients
* TODO: UI / clientside
* TODO: deployment to public cloud (AWS)

