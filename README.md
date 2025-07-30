# CARD SHOE ANALYZER - User Manual

## Overview

The **CARD SHOE ANALYZER** is a statistical tool designed to detect alterations in Casino Card
Shoes (6-deck shoes containing 312 cards). This program uses advanced statistical
methods including Chi-squared tests, Z-tests, and anomaly detection to identify if a shoe has
been tampered with.

## What Does This Program Do?

The analyzer examines card frequency distributions across multiple samples to detect:
- **Removed cards**: Cards that appear less frequently than expected
- **Added cards**: Cards that appear more frequently than expected  
- **Statistical anomalies**: Unusual patterns that indicate manipulation

## Primary Use Case: Analyzing Real Casino Data

While the program can generate test files, **its main purpose is to analyze real card samples
collected from casino play**. You collect card data from actual casino sessions and the program
tells you if the shoe appears altered.

---

## How to Use the Program

### Step 1: Prepare Your Casino Data File

Before using the analyzer, you need to create a text file containing your card samples from casino
play. This file should be named something like 'casino.txt' or 'my_samples.txt'.

#### File Format Requirements

Your file must follow this exact format:

[M] [N]					                                                                                                                                                                                            																																										          
AC AD AH AS 2C 2D 2H 2S 3C 3D 3H 3S 4C 4D 4H 4S 5C 5D 5H 5S 6C 6D 6H 6S 7C 7D 7H 7S 8C 8D 8H 8S 9C 9D 9H 9S TC TD TH TS JC JD JH JS QC QD QH QS KC KD KH KS										                                                                                       
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       
 1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  2  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       

**Structure:**
- **Line 1**: Two numbers: 'M' (number of samples) and 'N' (sample size)
- **Line 2**: Card headers - exactly 52 card names in order
- **Lines 3 to M+2**: Sample data - each line contains 52 numbers (one per card)

**Important**: Each number in the sample data lines corresponds to the card directly above it in the header line.

#### Card Naming Convention

Cards are represented as: `[Value][Suit]`
- **Values**: A, 2, 3, 4, 5, 6, 7, 8, 9, T, J, Q, K
- **Suits**: C=Clubs, D=Diamonds, H=Hearts, S=Spades

Examples: 'AC' = Ace of Clubs, 'TH' = Ten of Hearts, 'KS' = King of Spades

#### Example File Content

3 50																																															                                                                                                                                                                                                         
AC AD AH AS 2C 2D 2H 2S 3C 3D 3H 3S 4C 4D 4H 4S 5C 5D 5H 5S 6C 6D 6H 6S 7C 7D 7H 7S 8C 8D 8H 8S 9C 9D 9H 9S TC TD TH TS JC JD JH JS QC QD QH QS KC KD KH KS										                                                                                       
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       
 1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  2  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1										                                                                                       

**Reading this example:**
- **3 50**: 3 samples collected, 50 cards observed per sample
- **Header line**: Shows all 52 card types in order
- **Sample 1**: All cards appeared exactly once (normal distribution)
- **Sample 2**: AD appeared 0 times, 5D appeared 2 times, others appeared once
- **Sample 3**: All cards appeared exactly once

**Key point**: The number in each column corresponds to how many times that specific
card (shown in the header) appeared in that sample.

### Step 2: Run the Program

1. shoe_analyzer.exe (Windows version)
2. shoe_analyzer (Linux version)

### Step 3: Analyze Your Casino Data

1. **Choose Option 4** from the main menu: "Analyze Sample File"

2. **Enter your filename** when prompted (e.g., 'casino.txt')

3. **Review the results** - The program will show:
   - Overall Chi-squared analysis
   - Individual card analysis with significance levels
   - Summary statistics
   - Final assessment

### Step 4: Understanding the Results

#### Significance Levels
- **NORMAL**: No statistical evidence of alteration
- **MODERATE**: Moderate evidence of alteration (95% confidence)
- **STRONG**: Strong evidence of alteration (99% confidence)
- **EXTREME**: Extreme evidence of alteration (99.9% confidence)

#### Final Assessment
- **CLEAN SHOE**: No evidence of manipulation
- **POSSIBLY ALTERED**: Some moderate evidence present
- **LIKELY ALTERED**: Strong statistical evidence of tampering
- **DEFINITELY ALTERED**: Extreme evidence of manipulation

#### Export Results

The program will ask if you want to export detailed results to a text file for
record-keeping.

---

## Data Collection Guidelines

### Recommended Sample Parameters

For reliable results:
- **Minimum M×N**: 5,000 total observations
- **Recommended**: M=20-50 samples, N=250-100 cards per sample
- **Example**: 50 samples of 100 cards each = 5,000 total observations

### How to Collect Casino Data

1. **Observe multiple sessions** at the same table
2. **Record every card** that appears in each session
3. **Count occurrences** of each card type per session
4. **Format the data** according to the file format above

### Important Notes

- Larger sample sizes provide more reliable results
- The program will warn you if your sample size is too small
- Focus on collecting data from the same shoe/table for consistency

---

## Testing Features (Optional)

The program includes testing capabilities for validation:

### Option 1: Set Manual M and N
Configure sample parameters for test file generation.

### Option 2: Generate Normal Shoe File
Creates 'normal.txt' with data from an unaltered 6-deck shoe (for testing).

### Option 3: Generate Altered Shoe File  
Creates 'altered.txt' with data from a deliberately modified shoe (for testing).

These features help you understand how the program works, but **your main focus
should be Option 4 for analyzing real casino data**.

---
