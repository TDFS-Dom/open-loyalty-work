[![Build Status](https://travis-ci.org/DivanteLtd/open-loyalty.svg?branch=master)](https://travis-ci.org/DivanteLtd/open-loyalty)

# Open Loyalty

Fork framework here www.github.com/dataworksbi/open-loyalty

Code Framework here www.github.com/TDFS-Dom/open-loyalty-framework

Open Loyalty is a headless loyalty technology for visionaries and innovators who want to implement an effective loyalty program that cuts across multiple touchpoints. Our solution is 100% API-first and unlike old-fashioned, monolithic software, it’s easy to integrate with and ensures complete flexibility, speed, and effectiveness at all levels. 

Book a live demo here www.openloyalty.io

## Editions

Open Loyalty is available in two editions - **Hosted**, and **Dedicated**.
Here you can find Open Source Edition (v.3.2). It is limited to non-commercial projects, does not provide guaranteed performance and scalability and therefore, it is recommended for testing purposes only. It is also significantly different from the current commercial editions of Open Loyalty.  

**We strongly advise using Hosted or Dedicated in commercial projects.**

Hosted or Dedicated editions are not available publicly on GitHub.
To get the quotation, please visit www.openloyalty.io and send the request.

|                                     | Hosted    | Dedicated   |
| ----------------------------------- | --------- | ----------- |
| All loyalty & gamification features | Yes       | Yes         |
| Robust & efficient API              | Yes       | Yes         |
| Members limit                       | Unlimited | Unlimited   |
| Hosting                             | Cloud     | Self-hosted |
| High performance & scalability      | Yes       | Yes         |
| Maintenance & support               | Yes       | Yes         |
| Whitelabel                          | Yes       | Yes         |


## Business applications

There are a variety of ways Open Loyalty can be used to provide headless loyalty architecture. 
Based on it, you can build loyalty solutions like: 

* full loyalty programs for off-line and on-line channels
* mobile loyalty applications
* motivational programs for employees
* loyalty modules for your own product

## Performance and scalability
High performance and scalability are available in Hosted and Dedicated editions only.
In this [case study](https://www.openloyalty.io/building-a-massive-scale-loyalty-program-with-aws/) you can read more about how Open Loyalty reached over **1500 concurrent API calls 
with a response time under 1 second** and **Easy scalability with Kubernetes and AWS infrastructure**.

## Screenshots

![Admin Cockpit](https://user-images.githubusercontent.com/3582562/54033263-1db79500-41b4-11e9-8f2d-9b91acce50cf.png)

If you are a developer and want to attach source code, then you have to build base docker images:

Run this script only from ./docker/base directory
```
cd ./docker/base/
./build_dev.sh
```

and run containers:

```
cd ../../
docker-compose up
```

After that, execute the below command to initiate and set up the database:
```
docker-compose exec --user=www-data php phing setup
```

After starting Open Loyalty in developer mode, it exposes services under slightly different URLs:

 * http://10.10.10.22:8081/admin - the administration panel,
 * http://10.10.10.22:8081/client - the customer panel,
 * http://10.10.10.22:8081/pos - the merchant panel,
 * http://10.10.10.22:8888 - RESTful API port
 * http://10.10.10.22:8888/app_dev.php/doc - swagger-like API doc

Account admin:
```
admin
```
Account customer:
```
user@oloy.com
```
Account seller:
```
user@oloy.com
```
Password for all: 
```
open
```