# S3 Consistency Model

Created: May 8, 2019 7:14 PM
Updated: May 8, 2019 7:18 PM

- Read after write consistency for PUTS of new objects
    - This means that an object can be read IMMEDIATELY after it is created in S3
    - EXCEPTION: If you first do a GET and receive 404, then successfully PUT the object, you will immediately receive a GET 404 - eventually consistent
- Eventual Consistency for DELETES and PUTS of existing objects
    - If you read an object immediately after updating it, you may get an older version - eventually consistent
    - If you DELETE an object, you may be able to retrieve it immediately after - eventually consistent