# Anti-ccw-font-encrypt

Font mapping JSON of ccw.ttf &amp; ccw.eot

## Description

CCW uses font-mapping confusing to display search results. Though the result could be read from HTTP requests easily, the content looks like sh*t for all characters are not what they looks like in web page.

For example, `ABCDEFG` appears as `udvQiB$` at their pages.

However, if only numbers and English characters are replaced, it's easy to fill a chart by collecting data. But when it comes to Chinese characters this strategy will not work.

From FontLab's revealing, almost 300 Chinese characters were replaced. The thing is they didn't just replace the character to one another like old ways. Actually they didn't **replace** any character in coding aspect. They just **replace the character's Glyph to another one**. Checking Cmap doesn't work because of that.

Whatever, I collected all characters by OCR and mapped them into *JSON*. Bite me.

## Usage

The json in *mapping.json* maps `encrypted text → origin`. For example, if you get `u` from request and the related text appears in page is `A`. This means you can just translate `u` by our json like: 

```python
>>> json_data['u']
# 'A'
```

Here comes an example of a function you may need:

```python
def cvt(text):
     text = str(text)
     result = ''
     for c in text:
         if json_data.get(c):
             result += json_data[c]
         else:
             result += c
     return result
```
