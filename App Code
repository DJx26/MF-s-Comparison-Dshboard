app_code = '''
import streamlit as st
import pandas as pd
import requests
import matplotlib.pyplot as plt

st.set_page_config(page_title="Top Mutual Funds", layout="wide")
st.title("🏆 Top 6 Mutual Funds - FundPulse India")

@st.cache_data
def fetch_data():
    url = "https://www.moneycontrol.com/mutual-funds/performance-tracker/returns/large-cap-fund.html"
    headers = {"User-Agent": "Mozilla/5.0"}
    response = requests.get(url, headers=headers)
    tables = pd.read_html(response.text)
    df = tables[0]
    df.columns = df.columns.droplevel(0) if isinstance(df.columns, pd.MultiIndex) else df.columns
    df.columns = df.columns.str.strip()
    df = df.dropna()
    return df

df = fetch_data()

return_col = None
for col in df.columns:
    if "%" in col or "Return" in col or "1Y" in col:
        return_col = col
        break

if return_col is None:
    st.error("❌ Couldn't find a returns column.")
    st.write("Columns found:", df.columns.tolist())
else:
    df = df.rename(columns={return_col: "Return"})
    df["Return"] = df["Return"].astype(str).str.replace('%', '', regex=False)
    df["Return"] = pd.to_numeric(df["Return"], errors='coerce')
    top_funds = df.sort_values("Return", ascending=False).head(6).reset_index(drop=True)

    st.subheader("📈 Top 6 Mutual Funds by Return")
    st.dataframe(top_funds[["Scheme Name", "Return"]])

    st.subheader("📊 Return Comparison Chart")
    fig, ax = plt.subplots(figsize=(10, 5))
    ax.bar(top_funds["Scheme Name"], top_funds["Return"], color='skyblue')
    ax.set_ylabel("Return (%)")
    ax.set_title("Top 6 Mutual Funds")
    plt.xticks(rotation=45, ha='right')
    st.pyplot(fig)
'''

# 🛠️ Write the app code to a file (outside the triple quotes!)
with open("mutual_fund_app.py", "w") as f:
    f.write(app_code)
