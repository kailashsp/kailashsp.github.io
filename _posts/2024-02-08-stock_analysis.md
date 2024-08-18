---
title: "Fundamental Analysis of NSE Stocks with Gemini Pro Deployed in Hugging Face Space"
date: 2024-02-08 00:00:00 +0000
categories: [LLM]
tags: [GEMINI, STOCKS]
---

# Fundamental Analysis of NSE Stocks with Gemini Pro Deployed in Hugging Face Space

## Try out the demo: [NSE-stock-picker](https://huggingface.co/spaces/kailashsp/NSE-stock-picker)

Recently I have been reading up about financial management and how to create wealth in the long term. As everyone who starts up, I managed to end up with topic of stocks and the historical trend of almost all exchanges in general to go up. So its easy money right? Well you have to pick the right stock to capitalize on this uptrend. Fundamental analysis is the key here. 

So what's meant by the fundamental analysis of a stock. It revolves around the determining the fair value of a stock after going through its financial statements, balance sheet, the comparison of the stock with its peers in the market, also the future potential and the current trends in the market. 

Choosing stocks can become a complex and laborious task due to the multitude of variables that need to be considered, especially when dealing with a large number of stocks in the process. So to simplify this process of picking stock I have leveraged Gemini-pro to do a fundamental analysis for us and categorize the stock into Low, Medium and High. In my testing the best stocks are categorized into High confidence score.

If you don't want a technical breakdown you can try out the demo in Hugging Face space for free.

**Disclaimer:** The generated results should not be completely relied upon, and it is crucial to conduct thorough research before making any investment decisions. This approach aims to streamline the selection process by filtering through the extensive list of stocks.

## Fundamental Analysis with Gemini Pro: A Step-by-Step Guide

1. **Collecting Stock Data:**
   - We'll use an Excel file containing stock data as our data source.
   - The file includes information such as company names, symbols, and financial ratios.

2. **Generating Stock Fundamentals:**
   - For each stock, we'll generate a document containing its fundamentals.
   - This involves extracting relevant information from the Excel file and cleaning it.
   - We'll use the `generate_document()` function for this purpose.

3. **Integrating Gemini Pro:**
   - We'll use the `LLM` class to interact with the Gemini Pro model.
   - The model takes a prompt as input and generates a JSON response.

4. **Creating the Streamlit Application:**
   - We'll use Streamlit to build a user-friendly interface for our analysis.
   - The app includes a search box for stock selection and displays the analysis results.

## Breaking Down the Code

1. **`search_stocks()` Function:**
   - This function takes a search term as input and returns a list of matching stock symbols.
   - It uses the `stocks` DataFrame to perform the search.

2. **`generate_document()` Function:**
   - This function takes a stock URL as input and generates a Document object.
   - It uses the `UnstructuredURLLoader` class from `langchain_community` to load the URL.
   - The function then applies text cleaning operations to the extracted content.

3. **`stock_analysis_prompt`:**
   - This is a pre-defined prompt that guides Gemini Pro in analyzing the stock.
   - It includes placeholders for the stock name and context (stock fundamentals).

4. **Processing the Results:**
   - The JSON response from Gemini Pro includes a confidence score and a detailed analysis.
   - We display these results in the Streamlit application, along with a link to the stock's Finology page.

## Conclusion

This article demonstrated how to perform fundamental analysis using Gemini Pro and Streamlit. The resulting web application simplifies the process of analyzing stocks and provides insights to aid investment decisions.