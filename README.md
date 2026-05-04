# EFFECTUAL-WASTE-BINS-SITTING-AND-ROUTE-OPTIMIZATION
A Decision Support System framework that  utilizes Geographic information System (GIS), Geospatial data, and optimization algorithms to enhance the  efficiency of collection routes from waste bin points to a landfill location, thereby improving waste  management services. 
## Introduction 
Urban waste management in rapidly growing cities like Accra, Ghana, faces persistent challenges such as overflowing bins, inefficient collection routes, high operational costs, and uncollected waste fuelling illegal dumping. This project develops a GIS-based Decision Support System (DSS) that combines spatial Multi-Criteria Evaluation (MCE) and Vehicle Routing Problem (VRP) optimization to systematically improve waste bin placement and collection route efficiency across Ablekuma Central Municipality.

### Key Outcomes:
1. 🗺️ Identified 1,435 optimal new waste bin locations using weighted spatial analysis
2. 🚛 Optimized routes for a fleet of 4 collection trucks servicing 1,694 total bins
3. 📉 Projected 28–35% reduction in total travel distance vs. baseline routes
4. ⏱️ Total fleet travel time reduced to 210 minutes covering 75.8 km

## Study Area
- Ablekuma Central Municipality, Greater Accra Region, Ghana
- ParameterValuePopulation Density> 18,500
- persons/km²Daily Waste Generation120–170 tonnes
- Formal Collection Rate: 50–60%
- Coordinates Lat: 5°67′–5°81′N, Lon: 0°13′–0°24′W

The municipality is bounded by Ablekuma West (west), Accra Metropolitan (south & east), and Ablekuma North (north). Rapid urbanisation has led to uneven bin distribution, road congestion, and service gaps leaving up to 20% of waste uncollected.


## DSS Workflow: DSS Workflow: Waste Bin Sitting and Route Optimization
The DSS is structured into two integrated modules:
<img width="1337" height="1006" alt="UML chart" src="https://github.com/user-attachments/assets/d691389b-93e9-497c-a457-bca6617e2fd7" />

## Methodology
### Module 1 — Multi-Criteria Evaluation (Bin Siting)
Spatial criteria were standardised and weighted using the Analytic Hierarchy Process (AHP), then combined via Weighted Overlay Analysis in ArcMap 10.8.
| Criterion                                       | Weight   | Rationale                                    |
| :--------------------------------------         | :------- | :---------                                   |
| Demand (Building Density)                       | 40%      |High-density areas generate the most waste    |
| Accessibility (Road Proximity)                  | 35%      |Bins must be reachable by collection vehicles |
| Gap-Filling (Distance from Existing Bins)       | 15%      |Target underserved areas to promote equity    |
| Exclusion Constraint (Buildings, Roads, Rivers) | 10%      |Ensures only physically viable locations      |

Suitability Score Formula:

Final_Suitability = (Suit_Demand × 0.40) + (Suit_Accessibility × 0.35)
                  + (Suit_Gaps × 0.15) + (Suit_Exclusion × 0.10)

Exclusion Buffers Applied:
| Feature   | Buffer Zone        | 
| :----- | :---------- | 
| Buildings  | 2m    |         
| Roads   | 2m    |         
| River  | 10m     |         

### Module 2 — Vehicle Routing Problem (Route Optimisation)
Using ArcGIS Network Analyst, a capacitated VRP was solved to minimise total fleet travel time while ensuring all bins are serviced.

| VRP Parameter   | Value        | 
| :----- | :---------- | 
| Number of Vehicles | 4 Trucks    |         
| Vehicle Capacity  | 10 Tonnes each    |         
| Assumed Demand per Bin  | 1 Tonne     |    
| Service Time per Bin | 5 Minutes   |
| Landfill Unload Time|  20 Minutes  |
| Objective | Minimize Total Travel Time   | 
| Total Bins Serviced | 1,694 (259 existing + 1,435 new)   |

## Data Sources
| Dataset | Format | Source|
|  :------ | :-------- | :-------------
| Administrative Boundary | Vector  | GADM |
| Road Network & Buildings | Vector | OpenStreetMap|
| Existing Waste Bin Locations | Vector | Digitised from Google Earth Maps |
| Land Use Map | Vector | OpenStreetMap | 
| Digital Terrain Model | Raster | NASA Earth |
| DataPopulation Density | Vector | Ghana Statistical Service| 
| Dump Site / Landfill Location | Vector | OpenStreetMap |

## Tools & Software
- ArcGIS / ArcMap 10.8 — Spatial analysis, Weighted Overlay, Network Analyst
- ArcCatalog — Geodatabase and Network Dataset creation
- Google Earth Pro — Digitising existing bin locations and boundary verification
- Spatial Analyst Extension — Euclidean Distance, Kernel Density, Reclassify tools
- Network Analyst Extension — VRP solver and route generation

## Results
| Metric | Value | 
|  :------ | :-------- |
| New Bin Locations Identified | 1,435 |
| Total Bins Serviced | 1,694| 
| Optimised Fleet Travel Distance | 75.8 km |
| Optimised Fleet Travel Time | 210 minutes | 
| Estimated Distance Reduction | 28–35% vs. baseline | 
| Number of Zones / Trucks | 4 |

The MCDA process successfully targeted high-density, road-accessible, and previously underserved areas. The VRP solution distributes bin coverage across 4 geographic zones, with each truck operating capacity-optimised sequences before making landfill trips.

## Future Work
- Integrate IoT smart bin sensors for real-time fill-level monitoring
- Apply machine learning to predict waste generation by zone and season
- Extend the DSS to other municipalities across Greater Accra Region
- Incorporate traffic congestion data for time-of-day route optimisation
- Develop a web GIS dashboard for municipal decision-makers

## References
- Amankwaa, E., & Boafo, Y. (2021). Market Survey Report on Solid Waste Management in Accra. DOI: 10.13140/RG.2.2.23193.49762
Chapman-Wardy, C., et al. (2021). Modeling the Amount of Waste Generated by Households in the Greater Accra Region. Journal of Environmental and Public Health, 2021. DOI: 10.1155/2021/8622105
- Sulemana, A., et al. (2019). Effect of optimal routing on travel distance, travel time and fuel consumption of waste collection trucks. Management of Environmental Quality, 30(4). DOI: 10.1108/meq-07-2018-0134
- Ghahramani, M., et al. (2021). IoT-Based Route Recommendation for an Intelligent Waste Management System. IEEE Internet of Things Journal, 9(14). DOI: 10.1109/jiot.2021.3132126
