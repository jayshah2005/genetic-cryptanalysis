# Genetic Cryptanalysis Project

[![Java](https://img.shields.io/badge/Java-8+-blue.svg)](https://www.java.com/)
[![Python](https://img.shields.io/badge/Python-3.7+-blue.svg)](https://www.python.org/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

## Overview

This project uses a **Genetic Algorithm** to break Vigenere cipher encryption. It evolves populations of candidate keys to find those that produce decrypted text closest to English language patterns, measured by letter frequency analysis.

**Key Features:**
- GA execution with multiple mutation and crossover operators
- Automated result saving and analysis
- Python-based data visualization
- Comprehensive experimental framework

## Getting Started

### Requirements

- Java 8 or higher
- Python 3.7+ (for data analysis)
- matplotlib (for visualization)
- pandas (for data processing)

Install Python dependencies:

```bash
pip install matplotlib pandas
```

### Runnable Files

All commands run from the project root directory.

#### `src/GA.java`

**Command:** `javac src/*.java && java -cp src GA`  

**Description:** Main GA class for running individual experiments. Modify the `main` method to customize parameters (population size, mutation rate, crossover rate, etc.). Tests various parameter combinations and outputs fitness results to console.

**Runtime:** Varies based on parameters (typically 1-10 minutes per run).

#### `src/experiment.java`

**Command:** `javac src/*.java && java -cp src experiment`  

**Description:** Runs comprehensive experiments across multiple parameter sets. Tests both datasets (Data1.txt and Data2.txt) with different combinations of:
- Mutation rates: 0, 0.1, 0.5
- Crossover rates: 0.9, 1.0
- Mutation types: ASCII Mutation
- Crossover types: Two-Point Crossover

Each parameter combination is run 5 times for statistical significance. Results are saved to CSV files in the `Data/` directory.

**Runtime:** ~30-60 minutes depending on hardware.

#### `pythonAnalysis/graph.py`

**Command:** `python pythonAnalysis/graph.py`  

**Description:** Generates fitness evolution graphs from CSV data. Modify the file path in the script to visualize different experimental results. Creates line plots showing fitness progression across generations for different parameter combinations.

## Project Structure

```
genetic-cryptanalysis/
├── Assign2_Attachments/        # Encrypted datasets
│   ├── Data1.txt              # 26-char key ciphertexts
│   └── Data2.txt              # 40-char key ciphertexts
├── src/                        # Source code
│   ├── GA.java                # Main GA implementation
│   ├── experiment.java        # Comprehensive experiment runner
│   ├── chromosome.java        # Chromosome representation
│   ├── Evaluation.java        # Fitness functions & decryption
│   ├── FitnessComparator.java # Comparator for sorting
│   └── csvWriter.java         # Data logging utilities
├── Data/                       # Experimental results (CSV files)
│   ├── averages*.csv          # Average fitness per generation
│   └── bestAverages*.csv       # Best average fitness values
├── graphs/                     # Generated visualization graphs
├── pythonAnalysis/             # Python analysis scripts
│   ├── graph.py               # Graph generation
│   └── test.py                # Testing utilities
└── Final_Report_COSC_3P71_Assignment_1.pdf
```

## Usage

### Running Experiments

Execute the comprehensive experiment suite:

```bash
javac src/*.java && java -cp src experiment
```

**What happens:**
- Loads both datasets (Data1.txt and Data2.txt)
- Runs GA with multiple parameter combinations
- Tests ASCII mutation with two-point crossover
- Saves results to CSV files in `Data/` directory
- Each combination is run 5 times for statistical validity

### Running Individual Tests

For quick testing with custom parameters:

1. Open `src/GA.java`
2. Modify the `main` method parameters:
   - `popSize`: Population size (default: 300)
   - `maxGenSpan`: Maximum generations (default: 100)
   - `k`: Tournament selection sample size (default: 2)
   - `elitePercentage`: Elite preservation rate (default: 0.1)
   - `targetFitness`: Early stopping threshold (default: 0.01)
   - `mutationRates`: Array of mutation rates to test
   - `crossoverRates`: Array of crossover rates to test
3. Compile and run:
   ```bash
   javac src/*.java && java -cp src GA
   ```

### Analyzing Results

Generate graphs from collected data:

1. Open `pythonAnalysis/graph.py`
2. Update the CSV file path to point to your desired data file
3. Run:
   ```bash
   python pythonAnalysis/graph.py
   ```

## Results Interpretation

### Fitness Score

Lower values = better keys (closer to English letter frequencies). The fitness function measures the absolute difference between expected English letter frequencies and the actual frequencies in the decrypted text.

### Mutation Types

- **ASCII Mutation**: Randomly modifies a character in the key by ±2 positions in the alphabet
- **Inverse Mutation**: Inverts a random subsequence of the key

### Crossover Types

- **Uniform Crossover**: Each gene position is independently swapped between parents with 50% probability
- **Two-Point Crossover**: Swaps a contiguous segment between two randomly selected points

### Datasets

- **Data1.txt**: Shorter 26-character keys
- **Data2.txt**: Longer 40-character keys

### Parameter Combinations Tested

The experiment class tests:
- **Mutation Rates**: 0, 0.1, 0.5
- **Crossover Rates**: 0.9, 1.0
- **Runs per combination**: 5 (for statistical significance)

### Output Files

Results are saved in the `Data/` directory:
- `averages*.csv`: Average fitness values tracked every 10 generations
- `bestAverages*.csv`: Best average fitness across all runs for each parameter combination

File naming convention:
- `ASCIIMutation` or `InverseMutation` (mutation type)
- `TwoPointCrossover` or `UniformCrossover` (crossover type)
- `1` or `2` (dataset number)

### Sample Output

Experiment results include:
- Best chromosomes (decrypted keys) printed to console
- Fitness evolution tracked every 10 generations
- CSV files with detailed fitness data
- Graphs showing comparative performance (in `graphs/` directory)

## Technical Details

### Genetic Algorithm Components

- **Selection**: Tournament selection with configurable sample size (k)
- **Crossover**: Uniform or Two-Point crossover with configurable rate
- **Mutation**: ASCII or Inverse mutation with configurable rate
- **Elitism**: Top percentage of population preserved each generation
- **Fitness**: Letter frequency analysis comparing decrypted text to English language patterns

### Key Classes

- `GA`: Main genetic algorithm implementation
- `chromosome`: Represents a candidate key solution
- `Evaluation`: Contains fitness function and encryption/decryption methods
- `experiment`: Automated experiment runner with statistical analysis
- `csvWriter`: Utility for logging experimental data

---

*Built by Jay Shah for Brock University (COSC 3P71)*
