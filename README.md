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
ChatCompletionMessage(content='........', role='assistant', function_call=None, tool_calls=None)
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
...................
```

# 4.4 Sample Code for lyric creation with temperature = 0

```
# With n = 1, that means the number of stream back from OpenAI, max_tokens is 15 
# per response from OpenAI, temperature = 0 i.e., the deterministic behavior is strict


from openai import OpenAI
import time

client = OpenAI()

# initial prompt with system message and 2 task examples
messages_list = [{"role":"system", "content": "I am Roxette lyric completion assistant. When given a line from a song, I will provide the next line in the song."},
                 {"role":"user", "content": "I know there's something in the wake of your smile"},
                 {"role":"assistant", "content": "I get a notion from the look in your eyes, yeah"},
                 {"role":"user", "content": "You've built a love but that love falls apart"},
                 {"role":"assistant", "content": "Your little piece of Heaven turns too dark"},
                 {"role":"user", "content": "Listen to your"}]




for i in range(4):
    # create a chat completion
    chat_completion = client.chat.completions.create(model="gpt-4", 
                                    messages=messages_list,
                                    max_tokens = 15,
                                    n=1,
                                    temperature=0)

    # print the chat completion
    print(chat_completion.choices[0].message.content)

    new_message = {"role":"assistant", "content":chat_completion.choices[0].message.content} # append new message to message list
    messages_list.append(new_message)
    time.sleep(0.1)

```

**Output**
```
...................
```


# 4.5 Sample Code for lyric creation with temperature = 1

```
# With n = 1, that means the number of stream back from OpenAI, max_tokens is 15 
# per response from OpenAI, temperature = 0 i.e., the deterministic behavior is less strict
# but the resturn of response is still good enough


from openai import OpenAI
import time

client = OpenAI()

# initial prompt with system message and 2 task examples
messages_list = [{"role":"system", "content": "I am Roxette lyric completion assistant. When given a line from a song, I will provide the next line in the song."},
                 {"role":"user", "content": "I know there's something in the wake of your smile"},
                 {"role":"assistant", "content": "I get a notion from the look in your eyes, yeah"},
                 {"role":"user", "content": "You've built a love but that love falls apart"},
                 {"role":"assistant", "content": "Your little piece of Heaven turns too dark"},
                 {"role":"user", "content": "Listen to your"}]




for i in range(4):
    # create a chat completion
    chat_completion = client.chat.completions.create(model="gpt-4", 
                                    messages=messages_list,
                                    max_tokens = 15,
                                    n=1,
                                    temperature=1)

    # print the chat completion
    print(chat_completion.choices[0].message.content)

    new_message = {"role":"assistant", "content":chat_completion.choices[0].message.content} # append new message to message list
    messages_list.append(new_message)
    time.sleep(0.1)

```

**Output**
```
...................
```


# 4.5 Sample Code for lyric creation with temperature = 2

```
# With n = 1, that means the number of stream back from OpenAI, max_tokens is 15 
# per response from OpenAI, temperature = 2 i.e., the deterministic behavior is very loose and
# responses are very random


from openai import OpenAI
import time

client = OpenAI()

# initial prompt with system message and 2 task examples
messages_list = [{"role":"system", "content": "I am Roxette lyric completion assistant. When given a line from a song, I will provide the next line in the song."},
                 {"role":"user", "content": "I know there's something in the wake of your smile"},
                 {"role":"assistant", "content": "I get a notion from the look in your eyes, yeah"},
                 {"role":"user", "content": "You've built a love but that love falls apart"},
                 {"role":"assistant", "content": "Your little piece of Heaven turns too dark"},
                 {"role":"user", "content": "Listen to your"}]




for i in range(4):
    # create a chat completion
    chat_completion = client.chat.completions.create(model="gpt-4", 
                                    messages=messages_list,
                                    max_tokens = 15,
                                    n=1,
                                    temperature=2)

    # print the chat completion
    print(chat_completion.choices[0].message.content)

    new_message = {"role":"assistant", "content":chat_completion.choices[0].message.content} # append new message to message list
    messages_list.append(new_message)
    time.sleep(0.1)

```

**Output**
```
...................
```

Reference:
1. https://platform.openai.com/docs/quickstart?context=python
