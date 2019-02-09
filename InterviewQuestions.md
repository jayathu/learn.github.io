# Common Interview Questions

## Single Vs Doubly Linked List:

The choice between singly linked list and doubly linked list really depends on different factors like memory usage, whether or not the data structures are going to be used mostly for searching or mostly for updating (insertions and deletions) and things like that.  Singly linked lists require lesser memory for storage and they are simple to implement. Also, operations like insertions and deletions at next node are faster. However, reverse iteration is not possible in these lists. It’s also very important to keep a pointer to the head of a singly linked list, or else there’s no way to keep track of the list in the memory. Also, insertions and deletions at previous node requires us to traverse from head, all the way to that node, which is not very efficient. 

Doubly linked lists have an advantage of being able to traverse in both directions. So, deleting and inserting previous nodes is as easy as deleting next nodes. They work great for search operations but too many insertions and deletions could be expensive because of the overhead of maintaining an additional pointer to the previous node. 

So, in a nutshell, single linked lists work best for applications where the data need to be inserted or deleted in the end and there’s not many search operations to perform. Plus, they save memory. Doubly linked lists work great for applications where you’d require frequent search but not many insertions/deletions. They also use up more memory than the singly linked lists. 

## Managed Code Vs Native Code

Native Code runs on 32 or 64 bit platforms running Windows version of Operating System. These programs are computed directly by the CPU. When we say native code, we mean applications written specifically to run on a specific platform. Native code provides direct access to windows operating system and hardware. As a result they provide great power and flexibility but the same time, it incurs huge responsibility on the developers to write clean code, making code development complex.

Managed Code: Provides a runtime environment called Common Runtime Environment (CLR) that shields from this complexity and provides a prebuilt foundation. It abstracts a lot of complexity which may lead to lack of flexibility and potentially slower performance. Managed code are portable to run on any platform and easier to write. They may however cause slower performance and end up using a lot of resources. 

Example of projects I’ve worked on that may be called native code are all the standalone win32 applications written in C++ which does not use any of the CLR libraries that come with the IDE. One such project is a particle system written entirely in C++ and OpenGL as a class project.

Example of managed code would be a windows based form application that requires .NET framework to be installed on the system and uses the libraries that come with it. 

## Thread safe code. 

A thread safe code is a piece of code that can be executed by two or more threads simultaneously, without tampering the shared data in a way that would cause different results for each execution. In other words, no matter how many threads simultaneously execute a thread safe code, the results of each one of those execution are exactly same.

There were a several instances where I had to use threads to run a piece of code, in my game. The game runs code every update. Usually, we put all the functionalities that need to be run every frame, inside of update function. But there are some functionalities such as interpolations of positions, rotations or colors etc which could be implemented using threads, rather than making them run as part of an update function. This helps make the code more readable and manageable. Specifically, I used an engine called Unity and programmed using C#. The threads could be implemented using what they call ‘Co-routines’ : you could write a piece of function as part of a co-routine and ‘Start’ and ‘Stop’ co-routines. 

## What happens when you type a URL on to the browser? (Facebook Question)

When you first hit enter after typing the URL, the URL (host name) gets translated into the DNS

IP Address - identifies a computer or a server in the Internet. Its simply a number of this form: w.x.y.z (each of these placeholders can be numbers from 0 - 255) - 32 bits, each of these numbers are 8 bits here. (2 pow 32 - 4BN IP addresses in total)
IP address v6 - 2 pow 128 address in total.

Your computer has to look up domain name of the IP address using the DNS Server. Your computer probably doesn’t have your own DNS server but your ISP or campus server might have it. But if you haven’t visited the url before, so that the server has no idea of what the mapping is, how do  you solve the problem? Thankfully, there are hierarchies of servers, so your ISP may know other servers that are bigger fish that has its own DNS server that might know. If none of the servers in the hierarchy know what the mapping is, there will be some server in the hierarchy that knows where to find the mapping from:  there are ‘root’ servers that knows all of the .coms, or all of the .nets etc. So your initial req can bubble up to these root servers and the mapping can bubble down to your local computer eventually. 

GET / HTTP/1.0 : Once your local computer has the mapping, it sends out a message to that server (www.google.com for example) with the return address of its own IP address. 
Your ISP has the default router that takes care of routing this packet across the globe to the actual destination. 

Upon arrival of this message at the google server, Google happens to be a web server, so it looks up the message for a ‘/’ slash that indicates a file. So it grabs the corresponding file, wraps it up with the message and sends it back to the return address. The routers then take care of sending this packet across the internet to your local computer. 

Your local computer gets the file in the form of html that the browser is able to render on your screen. 

