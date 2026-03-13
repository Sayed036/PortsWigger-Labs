# 1. Basic SSRF against the local server

- SolutionClick a Product and Check out the Stock Checking Functionality
- Capture the request, you can see that there is a parameter called stockAPI which has a encoded string
- Send the request to the decoder and click smart decode to decode the string and know that it is directing to an internal page
- So now, change the stockAPI parameter to http://localhost/admin as given in Lab description and send the request
- Now you can able to see that the response is successful and on inspecting the code you can get the URL to delete user Carlos