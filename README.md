Abstract
 Intelligent Intersection Management (IIM) approaches aim to optimize urban traffic flow but face inherent limitations depending
 on their operational mode. Sequential approaches suffer from inefficiencies under high traffic demand, rigid cyclic operations, and
 poor scalability. Parallel approaches struggle with turning conflicts, unbalanced traffic flows, and strict lane discipline requirements.
 Synchronous approaches depend heavily on precise timing, reducing their flexibility. To address these challenges, we propose the
 Software-Defined Intelligent Intersections (SDI2) framework, an SDN-based IIM solution that intelligently orchestrates intersection
 managementthrough centralized control. The SDI2 framework dynamically switches between sequential, parallel, and synchronous
 modes based on real-time traffic patterns, effectively accommodating both individual vehicles and groups. This adaptive strategy
 optimizes traffic flow by reducing reaction times to green signals, minimizing unnecessary stopped delays by up to 89.5%, and
 significantly reducing energy waste by 63.3% and associated emissions by 76.9% compared to conventional approaches.
 ©2025 The Authors. Published by Elsevier B.V.
 This is an open access article under the CC BY-NC-ND license (http://creativecommons.org/licenses/by-nc-nd/4.0/)
 Peer review is the responsibility of the scientific committee of the 27th EWGT 2025..
 Keywords: Software-defined networking, adaptive intersection management, stopped delays, and fuel efficiency;
 1. Motivation
 Theincreasing disparity between limited physical road infrastructure and rapid vehicle growth has led to traffic con
gestion, environmental pollution, and economic and health issues (Afrin and Yodo, 2020; Reddy et al., 2024a; Samal et
 al., 2021). The global fleet of light-duty commercial and passenger vehicles is projected to grow from approximately
 1.31 billion in 2020 to 2.21 billion by 2050, further exacerbating these problems and demanding intelligent solu
tions. Intelligent Intersection Management (IIM) protocols, powered by advanced Information and Communication
 Technologies (ICT), autonomous vehicles (AVs), and software-defined networking (SDN) paradigms, offer promising
 approaches to addressing these challenges (Yang et al., 2020). These protocols can be broadly classified based on how
 vehicles access intersections: sequentially, parallelly, or synchronously (Reddy et al., 2024b).
 ∗ Corresponding author.
 E-mail address: radhakrishna.reddy@manipal.edu
 2352-1465 © 2025 The Authors. Published by Elsevier B.V.
 This is an open access article under the CC BY-NC-ND license (http://creativecommons.org/licenses/by-nc-nd/4.0/)
 Peer review is the responsibility of the scientific committee of the 27th EWGT 2025..
2
 Radha Reddy / Transportation Research Procedia 00 (2025) 000–000
 Sequential approaches allow vehicles on one road to proceed during a green phase before switching cyclically in a
 clockwise or counterclockwise direction. Parallel approaches enable vehicles from opposite road lanes to move simul
taneously before switching to the next pair of opposite lanes. Synchronous approaches coordinate vehicle movements
 by aligning arrival and departure times with traffic signals. Despite their advantages, these approaches have limita
tions (Reddy et al., 2024b). Sequential approaches, for instance, suffer from inefficiencies under high traffic demand,
 rigid cyclic operations, and poor scalability. Parallel approaches face challenges in managing turning conflicts, adapt
ing to unbalanced traffic flows, and requiring strict lane discipline. Synchronous approaches depend heavily on precise
 timing. These challenges highlight the necessity of hybrid models and adaptive systems to enhance traffic efficiency
 and address the evolving demands of modern transportation.
 To overcome these challenges, we propose the Software-Defined Intelligent Intersections (SDI2) framework, an
 SDN-based IIM solution capable of dynamically adapting its operational mode in response to real-time traffic pat
terns. When traffic consists of lone vehicles, the framework relies on the Synchronous Intersection Management
 Protocol (SIMP) (Reddy et al., 2022, 2024a). Conversely, when multiple vehicles need to cross in the same direc
tion, the Adaptive Intersection Management Protocol (AIMP) coordinates their movement, thereby maximizing traffic
 efficiency, minimizing stopped delays, and reducing energy waste and associated emissions. Through this hybrid ap
proach, this paper makes two key contributions. First, the SDI2 framework integrates multiple IIM approaches and
 dynamically adjusts its operational mode based on real-time traffic conditions, efficiently managing both lone vehicles
 and vehicle groups. Second, to optimize traffic flow for vehicle groups, AIMP dynamically allocates green phases and
 their durations based on vehicle crossing directions. The following section provides a detailed discussion of the SDI2
 framework.
 2. Software-defined intelligent intersections framework
 Figure 1 illustrates the architecture of the SDI2 framework,
 designed for a small road network with four signalized intersec
tions. Each intersection is equipped with roadside sensors, such
 as induction loop detectors and cameras, to monitor traffic con
ditions. This data is transmitted via roadside units (RSUs) and
 processed at local edge nodes. The system extracts key infor
mation, including vehicle presence, count, and intended crossing
 directions (left/straight/right).
 Based on this information, the SDN controller dynamically
 selects the appropriate IIM protocol. The SIMP protocol is in
voked if a vehicle is isolated, meaning no subsequent vehicle
 intends to cross in the same direction. Conversely, if multiple ve
hicles want to cross in the same direction, the AIMP protocol is
 activated. When invoking AIMP, the SDN controller schedules
 traffic light control phases (green, yellow, red) and adjusts phase
 durations. In contrast, under SIMP, phase durations remain pre
defined.
 Fig. 1: SDN-based intelligent road network.
 The SIMP protocol operates in cycles, serving one vehicle per non-conflicting road lane. These non-conflicting
 lanes are determined using the Conflicting Directions Matrix (CDM) (Reddy et al., 2022, 2024a), which regulates
 vehicle permissions at intersections. A vehicle at the intersection entrance triggers SIMP’s traffic signal control phases.
 Similar to SIMP, AIMP also utilizes road infrastructure but differs in its adaptive phase timing. By analyzing the
 number of consecutive vehicles intending to cross in the same direction from all inflow lanes, AIMP optimizes green
 phase durations accordingly, improving traffic flow efficiency.
 3. Evaluation
 The SDI2 framework was implemented and tested using the Simulation of Urban Mobility (SUMO) (Lopez et al.,
 2018), demonstrating its potential to enhance traffic efficiency and sustainability compared to the conventional Round
Robin (RR) (Chaudhuri et al., 2022) and synchronous SIMP approaches (Reddy et al., 2022). To simulate the three
 approaches, we injected traffic at a rate of 0.1 veh/s for 3600s on all eight inflow roads, following the same setup as
 scenario-1 in Reddy et al. (2024b). The remaining simulation parameters and values were adopted from Reddy et al.
Radha Reddy / Transportation Research Procedia 00 (2025) 000–000
 3
 (2024b), with a maximum vehicle speed of 30km/h. A total of 2846 vehicles completed their journey, and we recorded
 stopped delay, fuel consumption, and PMx emissions, as shown in Figure 2.
 Stopped Delay (s)
 Fuel Consumption (g)
 Emission of PMx (mg)
 Intersection Management Approaches
 (a) Stopped delay (s).
 Intersection Management Approaches
 (b) Fuel consumption (g).
 Intersection Management Approaches
 (c) PMx emissions (mg).
 Fig. 2: Comparing the results of various IM approaches at 30km/h.
 The results highlight the overall inefficiency of the RR approach, which exhibited the highest stopped delay (just
 over 400s), fuel consumption (approximately 600g), and PMx emissions (slightly above 40mg). In contrast, the IIM
 approaches, SIMP and SDI2, demonstrated strong performance, with SDI2 emerging as the best and SIMP as the
 second-best. The highest recorded values for SIMP were 44s, 252.6g, and 12.3mg, whereas for SDI2, these were 42s,
 220g, and 9.7mg, respectively.
 These results indicate that SDI2 significantly outperforms the conventional RR approach, reducing stopped delay
 by 89.5%, fuel consumption by 63.3%, and PMx emissions by 76.9%. Furthermore, SDI2 improves upon synchronous
 SIMP by 5% in stopped delay, 15% in fuel consumption, and 27% in PMx emissions. This performance gain stems
 from SDI2’s efficient invocation of the SIMP and AIMP protocols, which effectively serve both isolated vehicles and
 groups of vehicles. In contrast, the RR approach serves only groups of vehicles from one road at a time while blocking
 other roads, whereas SIMP serves one vehicle from each non-conflicting lane.
 The full paper will provide a detailed discussion of the SDI2 framework, including its components and function
ality. Future work will explore different simulation scenarios to assess the SDI2 applicability under varied traffic
 conditions, including platoons. Additionally, we plan to evaluate the energy efficiency of electric vehicles under the
 SDI2 framework.
 Acknowledgements
 This work was partially supported by the Manipal Institute of Technology, Manipal Academy of Higher Educa
tion, Manipal, India. It was also partially supported by FCT/MCTES within the Research Units CISTER, ISEP/IPP
 UIDP/UIDB/04234/2020.
 References
 Afrin T., Yodo N., A Survey of Road Traffic Congestion Measures towards a Sustainable and Resilient Transportation System. Sustainability.
 2020, 12(11), pp.4660.
 Reddy, R., Almeida, L., Santos, P.M., Kurunathan, H. and Tovar, E., 2024. Energy savings and emissions reduction of BEVs at an isolated
 complex intersection. Transportation Research Part D: Transport and Environment, 136, p.104403.
 Samal, S.R., Mohanty, M. Santhakumar, S.M., Adverse effect of congestion on economy, health and environment under mixed traffic scenario.
 Transportation in Developing Economies, 2021, 7(2), pp.15.
 Yang, J., Zhang, J. and Wang, H., 2020. Urban traffic control in software defined internet of things via a multi-agent deep reinforcement
 learning approach. IEEE Transactions on Intelligent Transportation Systems, 22(6), pp.3742-3754.
 Reddy, R., Almeida, L., Santos, P. and Tovar, E., 2024. Advantages of synchronizing vehicles intersection access. Transportation research
 procedia, 78, pp.475-482.
 Reddy, R., Almeida, L., Gait´an, M.G., Santos, P.M. and Tovar, E., 2023. Synchronous Management of Mixed Traffic at Signalized Intersections
 Toward Sustainable Road Transportation. IEEE Access, 11, pp.64928-64940.
 Chaudhuri, H., Masti, V., Veerendranath, V. and Natarajan, S., 2022. A Comparative Study of Algorithms for Intelligent Traffic Signal Control.
 In Machine Learning and Autonomous Systems, springer, pp.271-287.
 Lopez, P.A., Behrisch, M., Bieker-Walz, L., Erdmann, J., Fl¨otter¨od, Y.P., Hilbrich, R., L¨ucken, L., Rummel, J., Wagner, P. and Wießner, E.,
 2018, November. Microscopic traffic simulation using sumo. In 2018 21st IEEE international conference on intelligent transportation systems
 (ITSC), pp.2575-2582
