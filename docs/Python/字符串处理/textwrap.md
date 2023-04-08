# textwrap

```python
import textwrap

sample_text = '''
    The textwrap module can be used to format text for output in
    situations where pretty-printing is desired.  It offers
    programmatic functionality similar to the paragraph wrapping
    or filling features found in many text editors.
    '''
```

## fill()

```python
print(textwrap.fill(sample_text, width=50))
```

         The textwrap module can be used to format
    text for output in     situations where pretty-
    printing is desired.  It offers     programmatic
    functionality similar to the paragraph wrapping
    or filling features found in many text editors.

## dedent()

```python
dedented_text = textwrap.dedent(sample_text)

print("Dedented:")
print(dedented_text)
```

    Dedented:
    
    The textwrap module can be used to format text for output in
    situations where pretty-printing is desired.  It offers
    programmatic functionality similar to the paragraph wrapping
    or filling features found in many text editors.

## fill()とdedent()を結合する

```python
dedented_text = textwrap.dedent(sample_text).strip()
for width in [45, 60]:
    print(f"{width} Columns:\n")
    print(textwrap.fill(dedented_text, width=width))
    print()
```

    45 Columns:
    
    The textwrap module can be used to format
    text for output in situations where pretty-
    printing is desired.  It offers programmatic
    functionality similar to the paragraph
    wrapping or filling features found in many
    text editors.
    
    60 Columns:
    
    The textwrap module can be used to format text for output in
    situations where pretty-printing is desired.  It offers
    programmatic functionality similar to the paragraph wrapping
    or filling features found in many text editors.

## indent()

```python
dedented_text = textwrap.dedent(sample_text)
wrapped = textwrap.fill(dedented_text, width=50)
wrapped += '\n\nSecond paragraph after a blank line.'
final = textwrap.indent(wrapped, '> ')

print('Quoted block:\n')
print(final)
```

    Quoted block:
    
    >  The textwrap module can be used to format text
    > for output in situations where pretty-printing is
    > desired.  It offers programmatic functionality
    > similar to the paragraph wrapping or filling
    > features found in many text editors.
    
    > Second paragraph after a blank line.

```python
def should_indent(line):
    print(f'Indent {line!r}?')
    return len(line.strip()) % 2 == 0


dedented_text = textwrap.dedent(sample_text)
wrapped = textwrap.fill(dedented_text, width=50)
final = textwrap.indent(wrapped, 'EVEN ',
                        predicate=should_indent) # 条件をつける

print('\nQuoted block:\n')
print(final)
```

    Indent ' The textwrap module can be used to format text\n'?
    Indent 'for output in situations where pretty-printing is\n'?
    Indent 'desired.  It offers programmatic functionality\n'?
    Indent 'similar to the paragraph wrapping or filling\n'?
    Indent 'features found in many text editors.'?
    
    Quoted block:
    
    EVEN  The textwrap module can be used to format text
    for output in situations where pretty-printing is
    EVEN desired.  It offers programmatic functionality
    EVEN similar to the paragraph wrapping or filling
    EVEN features found in many text editors.

```python
dedented_text = textwrap.dedent(sample_text).strip()
print(textwrap.fill(dedented_text,
                    initial_indent='', # 最初のインデント
                    subsequent_indent=' ' * 4, # 続いてのインデント
                    width=50,
                    ))
```

    The textwrap module can be used to format text for
        output in situations where pretty-printing is
        desired.  It offers programmatic functionality
        similar to the paragraph wrapping or filling
        features found in many text editors.

## shorten()

```python
dedented_text = textwrap.dedent(sample_text)
original = textwrap.fill(dedented_text, width=50)

print('Original:\n')
print(original)

shortened = textwrap.shorten(original, 100)
shortened_wrapped = textwrap.fill(shortened, width=50)

print('\nShortened:\n')
print(shortened_wrapped)
```

    Original:
    
     The textwrap module can be used to format text
    for output in situations where pretty-printing is
    desired.  It offers programmatic functionality
    similar to the paragraph wrapping or filling
    features found in many text editors.
    
    Shortened:
    
    The textwrap module can be used to format text for
    output in situations where pretty-printing [...]
