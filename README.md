# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
1. Create a **socket server** and start listening for incoming client connections.
2. Accept the client connection and **receive the HTTP request** from the client.
3. If the request method is **GET**, open the HTML file and send its content as a response to the client.
4. If the request method is **POST**, extract the uploaded data from the request and store it in a file.
5. Send a response message to the client and **close the connection**.
## Program 
## Server.py
```
import socket

s = socket.socket()
s.bind(("localhost",8080))
s.listen(1)

print("Server running...")

while True:
    c,addr = s.accept()
    
    request = c.recv(1024).decode()
    print("Request received")

    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()

        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())

    elif "POST" in request:
        data = request.split("\n\n")[1]

        f = open("upload.txt","w")
        f.write(data)
        f.close()

        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())

    c.close()
```
## Client.py
```
import socket

s = socket.socket()
s.connect(("localhost",8080))

ch = input("1.Download 2.Upload : ")

# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())

    data = s.recv(4096)
    print(data.decode())

# Upload file
else:
    msg = input("Enter data to upload: ")

    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())

    data = s.recv(1024)
    print(data.decode())

s.close()
```
## OUTPUT
<img width="820" height="364" alt="image" src="https://github.com/user-attachments/assets/eddf77e7-a785-4d2e-840e-88a952eadcf6" />
<img width="825" height="337" alt="image" src="https://github.com/user-attachments/assets/2837c948-5952-45ad-95a4-f33b08d4f765" />
<img width="1359" height="347" alt="image" src="https://github.com/user-attachments/assets/e10d64e6-444e-4d8b-911e-6df2affe5bd2" />



## Result
Thus the socket for HTTP for web page upload and download created and Executed
