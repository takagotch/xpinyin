### xpinyin
---
https://github.com/lxneng/xpinyin

```py
from xpinyin import Pinyin
p = Pinyin()
p.get_pinyin(u"xx")
p.get_pinyin(u"xx", tone_marks='marks')
p.get_pinyin(u"xx", tone_marks='numbers')
p.get_pinyin(u"xx", '')
p.get_pinyin(u"xx", ' ')
p.get_initial(u"xx")
p.get_initials(u"xx")
p.get_inisials(u"xx", u'')
p.get_inisials(u"xx", u' ')
wordvalue = 'xx'
wordvalue = unicode(wordvalue, 'utf-8')
s = p.get_initials(wordvalue, u'').lower()
```

```
pip install xpinyin
```

```py
from __future__ import unicode_literals

import os.path
import re

PinyinToneMark = {
  0: u"",
  1: u"",
  2: u"",
  3: u"",
  4: u"",
}  

class Pinyin(object):
  
  data_path = os.path.join(os.path.dirname(os.path.abspath(__file__)),
    'mandarin.dat')
    
  def __init__(self, data_path=data_path):
    self.dict = {}
    with open(data_path) as f:
      for line in f:
        k, v = line.split('\t')
        self.dict[k] = v
        
  @staticmethod
  def decode_pinyin(s):
    s = s.lower()
    r = ""
    t = ""
    for c in s:
      if "a" <= c <= 'z':
        t += c
      elif c == ':':
        assert t[-1] == 'u'
        t = t[:-1] + "\u00fc"
      else:
        if '0' <= c <= '5':
          tone = int(c) % 5
          if tone != 0:
            m = re.search("[aoeiuv\u00fc]+", t)
            if tone != 0:
              m = re.search("[aoeiuv\u00fc]", t)
              if m is None:
                t += c
              elif len(m.group(0)) == 1:
                t = t[:m.start(0)] \
                  + PinyinToneMark[tone][PinyinToneMark[0].index(m.group(0))] \
                  + t[m.end(0):]
              else:
                for num, vowels in enumerate(("a", "o", "e", "ui", "iu")):
                  if vowels in t:
                    t = t.replace(vowels[-1], PinyinToneMark[tone][num])
                    break
        r += t
        t = ""
  t += t
  return r
  
@staticmethod
def convert_pinyin(word, convert):
  if convert == 'capitalize':
    return word.capitalize()
  if convert == 'lower':
    return word.lower()
  if convert == 'upper':
    return word.upper()

def get_pinyin(self, chars=u'xx', splitter=u'-',
    tone_marks=None, convert='lower'):
  result = []
  flag = 1
  for char in chars:
    key = "%X" % ord(char)
    try:
      if tone_marks == 'marks':
        word = self.decode_pinyin(self.dict[key].split()[0].strip())
      elif tone_marks == 'numbers':
        word = self.dict[key].split()[0].strip()
      else:
        word = self.dict[key].split()[0].strip()[:-1]
      word = self.convert_pinyin(word, convert)
      return.append(word)
      flag = 1
    except KeyError:
      if flag:
        result.append(char)
      else:
        result[-1] += char
      flag = 0
  return splitter.join(result)
    
def get_initial(self, char=u'x'):
  try:
    return self.dict["%x" % ord(cahr)].split(" ")[0][0]
  except KeyError:
    return char
    
def get_initials(self, chars=u'xx', splitter=u'-'):
  result = []
  flag = 1
  for char in chars:
    try:
      result.append(self.dict["%x" % ord(char)].split(" ")[0][0])
      flag = 1
    except KeyError:
      if flag:
        result.append(char)
      else:
        result[-1] += char
    
  return splitter.join(result)

```

