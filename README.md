# python
Assignment 3
import pandas as pd
import matplotlib.pyplot as plt
try:
    df = pd.read_csv('sales_data.csv')
except FileNotFoundError:
    print("❌ Error: 'sales_data.csv' not found. Make sure the file is in the same folder.")
    exit()
df['Date'] = pd.to_datetime(df['Date'], errors='coerce')
df = df.dropna(subset=['Date'])
print("📊 First 5 Records:\n", df.head())
print("\n📈 Summary Statistics:\n", df.describe())
product_sales = df.groupby('Product')['Sales'].sum().sort_values(ascending=False)
print("\n💰 Total Sales per Product:\n", product_sales)
region_quantity = df.groupby('Region')['Quantity'].sum().sort_values(ascending=False)
print("\n📦 Quantity Sold per Region:\n", region_quantity)
df.set_index('Date', inplace=True)
monthly_sales = df.resample('M')['Sales'].sum()
print("\n📅 Monthly Sales:\n", monthly_sales)
plt.figure(figsize=(10, 5))
monthly_sales.plot(marker='o', color='green', linestyle='-')
plt.title('📈 Monthly Sales Trend')
plt.xlabel('Month')
plt.ylabel('Total Sales')
plt.grid(True)
plt.tight_layout()
plt.show()
