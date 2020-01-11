# Documentation for Bitcurate Stack

Documentation to respawn all the backends incase any breakdown and to store any artifacts. **Do not share this repository to unauthorized developers!**

## Table of contents
  * [server](#server)
  * [vault](#vault)
  * [nginx](#nginx)
  * [jenkins](#jenkins)
  * [portainer](#portainer)
  * [how-to-start-backend](#how-to-start-backend)

## server

Our primary server is EC2 instance, name `bitcurate-backend`. Make sure you able to access aws console to view it.

- Name: bitcurate-backend
- Public IP: 18.139.35.113 (reserved IP)
- Public domain: dev.bitcurate.com

To ssh,

```bash
ssh -i 'bitcurate-backend.pem' ubuntu@dev.bitcurate.com
```

## vault

All basic auth in *.dev.bitcurate.com use same password, generated in [/nginx/reverse-proxy/psswd](https://github.com/bitcurate/nginx/blob/master/reverse-proxy/psswd). If you want to replace it, make sure nginx able to use it.

**Username: admin, Password: A5cwn9YVcqnekR6Y**

## [nginx](https://github.com/bitcurate/nginx)

Can readme inside [nginx](https://github.com/bitcurate/nginx) to get better understanding how to configure nginx for bitcurate. Configurations are pretty straightforward for experienced nginx.

## jenkins

Can visit our jenkins dashboard here, http://dev.bitcurate.com:8080/. Login detail in [vault](#vault).

Our primary CICD is jenkins, any master push from our github repositories, it will send a payload to our webhook and jenkins will update the deployments with latest code.

## portainer

Can visit our portainer dashboard here, https://portainer.dev.bitcurate.com/. Login detail in [vault](#vault).

Portainer is our primary docker web management, to check logs and status for our containers. Bitcurate is 100% docker.

## how-to-start-backend

These steps are foundation, any major restart due to any circumstances (scaling instance, AWS error, or anything) need to follow these steps.

### 1. Make sure jenkins are alive,

```bash
sudo service jenkins status
```

If you saw something like,

```text
Jan 06 12:27:23 ip-172-31-42-83 su[1421]: pam_unix(su:session): session opened for user jenkins by (uid=0)
```

You are good to go.

### 2. Visit [jenkins](http://dev.bitcurate.com:8080/),

<img src="pictures/jenkins.png" width="50%">

### 3. Trigger CD by sequence in jenkins,

To trigger any job in jenkins, press right hand side play on selected row.

1. [Operations](#operations)
2. [prometheus](#prometheus)
3. [coins-exchanges-classifier](#coins-exchanges-classifier)
4. [emotion-relevancy-sarcasm-api](#emotion-relevancy-sarcasm-api)
5. [multilanguage-sentiment](#multilanguage-sentiment)
6. [summarization-news](#summarization-news)
7. [kafka](#kafka)


