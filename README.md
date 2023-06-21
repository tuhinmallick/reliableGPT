# reliableGPT 💪

⚡️ Never worry about overloaded OpenAI servers, rotated keys, or context window limitations again!⚡️

reliableGPT handles:
* OpenAI APIError, OpenAI Timeout, OpenAI Rate Limit Errors, OpenAI Service UnavailableError / Overloaded
* Context Window Errors
* Invalid API Key errors 

👉 [Code Tutorial](https://colab.research.google.com/drive/1Kr_f_QSqlA5aiE9jNuxdQGLPMSODjfD0?usp=sharing)


![ezgif com-optimize](https://github.com/BerriAI/reliableGPT/assets/17561003/017046b0-0044-4df3-a740-d5edd9e23738)

### How does it handle failures?
* **Specify a fallback strategy for handling failed requests**: For instance, you can define `fallback_strategy=['gpt-3.5-turbo', 'gpt-4', 'gpt-3.5-turbo-16k', 'text-davinci-003']`, and if you hit an error then reliableGPT will retry with the specified models in the given order until it receives a valid response. This is optional, and reliableGPT also has a default strategy it uses. 

* **Specify backup tokens**:
Using your OpenAI keys across multiple servers? You can pass backup tokens using `add_keys()`. We will store and go through these, in case any get keys get rotated by OpenAI. For security, we use special tokens, and enable you to delete all your keys (using `delete_keys()`) as well. 

* **Context Window Errors**: 
For context window errors it automatically retries your request with models with larger context windows

# Getting Started
## Step 1. pip install package
```
pip install reliableGPT
```
## Step 2. The core package is 1 line of code
```python
from reliablegpt import reliableGPT
openai.ChatCompletion.create = reliableGPT(openai.ChatCompletion.create, user_email='ishaan@berri.ai')
```

# Advanced Usage 
## Handle **rotated keys** 
### Step 1. Add your keys 
```python
from reliablegpt import add_keys, delete_keys, reliableGPT
# Storing your keys 🔒
account_email = "krrish@berri.ai" # 👈 Replace with your email
token = add_keys(account_email, ["openai_key_1", "openai_key_2", "openai_key_3"])
```
Pass in a list of your openai keys. We will store these and go through them in case any get keys get rotated by OpenAI. You will get a **special token**, give that to reliableGPT.
### Step 2. Initialize reliableGPT 
```python
import openai 
openai.api_key = "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" ## Invalid OpenAI key

print("Initializing reliableGPT 💪")
openai.ChatCompletion.create = reliableGPT(openai.ChatCompletion.create, user_email= account_email, user_token = token)
```
reliableGPT💪 catches the Invalid API Key error thrown by OpenAI and rotates through the remaining keys to ensure you have **zero downtime** in production. 

### Step 3. Delete keys 
```python
#Deleting your keys from reliableGPT 🫡
delete_keys(account_email = account_email, user_token=token)
```

You own your keys, and can delete them whenever you want. 

## Support 
Reach out to us on Discord https://discord.com/invite/xqTmjKf9wC or Email us at ishaan@berri.ai & krrish@berri.ai

