# Event-driven Services 

NOTE (27 FEB 2019) - the dependencies model is not presently scheduled for implementation. We will keep the design information and re-evaluate the need at a future point in time.

Handling event-driven services creates a particular challenge for declarative application composition.  Consider the following
diagram: 

![event-driven-1](https://github.com/kappnav/design/blob/master/images/event-driven-1.png)

Line of business applications A, B, and C (LOBs A,B,C), consist of services S1 & S2, S3 & S4, and S5 & S6, respectively. 
Imagine all service-to-service flows are event streams.  The following table identifies assumed event streams used to communicate among services and the sources and sinks for each event stream: 

![event-driven-2](https://github.com/kappnav/design/blob/master/images/event-driven-2.png)

The difficulty with event driven services is that the event sender (source) does not necessarily know the event receiver (sink).  In order to avoid tight coupling we will invent a scheme to connect sources and sinks indirectly through event streams. 

To achieve this, we will use special labelling:  services that send an event (source) label themselves to define the stream to which they send events;  services that receive an event (sink) label themselves to define the stream from which they receive events: 

![event-driven-3](https://github.com/kappnav/design/blob/master/images/event-driven-3.png)

Applications are composed then, based on application label selectors and also on event stream matches.  Consider the following applications definitions: 

![event-driven-4](https://github.com/kappnav/design/blob/master/images/event-driven-4.png)

Consider also the following service definitions: 

![event-driven-5](https://github.com/kappnav/design/blob/master/images/event-driven-5.png)

Combining the label selectors on the applications plus matching up the event stream labels on the services, we'd have the following progression for LOB-A: 

1. label selector in LOB-A selects services s1 and s2
1. event stream label in service s1 (source) matches up with the event stream label in s3 (sink) and therefore selects service s3
1. event stream labels in service s3 (source) matche up with the event stream labels in s2, s4, and s6 (sinks) and therefore selects services s2, s4, and s6.  

The same progression would apply similarly to LOB B and LOB C. The resulting application view would look like this: 

![event-driven-6](https://github.com/kappnav/design/blob/master/images/event-driven-6.png)

If the progression stopped 1 level deep (i.e. no recursion) the view would look like this: 

![event-driven-7](https://github.com/kappnav/design/blob/master/images/event-driven-7.png)

In other words, perhaps the event stream label matching should stop at the application's immediate dependencies and not reveal indirect dependencies (i.e. service s3's dependency on service s6).  This could be controlled by a switch at the application level or at the level of each individual service. 
