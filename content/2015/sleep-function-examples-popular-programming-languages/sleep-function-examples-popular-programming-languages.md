---
title: Sleep Function Examples of Popular Programming Languages
date: 2015-01-23
redirect_from: /sleep-function-examples-popular-programming-languages/
---

{% image "./sleep-function.png", "Sleep function" %}

One of the most used functions of all time in programming is the sleep function. This widely spread function has come across at some point for us all. Usually at the beginning of learning how to program, we get the need to know how to processing of our finely tuned software. Most of the times this due to programming something in a funny way or just debugging and finding out what is going on.

Sleep function is part of every modern and not so modern programming language. It is used on many tasks but usually the main task of it is to wait something to happen. It usually works by suspending the execution of currently processing thread, but I think there are some solutions which just causes the program to “wait” until the time specified in the Sleep Function has passed.

The use cases where you have to use sleep function are quite minimal. I can only figure out one. If you have a job running on multiple web servers and the job updates on a regular basis. You apply a sleep function to the process and update them on a different interval so that at least one server has the information available all the time. Do you have any good examples of the sleep function?

Sleep Function Examples
-----------------------

Here I have gathered example code for the most used programming languages. If you think something is missing from the list, please post a comment and let me know.

Remember using programming languages sleep function is usually not the best way to do waiting. In my opinion you should always use function callbacks  which occur after something has happened and not sleep the program until it has.

### ABAP

Releases the work process to the listener and does an implicit database commit.

```
WAIT UP TO 10 SECONDS.
```

Does not release the process and does not do an implicit database commit.

```
CALL FUNCTION 'ENQUE\_SLEEP'

  EXPORTING

  seconds  \= 10.
```

### Assembly

There ain’t no actual Assembly sleep function. Most of the times the best result is achieved by [using nested loops](http://www.tek-tips.com/viewthread.cfm?qid=701937) where every time the inner loop gets down to zero the mother loop decreases. This is a very complicated thing to do and in order to get perfect timing you need to test it out a lot.

### C

C sleep function is a very simple one.

```
sleep(10);
```

### C#

C# sleep function is literally stopping the processing thread from continuing.

```
Thread.Sleep(10000);
```

### C++

C++ sleep function is the same as C.

```
sleep(10);
```

### COBOL

There is no COBOL sleep function. Sleep state is achieved by [contacting the running environment](http://stackoverflow.com/questions/11786621/how-to-sleep-in-mainframe-cobol) and using the sleep function of system.

### Delphi/Object Pascal

There is no Delphi/Object Pascal sleep function as the language requires you to do this [by using a function callback](http://prestwood.com/ASPSuite/eBoard/Thread.asp?MBID=3033).

### Java

Java sleep function is almost the same as in C#. This stops the thread processing for specified period of time.

```
Thread.sleep(1000);
```

### JavaScript

There is no way to stop execution with JavaScript sleep function, but it certainly has a good way to achieve timing. So remember, this does not stop the processing of JavaScript, but it gets something done after the specified time.

```
setTimeout(function(){ alert("Lennu.net"); }, 10000);
```

### MATLAB

MATLAB sleep function is called pause, and it can be used in two ways. If you don’t give the time parameter it will pause the processing and wait for a key press. This is based on the system you are running so it shouldn’t be trusted to very accurate.

```
pause(10)
```

### Objective-C

With Objective-C sleep function you can pause the great applications of iPhone, but remember once again that this is very bad practice in application development.

```
NSThread sleepForTimeInterval:10.0f\];
```

### Perl

Perl sleep function follows the same simple command which you can rely to stop the program for a specified amount of time.

```
sleep(10);
```

### PHP

As PHP has a lot of functions from Perl and the PHP sleep function is very similar.

```
sleep(10);
```

### PL/SQL

PL/SQL sleep function is a procedure which suspends active session for the specified time.

```
DBMS\_LOCK.Sleep(10);
```

### Python

In Python sleep function is located into time object which contains sleep that stop the execution for the time given to the function.

```
time.sleep(10)
```

### R

R sleep function is from the Sys object.

```
Sys.sleep(10)
```

### Ruby

Ruby sleep function follow the same simple syntax on sleep. This suspends the program from continuing.

```
sleep(10)
```

### Transact-SQL

Transact-SQL is a bit more advanced and can do great stuff if you need specific sleep times. It is not very accurate though.

```
WAITFOR DELAY '00:00:10'
```

### Visual Basic

Visual Basic sleep function is the shortest and quickest way to write program to suspend computing.

```
Sleep 10000
```

### Visual Basic .NET

Visual Basic sleep function is achieved from System which stops the current thread for specified amount of time.

```
System.Threading.Thread.CurrentThread.Sleep(10000)
```