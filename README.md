# CARD SHOE ANALYZER - User Manual

## Overview

The **CARD SHOE ANALYZER** is a statistical tool designed to detect alterations in Casino Card
Shoes (6-deck shoes containing 312 cards). This program uses advanced statistical
methods including Chi-squared tests, Z-tests, and anomaly detection to identify if a shoe has
been tampered with.

## What's New in Version 1.0.1

- **Enhanced file format support**: Now handles variable sample sizes automatically
- **Flexible data loading**: No longer requires M,N headers in files (calculated dynamically)
- **Improved analysis**: Works with samples of different sizes within the same dataset
- **Better compatibility**: Supports both legacy format files and new flexible formats

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

The program now supports **two file formats** for maximum flexibility:

##### Format 1: Legacy Format (with M N header)
```
[M] [N]
AC AD AH AS 2C 2D 2H 2S 3C 3D 3H 3S 4C 4D 4H 4S 5C 5D 5H 5S 6C 6D 6H 6S 7C 7D 7H 7S 8C 8D 8H 8S 9C 9D 9H 9S TC TD TH TS JC JD JH JS QC QD QH QS KC KD KH KS
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  2  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
```

##### Format 2: Flexible Format (NEW - no M N header required)
```
AC AD AH AS 2C 2D 2H 2S 3C 3D 3H 3S 4C 4D 4H 4S 5C 5D 5H 5S 6C 6D 6H 6S 7C 7D 7H 7S 8C 8D 8H 8S 9C 9D 9H 9S TC TD TH TS JC JD JH JS QC QD QH QS KC KD KH KS
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  2  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 2  1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
```

**Key Features of the New Format:**
- **No M N header required**: The program automatically detects the number of samples
- **Variable sample sizes**: Each sample can have a different total number of cards
- **Automatic calculation**: Total observations are calculated dynamically
- **Backward compatibility**: Still works with legacy format files

#### File Structure Explanation

**Header Line (Required)**: Card names in exact order
- Must contain exactly 52 card names in the standard order shown above

**Sample Data Lines**: Each line represents one sample session
- Each number corresponds to how many times that card (from header) appeared
- Sample lines can have different totals (variable sample sizes)
- The program automatically calculates total observations across all samples

#### Card Naming Convention

Cards are represented as: `[Value][Suit]`
- **Values**: A, 2, 3, 4, 5, 6, 7, 8, 9, T, J, Q, K
- **Suits**: C=Clubs, D=Diamonds, H=Hearts, S=Spades

Examples: 'AC' = Ace of Clubs, 'TH' = Ten of Hearts, 'KS' = King of Spades

#### Example File Content (New Flexible Format)

```
AC AD AH AS 2C 2D 2H 2S 3C 3D 3H 3S 4C 4D 4H 4S 5C 5D 5H 5S 6C 6D 6H 6S 7C 7D 7H 7S 8C 8D 8H 8S 9C 9D 9H 9S TC TD TH TS JC JD JH JS QC QD QH QS KC KD KH KS
 1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  2  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
 2  1  0  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1  1
```

**Reading this example:**
- **Header line**: Shows all 52 card types in order
- **Sample 1**: 52 total cards observed (all cards appeared exactly once)
- **Sample 2**: 51 total cards observed (AD appeared 0 times, 5D appeared 2 times, others once)
- **Sample 3**: 52 total cards observed (AC appeared 2 times, AH appeared 0 times, others once)

**Key improvement**: Notice how each sample can have different totals (52, 51, 52 cards), and the program automatically handles this variation.

### Step 2: Run the Program

1. shoe_analyzer.exe (Windows version)
2. shoe_analyzer (Linux version)

### Step 3: Analyze Your Casino Data

1. **Choose Option 4** from the main menu: "Analyze Sample File"

2. **Enter your filename** when prompted (e.g., 'casino.txt')

3. **Review the results** - The program will show:
   - Sample size information (including variable size detection)
   - Overall Chi-squared analysis
   - Individual card analysis with significance levels
   - Summary statistics
   - Final assessment

### Step 4: Understanding the Results

The program now provides enhanced information about your data:

#### Sample Information Display
- **Total samples**: Number of casino sessions analyzed
- **Total observations**: Total cards analyzed across all sessions
- **Average sample size**: Mean cards per session
- **Sample size range**: Shows if you have variable session sizes (e.g., "min=45, max=67 cards per sample")

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

For reliable results with the new flexible format:
- **Minimum total observations**: 5,000 total cards across all samples
- **Recommended approach**: 20-50 casino sessions with varying sample sizes
- **Example scenarios**:
  - 50 sessions averaging 100 cards each = 5,000 total observations ✓
  - 25 sessions with 150-250 cards each = 4,375-6,250 total observations ✓
  - 100 sessions with 50-75 cards each = 5,000-7,500 total observations ✓

### How to Collect Casino Data

1. **Observe multiple sessions** at the same table/shoe
2. **Record every card** that appears in each session
3. **Count occurrences** of each card type per session
4. **Don't worry about session length**: Each session can have different numbers of cards
5. **Format the data** according to the file format above

### Important Notes

- **Variable session sizes are now supported**: You don't need equal-length sessions
- **Larger total sample sizes provide more reliable results**: Focus on total observations
- **The program automatically handles calculations**: No need to manually compute M×N
- **Focus on data quality**: Ensure accurate card counting within each session

---

## Testing Features (Optional)

The program includes testing capabilities for validation:

### Option 1: Set Manual M and N
Configure sample parameters for test file generation. **Note**: This still uses fixed sample sizes for generated test files to maintain consistency in testing scenarios.

### Option 2: Generate Normal Shoe File
Creates 'normal.txt' with data from an unaltered 6-deck shoe (for testing).

### Option 3: Generate Altered Shoe File  
Creates 'altered.txt' with data from a deliberately modified shoe (for testing).

These features help you understand how the program works, but **your main focus
should be Option 4 for analyzing real casino data**.

---

## Migration from Previous Versions

If you have existing data files from previous versions:

### Files with M N Headers
- **No changes needed**: Your existing files will work exactly as before
- The program automatically detects and handles the legacy format

### Files without M N Headers
- **Now supported**: Just ensure you have the card header line
- The program will automatically count samples and calculate totals

### Upgrading Your Workflow
- **Keep using your current files**: Full backward compatibility maintained
- **Consider new format for new data**: Eliminates need to manually calculate M and N
- **Mix formats if needed**: You can use both formats with the same version of the program

---
