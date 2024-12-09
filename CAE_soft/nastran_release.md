定期发布 MSC Nastran的release note部分相关或重要内容.
-------------
2024.2
- MSC Nastran PEM workflow enhancements:
  - A new method to compress the Reduced Impedance Matrices (RIM) in the modal approach
  - An increased computational efficiency and reduction of memory requirements for the MSC Nastran PEM +workflow using the modal approach for RIM
- 32-bit real/64-bit integer hybrid H5 database: IDs are in 64-bit integers and results are stored in 32-bit real numbers. This allows for a significant reduction in memory usage and faster processing times
- Mass Matrix Support for Cohesive Elements in Linear Solution Sequences: Cohesive elements and materials based on Cohesive Zone Model (CZM) in SOL 400.
- Performance improvements: ACMS (Automated Component Modal Synthesis): for large stiff structures, typically modeled with solid finite elements.
    - Improved support for large models: increased maximum number of nodes and elements, reduced memory usage, and improved performance for large models. 
    -  MSC Nastran and ACMS are highly threaded. Use of multiple cores is highly recommended. For analyses requiring many thousands of eigenvalues, use of Distributed Memory Parallel (DMP) is highly recommended and should be used in combination with Shared Memory Parallel (SMP).
- Performance improvments: FASTFR (Fast Frequency Response software): The FSTFR module was re-written in order to take advantage of new and future architectures. When **structural damping (K4)** is present in the model, the modal representation of the K4 matrix must be computed. 
Efficiency improvements were made to this calculation, which can be very time consuming.