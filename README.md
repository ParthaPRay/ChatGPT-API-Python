# ChatGPT-API-Python
This repo contains the process to connect ChatGPT API by Python

0. Use Python

1. (**Optional**) Use Python Virtual Environment in Windows:

   Create "openai-env" inside the current folder you have selected in your terminal / command line:
  
   **python -m venv openai-env**

   Activate it:
   
   **openai-env\Scripts\activate**


    For MacOS or UNIX use: **source openai-env/bin/activate**

2. Install OpenAI Python Library

   **pip install openai**
   or
   **pip install --upgrade openai**

3. Setup API Key from **https://platform.openai.com/** after logging in your own account when Billing of minimum USD 5 should be there in your acount for accessng the API access purpose

![image](https://github.com/ParthaPRay/ChatGPT-API-Python/assets/1689639/2333a653-c325-4f12-8135-7ec753d5cf56)

Then in Windows, Set environment variable in the current session: 

**setx OPENAI_API_KEY your-api-key-here**

![Screenshot 2024-01-01 225826](https://github.com/ParthaPRay/ChatGPT-API-Python/assets/1689639/fd5e1620-3404-4534-b4fe-fd62e1f3c3f1)

===============================================================================================================================
For permanent setup:

* Right-click on 'This PC' or 'My Computer' and select 'Properties'.
* Click on 'Advanced system settings'.
* Click the 'Environment Variables' button.
* In the 'System variables' section, click 'New...' and enter OPENAI_API_KEY as the variable name and your API key as the variable value.

For verification check:

**echo %OPENAI_API_KEY%**

==================================================================================================================================

For single project deployment:

Create an **.env** file in your project folder and put the below line. Replace 'your_api_key' with your own API key such as sk-***********

OPENAI_API_KEY = your_api_key


4. Use below code

   ```python
from openai import OpenAI
client = OpenAI()

completion = client.chat.completions.create(
  model="gpt-3.5-turbo",
  messages=[
    {"role": "system", "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."},
    {"role": "user", "content": "Compose a poem that explains the concept of recursion in programming."}
  ]
)

print(completion.choices[0].message)


   

Reference:
1. https://platform.openai.com/docs/quickstart?context=python
