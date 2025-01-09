## Lifecycle of basic Federated Learning (FL)

1. Orchestration & Aggregation Server (OAS) sends a pretrained/untrained global model to all the participating clients.
2. Clients on receiving this model starts training it using their local data.
3. OAS expects these clients to return the model weights within a stipulated duration which is the accepting window of a round.
4. All the model weights received during the accepting window are then aggregated using an aggregation strategy (`FedAvg` is used commonly) to form a new global model.
5. Goto 1 unless convergence is achieved.

---
## Components:
#### Orchestratoion and Aggregation Server (OAS): 
- Orchestration: Sending and receiving model weights from multiple clients.
- Aggregation: Aggregation of model weights.

#### Client:
- Sending and receiving model weights from the server.
- Locally training the model on available data.

---

## Orchestration
#### Requirements 
- A bi-directional communication is required.
We can use Client Server architecture for Client -> Server communication and Pub-Sub for Server -> Client.

#### Architectures
##### Client Server:
Clients can send their local model using `Post` requests and retrieve the global model from the server using `Get` requests. 
How will client know that when to send or receive models?
This communication has to happen from server side and we need to make additional arrangements to the client server architecture to accomodate that.

##### Pub-Sub:
As the type of communication is related to starting or ending of various events in the lifecycle of FL and needs to be broadcasted to all the participating clients. `Pub-Sub` seems to be natural choice with our orchestrator as publisher of the events while all the clients subscribed to the Publisher for taking actions accordingly.


