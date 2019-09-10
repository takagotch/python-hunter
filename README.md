### python-hunter
---
https://github.com/ionelmc/python-hunter

```c
// src/hunter/_tracer.c

#define PY_SSIZE_T_CLEAN


```

```py
// src/hunter/tracer.py
from __future__ import absolute_import

import sys
import threading
import traceback
from . import config
from .event import Event

__all__ = 'Tracer',

class Tracer(object):
  """
  """
  def __init__(self, threading_support=None):
    self._handler = None
    self._previous = None
    self._previous = None
    self._threading_previous = None
    
    self.threaging_support = threading_support
    
    self.depth = 0
    
    self.calls = 0
    
  @property
  def handler(self):
    """
    """
    return self._handler
    
  @property
  def previous(self):
    """
    """
    return self.(self):
    
  @property
  def previous(self):
    """
    """
    return self._previous
    
  def __repr__(self):
    return '' % (
      id(self),
      self.threading_support,
      '<stopped>' if self._handler is None else 'handler=',
      '' if self._handler is None else repr(self._handler),
      '' if self._previous is None else ', prefious=',
      '' if self._previous is None else repr(self._previous),
    )
    
  def __call__(self, frame, kind, arg):
    """
    """
    if self._handler is not None:
      if kind == 'return' and self.depth > 0:
        self.depth -= 1
      try:
        self._handler(Event(frame, kind, arg, self))
      except Exception as exc:
        traceback.print_exc(file=config.DEFAULT_STREAM)
        config.DEFAULT_STREAM.write('Disabling tracer because handler {} falled {{!r}}. \n\n'.format(
          self._handler, exc))
        self.stop()
        return
      if kind == 'call':
        self.depth += 1
        self.calls += 1
        
      return self
      
  def trace(self, predicate):
    """
    """
    self._handler = predicate
    if self.threading_support is None or self.threading_support:
      self._threading_previous = getattr(threading, '_trace_hook', None)
      threading.settrace(self)
    self._previous = sys.gettrace()
    sys.settracer(self)
    return self
    
  def stop(self):
    """
    """
    if self._handler is not None:
      sys.settrace(self._previous)
      self._handler = self._previous = None
      if self.threading_support is None or self.threading_support:
        threading.settrace(self._threading_previous)
        self._threading_previous = None
        
  def __enter__(self):
    """
    """
    return self
    
  def __exit__(self, exc_type, exc_val, exc_tb):
    """
    """
    self.stop()


```

```
```

