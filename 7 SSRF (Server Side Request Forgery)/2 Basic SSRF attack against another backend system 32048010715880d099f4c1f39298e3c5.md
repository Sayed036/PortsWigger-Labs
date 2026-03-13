# 2. Basic SSRF attack against another backend system.

Solution : 

- Click a Product and Check out the Stock Checking Functionality
- Capture the request, you can see that there is a parameter called stockAPI which has an encoded string
- Send the request to the decoder and click smart decode to decode the string and know that it is directing to a internal page
- Here, instead of adding http://localhost/admin, we have to add the IP Address which ranges from 192.168.0.0 to 192.168.0.255 like http://192.168.0.X:8080/admin
- So, send the request to Intruder, clear the payloads, then select the X in Ip address and click add.Move to payloads tab, choose numbers in payload
- Then set the start value to 1, then end to 255 and step by 1
- Now, start the attack then you can able to see a 200 status code in response
- View the response of that request and note the IP address is http://192.168.0.24:8080/adminNow send that request with the IP we found in the repeater
- Now you can able to see that the response is successful and on inspecting the code you can get the URL to delete user Carlos
- If you are using a professional version, you can render the response for a better result
- Copy the URL that we found on 4th step's response
- Now Paste it on the stock API Parameter to solve the Lab