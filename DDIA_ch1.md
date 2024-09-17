# DDIA chapter 01 : Reliable Scalable And Maintainable Application

## Intro

- Modern applications are limited by Data, not by Computing power anymore. 
    - Data-intensive vs. Compute-intensive
- Example of 'common patterns of data usage'
```
1. Store data so that they, or another application, can find it again later (databases)
2. Remember the result of an expensive operation, to speed up reads (caches)
3. Allow users to search data by keyword or filter it in various ways (search indexes)
4. Send a message to another process, to be handled asynchronously (stream processing)
5. Periodically crunch a large amount of accumulated data (batch processing)
```
------
> Why should we lump them all together under an umbrella term like data systems? (even though they are quite different?)
- In system design interviews, many data systems are lumped as **database** (SQL/NoSQL/Kafka). 



## Three concerns that are important in most applications:
- **Reliability**: The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or software faults, and even human error)
- **Scalability**: As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth.
- **Maintainability** : Over time, many different people will work on the system (engineering and operations, both maintaining current behavior and adapting the system to new use cases), and they should all be able to work on it productively.

## Reliability
> "내가 실수해도 넌 잘못 작동하면 안 돼"
- Fault tolerable (to certain types), or, resilient
- Fault != Failure
    - Fault ~= partial failure 
- Fire drill : Chaos monkey
    - Amazon gameday 
    - Google DiRT : https://cloud.google.com/blog/products/management-tools/shrinking-the-time-to-mitigate-production-incidents?hl=en
    - Chaos toolkit : https://chaostoolkit.org/
- **Hardware faults**
- **Software Errors**
- **Human Errors**

## Scalability
> Cool our application is super-reliable but what happens if the traffic spikes 10x? 

- **Load Description**
    - Load parameters used to describe load include requests per second to a web server, read/write ratio in a database, number of simultaneously active users, and cache hit rate.
    - Be careful not to fall into statistical traps. 
        - For example, in some cases, the average may not be important at all. 
        - Extreme cases could be the cause of bottlenecks.
    - Twitter fan-in / fan-out
        - Lesson learnt : Simple model fits to most users, fan-out is good for hotspot users (or celebrities)
        This goes against the desires of many developers: It's not simple, but it's the (only) working solution. 
- **Performance description**

    - What happens to system performance when you increase load parameters while keeping system resources (CPU, memory, network bandwidth, etc.) unchanged?
    - How much do you need to increase resources to maintain performance when load parameters are increased?
    - The issues of throughput and response time are also valid here.
    - For batch processing systems, throughput is important when load increases, while for online systems, service response time is crucial.
