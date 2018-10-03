---
layout: post
title: 1st P4 European Workshop (P4EW)
date: 2018-09-24
header-img: assets/p4-background.png
---

### A presentation by the P4 Language Consortium and ONF in conjunction with ICNP 2018 
    
#### Held at Cambridge, UK on September 24, 2018

P4EW 2018 is the first P4 Language Consortium event in European. It aims to bring together P4 and P4->NetFPGA researchers from Europe and from around the world, and to foster the growth of the P4 Community.

P4EW, which will run as a workshop at ICNP 2018, will have proceedings. It aims to enable researchers to publish early stage work and small scale projects.

### Venue

University of Cambridge  
Department of Computer Science and Technology  
The Computer Laboratory  
William Gates Building  
15 JJ Thomson Avenue, Cambridge CB3 0FD

[Maps and directions](https://www.cl.cam.ac.uk/maps/)


#### Registration
[Registration is through ICNP 2018](http://icnp18.cs.ucr.edu/registration.html) 


### Agenda

---

* __8:30 - 9:00am__

    * Registration and Breakfast

---

* __9:00 - 9:15__
    
    * _Welcome and Introductions_

---    
    
* __9:15 - 10:15__

    * _Keynote_: Extending the range of P4 programmability (<a href="{{ site.baseurl }}/assets/P4EW_2018/Gordon_Brebner.pdf">slides</a>)    

      Speaker: [Professor Gordon Brebner](https://sites.google.com/site/gordonbrebner/Home) (Xilinx Labs)

      <details>
        <summary>
        Abstract
        </summary>
	In four years, P4 has evolved from being a paper proposal to being a
	packet processing programming language with increasing adoption
	worldwide, overseen by the P4 Language Consortium (P4.org).  The talk
	will first overview developments over this period, which have brought
	the community to the current P4_16 language specification, the PSA
	(Portable Switch Architecture) specification, and the P4Runtime API
	specification.  It will then discuss some current community efforts to
	extend the reach of P4.  One of the key developments in 2017 was
	language-architecture separation, leading to the P4_16 (language) and
	PSA (architecture) threads.  In practice, NICs (Network Interface
	Cards, notably Smart NICs) are a common target, so one community goal
	is to define a PNA (portable NIC architecture) specification, to
	complement the existing PSA specification.  Then, a bigger picture is
	to extend P4 to allow the description of architectures, which is the
	goal of the Programmable Target Architecture (PTA) research project of
	Stanford and Xilinx Labs.  The talk will describe this project, and a
	current prototype that compiles extended P4 descriptions to FPGA-based
	hardware implementations.  An important test case for the new approach
	will be the expression of both PSA and PNA (when ultimately defined)
	in the extended “P4 +” rather than in English as currently.
	Currently, P4 is focused on packet processing – through parsing,
	match-action pipelines, and deparsing.  Another current research
	project, involving MIT, NYU, Stanford, and Xilinx Labs, concerns
	extending P4 (language and architecture) to cover Traffic Management –
	providing programmable scheduling, shaping, policing, queueing, etc.
	The talk will overview this project, and a current prototype based on
	the PIFO scheduling model that was presented at SIGCOMM 2016.
	Finally, the talk will consider future evolution of the open source
	community around P4, including the development of comprehensive
	reference examples for both switch and NIC architectures, for both
	software and programmable hardware implementations.
      </details>

      <details>
        <summary>
        Biography
        </summary>
	Gordon Brebner is a Distinguished Engineer at Xilinx, Inc., the
	technology leader in highly flexible and adaptive processing
	platforms.  He works in Xilinx Labs, leading an international group
	researching issues surrounding networked and trusted processing
	systems of the future. His main personal research interests concern
	dynamically reconfigurable architectures, domain-specific languages
	with highly concurrent implementations, and high performance
	networking and telecommunications.  His group’s research led to the
	Xilinx SDNet product for P4-programmable networking at scalable 1G
	to 1T rates.  He holds around 40 patents, and has published around
	60 papers, in the general area of networking with FPGAs.  Prior to
	joining Xilinx in 2002, he was the Professor of Computer Systems and
	Head of the Department of Computer Science at the University of
	Edinburgh, and remains an Honorary Professor of Informatics there.
	He is an active contributor to the P4 language Consortium (P4.org),
	including co-chairing the P4 Language Design working group from its
	inception.  He received the inaugural P4.org Distinguished Service
	Award in 2018.
      </details>

----

* __10:15 - 10:45__

    * _Coffee break_

----

* __10:45 - 12:15__

    * _Named Data Networks using Programmable Switches._
Rui Muigel (University of Lisbon), Salvatore Signorello (University of Luxembourg), Fernando M. V. Ramos (University of Lisbon)

    * _Consensus for Non-Volatile Main Memory._
Huynh Tu Dang (Universit&agrave; della Svizzera italiana), Jaco Hofmann (TU Darmstadt), Yang Liu (Western Digital Research), Marjan Radi (Western Digital Research), Dejan Vucinic (Western Digital Research), Fernando Pedone (Universit&agrave; della Svizzera italiana), Robert Soul&eacute; (Universit&agrave; della Svizzera italiana) (<a href="{{ site.baseurl }}/assets/P4EW_2018/Robert_Soule.pdf">slides</a>)    

    * _Transparent Edge Gateway for Mobile Networks._
Ashkan Aghdai (NYU), Mark Huang (Huawei), David H. Dai (Huawei), Yang Xu (NYU), H. Jonathan Chao (NYU)


----

* __12:15 - 13:30__

    * _Lunch break_

----


* __13:30 - 14:40__

    * _Panel: P4 Education_

----

* __14:40 - 15:20__

    * _Lightning talks_

----

* __15:20 - 16:15__

    * _Coffee break and Posters_

----

* __16:15 - 17:30__

    * _Stateless Load-Aware Load Balancing in P4._
Benoit Pit--Claudel (Cisco Systems, &Eacute;cole Polytechnique), Yoann Desmouceaux Cisco Systems, &Eacute;cole Polytechnique), Pierre Pfister (Cisco Systems), Marc Townsley (Cisco Systems) (<a href="{{ site.baseurl }}/assets/P4EW_2018/Yoann_Desmouceaux.pdf">slides</a>)    

    * _P4LLVM: An LLVM based P4 Compiler._
Dangeti Tharun Kumar, S Venkata	Keerthy, Ramakrishna Upadrasta (IIT Hyderabad)

    * _pcube: Primitives for network data plane programming._
Rinku Shah, Aniket Shirke, Akash Trehan, Mythili Vutukuru, Purushottam Kulkarni (IIT Bombay)

----

* __17:30 - 17:45__

    * _Closing_

----





### Accepted Posters


* *Network Coding for Critical Infrastructure Networks.* Rakesh Kumar, Vignesh Babu, David M. Nicol (University of Illinois, Urbana-Champaign) 

* *ARP-P4: A hybrid ARP-Path/P4Runtime switch.*  Isaias Martinez-Yelmo, Joaquin Alvarez-Horcajo, Miguel Briso-Montiano, Diego Lopez-Pajares, Elisa Rojas (University of Alcal&aacute;) (<a href="{{ site.baseurl }}/assets/P4EW_2018/Joaquin_Horcajo.pdf">slides</a>)    

* *One for All, All for One: A Heterogeneous Data Plane for Flexible P4 Processing.* Jeferson Santiago da Silva, Thibaut Stimpfling, Thomas Luinaud, Bachir Fradj (Polytechnique Montréal), Bochra Boughzala (Kaloom Inc.) (<a href="{{ site.baseurl }}/assets/P4EW_2018/Jeferson_Santiago.pdf">slides</a>)    

* *Using P4 and Source Based Routing To Enable Performant Intents in Software Defined Networks.* Benjamin Lewis, Lyndon Fawcett, Dr. Matthew Broadbent, Prof. Nicholas Race (Lancaster University)

* *Verification of Generated RTL from P4 Source Code.* Radek I&scaron;a, Pavel Ben&aacute;ček (CESNET a.l.e.), Viktor Pu&scaron; (Netcope Technologies)

* *A P4-Based PON Architecture for 5G.* Adebanjo Haastrup, David Rincon, Sallent Sebastia, J. Ramon Piney (Universitat Polit&egrave;cnica de Catalunya)

* *Implementation of Sketch-based Entropy Estimation for Network Traffic Analysis Using P4.* Ku-Yeh Shih, Yu-Kuen Lai, Theophilus Wellem, Ho-Ping Lee, Po-Yu Huang, Yu-Jau Lin (Chung Yuan Christian University)

* *The P4->NetFPGA Workflow, and Experience Report from the Stanford CS344 Class.* Stephen Ibanez, Nick McKeown (Stanford University), Gordon Brebner (Xilinx Labs)

### Accepted Demos

* *Hardware-Accelerated Firewall for 5G Mobile Networks.*
Ruben Ricart-Sanchez (University of the West of Scotland), Pedro Malagon (Universidad Politecnica de Madrid), Jose M. Alcaraz-Calero (University of the West of Scotland), Qi Wang (University of the West of Scotland) 

* *Switch ASIC Programmability in Hybrid Mode.*
Matty Kadosh, Alan Lo, Yonatan Piasetzky, Omer Shabtai, Marian Pritsak (Mellanox Technologies), Guohan Lu (Microsoft)

* *RAYMAX P4-Enabled SmartNIC: Providing Service-Driven Data Center Networking.*
Yan Yan, Shen Tan (Raymax Technology), Reza Nejabati, Dimitra Simeonidou (University of Bristol)

* *VNF offloading on a multi-vendor P4 fabric controlled by ONOS via P4Runtime.*
Andrea Campanella, Carmelo Cascone (Open Networking Foundation) 

* *Network-assisted sorting.*
Petar Penkov, Hristo Stoyanov (Stanford University)

#### Registration
[Registration is through ICNP 2018](http://icnp18.cs.ucr.edu/registration.html) 

#### Travel Grants
[Refer to ICNP travel grants page](http://icnp18.cs.ucr.edu/grants.html)


### Technical Program Committee

* Noa Zilberman (chair), University of Cambridge
* Robert Soul&eacute; (chair), Universit&agrave; della Svizzera italiana
* Gianni Antichi, University of Cambridge
* Mario Baldi, Cisco
* Gordon Brebner, Xilinx Labs
* Paolo Costa, Microsoft Research
* Andy Fingerhut, Cisco Systems
* Nate Foster, Cornell University
* Timothy Griffin, University of Cambridge
* Mukesh Hira, VMWare
* Masoud Moshref, Barefoot Networks
* Fernando Ramos, University of Lisbon
* Christian Esteve Rothenberg, University of Campinas 


### Special Thanks to our Sponsors:


<table>
<tr>
<td align="center"><h3>Gold Level:</h3></td>
<td><img src="/assets/WestDigi_Logo_1L_RGB_B.png" width="300" alt="Western Digital" /></td>
<td><img src="/assets/exilinx-logo.png" width="300" alt="Xilinx" /></td>
</tr>
<tr>
<td align="center"><h3>Silver Level:</h3></td>
<td><img src="/assets/barefoot-logo.png" width="300" alt="Barefoot Networks" /></td>
</tr>
<tr>
<td align="center"><h3>Bronze Level:</h3></td>
<td><img src="/assets/Microsoft-logo_rgb_c-gray.png" width="300" alt="Microsoft" /></td>
<td><img src="/assets/stordis-slogan.png" width="300" alt="Stordis" /></td>
</tr>

</table>

Contact the workshop chairs for sponsorship opportunities. 


