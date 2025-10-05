import pandas as pd
import matplotlib.pyplot as plt
try:
    df = pd.read_csv("sales_data.csv", parse_dates=["Date"])
except FileNotFoundError:
    print("Error: sales_data.csv file not found. Please create it first.")
    exit()
 total_revenue = df["Revenue ($)"].sum()
  best_product_row = df.groupby("Product")["Quantity Sold"].sum().idxmax()
best_product_qty = df.groupby("Product")["Quantity Sold"].sum().max()
highest_sales_day_row = df.groupby("Date")["Revenue ($)"].sum().idxmax()
highest_sales_amount = df.groupby("Date")["Revenue ($)"].sum().max()
summary_text = f"""
Total Revenue: ${total_revenue}
Best-Selling Product: {best_product_row} ({best_product_qty} units sold)
Highest Sales Day: {highest_sales_day_row.date()} (Revenue: ${highest_sales_amount})
"""

# Save summary to sales_summary.txt
with open("sales_summary.txt", "w") as f:
    f.write(summary_text.strip())
    print(summary_text)
