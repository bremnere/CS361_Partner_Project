This project is a microservice for a login/ account creation system to be used with
zeroMQ sockets. Here is an example in Python for how to request data:
import zmq
def send_request(request_type, username, password):
	context = zmq.Context()
	socket = context.socket(zmq.REQ)
	socket.connect(“tcp://localhost:5555”)

	request = {
		‘type’: request_type,
		‘username’: username,
		‘password’: password
	}
	socket.send_json(request)
	response = socket.recv_string()

	socket.close()
	context.term()
	return response

response = send_request(‘create_account’, ‘newuser’, ‘newpass’)
print(response) 

To recieve data the client will need to wait for a response from the microservice.
zeroMQ will block with recv until the response is received. Once the response is
recieved it can be processed by the main program.


![cs361UML drawio](https://github.com/bremnere/CS361_Partner_Project/assets/122298391/00dd6f20-6816-46bb-bfa7-b7c68e136a6c)

Communication Contract: 
1.	I implemented my microservice for Mitch Smith.
2.	The microservice is completed.
3.	Mitch has access via GitHub and can also run the code locally.
4.	If you cannot access the microservice reach out to me via direct message on Discord. I am generally available in the evenings and on weekends.
5.	While I may have availability to work on issues at the last minute I cannot guarantee this. If you reach out with 48 hours notice I will certainly be able to assist you.
6.	The program should work with the simple zeroMQ REQ/REP pattern that we discussed. You should just need to add the corresponding sockets to your main program.
