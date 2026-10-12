# Machine Learning for Inverse Computation in a Two-Layer Planar Model Using FD-NIRS Measurements at 110 MHz

This repository contains the simulation data and source code associated with our study, **"Machine Learning for Hemoglobin Concentration Estimation in a Two-Layer Planar Model: A Monte Carlo Simulation Study."**

The study investigates the application of machine learning and mathematical methods to estimate hemoglobin concentrations in a two-layer planar tissue model using frequency-domain near-infrared spectroscopy (FD-NIRS) measurements at a modulation frequency of 110 MHz. The repository includes code for Monte Carlo (MC) simulations and inverse computation using different modeling approaches.

## Repository Structure

The repository is organized into three main directories:

- **`fitting/`** – Contains implementations of machine learning algorithms and mathematical models for inverse computation and hemoglobin concentration estimation.
- **`papers/`** – Contains research papers and reference materials relevant to this study.
- **`simulation/`** – Contains code for performing Monte Carlo simulations in a two-layer planar tissue model.

This repository is intended to support the reproducibility of our research and facilitate further investigations into machine learning-based inverse computation for FD-NIRS applications.

<img width="722" height="244" alt="image" src="https://github.com/user-attachments/assets/0fb23aaa-9cd5-44d2-8f4f-02fb8cf5753b" />
<figcaption align="center"><b>Figure 1:</b> Workflow of forward and inverse computations. Blue boxes represent the forward process, in which random hemoglobin concentrations and scattering proper-ties, together with variable first-layer thickness, are selected as input parameters for MC simulations to generate TD-NIRS data, followed by synthesis of FD-NIRS data via Fou-rier transform at 110 MHz. Orange boxes represent the inverse modeling framework using ML methods.</figcaption><br>

&emsp;&emsp;The whole process includes both forward and backward computations. Forward computation started from Sobel sampling of the optical properties of the 2 layer planar model. These properties were then be used as the input flof Monte Carlo simulation to generate Time domain NIRS or TD-NIRS. The TD-NIRS were transformed into FD-NIRS based on Fourier transform. The ranges of the optical properties and hemoglobin concentrations were refered to human head measurements using classical physics approach. 

**Table 1.** Ranges of hemoglobin concentrations and tissue properties used in MC simulations. The numerical value represents the layer number.

| Parameters | Range | Unit |
|:----------:|:-----:|:----:|
| HbO1 | [5, 20] | μM |
| HbO2 | [25, 55] | μM |
| Hb1 | [2.5, 12.5] | μM |
| Hb2 | [15, 35] | μM |
| d1 | [10, 20] | mm |
| a1 | [0.9, 6.9] | mm⁻¹ |
| a2 | [1.1, 4.2] | mm⁻¹ |
| b1 | [0.1, 2.5] | - |
| b2 | [0.3, 3.3] | - |


&emsp;&emsp;The software tool used for the Monte Carlo simulation is MCX. To balance the the time spending on simulation and data density, we conducted a total of 11000 simulations and got 11000 FD-NIRS measurements. Figure 1 shows the overall process of the study and Figure 2 shows the geometry of the 2 layer planar model<br>
<img width="648" height="361" alt="image" src="https://github.com/user-attachments/assets/f5200478-ab33-490e-b3a3-8dfe9443fe48" />
<figcaption align="center"><b>Figure 2:</b> The two-layer planar model used in MC simulations.</figcaption><br>

&emsp;&emsp; The inverse process were conducted by multiple machine learning approaches. These approaches include four variants of KNN, XGBoost, Gradient Boost, and Catboost. FD-NIRS measurements (Uac, Udc, phase) were fed into models and the hemoglobin concentrations ([HbO], [Hb]) and relevant optic properties were predicted for both layers. The mean absolute error and mean percentage error were measured for different ML models. The main purpose of the study is to comprehensively test the performance of different ML models in the 2-layer planar model reverse computation. <br>
