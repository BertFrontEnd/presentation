## Transcript of presentation

- # So, who tells the JS engine that he needs to execute some piece of the program?

- In reality, the engine does not work in isolation - its own code is executed inside a certain environment, which, for most developers, is either a browser or Node.js. In fact, today there are JS engines for a wide variety of types of devices - from robots to smart bulbs. Each such device represents its own version of the environment for the JS engine.

- # A common characteristic of all such environments is a built-in mechanism called an event loop.

- It supports the execution of program fragments, invoking the JS engine for this.

- This means that the engine can be considered the runtime of any JS-code called on demand. And the planning of events - sessions of JS-code execution, is done by environment mechanisms external to the engine.

- So, for example, when your program executes an Ajax-request to download some data from the server, you write a command to write this data to the response variable inside the callback, and the JS-engine tells the environment: “Listen, I'm going to pause the program, but when you finish executing this network request and receive some data, please call this callback."

- # Take a look at the following diagram

- (main.png)

- # Here we see the JS-engine. He has two main components: Heap or Memory Heap and Call Stack

- # Heap or Memory Heap - is where memory allocation takes place (memory-heap.png)

- # Call Stack - is where the so-called stack frames fall into the process of executing the code.(call-stack.png)

- # What are the Web APIs? (web-apis.png)

- # These are flows to which we do not have direct access, we can only perform calls to them. They are built into the browser, where asynchronous actions are performed

- # So, what is the event loop itself? Let's take a look at the following down

- (event-loop.png)

- # The Event Loop solves one main problem: it monitors the Call Stack and the Callback Queue.

- If the call stack is empty, the loop takes the first event from the queue and puts it on the stack, which causes this event to be executed.

- This iteration is called the tick of the Event Loop. Each event is just a Callback.

- # Consider the following example

- (code)

- # Let's take a step-by-step “execution” of this code and see what happens in the system

- # Nothing is happening yet - the browser console is clean, the Call Stack is empty (loop-01.png)

- # The console.log('Hi') command is added to the Call Stack (loop-02.png)

- # The console.log('Hi') command is executed (loop-03.png)

- # The console.log('Hi') command is removed from the Call Stack (loop-04.png)

- # The setTimeout (function cb1 () {...}) command is added to the Call Stack (loop-05.png)

- # The setTimeout (function cb1 () {...}) command is executed. The browser creates a timer that is part of the Web API. He will do the countdown (loop-06.png)

- # The setTimeout (function cb1 () {...}) command has completed and is removed from the Call Stack (loop-07.png)

- # The console.log('Bye') command is added to the Call Stack (loop-08.png)

- # The console.log('Bye') command is executed (loop-09.png)

- # The console.log('Bye') command is removed from the Call Stack (loop-10.png)

- # After at least 5000 ms have passed, the timer exits and puts the cb1 callback in the Callback Queue (loop-11.png)

- # The Event Loop takes c the cb1 function from the Callback Queue and places it on the Call Stack (loop-12.png)

- # The cb1 function is executed and adds console.log('cb1') to the Call Stack (loop-13.png)

- # The console.log('cb1') command is executed (loop-14.png)

- # The console.log('cb1') command is removed from the Call Stack (loop-15.png)

- # Cb1 function is removed from the Call Stack (loop-16.png)

- # For consolidate knowledge - animated form of Event Loop (loop-full.png)

to consolidate knowledge Event Loop of the code in an animated form

- It is interesting to note that the ES6 specification defines how the event loop should work, namely, it indicates that technically it is within the responsibility of the JS engine, which begins to play a more important role in the JS ecosystem. The main reason for this is because promises have appeared in ES6 and they need a reliable mechanism for scheduling operations in the Event Loop queue.

- # Thank you for your attention
