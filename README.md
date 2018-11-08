# spring-redis-cache




@Cacheable(value = "customer", key = "'firstName:' + #customer.firstName", condition = "#customer.firstName !=null")
*****************************************************
1) savingWithOutReturn : 
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "savingWithOutReturn","lastName": "savingWithOutReturn","address": "savingWithOutReturn"} 
DB Result : { "_id" : "savingWithOutReturn", "lastName" : "savingWithOutReturn", "address" : "savingWithOutReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithOutReturn]
GetCacheRecords with firstName : Null 

First PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False
Second GET Request - Hit to DB : False 
(A key is already in the cache with no return value/body. So when using get, it searching with key in cache and returns null value and DB hit is not performed)

--------
UPDATE:
--------
Request Body : {"firstName": "savingWithOutReturn","lastName": "savingWithOutReturn1","address": "savingWithOutReturn1"} 
DB Result : { "_id" : "savingWithOutReturn", "lastName" : "savingWithOutReturn1", "address" : "savingWithOutReturn1", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithOutReturn]
GetCacheRecords with firstName : Null 

Second PUT Request - Hit to DB :  False
First GET Request - Hit to DB : False
Second GET Request - Hit to DB : False

*****************************************************
2) savingWithReturn : 
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "savingWithReturn","lastName": "savingWithReturn","address": "savingWithReturn"}
DB Result : { "_id" : "savingWithReturn", "lastName" : "savingWithReturn", "address" : "savingWithReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithReturn]
GetCacheRecords with firstName : {"firstName": "savingWithReturn","lastName": "savingWithReturn","address": "savingWithReturn"}

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 


--------
UPDATE:
--------
Request Body : {"firstName": "savingWithReturn","lastName": "savingWithReturn1","address": "savingWithReturn1"}
DB Result : { "_id" : "savingWithReturn", "lastName" : "savingWithReturn", "address" : "savingWithReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithReturn]
GetCacheRecords with firstName : {"firstName": "savingWithReturn","lastName": "savingWithReturn","address": "savingWithReturn"}

PUT Request - Hit to DB : False
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 

*****************************************************
3) editAfterSavingWithoutReturn :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "editAfterSavingWithoutReturn","lastName": "editAfterSavingWithoutReturn","address": "editAfterSavingWithoutReturn"}
DB Result : { "_id" : "editAfterSavingWithoutReturn", "lastName" : "editAfterSavingWithoutReturn", "address" : "editAfterSavingWithoutReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:editAfterSavingWithoutReturn]
GetCacheRecords with firstName(editAfterSavingWithoutReturn) : Null -  Hit to DB : False
GetCacheRecords with firstName(harihsri) : Null - Hit to DB : True

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 
>

--------
UPDATE:
--------
Request Body : {"firstName": "editAfterSavingWithoutReturn","lastName": "editAfterSavingWithoutReturn1","address": "editAfterSavingWithoutReturn1"}
DB Result : { "_id" : "editAfterSavingWithoutReturn", "lastName" : "editAfterSavingWithoutReturn", "address" : "editAfterSavingWithoutReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:harihsri, customer::firstName:editAfterSavingWithoutReturn]
GetCacheRecords with firstName(editAfterSavingWithoutReturn) : Null.  - Hit to DB : False
GetCacheRecords with firstName(harihsri) : Null       - Hit to DB : False

PUT Request - Hit to DB : False
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 

*****************************************************
4) editAfterSavingWithReturn :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "editAfterSavingWithReturn","lastName": "editAfterSavingWithReturn","address": "editAfterSavingWithReturn"}
DB Result : { "_id" : "editAfterSavingWithReturn", "lastName" : "editAfterSavingWithReturn", "address" : "editAfterSavingWithReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:editAfterSavingWithReturn]
GetCacheRecords with firstName(editAfterSavingWithReturn) : {"firstName":"harihsri","lastName":"editAfterSavingWithReturn","address":"editAfterSavingWithReturn"} 
- Hit to DB : False
GetCacheRecords with firstName(harihsri) : Null - Hit to DB : True

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 
--------
UPDATE:
--------
Request Body : {"firstName": "editAfterSavingWithReturn","lastName": "editAfterSavingWithReturn1","address": "editAfterSavingWithReturn1"}
DB Result : { "_id" : "editAfterSavingWithReturn", "lastName" : "editAfterSavingWithReturn", "address" : "editAfterSavingWithReturn", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:harihsri, customer::firstName:editAfterSavingWithReturn]
GetCacheRecords with firstName(editAfterSavingWithReturn) : {"firstName":"harihsri","lastName":"editAfterSavingWithReturn","address":"editAfterSavingWithReturn"} 
- Hit to DB : False
GetCacheRecords with firstName(harihsri) : Null - Hit to DB : False

PUT Request - Hit to DB : False
First GET Request - Hit to DB :  False 
Second GET Request - Hit to DB : False 

----------------------------------------------------------------
########## @CachePut ###########################
-----------------------------------------------------------------


@CachePut(value = "customer", key = "'firstName:' + #customer.firstName", condition = "#customer.firstName !=null")
*****************************************************
5) savingWithOutReturnCP :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "savingWithOutReturnCP","lastName": "savingWithOutReturn","address": "savingWithOutReturn"} 
DB Result : { "_id" : "savingWithOutReturnCP", "lastName" : "savingWithOutReturnCP", "address" : "savingWithOutReturnCP", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithOutReturnCP]
GetCacheRecords with firstName : Null 

First PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False
Second GET Request - Hit to DB : False 
>
--------
UPDATE:
--------
Request Body : {"firstName": "savingWithOutReturnCP","lastName": "savingWithOutReturnCP1","address": "savingWithOutReturnCP1"}
DB Result : { "_id" : "savingWithOutReturnCP", "lastName" : "savingWithOutReturnCP1", "address" : "savingWithOutReturnCP1", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithOutReturn]
GetCacheRecords with firstName : Null 

Second PUT Request - Hit to DB :  True
First GET Request - Hit to DB : False
Second GET Request - Hit to DB : False

*****************************************************
6) savingWithReturnCP :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "savingWithReturnCP","lastName": "savingWithReturnCP","address": "savingWithReturnCP"}
DB Result : { "_id" : "savingWithReturnCP", "lastName" : "savingWithReturnCP", "address" : "savingWithReturnCP", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithReturnCP]
GetCacheRecords with firstName : {"firstName": "savingWithReturnCP","lastName": "savingWithReturnCP","address": "savingWithReturnCP"} 

First PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False
Second GET Request - Hit to DB : False 
>
--------
UPDATE:
--------
Request Body : {"firstName": "savingWithOutReturnCP","lastName": "savingWithOutReturnCP1","address": "savingWithOutReturnCP1"}
DB Result : { "_id" : "savingWithReturnCP", "lastName" : "savingWithReturnCP1", "address" : "savingWithReturnCP1", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:savingWithOutReturn]
GetCacheRecords with firstName : {"firstName": "savingWithOutReturnCP","lastName": "savingWithOutReturnCP1","address": "savingWithOutReturnCP1"} 

Second PUT Request - Hit to DB :  True
First GET Request - Hit to DB : False
Second GET Request - Hit to DB : False

*****************************************************
7) editAfterSavingWithoutReturnCP :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "editAfterSavingWithoutReturnCP","lastName": "editAfterSavingWithoutReturnCP","address": "editAfterSavingWithoutReturnCP"}
DB Result : { "_id" : "editAfterSavingWithoutReturnCP", "lastName" : "editAfterSavingWithoutReturnCP", "address" : "editAfterSavingWithoutReturnCP", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:harihsri]
GetCacheRecords with firstName(editAfterSavingWithoutReturnCP) : {"firstName": "editAfterSavingWithoutReturnCP","lastName": "editAfterSavingWithoutReturnCP","address": "editAfterSavingWithoutReturnCP"}
 -  Hit to DB : True
GetCacheRecords with firstName(harihsri) : Null - Hit to DB : false

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  True  (Key : editAfterSavingWithoutReturnCP)
Second GET Request - Hit to DB : False (Key : editAfterSavingWithoutReturnCP)
>

--------
UPDATE:
--------
Request Body : {"firstName": "editAfterSavingWithoutReturnCP","lastName": "editAfterSavingWithoutReturnCP1","address": "editAfterSavingWithoutReturnCP1"}
DB Result : { "_id" : "editAfterSavingWithoutReturnCP", "lastName" : "editAfterSavingWithoutReturnCP1", "address" : "editAfterSavingWithoutReturnCP1", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:editAfterSavingWithoutReturnCP, customer::firstName:harihsri]
GetCacheRecords with firstName(editAfterSavingWithoutReturn) : {"firstName": "editAfterSavingWithoutReturnCP","lastName": "editAfterSavingWithoutReturnCP","address": "editAfterSavingWithoutReturnCP"}  
- Hit to DB : False
GetCacheRecords with firstName(harihsri) : Null       - Hit to DB : False

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False (Key : editAfterSavingWithoutReturnCP)
Second GET Request - Hit to DB : False (Key : editAfterSavingWithoutReturnCP)


*****************************************************
8) editAfterSavingWithReturnCP :
*****************************************************
--------
INSERT:
--------
Request Body : {"firstName": "editAfterSavingWithReturnCP","lastName": "editAfterSavingWithReturnCP","address": "editAfterSavingWithReturnCP"}
DB Result : { "_id" : "editAfterSavingWithReturnCP", "lastName" : "editAfterSavingWithReturnCP", "address" : "editAfterSavingWithReturnCP", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:harihsri]
GetCacheRecords with firstName(editAfterSavingWithReturnCP) : {"firstName": "editAfterSavingWithReturnCP","lastName": "editAfterSavingWithReturnCP","address": "editAfterSavingWithReturnCP"}
 -  Hit to DB : True
GetCacheRecords with firstName(harihsri) : {"firstName":"harihsri","lastName":"editAfterSavingWithReturnCP","address":"editAfterSavingWithReturnCP"} - Hit to DB : false

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  True  (Key : editAfterSavingWithReturnCP)
Second GET Request - Hit to DB : False (Key : editAfterSavingWithReturnCP)

--------
UPDATE:
--------
Request Body : {"firstName": "editAfterSavingWithReturnCP","lastName": "editAfterSavingWithReturnCP1","address": "editAfterSavingWithReturnCP1"}
DB Result : { "_id" : "editAfterSavingWithReturnCP", "lastName" : "editAfterSavingWithReturnCP1", "address" : "editAfterSavingWithReturnCP1", "_class" : "com.sriharilabs.model.Customer" }
Redis Cache Data : [customer::firstName:editAfterSavingWithReturnCP, customer::firstName:harihsri]
GetCacheRecords with firstName(editAfterSavingWithReturnCP) : {"firstName": "editAfterSavingWithReturnCP","lastName": "editAfterSavingWithReturnCP","address": "editAfterSavingWithReturnCP"}
- Hit to DB : False
GetCacheRecords with firstName(harihsri) : {"firstName": "harihsri","lastName": "editAfterSavingWithReturnCP1","address": "editAfterSavingWithReturnCP1"}       - Hit to DB : False

PUT Request - Hit to DB : True
First GET Request - Hit to DB :  False (Key : editAfterSavingWithReturnCP)
Second GET Request - Hit to DB : False (Key : editAfterSavingWithReturnCP)




