# Stock Market Indexes Analysis and Normal VaR Back-Testing

In this project, I woud like to use various indexes historical data to implement a back-testing framework of a given Value-at-Risk of chosen confidence and time-frame, identifying various kind of VaR breaches.

I would like to implement a streamlined approach that generates returns, standard deviations and Normal Value-at-risks calculation, which can be deployed for different indexes, and can be adjusted for different time period, chosen at the reader's discretion.

I also want to generate some useful graphs for each index, that will help the reader the context behind the choice of the Normal VaR back-testing.

## Sections:



### 1. Loading and Displaying Indexes Data:

- ###### 1.1 Setting up the Environment  
    - Importing the Relevant Libraries
- ###### 1.2 Data Pre-processing
    - The Loading Index Data: A Streamlined Function 

- ###### 1.3 Index Data Displaying 
    - S&P 500 Pricing Data
    - CAC 40 Pricing Data
    - FTSE 100 Pricing Data
    - FTSE MIB Pricing Data
    - DAX 30 Pricing Data
    
### 2. Indexes Analysis, VaR Back-testing & Breaches Discovery:

- ###### 2.1 The Data Generation Sub-Classes:
    - Returns
    - Standard Deviations
    - Index Graphs
    - Returns Graphs
    - VaR Backtesting
    
### 3. Final Results:


- ###### 3.1 Complementary Graphs 
    - S&P 500 vs Major European Stock Market Indexes (2000-2024) 
    - Indexes Returns Empirical Statistical Distributions 
    - Indexes Returns Series


- ###### 3.2 VaR Back-Testing
    - S&P 500 VaR Breaches Summary Table
    - CAC 40 VaR Breaches Summary Table
    - FTSE 100 VaR Breaches Summary Table
    - FTSE MIB VaR Breaches Summary Table
    - DAX 30 VaR Breaches Summary Table

- ###### 3.3 Forward Returns, Predicted VaR and Index Level: All in one Graph

    - S&P 500 VaR Chart  
    - CAC 40 VaR Chart  
    - FTSE 100 VaR Chart 
    - FTSE MIB VaR Chart   
    - DAX 30 VaR Chart 

- ###### 3.4 Conclusions

Please go to the Jupyter notebook if you want to view the full code!
