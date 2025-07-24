%%writefile run_ngrok.py
from pyngrok import ngrok
import subprocess
import os
import time
ngrok.kill()

ngrok.set_auth_token("write ur  ngrok token ")
 
STREAMLIT_PORT = 8501
public_url = ngrok.connect(STREAMLIT_PORT, "http")
print(f"Your public URL is: {public_url}")
os.environ["BROWSER"] = "none"
time.sleep(2)
subprocess.run(["streamlit", "run", "mutual_fund_app.py"])
