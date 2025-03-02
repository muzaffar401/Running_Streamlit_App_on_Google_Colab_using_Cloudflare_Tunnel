# Running Streamlit App on Google Colab using Cloudflare Tunnel

## Introduction
This guide explains how to run a **Streamlit** app on **Google Colab** using **Cloudflare Tunnel**. Cloudflare Tunnel provides a secure way to expose localhost to the internet without port forwarding.

### Why Use Cloudflare Tunnel?
Cloudflare Tunnel allows you to securely access your local web application (like a Streamlit app) from anywhere without exposing your real IP address. It is an alternative to tools like **Ngrok** and **LocalTunnel**, but offers better security and stability.

## Step 1: Open Google Colab
1. Open [Google Colab](https://colab.research.google.com/).
2. Create a new notebook:
   - Click on **File > New Notebook**.

## Step 2: Install Streamlit
Streamlit is not installed by default in Colab, so we need to install it.
Run the following command:
```python
!pip install streamlit
```

To verify the installation, run:
```python
!streamlit --version
```
If a version number appears, Streamlit is installed successfully.

## Step 3: Create a Simple Streamlit App
Create a basic Streamlit app by writing the following code in a cell:
```python
%%writefile app.py
import streamlit as st

st.title("🎈 Streamlit App on Google Colab")
st.write("🚀 Congratulations! Your first Streamlit app is running!")

# User input example
name = st.text_input("What's your name?")
if name:
    st.write(f"Hello, {name}! 👋")
```

This command writes a file `app.py` containing our Streamlit app.
To check the file content, run:
```python
!cat app.py
```

## Step 4: Install Cloudflare Tunnel
Download and set up Cloudflare Tunnel by running these commands:
```python
!wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -O cloudflared
!chmod +x cloudflared
```
### Explanation:
- `wget` downloads the latest Cloudflare Tunnel executable.
- `chmod +x` makes it executable.

To verify the installation, run:
```python
!./cloudflared --version
```
If a version is displayed, Cloudflare is ready to use.

## Step 5: Run the Streamlit App with Cloudflare Tunnel
Start the Streamlit app and expose it using Cloudflare Tunnel:
```python
!streamlit run app.py & ./cloudflared tunnel --url http://localhost:8501
```
### Explanation:
- `streamlit run app.py` starts the Streamlit app.
- `&` allows the command to run in the background.
- `./cloudflared tunnel --url http://localhost:8501` creates a public URL.

After running the command, you will see an output like:
```
You can now view your Streamlit app in your browser.
https://random-url.trycloudflare.com
```
Click the generated URL to access your Streamlit app.

## Troubleshooting
### 1. Streamlit Not Installed?
Check with:
```python
!streamlit --version
```
If not installed, rerun:
```python
!pip install streamlit
```

### 2. Cloudflare Not Installed?
Check with:
```python
!./cloudflared --version
```
If not installed, rerun:
```python
!wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -O cloudflared
!chmod +x cloudflared
```

### 3. Public URL Not Opening?
- Restart Colab and rerun all steps.
- Disable VPN if using one.

## Summary of Commands
1. **Install Streamlit:**
   ```python
   !pip install streamlit
   ```
2. **Create Streamlit App:**
   ```python
   %%writefile app.py
   import streamlit as st
   st.title("🎈 Streamlit App on Google Colab")
   ```
3. **Install Cloudflare Tunnel:**
   ```python
   !wget https://github.com/cloudflare/cloudflared/releases/latest/download/cloudflared-linux-amd64 -O cloudflared
   !chmod +x cloudflared
   ```
4. **Run Streamlit App with Cloudflare:**
   ```python
   !streamlit run app.py & ./cloudflared tunnel --url http://localhost:8501
   ```
5. **Access your app:** Open the generated `trycloudflare.com` URL.

## Conclusion
You have successfully set up and run a Streamlit app on Google Colab using Cloudflare Tunnel. If you encounter issues, try restarting Colab and rerunning all steps.

🚀 Happy Coding! 🎉

