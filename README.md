# Machine learning for hemoglobin concentration estimation in a two-layer planar model using frequency-domain NIRS: A Monte Carlo simulation study

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


## Monte Carlo Simulation

Monte Carlo (MC) simulations were performed using **Monte Carlo eXtreme (MCX)**. To balance computational cost and dataset coverage, a total of 11,000 simulations were conducted, generating 11,000 sets of frequency-domain near-infrared spectroscopy (FD-NIRS) measurements. Figure 1 illustrates the overall workflow of the study, while Figure 2 presents the geometry of the two-layer planar tissue model used in the simulations.

<img width="648" height="361" alt="Two-layer planar tissue model used in Monte Carlo simulations" src="https://github.com/user-attachments/assets/f5200478-ab33-490e-b3a3-8dfe9443fe48" />

<p align="center"><b>Figure 2.</b> Geometry of the two-layer planar model used in MC simulations. It includes one source and four source-detector separations (S-D separations): D1, D2, D3, and D4. The S-D distances are 1, 2, 3, and 4 cm from the source, respectively. The whole geometry is a 100 nm by 100 nm by 100 nm cube, and the smallest unit is 1 mm3. The light source is a laser with a delta-function photon release pattern. The number of photons are 120 million in each of the release. </p>

## Inverse Computation Using Machine Learning

The inverse computation was performed using multiple machine learning (ML) algorithms, including four variants of k-nearest neighbors (KNN), XGBoost, Gradient Boosting (GB), CatBoost(CB), Artificial neural network(ANN), and random forest(RF). FD-NIRS measurements, including AC amplitude (Uac), DC amplitude (Udc), and phase, were used as model inputs to estimate oxyhemoglobin ([HbO]) and deoxyhemoglobin ([Hb]) concentrations, along with relevant optical properties, in both tissue layers.

Model performance was evaluated using mean absolute error (MAE) and mean absolute percentage error (MAPE). The primary objective of this study was to systematically compare the performance of different ML algorithms for solving the inverse problem in a two-layer planar tissue model and assess their potential for hemoglobin concentration estimation from FD-NIRS measurements.


## Robustness Evaluation Under Gaussian Noise

To evaluate the robustness of different machine learning models, zero-mean Gaussian noise was added to the simulated FD-NIRS measurements, including AC amplitude (Uac), DC amplitude (Udc), and phase. Four noise levels were considered to represent different degrees of measurement uncertainty.

For Uac and Udc, Gaussian noise was introduced using a standard deviation proportional to the original measurement values. For phase measurements, Gaussian noise was added using a fixed standard deviation in degrees.

The noise levels were defined as follows:

| Noise Level | Uac and Udc Noise (Relative STD) | Phase Noise (STD) |
|:-----------:|:--------------------------------:|:-----------------:|
| Level 1 | 0.75% | 0.15° |
| Level 2 | 1.50% | 0.30° |
| Level 3 | 3.75% | 0.75° |
| Level 4 | 7.50% | 1.50° |

The selected noise levels cover a range of measurement uncertainties, from relatively low noise to substantially elevated noise conditions. Model performance was evaluated under all four noise levels to assess the sensitivity and robustness of different machine learning approaches to measurement noise.
