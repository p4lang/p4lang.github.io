---
layout: post
title: P4 Developer Day
date: 2018-06-06
header-img: assets/p4-background.png
---
        
### A presentation by the P4 Language Consortium
    
#### Held at Stanford University on Wednesday, June 6, 2018 

### [Register Here!](https://www.eventbrite.com/e/p4-developer-day-2018-tickets-44765855880)

#### Special Thanks to our Sponsors:
<img src="/assets/att-logo.png" alt="AT&T" /> <img src="/assets/barefoot-logo.png" alt="Barefoot Networks" /> <img src="/assets/cisco-logo.png" alt="Cisco" /> <img src="/assets/Google-logo-p4-final2.png" alt="Google" /> 

### Slack

We will use Slack to make it easy for participants to ask the TAs questions.  
* Register at [bit.ly/join-p4-lang-slack](https://bit.ly/join-p4-lang-slack)
* Join the `#d2` channel
    
### Agenda 

---

* 8:00 - 8:30am

    * Registration and Breakfast

---

* 8:30 - 9:00am
    
    * Technical Set-up for Hands-on Lab

      In order to complete the Developer Day exercises, we will
      distribute a virtual machine with all required software
      installed.

---

* 9:00 - 9:10am
    
    * Welcome and Introductions

---    
    
* 9:10 - 10:30am
    
    * Introduction to Data Plane Programming

    * Language Basics
    
      Session 1 will provide a hand-on introduction to P4. Students
      will start by implementing a "Hello World"-style application to
      gain an understanding of P4 concepts. The lesson will
      progressively introduce core language features, such as
      header/metadata types, packet parsers, and controls. By the end
      of this session, students will be able to implement a basic IP
      router.

----

* 10:30 - 11:00am
    
    * _Break_

---
    
* 11:00 - 12:00
    
    * P4 Runtime
    
      Session 2 will cover software tools that are essential to
      developing P4 applications. Students will learn how to invoke
      the the P4 compiler, run the debugger, and start a P4 software
      switch. This session will also introduce the control-plane
      interfaces via P4 Runtime, a protocol-independent API
      auto-generated from the definition of a packet processing
      pipeline written in P4.
    
---
       
* 12:00 - 1:30pm

    * _Lunch_

---
* 1:30 - 2:00pm
    
    * Keynote: TBA

--
        
* 2:00-3:00
    
    * Monitoring and Debugging
    
      Session 3 will focus on a set of labs related to network
      monitoring and debugging. In this session, students will gain a
      deeper understanding of P4 language concepts, including custom
      headers and intrinsic metadata. In the first exercise, students
      will implement Explicit Congestion Notification (ECN) to set a
      congestion bit in a packet header when the queue depth exceeds a
      threshold. In the second exercise, MRI, students will implement
      a simplified version of In-Band Network Telemetry to track the
      path that packets travel through the network.

---

* 3:00 - 3:30pm
    
    * _Break_

---
    
* 3:30 - 4:30pm
    
    * Advanced Data Structures

      Session 4 covers advanced data structures. In this session,
      students will implement two data-plane applications. In the
      first, source routing, end-hosts specify paths through the
      network by using a stack of labels in the packet header. The
      switch must “pop” each label and forward out the appropriate
      interface. In the second, students will implement a network
      calculator. Packets containing arithmetic expressions are sent
      to a switch. The switch will evaluate the expressions, and
      return the results back to the sender.

* 4:30-5:30
    
    * Panel Discussion: TBA

---

* 5:30-6:30

    * Reception
    
