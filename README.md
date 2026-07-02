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



## File description and workflow

This repository provides example input data and Python code used to illustrate the implementation of the heavy-duty truck transition model developed in the manuscript. The code links perceived cost of ownership (PCO), vehicle-choice probabilities, stock turnover, fuel-cycle emissions, and mitigation-cost accounting.

### Main script

| File | Purpose | Main inputs | Main outputs |
|---|---|---|---|
| `defCVrr1.py` | Main Python script for calculating annual vehicle costs, choice probabilities, stock evolution, emissions, and marginal abatement-cost indicators. | `tt_output_fastsim_tractormix_S.xlsx`; `tt_vehicle_represent_params_tractormix.xlsx`; `year_varies_tractormix_S.xlsx`; `tt_mc_results_ltractor.xlsx`; `output_results.xlsx`; `final_probabilities_merged_with_categories.xlsx`; remain-rate file | `comtt_an_fu_con_results.xlsx`; `comtt_annual_cost1.xlsx`; `emission_details.xlsx`; `combined_results1.xlsx` |

The script contains two main calculation stages:

1. `calculate_annual_cost()` calculates annual cost and emission indicators for each powertrain option and writes the results to `comtt_annual_cost1.xlsx`.
2. `calculate_emission()` uses the annual cost results, calibrated adjustment factors, and best-fit choice constants to calculate vehicle-choice probabilities, market shares, stock turnover, total emissions, total costs, consumer-surplus indicators, and marginal abatement-cost indicators.

---

### Input files

| File | Role in the model | Main contents | Used by |
|---|---|---|---|
| `tt_mc_results_ltractor.xlsx` | Operating-profile input file | Representative truck-use records, including vehicle type, province, annual operating days, daily distance, trip frequency, load factor, road factor, temperature factor, and traffic factor. | `calculate_annual_cost()` |
| `tt_output_fastsim_tractormix_S.xlsx` | Vehicle-technology and performance input file | Vehicle purchase-price components, battery capacity, fuel or electricity consumption, fuel-consumption improvement factors, maintenance cost, insurance cost, vehicle mass, cargo capacity, infrastructure cost, refuelling/charging parameters, and fuel-cycle carbon intensity. | `calculate_annual_cost()` |
| `tt_vehicle_represent_params_tractormix.xlsx` | Representative vehicle and behavioural-parameter input file | Representative vehicle categories, regional wage assumptions, refuelling/charging availability parameters, and historical target probabilities used for calibration. | `calculate_annual_cost()` |
| `year_varies_tractormix_S.xlsx` | Year-varying policy and market input file | Fuel prices, regional fuel-price factors, subsidies, regional subsidy factors, carbon-tax assumptions, charging/refuelling efficiency, station distance, residual-value factors, annual retire factors, tonne-km cost, and remaining fossil-fuel share under E-fuel blending. | `calculate_annual_cost()` |
| `output_results.xlsx` | Calibrated category-level adjustment-factor file | Annual adjustment factors by owner and technology category. These factors are used to align the discrete-choice probabilities with calibrated market-share patterns. | `calculate_emission()` |
| `final_probabilities_merged_with_categories.xlsx` | Calibrated choice-constant and target-probability file | Annual cost records merged with calibrated probabilities, target probabilities, best-fit constants (`Best_Ci`), maximum calibration errors, and technology categories. | `calculate_emission()` |

---

### Intermediate and output files

| File | Type | Description | Generated by |
|---|---|---|---|
| `comtt_an_fu_con_results.xlsx` | Intermediate output | Detailed annual fuel-consumption, emissions, range, refuelling/charging convenience cost, range-anxiety cost, infrastructure cost, and other powertrain-level indicators before final PCO aggregation. | `calculate_annual_cost()` |
| `comtt_annual_cost1.xlsx` | Intermediate output | Annual perceived cost of ownership results by vehicle, province, year, and powertrain. This file is the direct input for the market-share, stock-turnover, and emissions calculation. | `calculate_annual_cost()` |
| `emission_details.xlsx` | Output | Powertrain-level emission intensity and total fleet emissions by year. | `calculate_emission()` |
| `combined_results1.xlsx` | Final output | Main integrated results, including market shares, stock details, annual total emissions, annual total costs, consumer-surplus indicators, and marginal abatement-cost indicators. | `calculate_emission()` |

`combined_results1.xlsx` contains the following sheets:

| Sheet | Description |
|---|---|
| `Market_Shares` | Annual average choice probabilities by powertrain. |
| `Stock_Details` | Annual stock-turnover records, including previous stock, scrapped vehicles, new sales, and resulting stock by powertrain. |
| `Summary` | Annual total emissions, total costs, annual consumer surplus, and cumulative consumer-surplus indicators. |
| `MAC` | Marginal abatement-cost and cumulative cost/emission indicators for the final model year. |
| `Subsidy_Details` | Reserved sheet for fuel-subsidy details when subsidy scenarios are activated. |

---

### Workflow

The relationship among files is as follows:

```text
Input data
│
├── tt_mc_results_ltractor.xlsx
│   └── Representative truck-use profile
│
├── tt_output_fastsim_tractormix_S.xlsx
│   └── Vehicle technology, cost, performance, and emission parameters
│
├── tt_vehicle_represent_params_tractormix.xlsx
│   └── Representative vehicle, wage, charging/refuelling availability, and calibration targets
│
├── year_varies_tractormix_S.xlsx
│   └── Year-varying fuel prices, subsidies, carbon tax, blending/remain-rate, and policy assumptions
│
└── remain-rate scenario file
    └── Annual remaining fossil-fuel shares under E-fuel blending assumptions

        ↓
calculate_annual_cost()

Intermediate outputs
│
├── comtt_an_fu_con_results.xlsx
│   └── Detailed fuel-consumption, emission, and operating-cost indicators
│
└── comtt_annual_cost1.xlsx
    └── Annual PCO results by powertrain

        + output_results.xlsx
        + final_probabilities_merged_with_categories.xlsx

        ↓
calculate_emission()

Final outputs
│
├── emission_details.xlsx
│   └── Powertrain-level emission details
│
└── combined_results1.xlsx
    ├── Market_Shares
    ├── Stock_Details
    ├── Summary
    ├── MAC
    └── Subsidy_Details




Running the example

Before running the script, make sure the input files are placed in the same folder as defCVrr1.py and use the file names expected by the code:
defCVrr1.py
tt_mc_results_ltractor.xlsx
tt_output_fastsim_tractormix_S.xlsx
tt_vehicle_represent_params_tractormix.xlsx
year_varies_tractormix_S.xlsx
output_results.xlsx
final_probabilities_merged_with_categories.xlsx

Then run:
python defCVrr1.py
python optimization.py




Input changing and result processing
Normally, there is no need to modify the calibration file due to the unchanged history data. If you need to change scenario setting, for example, daily vehicle travel parameters, find the corresponding input file scenario_setting .py for modification and run Mcsimulation.py, then the corresponding result file tt_mc_results .xlsx has changed.
