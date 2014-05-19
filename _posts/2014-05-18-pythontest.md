---
title: "python test"
layout: post
photo_url: "http://pic.baike.soso.com/p/20130621/20130621093244-1217468372.jpg"
comments: yes
---


```python
import gc, os, psutil
def test():
  x = 0
  for i in range(10000000):!
  # xrange
  x += i
  return x
def main():
  print test()
  gc.collect()
  p = psutil.Process(os.getpid())
  print p.get_memory_info()
  if __name__ == "__main__":
   main()
main()

```
以上是一小段python代码,仅供测试！

