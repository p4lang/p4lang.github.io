---
layout: post
title: 2nd P4 Workshop in Europe (EuroP4)
date: 2019-09-23
header-img: assets/p4-background.png
---

### A presentation by the P4 Language Consortium and ONF in conjunction with ANCS 2019 
    
#### Held at Cambridge, UK on September 23, 2019

EuroP4 2019 is the second P4 Language Consortium event in Europe.  
It aims to bring together P4 and P4->NetFPGA researchers from Europe and from around the world, and to foster the growth of the P4 Community.

EuroP4, which will run as a workshop at ANCS 2019, will have proceedings. It aims to enable researchers to publish early stage work and small scale projects and seeks three types of contributions:
* Papers  - up to 6 pages long (references included).
* Posters - up to 2 pages long (references included).
* Demos  - up to 2 pages long (references included).

Topics of an interest include, but are not limited to:
* All aspects of P4-based network protocol research including design, specification, verification, implementation, measurement, testing, and analysis.
* Contributions to network architecture using P4, e.g., specific algorithms and protocols for network virtualization or future Internet architectures.
* New applications and in-network computing enabled by P4
* P4-based and P4-NetFPGA based programmable data planes
* End-host networking with P4
* Tools and frameworks for development using P4
* Performance analysis and measurement of P4-based designs and systems
* Contributions to the evolution of the P4 language

### Venue

University of Cambridge  
Department of Computer Science and Technology  
The Computer Laboratory  
William Gates Building  
15 JJ Thomson Avenue, Cambridge CB3 0FD

[Maps and directions](https://www.cl.cam.ac.uk/maps/)

#### Registration
[Registration is through ANCS 2019](http://www.ancsconf.org/)

#### Travel Grants
[Refer to ANCS travel grants page](http://www.ancsconf.org/)

#### Camera Ready
Information available soon!


### Agenda

---

* __8:30 - 9:15am__

    * Registration and Breakfast

---

* __9:15 - 9:30__

    * _Welcome and Introductions_

---    

* __9:30 - 10:30__

    * _Keynote_: Undefined behaviours in P4 progams: find them, fix them or exploit them.

      Speaker: [Professor Costin Raiciu](http://nets.cs.pub.ro/~costin/) (University Politehnica of Bucharest)

      <details>
        <summary>
        Abstract
        </summary>
	P4 programs can exhibit a series of undefined behaviours including inexistent 
	header accesses, infinite loops, parser errors, and so forth, much like C programs 
	can include use-after-free errors, out-of-bounds accesses and so forth. Such bugs 
	were found in most programs examined, be they small or large. A part of my talk 
	will discuss what might happen if buggy programs are deployed in practice by 
	examining how different P4 targets behave when undefined behaviours are present 
	in P4 programs, finding that a range of exploits are possible whose severity 
	depends on the target.
	Luckily, P4 is not Turing-complete and automated approaches at finding such bugs 
	have been proposed and are quite promising. Works such as p4v, Vera or p4-assert 
	can find all bugs before deployment as long as the programmer can provide table 
	rules that will appear in practice or provide a control plane invariant which 
	are predicates that table rules will obbey at runtime. Still, these tools place a 
	significant verification burden on the programmer, and it the jury is still out 
	on whether they will be used in practice.
	In the remainder of my talk I will cover existing approaches to find bugs in P4 
	programs, as well as presenting new work towards elliminating the need for programmer 
	input in the verification process. 
      </details>

      <details>
        <summary>
        Biography
        </summary>
	Costin Raiciu is Associate Professor at University Politehnica of Bucharest where 
	he leads the Netsys group. Costin finished his PhD at UCL in 2011. His current 
	research focus is on network verification. In his past work, Costin was one of the 
	main people behind the development, implementation and standardization of Multipath 
	TCP, a protocol that is now deployed by Apple and Samsung on their mobile devices. 
	Recently, Costin worked on NDP, which is a radical redesign of the datacenter networking 
	stack (ACM SIGCOMM 2017).     
      </details>

----

* __10:30 - 11:00__

    * _Coffee break_

----

* __11:00 - 12:15__

    * _Offloading data plane functions to the multi-tenant Cloud Infrastructure using P4._
Tomasz Osinski (Orange Labs & Warsaw University of Technology), Mateusz Kossakowski (Orange Labs & Warsaw University of Technology), Halina Tarasiuk (Warsaw University of Technology), Roland Picard (Orange Labs)

    * _P4DNS: In-Network DNS._
Jackson Woodruff (University of Cambridge), Murali Ramanujam (University of Cambridge), Noa Zilberman (University of Cambridge)

    * _Cryptographic Hashing in P4 Data Planes._
Dominik Scholz (Technical University of Munich), Andreas Oeldemann (Technical University of Munich), Fabien Geyer (Technical University of Munich), Sebastian Gallenm&uuml;ller (Technical University of Munich), Henning Stubbe (Technical University of Munich), Thomas Wild (Technical University of Munich), Andreas Herkersdorf (Technical University of Munich), Georg Carle (Technical University of Munich)


----

* __12:15 - 13:45__

    * _Lunch break_

----

* __13:45 - 15:00__

    * _daPIPE - A Data Plane Incremental Programming Environment._
Mario Baldi (Cisco Systems and Politecnico di Torino)

    * _Random Linear Network Coding on Programmable Switches._
Diogo Gon&ccedil;alves (University of Lisbon), Salvatore Signorello (University of Lisbon), Fernando M.V. Ramos (University of Lisbon), Muriel Medard (MIT)

    * _Towards Understanding the Performance of P4 Programmable Hardware._
Hasanin Harkous (Technical University of Munich/ Nokia Bell Labs), Michael Jarschel (Nokia Bell Labs), Mu He (Technical University of Munich), Rastin Pries (Nokia Bell Labs), Wolfgang Kellerer (Technical University of Munich)

----

* __15:00 - 15:15__

    * _Posters and Demos introduction and pitch_

----

* __15:15 - 16:15__

    * _Coffee break with Posters and Demos_

----

* __16:15 - 17:15__ (No Proceedings Track)

    * _Towards Neural Network Inference on Programmable Switches._
Jonatan Langlet (Karlstad University), Andreas Kassler (Karlstad University), Deval Bhamare (Karlstad University)

    * _In-Network Traffic Redundancy Elimination over Programmable Data Plane._
Hongrok Choi (Korea University), Seokwon Jang (Korea University), Sangheon Pack (Korea University)

    * _An Analysis Framework for Programmable Networks._
Doganalp Ergenc (University of Hamburg), G&ouml;ksel Simsek (METU), Ertan Onur (METU)

    * _Estimation of logarithmic and exponential functions entirely in P4-programmable data planes._
Damu Ding (FBK CREATE-NET research center), Marco Savi (FBK CREATE-NET research center), Domenico Siracusa (FBK CREATE-NET research center)

    * _Resource-Efficient Service Function Chaining in Programmable Data Plane._
Hochan Lee (Korea University), Jaewook Lee (Korea University), Haneul Ko (Korea University), Sangheon Pack (Korea University)

    * _How NRENs can benefit from P4._
Mauro Campanella (GARR), Pavel Benacek (CESNET), Ivana Golub (PSNC), Xavier Jeannin (RENATER), Damian Parniewicz (PSNC), Marco Savi (FBK), Frederic Loui (RENATER)

----

* __17:15 - 17:30__

    * _Closing_

----

* __18:00 onwards__

    * _Social Event_
This event will be held in conjuction with the IEEE ANCS reception. Check [ANCS 2019](http://www.ancsconf.org/) website for more information.


### Accepted Posters

* *P4MT: Multi-Tenant Support Prototype for International P4 Testbed.* Jim Hao Chen (iCAIR/Northwestern University), Buck Chung (National Chiao Tung University), Chien-Chao Tseng (National Chiao Tung University), Joe Mambretti (iCAIR/Northwestern University)

* *Sketch-based Entropy Estimation for Network Traffic Analysis using Programmable Data Plane ASICs.*  Yu-Kuen Lai (Chung-Yuan Christian University), Ku-Yeh Shih (Chung-Yuan Christian University), Po-Yu Huang (Chung-Yuan Christian University), Ho-Ping Lee (Chung-Yuan Christian University), Yu-Jau Lin (Chung-Yuan Christian University), Te-Lung Liu (Narlabs), Jim Chen (Northwestern University)

* *Graph-to-P4: A P4 boilerplate code generator for parse graphs.* Eder Ollora Zaballa (Technical University of Denmark), Zifan Zhou (Technical University of Denmark)

* *Asynchronous Extern Functions in Programmable Software Data Planes.* Daniel Horpacsi (ELTE E&ouml;tv&ouml;s Lor&aacute;nd University, Budapest, Hungary), Sandor Laki (ELTE E&ouml;tv&ouml;s Lor&aacute;nd University, Budapest, Hungary), Peter Voros (ELTE E&ouml;tv&ouml;s Lor&aacute;nd University, Budapest, Hungary), Mate Tejfel (ELTE E&ouml;tv&ouml;s Lor&aacute;nd University, Budapest, Hungary), Gergely Pongracz (Ericsson Research), Laszlo Molnar (Ericsson Research) 


### Accepted Demos

* *P4-NetFPGA-based network slicing solution for 5G MEC architectures.* Ruben Ricart-Sanchez (University of the West of Scotland), Pedro Malagon (Universidad Politecnica de Madrid), Jose M. Alcaraz-Calero (University of the West of Scotland), Qi Wang (University of the West of Scotland)

* *Using P4 on Fixed-Pipeline and Programmable Stratum Switches.* Brian O'Connor (ONF), Yi Tseng (ONF), Maximilian Pudelko (ONF), Alireza Ghaffarkhah (Google), Devjit Gopalpur (Google)

* *How to measure the speed of light with programmable data plane hardware?.* Ralf Kundel (TU Darmstadt), Fridolin Siegmund (TU Darmstadt), Boris Koldehofe (TU Darmstadt)



### General Chairs
* [Noa Zilberman](https://www.cl.cam.ac.uk/~nz247/), Univeristy of Cambridge
* [Robert Soulé](http://www.cs.yale.edu/homes/soule/), Yale University

### Program Chairs
* [Gianni Antichi](https://gianniantichi.github.io/), Queen Mary University of London
* [Fernando Ramos](http://fvramos.at.di.fc.ul.pt/), University of Lisbon

### Web Chair
* [Salvatore Signorello](https://wwwfr.uni.lu/snt/people/salvatore_signorello), University of Lisbon

### Technical Program Committee

* [Gordon Brebner](https://sites.google.com/site/gordonbrebner/Home), Xilinx
* [Paolo Costa](https://www.microsoft.com/en-us/research/people/pcosta/), Microsoft Research
* [Jon Crowcroft](https://www.cl.cam.ac.uk/~jac22/), University of Cambridge
* [Ben Pfaff](https://benpfaff.org), VMware
* Georgios Nikolaidis, Barefoot Networks
* [Marco Chiesa](https://marchiesa.bitbucket.io/), KTH
* [Gabor Retvari](http://lendulet.tmit.bme.hu/~retvari/), University of Budapest
* [Roberto Bifulco](http://robertobifulco.it/), NEC
* [Ran Ben Basat](http://www.bbasat.com/), Harvard University
* [Andreas Kassler](https://www.kau.se/forskare/andreas-kassler), Karlstads University
* [Mario Baldi](http://staff.polito.it/mario.baldi/), Cisco and Polytechnic of Turin
* [Christian Rothenberg](http://www.dca.fee.unicamp.br/~chesteve/), University of Campinas
* [Muhammad Shahbaz](https://mshahbaz.github.io/), Stanford University
* [Aurojit Panda](https://cs.nyu.edu/~apanda/), New York University
* Marcin Wojicik, University of Cambridge

### Special Thanks to our Sponsors:

<table>
<tr>
<td align="center"></td>
<td><img src="/assets/Stordis_logo_flat_grey+slogan.png" width="300" alt="Stordis" /></td>
<td><img src="/assets/delta_logo.png" width="300" alt="Delta" /></td>
</tr>
<tr>
<td align="center"></td>
<td><img src="/assets/FCT_logo.png" width="300" alt="FCT" /></td>
<td><img src="/assets/Lasige_Logo.jpg" width="300" alt="Lasige" /></td>
</tr>
</table>


