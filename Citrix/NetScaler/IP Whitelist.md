#To restrict access to known IP addresses only.#

**1. Create a RESPONSE ACTION**
Feedback to user that connection is unauthorised...
  add responder action act_unauthorised respondwith '"HTTP/1.1 403 Forbidden\r\n\r\n" + "The client: " + CLIENT.IP.SRC + " is not authorised to access URL:" + "HTTP.REQ.URL.HTTP_URL_SAFE"'
  *or just...*
  
