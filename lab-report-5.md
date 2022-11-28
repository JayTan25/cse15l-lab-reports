# Lab Report 5

## Grade.sh 

```
rm -rf student-submission
git clone $1 student-submission
echo "Cloned"
score=0
CPATH="..:../lib/hamcrest-core-1.3.jar:../lib/junit-4.13.2.jar"
cd student-submission


if [[ -f "ListExamples.java" ]]
then 
    echo "File Found"
else 
    echo "File not Found"
    echo "File may be in wrong directory"
    exit 1
fi

javac -cp $CPATH *.java

if [[ $? -eq 0 ]]
then
    echo "Compiled"
else
    echo "Compile Error"
    exit 1
fi

java -cp $CPATH org.junit.runner.JUnitCore TestListExamples > error.txt
if [[ $(grep -c "testFilter" error.txt) -eq 0 ]]
then
    let "score+=1"
    echo "[PASSED testFilter]"
else
    echo "[FAILED testFilter]"
fi

if [[ $(grep -c "testMerge" error.txt) -eq 0 ]]
then
    let "score+=1"
    echo "[PASSED testMerge]"
else
    echo "[FAILED testMerge]"
fi


echo "Score: $score / 2"
```

## Screenshots 
![1](lab-5-screenshots/gradesh1.jpg)

![1](lab-5-screenshots/gradesh2.jpg)

![1](lab-5-screenshots/gradesh3.jpg)


# Tracing Grade.sh
I am going to trace screenshot 3, which reveals that the methods are correct and received a full score.

## Lines with Commands
On line 9, the command of `-f` was used. The standard output
would be if the file was found or not. The return code was 0 since there was a file called `ListExamples.java`. 

On line 29, the command `grep` was used. The standard output would be if the line containing it was true or false. In this case, the return code was a 0.

On line 28, the command `>` was used. The standard output would be the redirection of the code. The return code was 0 in this case.

## If Statements
On line 9, there was an if statement to check if the file `ListExamples.java` existed or not. In this instance, the condition was true because the file did exists in the file `student-submissions`

On line 20, there was an if statement to check if to check if it could compile or not. This condtion was true because there were no compile errors in that file.

On line 29, there was an if statement to check if the `testFilter` method passed or not. This condition was true because the method did not contain any error when running it.

On line 37, there was an if statement that checked if the method `testMerge` passed or not. This condition was true because there were no compile errors in that file. 

## Lines That Do Not Run
Lines 13-15 do not run because the if branch does not evaluate this block of code. 

Lines 24 and 25 do not run because the file was able to compile, so the lines in the else statement were not execuated. 

Line 34 did not run because the  `testFilter` method passed the test. So, line 34 was not executed because it did not reach the else statement

Line 42 did not run because the `testMerge` method passed the test. Line 34 was not executed because it did not reach the else statement. 