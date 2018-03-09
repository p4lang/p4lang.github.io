---
layout: post
title: East Coast P4 Developer Day, Spring 2018
date: 2018-03-09
header-img: assets/p4-background.png
---
        
### A presentation by the P4 Language Consortium
    
### Held at Cornell Tech on Friday, March 9, 2018 

### [Registration](https://www.eventbrite.com/e/east-coast-p4-developer-day-spring-2018-tickets-42621110890)
    
### Directions

#### Address: 2 West Loop Road, New York, NY
        
<iframe src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3022.2519232660593!2d-73.95805328469173!3d40.756483542830026!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x89c258de874a2063%3A0xf4ce5ba912eb3aaf!2s2+W+Loop+Rd%2C+New+York%2C+NY+10044!5e0!3m2!1sen!2sus!4v1520528056130" width="800" height="250" frameborder="0" style="border:0" allowfullscreen></iframe>

#### Transportation Options    

* The [Subway](http://web.mta.info/maps/submap.html) is the easiest,
  fastest, and cheapest way to get to Roosevelt Island.    
    * Take the F train​ to the “Roosevelt Island”​ stop.
    * Single ride tickets are $3.00.
* The [Tram](https://rioc.ny.gov/tramtransportation.htm) is a fun way
  to travel to Roosevelt Island from Manhattan.    
    * Take the Tramway Car at 59th Street & Second Avenue Station
      (travel time is 4-5 minutes). Exit at the Tramway Station on
      Roosevelt Island.
    * Single ride tickets are $3.00.
* The [Astoria](https://www.ferry.nyc/routes-and-schedules/route/astoria/)
  route of the NYC Ferry offers another great transportation option. 
    * The route connects Roosevelt Island to Astoria, Long Island City, Midtown East, and Wall Street.
    * Current one-way fare is $2.75.   
* The [Red Bus](https://rioc.ny.gov/bustransportation.htm) operates in
  and around Roosevelt Island and is FREE to ride    
    * Click [here](https://rioc.ny.gov/bustransportation.htm) to view the Red Bus Schedule
* [Q102 MTA Bus](https://bustime.mta.info/m/?q=Q102) is another way to
  get around within the Island and travel from other boroughs.
* Driving is another way to and around the Roosevelt Island. You can
  find Parking at the [Motorgate
  Garage](https://rioc.ny.gov/parking.htm) located on 688 Main Street,
  Roosevelt Island.    
* The Island is only 2 miles in length, so walking​ is a great option for
  getting around.
            
#### Security
    
  After arriving on campus you will first need to proceed to the
  security desk to pick up your security badge for the day. You will
  need this badge with you at all times to navigate in & out of the
  building. After your badge is picked up, you will then proceed to
  the registration desk where you can get your P4 Developer Day badge.

### Virtual Machine

We have created a virtual machine that has all of the software needed to complete the developer day exercises already installed. You can either download a virtual machine image or build it from source. Note that both of these procedures can take around 45 minutes depending on the speed of your network connection.

* To download the virtual machine image
    1. Install VirtualBox  
       [https://virtualbox.org](https://virtualbox.org)
    1. Download virtual machine image  
       [P4 Tutorial 2018-03-05.ova](https://drive.google.com/open?id=1ACkpD66zoBJHCX2K50OO8-pssJGZhzMr)
    1. Import virtual machine into VirtualBox  
       Open VirtualBox, select "File > Import Appliance", and navigate to the downloaded file.
    1. Boot virtual machine  
       Select "P4 Tutorial 2018-03-05", and click "Start". 

* To build the virtual machine from source
    1. Install VirtualBox  
       [https://virtualbox.org](https://virtualbox.org)
    1. Install Vagrant  
       [https://vagrantup.com](https://vagrantup.com)
    1. Clone the tutorial repository  
       `$ git clone https://github.com/p4lang/tutorials`
    1. Navigate to the vm directory  
      `$ cd tutorials/P4D2_2018_East/vm/`
    1. Build the virtual machine  
      `$ vagrant up`
    
* Final steps  
  After the machine boots, you should have a graphical desktop with
  all required software pre-installed, logged in as username "p4"
  (with password "p4"). You may want to install the VirtualBox Guest
  Additions to optimize the graphics and clipboard interaction with
  your host OS. See the [VirtualBox
  manual](https://www.virtualbox.org/manual/ch04.html) for more
  details.

### Slack

We have set up a Slack to make it easy for participants to ask the TAs questions.  
* Register at [bit.ly/join-p4-lang-slack](https://bit.ly/join-p4-lang-slack)
* Join the `#east-coast-d2` channel
    
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
    
    * [Welcome and Introductions](/assets/P4_D2_East_2018_00_welcome.pdf)

      Speaker: [Nate Foster](http://www.cs.cornell.edu/~jnfoster) (Cornell University)

---    
    
* 9:10 - 10:45am
    
    * Introduction to Data Plane Programming

      Instructor: [Stephen Ibanez](https://web.stanford.edu/~sibanez) (Stanford University)
    
    * [Language Basics](/assets/P4_D2_East_2018_01_basics.pdf)

      Instructor: [Stephen Ibanez](https://web.stanford.edu/~sibanez) (Stanford University)
    
      Session 1 will provide a hand-on introduction to P4. Students
      will start by implementing a "Hello World"-style application to
      gain an understanding of P4 concepts. The lesson will
      progressively introduce core language features, such as
      header/metadata types, packet parsers, and controls. By the end
      of this session, students will be able to implement a basic IP
      router.

----

* 10:45 - 11:15am
    
    * _Break_

---
    
* 11:15 - 11:50
    
    * [Software Tools](/assets/P4_D2_East_2018_02_p4runtime.pdf)

      Instructor: [Praveen Kumar](http://www.cs.cornell.edu/~praveenk) (Cornell University)
    
      Session 2 will cover software tools that are essential to
      developing P4 applications. Students will learn how to invoke
      the the P4 compiler, run the debugger, and start a P4 software
      switch. This session will also introduce the control-plane
      interfaces via P4 Runtime, a protocol-independent API
      auto-generated from the definition of a packet processing
      pipeline written in P4.
    
---
       
* 12:10 - 1:30pm

    * _Lunch_

---
    
* 1:30 - 3:00pm
    
    * [Monitoring and Debugging](/assets/P4_D2_East_2018_03_monitoring.pdf)


      Instructor: [Mina Tahmasbi Arashloo](http://www.cs.princeton.edu/~arashloo/) (Princeton University)
    
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

* 3:30 - 3:50

    * Keynote: [Towards Self-Driving Networks](/assets/P4_D2_East_2018_jrex_keynote.pdf)

      Speaker: [Jennifer Rexford](http://www.cs.princeton.edu/~jrex) (Princeton University)

---

    
* 3:50 - 5:00pm
    
    * Advanced Data Structures

      Instructor: [Sean Choi](https://stanford.edu/~yo2seol/) (Stanford University)
    
      Session 4 covers advanced data structures. In this session,
      students will implement two data-plane applications. In the
      first, source routing, end-hosts specify paths through the
      network by using a stack of labels in the packet header. The
      switch must “pop” each label and forward out the appropriate
      interface. In the second, students will implement a network
      calculator. Packets containing arithmetic expressions are sent
      to a switch. The switch will evaluate the expressions, and
      return the results back to the sender.

---

* 5:00 - 5:45
    
    * Panel Discussion

      Moderator: [Nate Foster](http://www.cs.cornell.edu/~jnfoster) (Cornell University)
    
      Panelists:
        * [Mina Tahmasbi Arashloo](http://www.cs.princeton.edu/~arashloo/) (Princeton University)
        * [Anthony Dalleggio](https://www.linkedin.com/in/anthonydalleggio/) (JP Morgan Chase & Co.)
        * [Sandesh Kumar Sodhi](https://www.linkedin.com/in/sandeshksodhi/) (Juniper Networks)

---
    
* 5:45-5:55
    
    * Closing Remarks

      Speaker: [Nate Foster](http://www.cs.cornell.edu/~jnfoster) (Cornell University)
    
---

* 6:00-7:30

    * Reception

      [Riverwalk Bar & Grille](http://www.riverwalkbarandgrill.com/) (425 Main St., Roosevelt Island)
    