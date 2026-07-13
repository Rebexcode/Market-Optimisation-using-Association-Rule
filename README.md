# Market Optimisation using Association Rule Learning

This project demonstrates **Market Basket Analysis** using **Association Rule Learning** techniques in Python.  
The repository contains two notebook implementations:

- **Apriori** (`apriori.ipynb`)
- **Eclat-style workflow** (`eclat.ipynb`, implemented using `apyori`)

The goal is to identify product combinations that are frequently purchased together, and to extract actionable insights for retail decision-making such as product placement, cross-selling, and promotion strategy.

## Table of Contents

1. [Project Overview](#project-overview)  
2. [Dataset](#dataset)  
3. [Methods Implemented](#methods-implemented)  
4. [Repository Structure](#repository-structure)  
5. [Installation and Requirements](#installation-and-requirements)  
6. [How to Run](#how-to-run)  
7. [Implementation Details](#implementation-details)  
8. [Sample Output Interpretation](#sample-output-interpretation)  
9. [Business Use Cases](#business-use-cases)  
10. [Limitations](#limitations)  
11. [Possible Improvements](#possible-improvements)  
12. [License](#license)

## Project Overview

Market Basket Analysis is a data mining technique used to discover relationships between items in transaction data.

In this project:

- Transaction records are loaded from a supermarket basket dataset.
- Data is transformed into a list-of-transactions format suitable for rule mining.
- Association rules are generated using configurable thresholds.
- Results are organized in tabular form using `pandas` for easier interpretation.

The notebooks are intended to be educational and easy to follow for beginners learning association rule mining.

## Dataset

The code expects a CSV file named:

`Market_Basket_Optimisation.csv`

Expected structure (as used in the notebooks):

- **7501 transactions** (rows)
- Up to **20 items per transaction** (columns)
- No explicit header row (loaded with `header=None`)

Example loading logic in the notebooks:

- Read CSV as a raw matrix
- For each row, convert all item entries to strings
- Build a Python list where each element is one transaction

## Methods Implemented

### 1) Apriori (`apriori.ipynb`)

The Apriori notebook uses the `apyori` package to generate association rules with:

- `min_support = 0.003`
- `min_confidence = 0.2`
- `min_lift = 3`
- `min_length = 2`
- `max_length = 2`

The resulting rules are converted into a DataFrame with columns:

- Left Hand Side
- Right Hand Side
- Support
- Confidence
- Lift

Rules are then sorted by descending **Lift** to prioritize stronger associations.

### 2) Eclat-style workflow (`eclat.ipynb`)

The Eclat notebook follows a similar mining flow and threshold setup via `apyori`.  
Output is presented as pairwise item relationships with support scores.

In this notebook, results are organized into a DataFrame with columns:

- Product 1
- Product 2
- Support

The table is sorted by descending **Support** to highlight the most frequently co-occurring item pairs.

## Repository Structure

```text
Market-Optimisation-using-Association-Rule/
├── apriori.ipynb
├── eclat.ipynb
├── README.md
└── LICENSE
```

## Installation and Requirements

### Requirements

- Python 3.x
- Jupyter Notebook or Google Colab
- Required Python packages:
  - `pandas`
  - `numpy`
  - `matplotlib`
  - `apyori`

### Install dependencies

```bash
pip install pandas numpy matplotlib apyori
```

## How to Run

### Option A: Google Colab

1. Open `apriori.ipynb` or `eclat.ipynb` in Colab.
2. Upload `Market_Basket_Optimisation.csv` to the Colab runtime.
3. Run cells from top to bottom.

### Option B: Local Jupyter environment

1. Clone the repository:
   ```bash
   git clone https://github.com/Rebexcode/Market-Optimisation-using-Association-Rule.git
   cd Market-Optimisation-using-Association-Rule
   ```
2. Install dependencies:
   ```bash
   pip install pandas numpy matplotlib apyori
   ```
3. Place `Market_Basket_Optimisation.csv` in the project root.
4. Launch Jupyter:
   ```bash
   jupyter notebook
   ```
5. Open and run `apriori.ipynb` or `eclat.ipynb`.

## Implementation Details

### Data preprocessing

Both notebooks preprocess transactions using:

- `pd.read_csv(..., header=None)`
- Nested loops to iterate rows and columns
- Conversion of all values to strings for algorithm compatibility

### Rule generation

Rules are generated using `apyori.apriori(...)` with threshold filtering.  
These thresholds control the quality and quantity of discovered rules:

- **Support**: how often item combinations appear
- **Confidence**: conditional likelihood of RHS given LHS
- **Lift**: strength of rule relative to random co-occurrence

### Result inspection and formatting

Custom helper logic is used to extract rule components and metrics into structured DataFrames, making the output easier to rank and compare.

## Sample Output Interpretation

Some observed associations include item pairs such as:

- herb & pepper → ground beef
- pasta → escalope
- whole wheat pasta → olive oil
- light cream → chicken

How to interpret:

- Higher **support** means the pair is more common overall.
- Higher **confidence** means stronger predictive reliability.
- Higher **lift** (> 1) indicates positive association beyond chance.

For practical prioritization, lift is often preferred when selecting rules for decision-making.

## Business Use Cases

Insights from this project can support:

1. **Shelf layout optimization**  
   Place associated products nearby to increase basket size.

2. **Cross-sell recommendations**  
   Suggest likely companion items during checkout.

3. **Promotion and bundling strategy**  
   Design bundle offers based on frequent co-purchases.

4. **Inventory planning**  
   Improve forecasting for linked-demand products.

## Limitations

- Results depend heavily on chosen thresholds.
- Only pairwise rules are retained (`min_length=2`, `max_length=2`).
- No advanced validation or holdout evaluation is included.
- The notebooks are exploratory and not packaged as production pipelines.

## Possible Improvements

- Add parameter tuning for support/confidence/lift.
- Compare true Eclat implementation against Apriori results.
- Include visual analytics (top rules, support-confidence plots).
- Add reusable Python modules/scripts outside notebooks.
- Add unit tests and data validation checks.
- Extend to multi-item rule lengths (>2).

## License

This project is licensed under the MIT License.  
See the [LICENSE](LICENSE) file for details.
