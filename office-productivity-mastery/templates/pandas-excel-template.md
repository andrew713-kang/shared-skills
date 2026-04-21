# Pandas Excel Modeling Template

```python
import pandas as pd
import numpy as np
from datetime import datetime

def create_financial_model():
    # 1. Define Assumptions (Input)
    assumptions = {
        'Growth Rate': 0.15,
        'COGS Margin': 0.40,
        'OpEx Ratio': 0.30,
        'Tax Rate': 0.20,
        'Start Year': 2024
    }

    years = [2024, 2025, 2026, 2027, 2028]

    # 2. Build DataFrame
    data = {
        'Revenue': [1000 * (1 + assumptions['Growth Rate'])**i for i in range(5)],
    }
    df = pd.DataFrame(data, index=years)

    # 3. Calculate Metrics
    df['COGS'] = df['Revenue'] * assumptions['COGS Margin']
    df['Gross Profit'] = df['Revenue'] - df['COGS']
    df['OpEx'] = df['Revenue'] * assumptions['OpEx Ratio']
    df['EBIT'] = df['Gross Profit'] - df['OpEx']
    df['Tax'] = df['EBIT'] * assumptions['Tax Rate']
    df['Net Income'] = df['EBIT'] - df['Tax']

    # 4. Export to Excel with Formatting
    output_path = "Financial_Model_v1.xlsx"
    writer = pd.ExcelWriter(output_path, engine='xlsxwriter')

    # Input Sheet
    pd.DataFrame.from_dict(assumptions, orient='index', columns=['Value']).to_excel(writer, sheet_name='Inputs')

    # Model Sheet
    df.to_excel(writer, sheet_name='Model')

    # Formatting
    workbook = writer.book
    worksheet = writer.sheets['Model']

    # Define formats
    money_fmt = workbook.add_format({'num_format': '$#,##0'})
    bold_fmt = workbook.add_format({'bold': True})

    # Apply formats
    worksheet.set_column('B:G', 15, money_fmt)
    worksheet.set_row(0, None, bold_fmt)

    writer.close()
    print(f"Model saved to {output_path}")

if __name__ == "__main__":
    create_financial_model()
```

## Key Elements

1.  **Separation of Concerns**: Assumptions (Input) vs Logic (Calc).
2.  **Scalability**: Use Loops/Vectorization for recurring years.
3.  **Professional Formatting**: Use `xlsxwriter` to format cells as Currency/Bold.
