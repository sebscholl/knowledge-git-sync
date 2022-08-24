# S3 CORS (Cross Origin Resource Sharing)

Created: May 8, 2019 7:10 PM
Updated: May 8, 2019 7:14 PM

Limit the number of websites that can access your objects in S3 using CORS policies.

**Example**

Were there two buckets (b1 and b2) where b1 has a static site and b2 has images. A client would request the site from b1, it would get delivered, and then the client would request any images from b2. However, the ORIGIN of the site came from b1. UNLESS b2 has specified that b1 is an allowed origin, it will reject the request.