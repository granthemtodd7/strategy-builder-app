streamlit
yfinance
pandas
numpy
import streamlit as st
import pandas as pd
import yfinance as yf

st.set_page_config(page_title="Strategy Builder (MVP)", layout="wide")
st.title("Strategy Builder — Hello App")

st.markdown("""
This is the starting point. In later steps you'll:
- add indicators & parameters
- define entry/exit rules
- run backtests & optimization
- get AI suggestions
""")

# Simple smoke test UI
col1, col2, col3 = st.columns([2,1,1])
with col1:
    symbol = st.text_input("Symbol", "SPY")
with col2:
    start = st.text_input("Start (YYYY-MM-DD)", "2018-01-01")
with col3:
    interval = st.selectbox("Interval", ["1d", "1wk", "1mo"], index=0)

if st.button("Fetch data"):
    try:
        df = yf.download(
            symbol,
            start=start,
            interval=interval,
            auto_adjust=True,
            progress=False,
            threads=False,
        )
        if df is None or df.empty:
            st.error("No data returned. Try a later start date or a different symbol.")
        else:
            st.success(f"Downloaded {len(df)} bars for {symbol}")
            st.dataframe(df.tail(10))
            st.line_chart(df["Close"])
    except Exception as e:
        st.exception(e)

st.caption("© Educational use only. Backtests are not predictive of future results.")
