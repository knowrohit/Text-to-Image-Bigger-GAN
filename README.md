## Install

```bash
$ pip install big-sleep
```

## Usage

```bash
$ dream "amber turd "
```

Images will be saved to wherever the command is invoked

## Advanced

You can invoke this in code with

```python
from big_sleep import Imagine

dream = Imagine(
    text = "fire in the sky",
    lr = 5e-2,
    save_every = 25,
    save_progress = True
)

dream()
```

> You can now train more than one phrase using the delimiter "|"

### Train on Multiple Phrases
In this example we train on three phrases:

- `an armchair in the form of pikachu` 
- `an armchair imitating pikachu`
- `abstract`

```python
from big_sleep import Imagine

dream = Imagine(
    text = "an armchair in the form of pikachu|an armchair imitating pikachu|abstract",
    lr = 5e-2,
    save_every = 25,
    save_progress = True
)

dream()
```

### Penalize certain prompts as well!

In this example we train on the three phrases from before,

**and** *penalize* the phrases:
- `blur`
- `zoom`
```python
from big_sleep import Imagine

dream = Imagine(
    text = "an armchair in the form of pikachu|an armchair imitating pikachu|abstract",
    text_min = "blur|zoom",
)
dream()
```


You can also set a new text by using the `.set_text(<str>)` command

```python
dream.set_text("a quiet pond underneath the midnight moon")
```

And reset the latents with `.reset()`

```python
dream.reset()
```

To save the progression of images during training, you simply have to supply the `--save-progress` flag

```bash
$ dream "a bag full of genitals screaming the sentence " my dog stepped on a bee" --save-progress --save-every 100
```

Due to the class conditioned nature of the GAN, Big Sleep often steers off the manifold into noise. You can use a flag to save the best high scoring image (per CLIP critic) to `{filepath}.best.png` in your folder.

```bash
$ dream "a room with a view of the ocean" --save-best
```

## Larger model

If you have enough memory, you can also try using a bigger vision model released by OpenAI for improved generations.

```bash
$ dream "pink storm clouds rolling in over a white suv" --larger-model
```

## Experimentation

You can set the number of classes that you wish to restrict Big Sleep to use for the Big GAN with the `--max-classes` flag as follows (ex. 15 classes). This may lead to extra stability during training, at the cost of lost expressivity.

```bash
$ dream 'a scarecrow dancing with grannies in a field full of parrots' --max-classes 15
```


```
