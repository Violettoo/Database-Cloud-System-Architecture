# Exercise-7: Advanced NoSQL Query Operators 

Question 1: The $inc vs. $set Paradigm 

Why is it architecturally safer to use $inc natively in the database instead of a "Read-Modify-Write" loop in JavaScript?

  i) Prevents Race Conditions (Atomicity): When you use a native operator like $inc, MongoDB locks the document and updates the number instantly on the database side. If multiple IoT devices or users send messages at the exact same millisecond, MongoDB queues them up and increments them perfectly.
  
  ii) The Risk of JavaScript Updates: If you pulled the number into Node-RED first, added 1 via JavaScript code, and used $set to write it back, it wouldn't be safe under heavy traffic. If two messages arrive at the same time, both might read a count of 100, both will calculate 101 in Node-RED, and both will save 101 back to the       database. One full transmission count would be completely lost. Native $inc guarantees that never happens.

Question 2: Efficient Payload Management   

Describe how utilizing native database array operators ($addToSet, $pull) significantly reduces network bandwidth compared to rewriting the entire array.   

  i) Delta-Only Updates: Using native array operators means Node-RED only sends a tiny, lightweight "instruction" across your network (e.g., {"$push": {"sensors attached": "light_level"}}). This tiny instruction packet remains the exact same size whether your array holds 3 items or 10,000 items.
  
  ii) Eliminates High Round-Trip Overhead: Without native operators, you would have to download the entire array from MongoDB into Node-RED's memory (wasting downstream bandwidth), update it, and send the entire massive array back up to MongoDB (wasting upstream bandwidth). Over thousands of smart campus sensors sending updates every second, using native operators slashes your network overhead, saves RAM, and prevents your gateway from lagging.
