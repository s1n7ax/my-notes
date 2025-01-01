# Text to Numbers

## Summary

- What is tokenization?
- Why not use ASCII?
- How to tokenize?

## Content

### What tokenization do?

Tokenization simply converts the characters into numbers.

### Why not use ASCII?

ASCII represents letters in numbers but it's hard to build a meaning of
sentences just by encoding letters to numbers.

Ex:-

Both of the following words has the same set of characters so encoding each
letter individually makes it hard to get the meaning.

```text
S I L E N T
L I S T E N
```

So instead of encoding each characters, word or words will be tokenized

### How to tokenize

> [!WARNING] |
> `tf.keras.preprocessing.text.Tokenizer` is now deprecated
> Use `tf.keras.layers.TextVectorization`

```python
from tensorflow.keras.layers import TextVectorization

vectorize_layer = TextVectorization()

# text vectorization should adapt to the existing text to check the frequency
# of the token & build the vocabulary
vectorize_layer.adapt(['I love you', 'I love cat', 'I love dog'])

# vocabulary returns the unique tokens based on the frequency they are used
vectorize_layer.get_vocabulary()
'''
['', '[UNK]', 'love', 'i', 'you', 'dog', 'cat']
'''
# Here, '' represents the padding and [UNK] for any word that's not in the
# vocabulary

vectorize_layer('I love programming')
```

If a new text contains all the tokens, the relevant index will be used in the
tokenization

```python
# ['', '[UNK]', 'love', 'i', 'you', 'dog', 'cat']
#   0     1        2     3     4      5      6

vectorize_layer('I love cat').numpy()
'''
array([3, 2, 6])
'''

vectorize_layer('I love programming').numpy()
'''
array([3, 2, 1])
'''
# Since 'programming' is an unknown token in the vocabulary, it's considered to
# be a [UNK]
```
