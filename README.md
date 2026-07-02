#  manual of TransTEC model

Introduction
TransTEC (Transformation of transportation energy and carbon) tool enables levelized assessments of the full life cycle costs of advanced technology commercial vehicles. Medium- and heavy-duty commercial vehicles operate in diverse vocations with varied duty cycles, performance, and technical and economic requirements. TransTEC accounts for these operational variations as well as technology considerations associated with decarbonization.



Benefits of TransTEC Methodology
Perceived cost of ownership is a key metric in fleets’ decision making about whether to adopt advanced commercial vehicles. TransTEC takes a holistic approach, looking at full lifecycle costs, allowing fleet operators to objectively assess the costs and savings of converting legacy diesel vehicles to advanced technologies, such as battery electric or fuel cell vehicles.

In addition to calculating the direct costs of purchasing, maintaining, refueling/charging, and operating a commercial vehicle, TransTEC quantifies the implicit costs of new technologies, such as range limitations, charging/refueling dwell times, and cargo capacity loss. TransTEC also provides room to adapt as the industry and technology evolve.

TransTEC offers advantages in scalability, integration, and flexibility. Due to its modular architecture, TransTEC can be expanded and integrated with existing models. TransTEC is a fully integrated Python model that takes an end-to-end, unified approach to assessing costs and enables consistent comparisons across technologies and industries, including trade-offs between conventional energy, battery electric vehicles, and fuel cell electric vehicle scenarios. Inputs and functions can be changed based on a variety of objectives, addressing the need for a general, inclusive analysis approach. TransTEC's source code is freely and publicly available.



Uses and applications
Researchers use TransTEC to:
•	Identify quantitative, goal-driven research and development needs.
•	Inform critical technical targets for medium- and heavy-duty electric vehicles and related electrical components to accelerate commercialization.
•	Assess electric vehicle charging and hydrogen fueling infrastructure needs and inform operations.
•	Help industry partners assess and prioritize research needs and measure technology impacts.
•	Conduct perceived cost of ownership analyses for conventional and electrified vehicles across various commercial vehicle vocations to predict project parity.
•	Measure the degree of decarbonization in commercial vehicle.
•	Design the optimal decarbonization path under different policies and decarbonization targets.



File structure and running
The Scenario Simulate module sets the operation scenario parameters, such as vehicle category, daily driving distance, frequency, and load.
Calibrate module calibrates the historical data of market share.
Calculate PCO module calculates the PCO by importing parameter files in each year cycle. powertrain_factors.xlsx mainly involves vehicle-related parameters, battery capacity, vehicle price, depreciation rate, etc. year_varies_factors.xlsx mainly stores year-related parameters, subsidies, carbon taxes. single_factor_annual_cost .xlsx is used to store intermediate results, the final result is stored in PCO_result .xlsx.
The calibration results and PCO results are imported in Calculate market share & GHG emission module for market penetration prediction. The final result includes PCO, market share and GHG emission.



Input changing and result processing
Normally, there is no need to modify the calibration file due to the unchanged history data. If you need to change scenario setting, for example, daily vehicle travel parameters, find the corresponding input file scenario_setting .py for modification and run Mcsimulation.py, then the corresponding result file tt_mc_results .xlsx has changed.
