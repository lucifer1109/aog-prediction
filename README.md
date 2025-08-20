# aog-prediction
Predicting aircraft-on-ground risk using open source data

What is AOG?
Aircraft on Ground (Or AOG, as is most commonly referred) is a scecnario in which an aircraft that is supposed to be flying and in service is unexpectedly grounded due to problems like parts failure, structural damage, electronics failure and other such anomalies. Since every second an aircraft spends on the ground is money lost for airlines, and AOG can take a long time to be resolved (thus grounding the aircraft for a long time), airlines lose millions due to these events. Owing to the critical nature of AOG, predicting it becomes a crucial task for any airline. That is where this project comes in.

Why am I building this project?
Spoiler alert: This project is not going to solve the AOG problem. Hey, I am a college student interested in the world of aviation and supply chain logistics. There is no way me working alone behind a laptop will solve a multi-billion dollar global issue. But what it most certainly can do is help me understand the problem, and hopefully figure out a way to actually go about solving it. Who knows? Maybe I'll look back on this years from, thinking back to where it all began.

The Data
The first step towards building a prediction model is obtaining a dataset. Now since AOG is a relatively scarce and specific issue, there isn't a lot of publicly available data that is particularly relevant to this project. Therefore, I will be generating synthetic (but realistic) data for this project.


Dataset Creation & Assumptions
This synthetic Aircraft-on-Ground (AOG) dataset was generated entirely in Python using NumPy and Pandas, simulating the health and operational metrics of a fleet of 100 aircraft over multiple observations.

How It Was Generated
	1.	Aircraft Fleet Simulation
	•	aircraft_id was randomly assigned integers between 1 and 100 to simulate a fleet of 100 aircraft.
	•	Multiple rows per aircraft represent independent snapshots of its operational state.
	2.	Flight Hours (flight_hours)
	•	Random integers between 100 and 10,000 were generated to represent total cumulative flight hours.
	•	Assumption: All aircraft have at least minimal operational hours (100) and a reasonable upper bound for a commercial fleet (10,000).
	3.	Cycles Since Last Maintenance (cycles_since_last_maintenance)
	•	Random integers between 0 and 500, representing the number of takeoff–landing cycles since last maintenance.
	•	Assumption: Maintenance schedules typically trigger around 400–500 cycles, so values above 400 are considered high-risk.
	4.	Engine Oil Temperature (oil_temp)
	•	Random numbers drawn from a normal distribution with mean = 85°C, standard deviation = 5.
	•	Assumption: Normal operating oil temperature is around 85°C; values above 95°C indicate overheating risk.
	5.	Vibration (vibration)
	•	Random numbers from a normal distribution (mean = 0.5 g, SD = 0.1 g).
	•	Assumption: Aircraft engines vibrate slightly under normal conditions; excessive vibration (>0.7 g) indicates potential mechanical issues.
	6.	Pressure Ratio (pressure_ratio)
	•	Random numbers from a normal distribution (mean = 32, SD = 3).
	•	Assumption: Typical jet engine pressure ratios fall near 32; deviations can indicate performance degradation.
	7.	Target Variable – AOG Flag (AOG_flag)
	•	Created using threshold-based rules to simulate aircraft being grounded:

AOG_flag = (cycles_since_last_maintenance > 400) | 
           (vibration > 0.7) | 
           (oil_temp > 95)


	•	1 indicates the aircraft is “grounded” due to maintenance or abnormal operational readings.
	•	0 indicates normal operation.

Randomization Mechanisms
	•	np.random.randint() → used for discrete features (aircraft_id, flight_hours, cycles_since_last_maintenance).
	•	np.random.normal() → used for continuous features (oil_temp, vibration, pressure_ratio) to simulate natural variation.
	•	np.random.seed(42) → ensures reproducibility so anyone can generate the same dataset.

Assumptions Made
	•	Each observation is independent; the dataset does not simulate time-series flight sequences.
	•	Thresholds for AOG (cycles > 400, vibration > 0.7, oil_temp > 95) are simplified approximations for demonstration.
	•	Real aircraft would have many more sensors and features (fuel flow, engine pressures at multiple stages, altitude, etc.).
	•	The dataset focuses on predictive maintenance signals relevant to AOG events, not complete operational reality.

Purpose of These Assumptions
	•	Simplifies model building for a student project while still being realistic enough for ML, Power BI dashboarding, and storytelling.
	•	Provides a baseline for predictive modeling: you can apply logistic regression, decision trees, XGBoost, or other classifiers.
	•	Serves as a proof-of-concept dataset to illustrate how airlines or MRO providers might predict and reduce AOG events.
