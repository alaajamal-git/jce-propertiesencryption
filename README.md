# jce-propertiesencryption

This project contains Config-Server service only that configured to read encrypted values from properties files.
-if we want to encrypt the values using symmetric algorithm we should use the property encrypt.key=fgr3444GFeds23DSAArrgrVbr in bootstrap file within the Config-Server which is the key uses in encryption and decryption processes.
-if we want to encrypt the values using an asymmetric algorithm we should first generate the pub,pri pair file using keytool of java and then use this file in enc/dec processes by adding three properties:
encrypt.key-store.location=file:///${user.home}\\key\\server.keystore  # location of file
encrypt.key-store.password=alaajamal # the password of file
encrypt.key-store.alias=teiid # the alias of the file

these values were set in bootstrap file within the Config-Server.

Run Steps:
1.  Encrypt on property value using :
     post : http://localhost:8012/encrypt
     body : {guest}

2.  Use the encrypted value {the response of last request} in the destination property file:
      property={cipher}encryptedvalue
      i.e.
      spring.rabbitmq.password={cipher}AQA43Iz5a9x/MNCYcjsTBmomPOZHs016VAFteB8H+qlpwH8nw7Cm7PdwrtRS2zDiFdw7HX9vstgwK9Trra5xiiXsIKxv97FuFhTKdG64taFtcFwZk6TSzBTcAyhcAy8WQ/hAYnncfx3/Dcv6yt092UITrCri3jU/vz6xkjhrY9/dAfKB0hkg5hD+M4aNpUjyv9bC4omlYVdYktiw804JegtQjsmYxXF/PNqM6+kxtD+xG6bnEOrk1tVH+qYYCURCF1UXKKqsWJoh3zRlyDkyGfJNAlh5J8QMTTkpzDkVPtPQER86l3SKUQwT4mBRoXb/frAt0+vFTorH/u9v5JeqfGiYWYjSbyn9o6W0tlyYkQc7uD80sPxj5MwBmJFnD8PVtQQ=
      
3.  Test the properties runs on Config-Server:
GET : http://localhost:8012/users-ws/default

We will see the decrypted values in the response
