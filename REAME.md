##ReadMe
This is a dockerized version of the [wso2emm](http://wso2.com/products/enterprise-mobility-manager) version 2.0.1


##Build the image
1. clone the repository.
2. cd into the repository.
3. ```docker build -t <nameofyourchoice> .```
##Run the image

1. ```docker  run -d --name <nameofyourchoice> -p 9433:9433 -p 9763:9773 <containername>```

2. Then you can access EMM Admin Console in the following URL

   ```
   https://localhost:9443/emm
   ```

##Configure your server

[Follow the General Server Configurations manual](https://tr.im/5dwWr)

After completing the server configuration modify the following files:

+ app-manager.xml


+ identity.xml


+ sso-idp-config.xml 


+ sso-idp-config.xml


+ sso-sp-config.properties

1. **app-mamager.xml** file which is located in /repository/conf Change the below url according to the docker container IP address {code} https://localhost:9443/samlsso {code} For an example, my docker container IP is 172.17.0.2 . So I have changed the url as below {code} https://172.17.0.2:9443/samlsso {code}

2. **identity.xml** file which is located in /repository/conf/identity Change the below url according to the docker container IP address {code} https://localhost:9443/samlsso {code} 

3. **sso-idp-config.xml**file which is located in /repository/conf/identity {code} https://localhost:9443/publisher/acs https://localhost:9443/publisher/acs {code} You can see "localhost" keyword in several urls inside sso-idp-config.xml file .So; if you cannot access any pages in other applications, you can replace the localhost with container IP address. 

4. **sso-sp-config.properties** file which is located in /repository/conf/security directory. Change the below url according to the docker container IP address {code} SAML2.IdPURL=https://localhost:9443/samlsso {code} 