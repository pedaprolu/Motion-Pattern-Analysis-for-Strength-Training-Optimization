Project Motivation
Being passionate about fitness and trained in martial arts, I identified a limitation in current wearable technology: while cardiovascular tracking is well-supported, strength training analysis remains underdeveloped. This project was driven by the desire to build a tool that supports individuals in achieving their fitness goals with greater safety and effectiveness.

Overview
This repository contains the complete codebase and assets for a context-aware fitness tracking system capable of:

Recognizing various strength training exercises

Counting exercise repetitions

Identifying incorrect form during execution

The solution utilizes data obtained from wearable sensors and incorporates machine learning to provide insights comparable to those given by a personal fitness coach.

Features

Exercise Classification: Automatically detects major barbell exercises including Bench Press, Deadlift, Overhead Press, Barbell Row, and Squat

Repetition Counting: Tracks the number of reps performed during each exercise with precision

Form Detection: Identifies common technique faults in real time to promote safe training (feature in progress)

Practical Implementation: Developed using real-life workout sensor data from wrist-mounted Meta Motion devices

Acknowledgments
This work was influenced by Dave Ebbelaar’s research, especially his paper titled "Exploring the Possibilities of Context-Aware Applications for Strength Training". The concepts and methodologies in this project are built upon that foundation. His contributions can be explored further on his GitHub profile: @daveebbelaar.

Technologies Used

Hardware

Meta Motion Sensor (Wrist-Worn): Captures data from accelerometers and gyroscopes

Software

Programming Language: Python

Libraries:

For data manipulation: pandas, numpy, scipy

For model development: scikit-learn

For visualizations: matplotlib, seaborn

Development Tools:

Jupyter Notebooks for experimentation

Pickle for saving/loading preprocessed datasets

Project Structure

bash
Copy
Edit
├── LICENSE  
├── README.md               # Summary and usage instructions  
├── data  
│   ├── external            # Third-party source datasets  
│   ├── interim             # Cleaned intermediate data  
│   ├── processed           # Final datasets ready for modeling  
│   └── raw                 # Original sensor readings  
├── docs                    # Documentation and guides  
├── models                  # Trained models and output predictions  
├── notebooks               # Analysis and experiment notebooks  
├── references              # Supporting papers and manuals  
├── reports                 # Analytical results and visual reports  
├── src                     # Source code modules  
│   ├── data                # Data loading and transformation scripts  
│   ├── features            # Feature generation scripts  
│   ├── models              # Training and evaluation code  
│   └── visualization       # Visualization logic  
└── requirements.txt        # Python dependencies  
How It Works

1. Data Collection
Sensor data is recorded using wrist-worn Meta Motion devices that simulate smartwatch placement. The sensors collect acceleration (X, Y, Z axes) and angular velocity while performing key barbell exercises such as:

Bench Press

Deadlift

Overhead Press

Barbell Row

Squat

2. Data Processing

Outlier Filtering: Local Outlier Factor (LOF) was used to eliminate unusual entries

Signal Smoothing: Applied low-pass filters to minimize noise

Temporal Segmentation: Aggregated data across time windows to extract meaningful metrics like mean and standard deviation

Frequency Transformation: Leveraged Fourier Transforms to identify cyclic patterns in motion data, enabling repetition detection

3. Feature Engineering

PCA: Principal Component Analysis reduced dimensionality while preserving essential motion signals

K-Means Clustering: Grouped similar movement types to differentiate exercises with overlapping features

Scalar Magnitudes: Calculated overall motion intensity using orientation-invariant values from sensor readings

4. Model Training
Machine learning models were trained to execute three primary tasks:

Exercise Classification: Random Forest achieved 98.5% accuracy in identifying exercises

Repetition Counting: Implemented peak detection to count reps with ~95% accuracy

Form Error Detection: Trained dedicated models to recognize incorrect form, e.g., poor bench press technique

5. Results

Exercise Recognition Accuracy: 98.5%

Repetition Count Error Margin: ~5%

Form Detection Accuracy: 98.5%

Key Files

src/data/make_dataset.py: Converts raw data into structured format

src/features/build_features.py: Creates machine learning features

src/models/train_model.py: Model training and evaluation pipeline

src/visualization/visualize.py: Generates visual interpretations of the results
