# T31 -- Farmer Mandi Price Assistant

### Live Link

https://farmer-mandi-price-assistant-t31.ai.studio/

A dataset-grounded Farmer Mandi Price Assistant developed using **Google AI Studio**. The chatbot answers farmer mandi-price queries using the supplied mandi-price dataset. It supports English, Hindi, Marathi, historical price lookups, recent 7-observation trends, and a simple educational "sell now or wait" interpretation based on the observed historical trend.

> **Important:** This project uses a supplied/synthetic teaching dataset covering historical records from 1 December 2025 to 28 February 2026. It is **not a live mandi-price service** and does not predict future prices.

---

## 1. Project Objective

The objective of this project is to build a working Farmer Mandi Price Assistant that can:

- Answer mandi-price queries using only the supplied dataset.
- Identify the relevant commodity, market, and date.
- Provide the appropriate mandi price.
- State the exact date of the data used.
- Calculate a recent 7-observation price trend when requested.
- Provide a simple educational "sell now or wait" explanation based on the observed trend.
- Handle English, Hindi, and Marathi queries.
- Clearly state when a requested commodity-market combination or current/live price is unavailable.
- Avoid inventing or guessing prices.

---

## 2. Dataset

The chatbot uses the supplied mandi-price dataset as its source for price-related information.

### Dataset coverage

| Attribute | Details |
|---|---|
| Records | 3,600 |
| Dates | 1 Dec 2025 -- 28 Feb 2026 |
| Commodities | 10 |
| Markets | 8 |
| State | Maharashtra |
| Columns | 8 |

### Commodities

- Cotton
- Grapes
- Maize
- Onion
- Pomegranate
- Potato
- Soybean
- Tomato
- Tur (Arhar)
- Wheat

### Markets

- Ahmednagar
- Jalgaon
- Lasalgaon
- Nagpur
- Nashik
- Pimpalgaon
- Pune
- Solapur

### Dataset columns

- `date`
- `commodity`
- `market`
- `state`
- `min_price_inr_per_quintal`
- `max_price_inr_per_quintal`
- `modal_price_inr_per_quintal`
- `arrivals_quintal`

The **modal price** is used as the default/general mandi price unless the user specifically asks for the minimum or maximum price.

---

## 3. Key Features

### Latest Available Price

The chatbot identifies the latest available record for the requested commodity and market and returns:

- Modal price
- Exact date of the data
- Relevant market and commodity

The chatbot does not describe historical data as today's live price.

### Historical Price

If a specific date is provided, the chatbot retrieves the matching record for that commodity, market, and date.

### 7-Observation Trend

The project defines the recent "7-day trend" as the **last seven available observations** for the requested commodity-market pair.

The calculation uses modal prices:

**Percentage change**

`(Latest modal price − Starting modal price) / Starting modal price × 100`

Trend classification:

- More than **+2%** → Increasing
- Between **−2% and +2%** → Stable
- Less than **−2%** → Decreasing

The chatbot reports the observations used, starting price, latest price, percentage change, and trend direction.

### Sell Now or Wait

The chatbot provides a simple educational interpretation based on the recent historical trend:

- **Increasing:** waiting may be more favorable based on the recent historical movement.
- **Decreasing:** selling sooner may be more favorable based on the recent historical movement.
- **Stable:** there is no strong historical timing signal.

This is **not a guaranteed forecast or professional agricultural/financial advice**. The dataset cannot determine whether prices will continue to rise or fall.

### Multilingual Support

The chatbot supports:

- English
- Hindi
- Marathi
- Common Hinglish-style queries

### Unavailable Data Handling

When the requested commodity-market-date combination is not present, the chatbot states that the information is unavailable rather than inventing a price.

For current/today requests outside the dataset period, the chatbot clearly distinguishes between unavailable live/current data and the latest historical record.

---

## 4. Technology and Development

The project was developed using **Google AI Studio** and its AI-assisted application development capabilities.

### Technologies Used

- **Google AI Studio** -- application development, AI-assisted coding, prompt/instruction development, and deployment
- **Gemini** -- conversational AI capabilities
- **HTML** -- chatbot interface structure
- **CSS** -- user interface styling
- **JavaScript** -- chatbot interaction and application logic
- **Excel** -- supplied mandi-price dataset and testing/verification files
- **GitHub** -- source-code and project-file management

Google AI Studio was used to develop and refine the chatbot, including its instructions for interpreting user queries, grounding price responses in the supplied dataset, handling multiple languages, calculating recent trends, and providing appropriate unavailable-data responses.

The chatbot's price-related responses are intended to remain grounded in the supplied mandi dataset rather than relying on external live market-price sources.

---

## 5. Development Approach

The chatbot was developed iteratively using Google AI Studio.

The development process included:

1. Preparing and analyzing the supplied mandi-price dataset.
2. Defining the chatbot's expected behaviour and response rules.
3. Developing the chatbot application in Google AI Studio.
4. Creating instructions for commodity, market, date, and price identification.
5. Adding historical-price lookup functionality.
6. Defining the 7-observation trend calculation.
7. Adding the educational "sell now or wait" interpretation.
8. Improving English, Hindi, Marathi, and Hinglish query handling.
9. Adding unavailable-data handling.
10. Testing the chatbot using a structured 20-query test set.
11. Comparing outputs against the supplied dataset.
12. Refining the chatbot based on failed or partial test cases.
13. Re-running the final test set after improvements.

---

## 6. Repository Structure

```text
T31-Farmer-Mandi-Price-Assistant/
│
├── README.md
│
├── data/
│   └── mandi_prices.xlsx
│
├── testing/
│   ├── 20_Query_Initial_Testing.xlsx
│   └── 20_Query_Final_Testing.xlsx
│
├── documentation/
│   ├── Final_Report.pdf
│   └── Submission_Workbook.xlsx
│
├── evidence/
│   ├── 01_latest_price.png
│   ├── 02_historical_price.png
│   ├── 03_seven_day_trend.png
│   ├── 04_sell_or_wait.png
│   ├── 05_hindi_query.png
│   ├── 06_marathi_query.png
│   └── 07_unavailable_query.png
│
├── screenrecording/
│   └── app.mp4
│
└── .gitignore
```

---

## 7. How to Use the Chatbot

### Online version

The deployed chatbot can be accessed through the following Google AI Studio application:

https://farmer-mandi-price-assistant-t31.ai.studio/

Open the link and enter a supported mandi-price query.

### Example queries

```text
What is the latest price of onion in Lasalgaon?

What was the price of wheat in Pune on 15 January 2026?

What is the 7-day trend for tomato in Nashik?

Should I sell or wait for grapes in Nashik?

नागपुर में कपास का सबसे नया भाव कितना है?

नाशिकमध्ये द्राक्षांचा भाव काय आहे?

What is the price of rice in Mumbai?
```

The final query demonstrates unavailable-data handling because rice is not one of the commodities contained in the supplied dataset.

---

## 8. Testing and Verification

The project uses a 20-query test set covering:

- Latest price queries
- Exact historical-date queries
- 7-observation trend queries
- Sell/wait queries
- English queries
- Hindi queries
- Marathi queries
- Hinglish queries
- Unavailable-data cases

### Initial Testing

The initial test file records the problems found during early testing, including failed and partial cases.

File:

`testing/20_Query_Initial_Testing.xlsx`

### Final Testing

After improvements to the chatbot's instructions and application logic, the final test set was re-run.

**Final result: 20/20 Pass**

File:

`testing/20_Query_Final_Testing.xlsx`

---

## 9. Price Verification

Price-bearing test cases were checked against the source dataset.

The verification process checks that:

- The quoted price matches the corresponding dataset record.
- The correct commodity is used.
- The correct market is used.
- The correct date is used.
- No price is invented when a matching record is unavailable.

The complete verification evidence is included in:

`documentation/Submission_Workbook.xlsx`

---

## 10. Improvement Process

The chatbot was iteratively improved based on testing results in Google AI Studio.

Key improvement areas included:

1. Clarifying the distinction between latest historical data and current/live price.
2. Defining a consistent 7-observation trend calculation.
3. Improving trend-direction responses.
4. Adding a clearer educational sell/wait interpretation.
5. Improving Hindi and Marathi commodity/market query handling.
6. Improving unavailable-data responses.
7. Improving the readability and interpretation of chatbot responses.
8. Re-testing the final chatbot using the 20-query test set.

The project documentation contains the AI Use Log and improvement evidence.

---

## 11. Evidence

The `evidence` folder contains screenshots from the working chatbot demonstrating the major required functions.

### Latest price

`01_latest_price.png`

Demonstrates a latest available mandi price with its exact data date.

### Historical price

`02_historical_price.png`

Demonstrates a price lookup for a specified historical date.

### 7-observation trend

`03_seven_day_trend.png`

Demonstrates recent trend calculation and classification.

### Sell or wait

`04_sell_or_wait.png`

Demonstrates the educational trend-based timing explanation.

### Hindi

`05_hindi_query.png`

Demonstrates Hindi query handling.

### Marathi

`06_marathi_query.png`

Demonstrates Marathi query handling.

### Unavailable data

`07_unavailable_query.png`

Demonstrates that the chatbot does not invent prices for unavailable commodity-market combinations.

---

## 12. Responsible AI

The project follows these principles:

- Price-related answers are grounded in the supplied dataset.
- The chatbot does not intentionally invent prices.
- Historical data is not presented as live/current data.
- Test outputs are verified against the source data.
- AI-generated content and development activities are documented through the AI Use Log.
- No real personal or confidential data is used.
- The sell/wait explanation is presented as educational rather than guaranteed financial or agricultural advice.
- The chatbot clearly communicates limitations when information is unavailable.

---

## 13. Limitations

This project has several limitations:

- The dataset is historical/synthetic teaching data rather than a live mandi feed.
- The available dataset ends on 28 February 2026.
- The chatbot cannot provide verified current mandi prices outside the supplied data.
- The trend calculation describes recent historical movement; it is not a forecasting model.
- The sell/wait explanation does not guarantee future prices.
- AI-generated responses can require validation against the underlying dataset.
- A production system would require a verified live data source, timestamps, source identifiers, monitoring, and stronger audit controls.

---

## 14. Recommendation

The Farmer Mandi Price Assistant is suitable as an **educational historical mandi-price and trend assistant** developed using Google AI Studio.

It should not be treated as an autonomous price-prediction or trading system. Any real-world selling decision should consider additional factors such as current local market conditions, quality, arrivals, storage costs, transportation, weather, and verified live market information.

---

## 15. Project Deliverables

The repository contains the major project deliverables:

- Working Google AI Studio chatbot
- Supplied mandi dataset
- Initial 20-query testing results
- Final 20-query testing results
- Price verification evidence
- Final submission workbook
- Final report
- Chatbot screenshots/evidence
- Screen recording
- AI use and improvement documentation
- Project README

---

## 16. Author

**Devarath Nediyirippil**

T31 -- Farmer Mandi Price Assistant

MBA / DSDA - AI Powered Tools Project  
