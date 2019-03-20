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

```
```

