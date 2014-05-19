---
title: "python test"
layout: post
photo_url: "http://ww4.sinaimg.cn/mw600/94d3f261gw1dvanmieo5fj.jpg"
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

