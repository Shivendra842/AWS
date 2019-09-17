go to bin folder of mongo db.

open bin folder in cmd.

create folder structure
	D:\data\db

IN cmd..
	mongod.exe
in another cmd in bin
	mongo

-------------------------------------------------------------

collection is equivalent to table in RDMS
document is a set of key-value pair 

document in mongodb is equivalent to row in RDBMS
fields in mongodb is equivalent to columns in RDBMS
------------------------------------------------
WriteResult({ "nMatched" : 1, "nUps
> db.employees.find().pretty()
{
        "_id" : 1001,
        "firstName" : "Shivendra",
        "lastName" : "Singh",
        "salary" : 20000,
        "age" : 23,
        "isEmployeed" : true
}
{
        "_id" : 1002,
        "firstName" : "Shivam",
        "lastName" : "Singh",
        "salary" : 30000,
        "age" : 22,
        "isEmployeed" : true
}
{
        "_id" : 1003,
        "firstName" : "Hari",
        "lastName" : "Galla",
        "salary" : 22000,
        "age" : 22,
        "isEmployeed" : true
}
{
        "_id" : 1004,
        "firstName" : "Anamika",
        "lastName" : "Yadav",
        "salary" : 24000,
        "age" : 22,
        "isEmployeed" : true
}
{
        "_id" : 1006,
        "firstName" : "Vikash",
        "lastName" : "Kumar",
        "age" : 22,
        "isEmployeed" : false
}
{
        "_id" : 1005,
        "firstName" : "Jahanvi",
        "lastName" : "Shrivastava",
        "salary" : 25000,
        "age" : 23,
        "isEmployeed" : true,
        "gender" : "female"
}
-------------------------------------------------

use dbs_name - create a database if no database of that name available else return the existing database and migrate to that database.
show dbs-   return all the database available, if no collection in a database that database will not show up untill collection is created.
db - shows the working database
db.dropDatabase()   -   drop the database.
db.createCollection(name,options)   - createa a new collection.

        

 db.employees.insert([{_id:1001,firstName:"Shivendra",lastName:"Singh",salary:20000,age:23,isEmployeed:true},{_id:1002,firstName:"Shivam",lastName:"Singh",salary:30000,age:22,isEmployeed:true}])

 db.employees.insert([{_id:1003,firstName:"Hari",lastName:"Galla",salary:22000,age:22,isEmployeed:true},{_id:1004,firstName:"Anamika",lastName:"Yadav",salary:24000,age:22,isEmployeed:true}])

 db.employees.insert([{_id:1005,firstName:"Jahanvi",lastName:"Garg",salary:22000,age:22,isEmployeed:false},{_id:1006,firstName:"Vikash",lastName:"Kumar",age:22,isEmployeed:false}])


db.collection_name.insert({"name":"shivam"})  -  insert data in the collection_name
db.collection_name.drop()   - drop the collection
db.collection_name.find() - show all the data in collection.
db.collection_name.find().pretty()  - show all the data in collection if json format.
db.collection_name.find({_id:1001})  - display all the details of _id 1001
db.collection_name.find({_id:1001},{age:0,lastName:0}).pretty()     - display all the details except age,lastName of employee with _id 1001 in json format
db.collection_name.update({_id:1005},{$set:{lastName:"Shrivastava"}})   - update the lastName of employee where id is 1005
	if $set is not used and only where and what value are given then the whole data is overwrited.
	if field is already not present then the field is created and value is added.
ex: db.employees.update({_id:1005},{$set:{gender:"female"}})

db.employees.update({_id:1005},{$inc:{salary:5000}})  -  increase the salary by 5000 where _id is 1005

db.employees.update({_id:1005},{$set:{gender:"female",age:22}})  - updating both gender and age in single query

db.employees.save({_id:1005,name:"Jahanvi Shrivastava",salary:25000,age:23,isEmployeed:true,gender:"female"})    - replace the details of _id:1005 with new details entered.

db.employees.remove({_id:1005})  - remove the documents of _id=1005  
 db.employees.remove({firstName:"Tanmay"})  -> if multiple Tanmay then all of them will be removed

db.employees.remove({})  - remove all the documents

db.employees.remove({lastName:/s/})   -> pattern matching, if lastname starts with 2

db.employees.find({},{firstName:1,_id:0})   -> correct query 

db.employees.find({},{firstName:1,lastName:0})   -> incorrect query, cannot have inclusion and exclusion at the same time

db.employees.find({},{gender:"female"}).pretty()  -> correct query
	output:
		{ "_id" : 1001 }
		{ "_id" : 1002 }
		{ "_id" : 1003 }
		{ "_id" : 1004 }
		{ "_id" : 1006 }
		{ "_id" : 1005, "gender" : "female" }

db.employees.find({},{firstName:1,_id:0}).limit(2)  -> only two documents will  be displayed. Find function can also contain query. If limit greater than total number of documents then all the documents are displayed.
		if no argument is passed in limit then all documents are displayed.
db.employees.find({}).skip(1)  -> skip the given number of documents. default value is 0

db.COLLECTION_NAME.find().sort({KEY:1})   -> sort the documents.  1 ascending, -1 descending
 ex db.employees.find().sort({lastName:1}).pretty()
	db.employees.find().sort({_id:-1}).pretty()

 db.employees.update({_id:1005},{$unset:{gender:0}}) -> to delete a field for given id

db.employees.count()  -> count the number of documents

db.employees.insert([{_id:1007,firstName:"Vikash",lastName:"Jha"}])

db.employees.update({firstName:"Vikash"},{$set:{lastName:"Kumar"}},{multi:true})


db.employees.update({firstName:"Vikash"},{$set:{foodILike:["idle","dosa"]}})


------------------------------------------discrepancy  check first---------------------------------

db.employees.update({firstName:"Vikash"}, {$push:{foodILike:"Pizza"}},{multi:true})   -> first entery entered in multi:true not given

db.employees.update({firstName:"Vikash"}, {$pop:{foodILike:"Pizza"}},{multi:true})   -> first entry will be removed is multi:true not given
-------------------------------------------------------------------------------------------------------------
-



db.employees.update({firstName:"Vikash"}, {$pull:{foodILike:"Pizza"}},{multi:true})   -> all entry removed

db.employees.update({firstName:"Tanmay"},{$set:{lastName:"Acharya",gender:"male"}},{upsert:true})   -> is document not present then new doucment is created and upserted

db.employees.find({$or:[{firstname:"Mahima"},{firstname:"Kavita"}]});  -> or operator

db.employees.find({age:{$gt:40}});    -> greater than 40 

db.employees.find({age:{$lt:40}});    -> less than 40

db.employees.find({age:{$gt:40}}).limit(1);   -> limit to one output

db.employees.find({"address.city":"Pune"}).pretty()      get address[ city:]

db.employees.find({},{firstname:1,lastname:1}).pretty()

db.employees.find().forEach(function(doc){print("EmpName:" + doc.firstname + "Emp Salary:"+ doc.salary)})   -> all the documents (doc) from the collection is specified format.
 	output
	EmpName:TanmayaEmp Salary:39000
	EmpName:ShilpaEmp Salary:20000
	EmpName:KadiresanEmp Salary:25000
	EmpName:VandanaEmp Salary:47000
	EmpName:SugumaraEmp Salary:23000
	EmpName:UmaEmp Salary:300000
	EmpName:KavitaEmp Salary:42000
	EmpName:MahimaEmp Salary:1200000

db.employees.find({salary:{$in:[20000,50000]}});   ->   20000 or 50000

db.employees.find({salary:{$in:[20000,100000]},age:{$gt:31}});    20000 or 1000000


 var mycursor=db.employees.find().sort({firstname:-1}).limit(5)
while(mycursor.hasNext()){print(tojson(mycursor.next()))}

 var mycursor=db.employees.find({},{firstname:1,lastname:1}).sort({firstname:-1}).limit(5)
 while(mycursor.hasNext()){print(tojson(mycursor.next()))}

var mycursor=db.employees.find({},{firstname:1,lastname:1}).sort({firstname:-1}).limit(5).skip(3)
while(mycursor.hasNext()){print(tojson(mycursor.next()))}

--------------------grouping
db.employees.aggregate([{$match:{"gender":"female"}}]).pretty()   -> having gender=female

db.employees.aggregate([{$group:{_id:"$gender",empcount:{$sum:1}}}])  count of number of male and female employee

db.employees.aggregate([{$match:{gender:"female"}},{$group:{_id:"$gender",empcount:{$sum:1}}}])
	output:
 	"_id" : "female", "empcount" : 4 }


db.employees.aggregate([{$match:{firstname:"Kavita"}},{$unwind:"$contacts"}]).pretty()   -> unwind the data according to contact

db.employees.aggregate([{sort:lastname:1}])


db.employees.aggregate([{$project:{LASTNAME:{$toUpper:"$lastname"}}},{$sort:{lastname:1}}])
	output:
	{ "_id" : 1, "LASTNAME" : "ACHARAYA" }
	{ "_id" : 2, "LASTNAME" : "BHOSALE" }
	{ "_id" : 3, "LASTNAME" : "KAUSHIK" }
	{ "_id" : 4, "LASTNAME" : "KOLESHWAR" }
	{ "_id" : 5, "LASTNAME" : "H" }
	{ "_id" : 6, "LASTNAME" : "P" }
	{ "_id" : 7, "LASTNAME" : "ARORA" }
	{ "_id" : 8, "LASTNAME" : "SHARMA" }

 db.employees.aggregate([{$project:{LASTNAME:{$toUpper:"$lastname"}}},{$sort:{LASTNAME:1}}])

db.employees.aggregate([{$project:{DOBYear:{$year:"$DOB"}}}]);
	output
	{ "_id" : 1, "DOBYear" : 1990 }
	{ "_id" : 2, "DOBYear" : 2002 }
	{ "_id" : 3, "DOBYear" : 1990 }
	{ "_id" : 4, "DOBYear" : 2014 }
	{ "_id" : 5, "DOBYear" : 2014 }
	{ "_id" : 6, "DOBYear" : 2019 }
	{ "_id" : 7, "DOBYear" : 2014 }
	{ "_id" : 8, "DOBYear" : 2002 }

db.employees.aggregate([{$project:{DOBYear:{$month:"$DOB"}}}]);
	{ "_id" : 1, "DOBYear" : 7 }
	{ "_id" : 2, "DOBYear" : 3 }
	{ "_id" : 3, "DOBYear" : 1 }
	{ "_id" : 4, "DOBYear" : 8 }
	{ "_id" : 5, "DOBYear" : 11 }
	{ "_id" : 6, "DOBYear" : 9 }
	{ "_id" : 7, "DOBYear" : 5 }
	{ "_id" : 8, "DOBYear" : 4 }
db.employees.aggregate([{$project:{DOBYear:{$week:"$DOB"}}     }]);
	{ "_id" : 1, "DOBYear" : 29 }
	{ "_id" : 2, "DOBYear" : 10 }
	{ "_id" : 3, "DOBYear" : 4 }
	{ "_id" : 4, "DOBYear" : 32 }
	{ "_id" : 5, "DOBYear" : 45 }
	{ "_id" : 6, "DOBYear" : 37 }
	{ "_id" : 7, "DOBYear" : 18 }
	{ "_id" : 8, "DOBYear" : 14 }
> db.employees.aggregate([{$project:{DOBYear:{$dayOfMonth:"$DOB"}}     }]);
	{ "_id" : 1, "DOBYear" : 25 }
	{ "_id" : 2, "DOBYear" : 11 }
	{ "_id" : 3, "DOBYear" : 31 }
	{ "_id" : 4, "DOBYear" : 10 }
	{ "_id" : 5, "DOBYear" : 11 }
	{ "_id" : 6, "DOBYear" : 17 }
	{ "_id" : 7, "DOBYear" : 6 }
	{ "_id" : 8, "DOBYear" : 9 }
>


