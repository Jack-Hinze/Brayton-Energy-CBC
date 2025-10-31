# Brayton-Energy-CBC
A stand alone executable file that solve the thermodynamic state points of a Closed Brayton Cycle.

Brayton Energy CBC Model
Date: 10/23/24
Author: Jack Hinze

Purpose:
This simple cycle model allows the user to quickly assess the impact of changing:
	1. Performance Parameters
	2. Operating Temperatures
	3. System Losses
	4. Radiator Perforance
	
The outputs of this model are:
	1. State points (Temperature, Pressure, and Mass Flow)
	2. System Efficiency
	3. Size of turbomachinery and shaft speed
	4. Size of the radiator 
	
Operating Instructions
The model has be set up with typical parameters for a 50kWe engine. The model can be queried to determine the impact of various input parameters on the output parameters. Several examples are provided below:
	1. Compressor Inlet Temperature (CIT) Investigation
		CIT is a strong driver of cycle performance and radiator area. Generally, increasing CIT will decrease radiator area at the expense of cycle efficiency
	2. Turbine Inlet Temperature (TIT) Investigation
		TIT is a strong driver of efficiency with no thermodynamic downside. Increasing the TIT to the maximum possible value will increase efficiency and decrease radiator area.
	3. Pressure Ratio (PR) Investigation
		An optimal pressure ratio exists that maximizes efficiency for a given set of inputs. It is normally around 2. 
	4. Performance Parameter Investigation
		Changing the HX effectiveness and pressure drop has an impact on cycle efficiency. However care must be taken to ensure reasonable values are set, typically 1% dP/P for HX and max effectiveness of 95%.
	
	
Variable Info
Inputs
Name			Units				Description
η_comp				-					Isentropic efficiency of the compressor
η_turb				-					Isentropic efficiency of the turbine
ε_recup				-					Effectiveness of the recuperator
ε_HRHX				-					Effectiveness of the Heat Rejection Heat Exchanger (HRHX)
eff_gen				-					Efficiency of the generator (alternator) including I^2R and windage losses. Heat retained in cycle.
eff_rect			-					Efficiency of the active rectifier. Heat rejected externally.
n_bearings			- 					The number of bearings in the system
Bearing_loss		W					Heat generation per bearings
frac_bleed			-					Fraction of compressor discharge mass flow this passes over the bearing for cooling. Returns at turbine discharge.
f_dp_recup_hp		-					Fractional pressure drop on HP side of recuperator. As a function of the inlet pressure.			
f_dp_recup_lp		-					Fractional pressure drop on LP side of recuperator. As a function of the inlet pressure.			
f_dp_PHX			-					Fractional pressure drop of the PHX. As a function of the inlet pressure.			
f_dp_HRHX			-					Fractional pressure drop of the HRHX. As a function of the inlet pressure.			
f_dp_Alt			-					Fractional pressure drop of the Alternator. As a function of the inlet pressure.			
f_dp_Pipe			-					Fractional pressure drop of each transition region. These are between state points: (2,3); (6,7); (8,9); (10,11); (13,1).As a function of the inlet pressure.			
Num_faces			-					Defines if the radiator is radiating from one side or 2 in order to determine the solar loading
Q_dot_spec_solar	W/m2				Solar flux at the location of the radiator
vf_amb				-					View factor between the radiator and the ambient temperature. Value from 0 (no visibility) to 1 (no blockage).
T_amb				K					Temperature that the radiator is rejecting heat to
abs_rad				-					Solar absorbtivity of the radiator
emis_rad			-					Emissivity of the radiator coating
vf_solar			-					View factor between the radiator and the sun. Value from 0 (no visibility) to 1 (no blockage).
dT_PFL_Face			K					Approach temperature between the Pumped Fluid Loop (PFL) to the radiating face of the radiator
cp_rad				J/kg-K				Specific heat of the radiator fluid
f_1$				-					Fluid name of fluid 1. Can be any fluid in the EES database that behaves as an ideal gas.
f_2$				-					Fluid name of fluid 2. Can be any fluid in the EES database that behaves as an ideal gas.
MW_mix				-					Molecular weight of the fluid mixture. Must be bounded the molecular weight of the 2 components
T_TIT				K					Turbine Inlet Temperature
CIT					K					Compressor Inlet Temperature
PR					-					Pressure Ratio of compressor. Defined as P_discharge/P_inlet
P_low				kPa					Absolute pressure at the compressor inlet
CR_HRHX				-					Capacitance ratio between the fluid loop and the working fluid in the HRHX. This value can be manipulated to change the fluid loop flow rate.
Power				W					The desired power at the output of the active rectifier


Outputs
T_i					K					Temperature at state point i
P_i					kPa					Pressure at state point i
m_dot_i				kg/s				Mass flow at state point i
D_comp				mm					Diameter of compressor with typical specific speed and head coefficient
D_turb				mm					Diameter of turbine with typical u/C0 parameter
Shaft_speed			RPM					Shaft speed required for compressor and turbine sizing	
Q_dot_Recup			W					Heat transfer in the recuperator
Q_dot_PHX			W					Heat transfer from heat source to working fluid			
Q_dot_HRHX			W					Heat transfer from working fluid to radiator fluid	
T_in_rad			K					Temperature of the water into the radiator
T_out_rad			K					Temperature of the water out of the radiator
A_rad				m2					Predicted radiator area
Q_dot_rad			W					Heat transfer from fluid loop to ambient temperature
m_dot_rad			kg/s				Flow rate of the radiator fluid loop fluid	
