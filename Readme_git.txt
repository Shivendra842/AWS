Steps to follow to add file to git repository
------------------------------------------------------
git init

touch Demo1.txt

git add Demo1.txt

git commit -m "first commit"


git config --global http.proxy http://10.102.22.17:8080


git remote add origin https://github.com/Shivendra842/GitDemo.git

git push -u origin master


Command to Create a branch 
-------------------------------------------------------------------
git branch <branchName>

eg:

git branch Developer

Command to switch to another branch
----------------------------------------------------------
git checkout <branchName>

eg:

git branch Developer

command to push file to branch
-----------------------------------------------
git push -u origin <branchName>

eg:
git push -u origin master
git push -u origin Developer



--------------------------------------------LAB 1------------------------------------------
1. Create a repository  name A on github.
2. Create directories named B,C,D,E on your system.
3. git init all.
4. Create a file named info.txt in B.
5. git add info.txt
6. git commit -m "First commit to info.txt"
7. in B -> git branch Developer and git branch Tester.
8. in B -> git push --set-upstream https://github.com/Shivendra842/A.git Developer   ->to push all Developer to A
9. in B -> git push --set-upstream https://github.com/Shivendra842/A.git Tester	->to push all Developer to A
10.cd to C
11.in C ->  git pull https://github.com/Shivendra842/A.git Developer
12.create file named MyJavaCode.txt in C
13.in C -> git add MyJavaCode.txt
14.in C-> git commit -m "First commit for MyJavaCode"
15. cd to D
16.in D-> create a file named  MyJUnitTestCase.txt
17. in D-> git commit -m "First commit to MyJUnitTestCase"
18. in D -> git pull D:/Module4Demo/C/.git      ->pull all the data from C to D
19 make some changes to file MyJavaCode in D
20. git add MyJavaCode.txt
21. git commit -m "Second commit to MyJavaCode"
22. push all the data to A (Remote repository)
	git push --set-upstream https://github.com/Shivendra842/A.git master
23. in c pull all the data from A (Remote repository)
	git pull https://github.com/Shivendra842/A.git

	After this a conflict msg will be displayed
	****************************************************
	remote: Enumerating objects: 12, done.
	remote: Counting objects: 100% (12/12), done.
	remote: Compressing objects: 100% (6/6), done.
	remote: Total 11 (delta 2), reused 11 (delta 2), pack-reused 0
	Unpacking objects: 100% (11/11), done.
	From https://github.com/Shivendra842/A
	 * branch            master     -> FETCH_HEAD
	Auto-merging MyJavaCode.txt
	CONFLICT (add/add): Merge conflict in MyJavaCode.txt
	Automatic merge failed; fix conflicts and then commit the result.
	*****************************************************

24. git status -> in C
	go to the file having conflict. you will see <<<<<<< HEAD ============ >>>>>>>>>> in that file.
25. do the changes you want to commit.
26. git add .
27. git commit -m "conflict resolved"

---------------------------------------------------------------------------------------------------

git add means stagin a file for commit.
if file is added then some changes are made and status is checked using git status, it will not commit 
new changes even if the commit id done as the file is staged for previous changes only.




