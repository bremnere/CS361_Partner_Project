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

