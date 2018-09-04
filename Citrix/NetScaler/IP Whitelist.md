# To restrict access to known IP addresses only

### 1. Create a RESPONSE ACTION
Feedback to user that connection is unauthorised...<br/>
```
add responder action act_unauthorised respondwith '"HTTP/1.1 403 Forbidden\r\n\r\n" + "The client: " + CLIENT.IP.SRC + " is not authorised to access URL:" + "HTTP.REQ.URL.HTTP_URL_SAFE"'
```
<br/>
### 2. Create a DATASET
Create a data-set for a list of IP Addresse that will be allowed to access the vServer.<br/>
```
add policy dataset ds_ip_allowed ipv4
```
### 3. Add required IP addresses
Add the required IP addresses to the data-set.<br/>
```
bind policy dataset ds_ip_allowed 111.222.333.444
bind policy dataset ds_ip_allowed 222.333.444.555
```
### 4. Create a RESPONSE POLICY
Create a Response Policy that is true if the connection is NOT on the allowed IP list, with the Action created above.<br/>
```
add responder policy ResPol_UnauthorisedIP "CLIENT.IP.SRC.TYPECAST_TEXT_T.EQUALS_ANY(\"ds_ip_allowed\").NOT" act_unauthorised
```
### 5. Bind the POLICY
Bind the Policy to the vServer as a Responder Policy.
