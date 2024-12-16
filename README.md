
# Triangular Arbitrage Detection in Forex Market

This project is a **Python-based tool** that identifies **triangular arbitrage opportunities** in the foreign exchange (Forex) market. It fetches historical exchange rates for currency pairs, calculates potential arbitrage opportunities, and saves the results to an in-memory DataFrame, with an option to export to CSV. 

## Features
- Fetches **historical data** for currency pairs from Yahoo Finance using the `yfinance` library.
- Identifies **triangular arbitrage** opportunities based on the exchange rates of three currency pairs.
- Provides **real-time analysis** by iterating over historical data to find and display arbitrage opportunities.
- Saves detected opportunities in a **DataFrame**, which can be accessed in memory, and optionally exported to a CSV file.

## Triangular Arbitrage Overview

**Triangular arbitrage** involves exploiting price discrepancies between three related currency pairs, such as:
- EUR/USD
- USD/JPY
- EUR/JPY

The code calculates the **cross rate** for EUR/JPY using EUR/USD and USD/JPY, and compares it with the actual EUR/JPY market rate. If a discrepancy exists that exceeds a certain threshold, it is flagged as an arbitrage opportunity.

### Arbitrage Formula

The cross rate is calculated using the following formula:
```
Calculated_EURJPY = EUR/USD * USD/JPY
```

If the difference between the calculated EUR/JPY and the actual EUR/JPY exceeds 0.01, an arbitrage opportunity is detected.

## Prerequisites

To run this project, you'll need the following installed on your system:
- **Python 3.x**
- **pandas** for data manipulation.
- **yfinance** for fetching exchange rate data.
  
You can install the required libraries using the following command:
```bash
pip install pandas yfinance
```

## How to Run the Code

1. **Clone the repository** or download the project files.
   
2. Install the required dependencies:
   ```bash
   pip install pandas yfinance
   ```

3. Run the script:
   ```bash
   python triangular_arbitrage.py
   ```

4. The program will:
   - Fetch historical exchange rate data for **EUR/USD**, **USD/JPY**, and **EUR/JPY**.
   - Calculate triangular arbitrage opportunities over the past year.
   - Display the detected opportunities in the terminal.

5. **Optional:** The detected arbitrage opportunities are saved in-memory as a DataFrame. You can also export them to a CSV file:
   ```bash
   Opportunities saved to 'arbitrage_opportunities.csv'.
   ```

## Code Walkthrough

### 1. `fetch_historical_data()`
This function fetches **historical exchange rate data** from Yahoo Finance using the `yfinance` library. It takes in a currency pair (e.g., `EURUSD`) and returns a DataFrame containing the historical close prices for the specified period.

### 2. `calculate_triangular_arbitrage()`
This function takes in the exchange rates for **EUR/USD**, **USD/JPY**, and **EUR/JPY** on a specific date. It calculates the theoretical EUR/JPY rate using the EUR/USD and USD/JPY rates, and compares it with the actual EUR/JPY rate to determine whether an arbitrage opportunity exists.

### 3. `list_past_arbitrage_opportunities()`
This is the main function that:
- Fetches historical data for the three currency pairs.
- Joins the datasets to align exchange rates by date.
- Iterates through the historical data to detect and store arbitrage opportunities.
- Saves the detected opportunities in a DataFrame (`stored_opportunities_df`) and optionally exports them to a CSV file.

### Sample Output

When the script runs, you will see output similar to this in the terminal:
```
Fetching historical data...
Data for EURUSD:
             Close
Date              
2023-01-02  1.0658
2023-01-03  1.0617
...
Joining historical data...
Joined Data (first few rows):
            EURUSD=X  USDJPY=X  EURJPY=X
Date                                   
2023-01-02    1.0658   130.760   139.30
2023-01-03    1.0617   131.120   139.10
...
Detected Arbitrage Opportunities:
          Date  Calculated_EURJPY  Actual_EURJPY Opportunity
0   2023-10-11         157.616904       157.598999         YES
1   2023-10-12         158.340050       158.328995         YES
...
```

### Saving Results to CSV

If you want to save the detected opportunities to a CSV file, they will be saved as:
```bash
arbitrage_opportunities.csv
```

The CSV file will contain the following columns:
- **Date**: The date of the exchange rates.
- **Calculated_EURJPY**: The theoretical EUR/JPY cross rate based on EUR/USD and USD/JPY.
- **Actual_EURJPY**: The actual EUR/JPY rate from the market.
- **Opportunity**: Whether an arbitrage opportunity was detected (YES/NO).

## Future Enhancements

- **Live Data Integration**: Extend the script to work with real-time exchange rates, allowing users to act on arbitrage opportunities as they emerge.
- **Alert System**: Integrate **SMS, WhatsApp, or Telegram notifications** to alert traders when an arbitrage opportunity is detected.
- **Customization**: Allow users to customize the currency pairs they want to monitor for arbitrage opportunities.
  
## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

```

---
