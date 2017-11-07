# Python Recipe for Strings and Text

## Handling strings in a basic way

**Version A**

### Problem

You need a basic way of handling strings.

### Solution

Let's see a brief example section for working with strings:

```python
>>> s = "Life is beatiful and exciting"
>>> 'a' in s
True
>>> 'v' in s
False
>>> s + ", Robert!"
'Life is beatiful and exciting, Robert!'
>>> " Life" * 3
' Life Life Life'
>>> "-" * 60
'------------------------------------------------------------'
>>> len(s)
29
>>> s.find('a')
10
>>> s.find('v')
-1
>>> s.find('a', 11)
17
>>> s.find('e', 18, 22)
21
>>> s.split()
['Life', 'is', 'beatiful', 'and', 'exciting']
>>> s.split('i')
['L', 'fe ', 's beat', 'ful and exc', 't', 'ng']
>>> t = ['Life', 'is', 'beatiful', 'and', 'exciting']
>>> " ".join(t)
'Life is beatiful and exciting'
>>> t = ['L', 'fe ', 's beat', 'ful and exc', 't', 'ng']
>>> "i".join(t)
'Life is beatiful and exciting'
>>> s.lower()
'life is beatiful and exciting'
>>> s.upper()
'LIFE IS BEATIFUL AND EXCITING'
>>> s.title()
'Life Is Beatiful And Exciting'
>>> s.swapcase()
'lIFE IS BEATIFUL AND EXCITING'
>>> s.ljust(60, '*')
'Life is beatiful and exciting*******************************'
>>> s.center(60, '*')
'***************Life is beatiful and exciting****************'
>>> s.rjust(60, '*')
'*******************************Life is beatiful and exciting'
>>> s.count('a')
2
>>> s.count('e')
3
>>> s.count('i')
5
>>> s.count('o')
0
>>> s.count('u')
1
>>> "Life".isalpha()
True
>>> "Life ".isalpha()
False
>>> "1234567890".isdigit()
True
>>> "1234567890a".isdigit()
False
>>> s.lstrip("Life is")
'beatiful and exciting'
>>> s.rstrip("and exciting")
'Life is beatiful'
>>> s.strip("Ling")
'fe is beatiful and excit'
>>> s.replace("Life", "Love")
'Love is beatiful and exciting'
>>> s.encode('utf-8')
b'Life is beatiful and exciting'
>>> s = "Life is beatiful and exciting, José!"
>>> s.encode('utf-8')
b'Life is beatiful and exciting, Jos\xc3\xa9!'
>>> e_with_acute = b'\xc3\xa9'
>>> e_with_acute.decode()
'é'
>>> import string
>>> string.digits
'0123456789'
>>> string.hexdigits
'0123456789abcdefABCDEF'
>>> string.octdigits
'01234567'
>>> string.ascii_letters
'abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> string.ascii_lowercase
'abcdefghijklmnopqrstuvwxyz'
>>> string.ascii_uppercase
'ABCDEFGHIJKLMNOPQRSTUVWXYZ'
>>> string.printable
'0...9a...zA...Z!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~ \t\n\r\x0b\x0c'
>>> string.punctuation
'!"#$%&\'()*+,-./:;<=>?@[\\]^_`{|}~'
>>> string.whitespace
' \t\n\r\x0b\x0c'
```
