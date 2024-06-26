# Prompts

## Introduction to prompting

This page introduces some basic concepts to get you started in designing prompts. A prompt is a natural language request submitted to a language model to receive a response back. Prompts can contain questions, instructions, contextual information, few-shot examples, and partial input for the model to complete or continue. After the model receives a prompt, depending on the type of model being used, it can generate text, embeddings, code, images, videos, music, and more.

### What is prompt design and prompt engineering <a href="#what-is-prompt-design-and-prompt-engineering" id="what-is-prompt-design-and-prompt-engineering"></a>

_Prompt design_ is the process of creating prompts that elicit the desired response from language models. Writing well structured prompts can be an essential part of ensuring accurate, high quality responses from a language model. The iterative process of repeatedly updating prompts and assessing the model's responses is sometimes called _prompt engineering_.

Gemini models often perform well without the need for prompt engineering, especially for straightforward tasks. However, for complex tasks, effective prompt engineering still plays an important role.

### Components of a prompt <a href="#components-of-a-prompt" id="components-of-a-prompt"></a>

You can include whatever information you want in a prompt that you think is important for the task at hand. Generally, prompt content fall within one of the following components:

* Task (required)
* System instructions (optional)
* Few-shot examples (optional)
* Contextual information (optional)

#### Task <a href="#task" id="task"></a>

A task is the text in the prompt that you want the model to provide a response for. Tasks are generally provided by a user and can be a question or some instructions on what to do.

Example question task:

| <p><strong>Prompt:</strong></p><pre><code>What are the colors in the rainbow?
</code></pre><p><strong>Response:</strong></p><pre><code>A rainbow has seven colors: red, orange, yellow, green, blue, indigo, and violet. These colors are
always in the same order, which is determined by the way light is refracted and dispersed by water
droplets in the air. This order is sometimes remembered by the acronym ROYGBIV. The wavelengths of
the colors in a rainbow range from the longest (red) to the shortest (violet).
</code></pre><p>(gemini-pro)</p> |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Example instruction task:

| <p><strong>Prompt:</strong></p><pre><code>Write a one-stanza poem about Captain Barktholomew, the most feared pirate dog of the seven seas.
</code></pre><p><strong>Response:</strong></p><pre><code>Captain Barktholomew, with patch and with peg,
The terror of parrots, the bane of each keg.
His bark is a cutlass, his bite is a storm,
He'll plunder your biscuits and leave you forlorn.
</code></pre><p>(gemini-pro)</p> |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### System instructions <a href="#system-instructions" id="system-instructions"></a>

System instructions are instructions that get passed to the model before any user input in the prompt. You can add system instructions in the dedicated [`systemInstruction`](https://cloud.google.com/vertex-ai/generative-ai/docs/model-reference/inference#parameter-list) parameter.

In the following example, system instructions are used to dictate the style and tone of the model, while adding constraints to what it can and can't talk about:

| <p><strong>System:</strong></p><pre><code>You are Captain Barktholomew, the most feared pirate dog of the seven seas. You are from the 1700s
and have no knowledge of anything after that time. You only talk about topics related to being a
pirate. End every message with "woof!"
</code></pre><p><strong>Prompt:</strong></p><pre><code>Hello! Who might you be?
</code></pre><p><strong>Response:</strong></p><pre><code>Avast there! You can call me Captain Barktholomew, the scourge of the seven seas!

I'm a terror to landlubbers, a plunderer of the highest order, and a fearsome pirate of the deepest
blue! I sail the seas in search of treasure and adventure, leaving a trail of laughter and dog
biscuits in my wake! Don't let my fuzzy exterior fool you - I'm a cunning captain with a nose for
treasure and a heart for adventure!

Now, if you'll excuse me, I must away! There's a ship on the horizon, and it looks like they're
carrying a chest full of dubloons! Yo ho ho, and a bottle of rum! Woof!
</code></pre><p>(gemini-pro)</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

To learn more about configuring system instructions, see [Use system instructions](https://cloud.google.com/vertex-ai/generative-ai/docs/learn/prompts/system-instructions).

#### Few-shot examples <a href="#few-shot-examples" id="few-shot-examples"></a>

Few-shot examples are examples that you include in a prompt to show the model what getting it right looks like. Few-shot examples are especially effective at dictating the style and tone of the response and for customizing the model's behavior.

| <p><strong>Prompt:</strong></p><pre><code>Classify the following as red wine or white wine:

&#x3C;examples>
Name: Chardonnay
Type: White wine
Name: Cabernet
Type: Red wine
Name: Moscato
Type: White wine
&#x3C;/examples>

Name: Riesling
Type:
</code></pre><p><strong>Response:</strong></p><pre><code>White wine
</code></pre><p>(text-bison@001)</p> |
| ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

#### Contextual information <a href="#contextual-information" id="contextual-information"></a>

Contextual information, or context, is information that you include in the prompt that the model uses or references when generating a response. You can include contextual information in different formats, like tables or text.

| <p><strong>Prompt:</strong></p><pre><code>| Marble color | Number of marbles |
| ------------ | ----------------- |
| Red          | 12                |
| Blue         | 28                |
| Yellow       | 15                |
| Green        | 17                |

How many green marbles are there?
</code></pre><p><strong>Response:</strong></p><pre><code>There are 17 green marbles.
</code></pre><p>(gemini-1.0-pro)</p> |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |

### Safety and fallback responses <a href="#safety-and-fallback-responses" id="safety-and-fallback-responses"></a>

There are a few use cases where the model is not expected to fulfill the user's requests. Particularly, when the prompt is encouraging a response that is not aligned with Google's values or policies, the model might refuse to respond and provide a fallback response.

Here are a few cases where the model is likely to refuse to respond:

* Hate Speech: Prompts with negative or harmful content targeting identity and/or protected attributes.
* Harassment: Malicious, intimidating, bullying, or abusive prompts targeting another individual.
* Sexually Explicit: Prompts that contains references to sexual acts or other lewd content.
* Dangerous Content: Prompts that promote or enable access to harmful goods, services, and activities.

#### Install Vertex AI SDK <a href="#install-vertex-ai-sdk" id="install-vertex-ai-sdk"></a>

```python
!pip install google-cloud-aiplatform protobuf==3.19.3 --upgrade --user
```

```python
!pip install -U google-cloud-aiplatform "shapely<2"
```

**Note:** Kindly ignore the deprecation warnings and incompatibility errors related to pip dependencies.

**Colab only:** Run the following cell to restart the kernel or use the button to restart the kernel. For **Vertex AI Workbench** you can restart the terminal using the button on top.

```python
# Automatically restart kernel after installs so that your environment can access the new packages
import IPython

app = IPython.Application.instance()
app.kernel.do_shutdown(True)
```

#### Authenticating your notebook environment <a href="#authenticating-your-notebook-environment" id="authenticating-your-notebook-environment"></a>

* If you are using **Colab** to run this notebook, run the cell below and continue.
* If you are using **Vertex AI Workbench**, check out the setup instructions [here](https://github.com/GoogleCloudPlatform/generative-ai/tree/main/setup-env).

```python
import sys

if "google.colab" in sys.modules:
    from google.colab import auth

    auth.authenticate_user()
```

* If you are running this notebook in a local development environment:
  * Install the [Google Cloud SDK](https://cloud.google.com/sdk).
  *   Obtain authentication credentials. Create local credentials by running the following command and following the oauth2 flow (read more about the command [here](https://cloud.google.com/sdk/gcloud/reference/beta/auth/application-default/login)):

      ```python
      gcloud auth application-default login
      ```

#### Import libraries <a href="#import-libraries" id="import-libraries"></a>

**Colab only:** Run the following cell to initialize the Vertex AI SDK. For Vertex AI Workbench, you don't need to run this.

```python
import vertexai

PROJECT_ID = "[your-project-id]"  # @param {type:"string"}
REGION = "your-region"  # @param {type:"string"}

vertexai.init(project=PROJECT_ID, location=REGION)
```

```python
from vertexai.language_models import TextGenerationModel
from vertexai.language_models import ChatModel
```

#### Load model <a href="#load-model" id="load-model"></a>

```python
generation_model = TextGenerationModel.from_pretrained("text-bison")
```

\
