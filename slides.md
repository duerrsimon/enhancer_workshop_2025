---
# You can also start simply with 'default'
theme: default
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background:
# some information about your slides (markdown enabled)
title: Gradio Workshop
info: |
  Duild FAIR web apps for science with Gradio and HuggingFace Spaces
# apply unocss classes to the current slide
class: text-center
# https://sli.dev/features/drawing
drawings:
  persist: false
# slide transition: https://sli.dev/guide/animations.html#slide-transitions
transition: slide-left
# enable MDC Syntax: https://sli.dev/features/mdc
mdc: true
# take snapshot for each slide in the overview
overviewSnapshots: true
---

# Gradio Workshop
<br>

<div class="flex items-center">

<img src="https://rse.swiss/images/logo.png" class="w-1/3 mx-auto mb-4" />
<img src="https://static.wixstatic.com/media/8f5290_c0e46a78716b4d23978261fb0a7dd2ce~mv2.png/v1/fill/w_702,h_180,al_c,lg_1,q_95,enc_avif,quality_auto/8f5290_c0e46a78716b4d23978261fb0a7dd2ce~mv2.png" class="w-1/3 mx-auto mb-4" />
</div>

Simon Dürr, HES-SO Valais-Wallis, EnhanceR Ambassador

<div class="pt-12">
  <span @click="$slidev.nav.next" class="px-2 py-1 rounded cursor-pointer" hover="bg-white bg-opacity-10">
    Press Space for next page <carbon:arrow-right class="inline"/> or use navigation in lower left corner to navigate.
  </span>
</div>

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub" title="Open in GitHub"
    class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->


---
transition: fade-out
---


<iframe src="https://simonduerr-proteinmpnn.hf.space" style="  transform: scale(0.71);
  transform-origin: 0 0;
  width: 150.33%;
  height: 150.33%;"> </iframe>



---

# Topics


<h3 class="mt-10 mb-4">We will cover</h3>

- **Gradio** - What is it and how to use it
- 🤗 **HuggingFace Spaces** - Share your app on HuggingFace Spaces
- **Application Programming Interface (API)** - How to make it FAIR

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/features/slide-scope-style
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>


---
class: text-center
---
# The field I work in

<img src="/assets/toomanypapers.gif" class="mx-auto my-auto" />

## soo many papers and models, so little time


---
class: text-center
---

<br><br><br>
## Protein Design is bascially machine learning now.  <br>

<br>
<br>

# So we have borrowed also some tools from the machine learning community.



---
class: text-center
---

<br>

## Lets take a step back

<br><br>

# How did researchers share their methods before the AI craze on the internet? 
<br><br>
<span class="text-4xl text-indigo-900 font-bold" v-click>Webservers</span>



---
class: text-center
---

# Building a webserver
<img src="/assets/oldway.png">

---
---

# Webservers go offline over time

<img src="/assets/future_webservers.png" class="mx-auto w-3/4" />
---
---


# Web Development got more complex over time.

*sarcasm* Did you know that during this talk 3 new web frameworks were released? */sarcasm*

<img src="/image-7.png" class="mx-auto w-2/3" />

Modern web development is a **mess**. 

**Vibe coding** (v0, lovable etc.) makes it even easier to quickly create messy websites. 



---
class: text-center
---

<br><br>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/a/aa/FAIR_data_principles.jpg/1200px-FAIR_data_principles.jpg?20161122143747" class="mx-auto w-2/3" />

Webservers implemented by scientists are often only **FA** and not **IR**

---
---

# Alternatives

In the protein design field we have seen many people using Google Colab. 

<span v-click> Requires maintenance because google changes the environment from time to time. 
Limited User interface. </span>

<img src="/assets/colabfold.png" v-click>

---
---

<img src="/assets/new_way_demos.png">

---
---

# Streamlit

A UX framework to build multi-page webapps. 

But no API
<img src="/assets/streamlit.gif" />



---
---

# Gradio

A library to create web applications from Python. 

Almost as simple as `argparse`. 

Other alternatives: Streamlit (no API), Shiny (clunky setup and no API), Flask (more advanced webserver).

Develop locally, use anywhere. 

---
---

# Where to host?

Gradio runs inside Google Colab, locally, on your local server infrastructure or on HuggingFace Spaces.

<img src="/image-4.png" class="w-2/3 mx-auto" />

<div class="text-center mt-10 text-blue-600"> <a href="https://huggingface.com">huggingface.com</a> </div>



---
layout: iframe
url: https://www.gradio.app/playground
---



---
---

# Public link sharing

Make available a tunnel to your GPU (bypassing VPN/firewalls) via HTTP. `app.launch(share=True)` 

<img src="/image.png" class="mx-auto w-3/4" />

`app.launch(share=True)`



---
---

# Custom Components

Gradio custom components are reusable UI elements that can be shared across multiple Gradio apps.

Frontend is built using Svelte (main place to implement new components).

Backend is Python and used for validation of inputs/outputs.

Custom components are available via `pip install gradio_<component>`

[Custom component gallery](https://www.gradio.app/custom-components/gallery)


---
---

# Minimal Custom Component

```svelte {*|9|34}{maxHeight:'400px'}
<script lang="ts">
	import type { LoadingStatus } from "@gradio/statustracker";
  import { Block } from "@gradio/atoms";
	import { StatusTracker } from "@gradio/statustracker";
	import type { Gradio } from "@gradio/utils";

  [..]

  export let value = "";
	export let elem_id = "";
	export let elem_classes: string[] = [];
	export let scale: number | null = null;
	export let min_width: number | undefined = undefined;
	export let loading_status: LoadingStatus | undefined = undefined;
  export let mode: "static" | "interactive";
</script>

<Block
	visible={true}
	{elem_id}
	{elem_classes}
	{scale}
	{min_width}
	allow_overflow={false}
	padding={true}
>
	{#if loading_status}
		<StatusTracker
			autoscroll={gradio.autoscroll}
			i18n={gradio.i18n}
			{...loading_status}
		/>
	{/if}
    <p>{value}</p>
</Block>
```


---
---
# Gradio Molecule3D

```
pip install gradio_molecule3d
```

<video controls autoplay>
<source src="/assets/molecule3d_gradio.mp4"  />
</video>

---
---

# Use Gradio Molecule3D

```python
from gradio_molecule3d import Molecule3D

 reps =    [
    {
      "model": 0,
      "style": "cartoon",
      "color": "whiteCarbon",
      "residue_range": "",
      "around": 0,
      "byres": False,
    },
    {
      "model": 0,
      "chain": "A",
      "resname": "HIS",
      "style": "stick",
      "color": "red"
    }
  ]

with gr.Blocks() as demo:
    inp = Molecule3D(label="Input molecule", reps=reps)

```

---
---

# Gradio Molecule2d

<iframe
	src="https://simonduerr-gradio-molecule2d.hf.space"
	frameborder="0"
	width="850"
	height="450"
></iframe>

---
---

# Other custom components

<img src="/assets/gradio_ccs.png" />


---
---

# Rest API 

```bash
pip install gradio_client
```

```python
from gradio_client import Client, handle_file

client = Client("https://mlsb-strong-docking-baseline.hf.space/")
result = client.predict(
		input_sequence="AAAA",
		input_ligand="CCC",
		input_msa=handle_file('input.msa'),
		input_protein=handle_file('input.pdb'),
		api_name="/predict"
)
print(result)
```

Find API docs for each space at the bottom:
![alt text](/image-2.png)


---
---

# REST API features

- automatic API docs
- supports standard HTTP requests (e.g. `curl`)
- advanced library `gradio_client` for queuing, streaming inputs, callbacks, ...
- session states


---
---

# Arbitrary HTML

Browsers have security rules. If you want to return arbitrary short HTML snippets use an `iframe` with `srcdoc`

```python
def predict(input):
    # do something to generate output html
    x = ("""<!DOCTYPE html><html> [..] </html>""") # do not use ' in this input
    return f"""<iframe  [..] srcdoc='{x}'></iframe>

[...]

with gr.Blocks() as app:
  out = gr.HTML()

[...]

```

---
---

# Generators

Sometimes your model might return a series of predictions. 

Simply return a generator and your app will show immediate outputs. 

```
def my_generator(x):
    for i in range(x):
        yield i
```



---
layout: two-cols
---


You can use Gradio Spaces (cannot change the underlying Docker image) or Docker spaces with full control. 

In Gradio spaces you use `packages.txt` for `apt-get` installable packages and `requirements.txt` for python packages. 

::right::

<img src="/image-5.png" class="mx-auto" />




---
---

# ProteinMPNN Dockerfile

```dockerfile
FROM nvidia/cuda:11.7.1-cudnn8-devel-ubuntu22.04
RUN apt-get update
RUN apt-get install -y python3 python3-pip git wget
 
WORKDIR /code
COPY ./requirements.txt /code/requirements.txt
RUN python3 -m pip install --upgrade pip 

RUN pip install gradio==3.46.0
RUN pip install --no-cache-dir --upgrade -r /code/requirements.txt
RUN useradd -m -u 1000 user
USER user
ENV HOME=/home/user \
    PATH=/home/user/.local/bin:$PATH

WORKDIR $HOME/app
COPY --chown=user . $HOME/app

EXPOSE 7860
ENV GRADIO_SERVER_NAME="0.0.0.0"

CMD ["python3", "app.py"]
```



---
layout: two-cols
---

## Community grant

**Default** 2 CPU cores, 16GB of RAM

For academic projects you can ask HuggingFace to grant you a free GPU (e.g T4/A10G ...)

![Community grant](/assets/community_grant.png)

Works for Gradio and Docker spaces.


::right::

# ZeroGPU

Only for Gradio Spaces. 

![ZeroGPU](/assets/zerogpu.gif)



---
---

# Use from within pymol

Create a `script.py` file  and load it in pymol using `run path/to/script.py`


## 1. install gradio client
```python
from pymol import cmd

try:
    from gradio_client import Client
except ImportError:
    print("gradio_client not installed, trying install:")
    import pip 
    pip.main(['install', 'gradio_client'])
    from gradio_client import Client
```



---
---

## 2. PyMol command

```python
def pymol_command(
    name_of_input: str,
):
    input_pdb = cmd.get_pdbstr(name_of_input)

    t = threading.Thread(target=call_api,
                         args=(input_pdb),
                         kwargs={},
                         daemon=True)
    t.start()

cmd.extend("mymodel", pymol_command)
```

use as `mymodel PYMOLMODELNAME` from PyMol CMD

<img src="/image-3.png" class="w-2/3 mx-auto" />

---
---

## 3. call API

```python
def call_api(input_pdb):
    client = Client(gradio_link)

    job = client.submit(
				input_pdb,	# TextBox input
				api_name="/predict"
    )
    start = time.time()
    while (job.done() == False):
        status =  job.status()
        elapsed = time.time()-start 
        elapsed = time.strftime("%H:%M:%S", time.gmtime(elapsed))
        print(f"\r protpardelle running since {elapsed}", end="")
        time.sleep(1)
    results = job.result()
    results = json.loads(results)
    for (name,pdb_content) in results:
        cmd.read_pdbstr(pdb_content, os.path.basename(name))
```

---
---

# Summary

- Gradio makes it easy to create web apps for almost any purpose
- The whole ecosystem is open source
- Run locally, on your server or in the cloud
- HuggingFace Spaces makes it easy to share your app with the world
- REST API makes automatically making your app FAIR
- Gradio can be easily extended with custom components

---
layout: center
class: text-center
---

# Learn More

[Documentation](https://www.gradio.app/guides/quickstart) · [GitHub](https://github.com/gradio-app/gradio) · [Showcases](https://huggingface.co/collections/simonduerr/protein-design---protein-structure-prediction-64f9c6fda9295717466dbe8f)

X/Bluesky @simonduerr

<PoweredBySlidev mt-10 />



