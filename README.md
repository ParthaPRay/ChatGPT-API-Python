# ChatGPT-API-Python
This repo contains the process to connect ChatGPT API by Python

0. # Use **Python**

# 1.  (**Optional**) Use Python Virtual Environment in Windows:

   Create "openai-env" inside the current folder you have selected in your terminal / command line:
  
```python
   python -m venv openai-env
```

   Activate it:
   
   ```
   openai-env\Scripts\activate
   ```


    For MacOS or UNIX use: 

    ```
    source openai-env/bin/activate
    ```

# 2. Install OpenAI Python Library

   ```python
   pip install openai
   ```
   or
   ```python
   pip install --upgrade openai
   ```

# 3. Setup API Key from **https://platform.openai.com/** after logging in your own account when Billing of minimum USD 5 should be there in your acount for accessng the API access purpose

![image](https://github.com/ParthaPRay/ChatGPT-API-Python/assets/1689639/2333a653-c325-4f12-8135-7ec753d5cf56)

Then in Windows, Set environment variable in the current session: 

```
setx OPENAI_API_KEY your-api-key-here
```

![Screenshot 2024-01-01 225826](https://github.com/ParthaPRay/ChatGPT-API-Python/assets/1689639/fd5e1620-3404-4534-b4fe-fd62e1f3c3f1)

**For permanent setup:**

* Right-click on 'This PC' or 'My Computer' and select 'Properties'.
* Click on 'Advanced system settings'.
* Click the 'Environment Variables' button.
* In the 'System variables' section, click 'New...' and enter OPENAI_API_KEY as the variable name and your API key as the variable value.

For verification check:

```
echo %OPENAI_API_KEY%
```


**For single project deployment:**

Create an **.env** file in your project folder and put the below line. Replace **your_api_key** with your own API key such as sk-***********

```
OPENAI_API_KEY = your_api_key
```


# 4.1. Sample Code

**Making API Request and shows stream object created at OpenAI**

```python
from openai import OpenAI

client = OpenAI()

stream = client.chat.completions.create(
    model="gpt-4",
    messages=[{"role": "user", "content": "Say this is a test"}],
    stream=True,
)

#Prints whole stream
print(stream)

```

**Output**
```
<openai.Stream object at 0x0000018CA230D290>
```


# 4.2. Sample Code

**Making API Request and prints whole message of stream**

```
from openai import OpenAI

client = OpenAI()

completion = client.chat.completions.create(
  model="gpt-4",   #gpt-3.5-turbo can be used 
  messages=[
    {"role": "system", "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."},
    {"role": "user", "content": "Compose a poem that explains the concept of recursion in programming."}
  ]
)

#Prints whole message
print(completion.choices[0].message)
```

**Output**
```
ChatCompletionMessage(content='Within the puzzling world of codes so deep,\nLies a pattern so cunning, it lulls data to sleep.\nA function that mirrors the echoing canyon,\nBehold the enigma we call recursion!\n\nA method, a function, calls its own name,\nIn a loop of echoes that plays the game.\nEach call a reflection of the timeless verse,\nOf self-reference, there could be nothing worse.\n\n"Compute thyself!" an order is passed,\nA whisper to the next, "Replicate tasks."\nGather and jumble, yet stay in line,\nCompress and return, such marvels combine!\n\nA base case beckons, the end is near,\nA condition to halt, else the loop you\'ll wear.\nWithout the key, the function implores,\nIn an infinite maze of self-inflicted chores.\n\nUnwinding the spool, one layer at a time,\nThe return values ascend in perfect rhyme.\nEvery iteration is a step towards the tale,\nThat the master function wishes to unveil.\n\nPatterns that blossom, rules that abide,\nData structures transformed in recursive stride.\nFrom factorials to Fractals, the Fibonacci day,\nIn the recursive call, find power they say.\n\nTo fathom recursion, constant practice you need,\nFor it\'s not mere repetition, but a digital seed.\nOnce you embrace it, there\'s no looking back,\nIts elegance, its simplicity, leaves no slack.\n\nBeware of the depth, the stack might overflow,\nHope the error message doesn\'t steal the show.\nRecursion, my friend, is straightforward but coy,\nWield it with wisdom, its beauty to enjoy.', role='assistant', function_call=None, tool_calls=None)
```


# 4.3. Sample Code

**Making API Request and prints whole content of message of stream in plain text**

```
from openai import OpenAI

client = OpenAI()

completion = client.chat.completions.create(
  model="gpt-4",   #gpt-3.5-turbo can be used 
  messages=[
    {"role": "system", "content": "You are a poetic assistant, skilled in explaining complex programming concepts with creative flair."},
    {"role": "user", "content": "Compose a poem that explains the concept of recursion in programming."}
  ]
)

# Extract and print only the content of the response
response_content = completion.choices[0].message.content

print(response_content)
```

**Output**
```
Within the puzzling world of codes so deep,
Lies a pattern so cunning, it lulls data to sleep.
A function that mirrors the echoing canyon,
Behold the enigma we call recursion!

A method, a function, calls its own name,
In a loop of echoes that plays the game.
Each call a reflection of the timeless verse,
Of self-reference, there could be nothing worse.

"Compute thyself!" an order is passed,
A whisper to the next, "Replicate tasks."
Gather and jumble, yet stay in line,
Compress and return, such marvels combine!

A base case beckons, the end is near,
A condition to halt, else the loop you'll wear.
Without the key, the function implores,
In an infinite maze of self-inflicted chores.

Unwinding the spool, one layer at a time,
The return values ascend in perfect rhyme.
Every iteration is a step towards the tale,
That the master function wishes to unveil.

Patterns that blossom, rules that abide,
Data structures transformed in recursive stride.
From factorials to Fractals, the Fibonacci day,
In the recursive call, find power they say.

To fathom recursion, constant practice you need,
For it's not mere repetition, but a digital seed.
Once you embrace it, there's no looking back,
Its elegance, its simplicity, leaves no slack.

Beware of the depth, the stack might overflow,
Hope the error message doesn't steal the show.
Recursion, my friend, is straightforward but coy,
Wield it with wisdom, its beauty to enjoy.
```
   

Reference:
1. https://platform.openai.com/docs/quickstart?context=python
