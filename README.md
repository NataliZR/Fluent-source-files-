# Fluent-source-files-
This repository contains Ansys Fluent source files for conducting fluid dynamics simulations. The files are designed to model a lava dome growth using the geometry that approximates the horizontal propagation of the lava dome at Volcán de Colima. 

Description:

The Fluent source files provided here are tailored for simulating experiment 4.2, as outlined in Zeinalova et al., 2024 (https://doi.org/10.1093/gji/ggad415). This simulation focuses on a 2D laminar, incompressible, two-phase, immiscible viscous fluid flow, representing the extrusion of the lava (phase 2) into the air (phase 1). The model incorporates the nonlinear convective and radiative heat transfer at the lava–air interface, along with considerations for the latent heat of crystallization. Additionally, the simulation accounts for temperature-dependent volume fraction of crystals at the equilibrium state (phi_eq). 


The source files include case and data files, UDF (User-Defined Function) functions written in C, and the journal file. This set of files is designed to simulate the specified experiment(exp. 4.2), offering a well-rounded package that includes the necessary components for the simulation in Ansys Fluent. The UDF functions, in particular, contribute to the customization and incorporation of specific functionalities, ensuring the simulation aligns with the conditions and parameters outlined in Zeinalova et al., 2024.

Installation
To utilize these Fluent source files, you'll need Ansys Fluent 2021R2 installed on your system. 
The simulation was executed on an HPC cluster operating on Linux 4.18.0-372.46.1.el8_6.x86_64.
Ensure you have the necessary software and licenses before running these simulations. This file is written with the assumption that the user is familiar with the Fluent interface and the ribbon structure. 
To become acquainted with Ansys Fluent, please refer to Fluent's User Guide (https://ansyshelp.ansys.com/Views/Secured/corp/v241/en/flu_ug/flu_ug.html).

Usage
File Structure:

/Case Description:
Contains comprehensive information detailing the methods, boundary conditions, and model parameters specified for the experiment.

/Case-Data File (Exp4_2_Zeinalova2024.cas/dat):
Contains the mesh, initial,  boundary and cell zone conditions, and solution parameters tailored for experiment 4.2, as described in Zeinalova et al. 2024.

/Scripts (UDF_code.c):
Includes a supplementary C script  featuring User-Defined Function (UDF) implementations. These functions account for different heat sources, such as nonlinear heat transfer and latent heat, incorporate kinetic equation, and apply specific rheology for the lava viscosity.

/Journal File (journal.cav):
A journal file contains a sequence of Fluent commands to run simulations on HPC. 


To run the simulations, follow these steps:

1. Open Ansys Fluent and read the case/data file (Exp4_2_Zeinalova2024.cas/dat) from the designated directory. All necessary parameters including case settings, boundary conditions, solver settings are being set up. The zone for the conduit is already appropriately patched.

2. Make sure that the libraby from UDF file is compiled without errors. 
Check the following aspects:

-Confirm whether the viscosity of the lava is defined using the user-defined function mvp11::libudf1 (Materials->lava->Viscosity)
-Ensure that the energy source terms are implemented through the user-defined functions: udf sourceEn::libudf1 for the latent heat term and udf source_nonlinear::libudf1 for the nonlinear convective and radiative heat transfer (Cell zone conditions->fluid->Source terms->Energy)
-Check if the additional kinetic equation is included (Cell zone conditions->fluid->phase 2->Source terms->User Scalar 0)
-Verify if the function Hook vof_store::libudf1 is user-defined (User defined->Function Hooks->Execute at End)


3. DO NOT INITIALIZE SOLUTION

4. Run the simulation and monitor convergence.

Please note that during experiment 4.2 adjustments were made by varying the extrusion rate and elevating the threshold of the lava viscosity. For detailed description of the experiment please refer to the work of Zeinalova et.al, 2024 (https://doi.org/10.1093/gji/ggad415). 






Acknowledgments
This project is funded by the Deutsche Forschungsgemeinschaft (project DFG IS203/14-1).

Contact Information
For any questions or suggestions regarding this project, feel free to contact:

Natalya Zeinalova (natalya.zeinalova@kit.edu)
