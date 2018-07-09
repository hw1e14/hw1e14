title: 'Python Transations 库实现有限状态机（Finite-state machine, FSM）'
tags:
  - python
date: 2018-07-09 13:26:40
---


# 以视频播放器为例：

## State List:
- play
- pause
- stop

## Action List:
- toggle
- forward
- backward
- stop

## State Change Table View(list all transtions from one state to another with actions to trigger):
|       | play            | pause            | stop |
|-------|------------------|------------------|------|
| play | forward/backward | toggle           | stop |
| pause | toggle           | forward/backward | stop |
| stop  | toggle           |         -        |   -  |


## Sample Code:
```python
from transitions import Machine

class Player(object):
    pass

model = Player()

states = ['play', 'pause', 'stop']

actions = ['toggle', 'forward', 'backward', 'stop']

transitions = [
    {'trigger': 'forward', 'source': 'play', 'dest': 'play' },
    {'trigger': 'backward', 'source': 'play', 'dest': 'play' },
    {'trigger': 'toggle', 'source': 'play', 'dest': 'pause'},
    {'trigger': 'stop', 'source': 'play', 'dest': 'stop'},
    {'trigger': 'toggle', 'source': 'pause', 'dest': 'play'},
    {'trigger': 'forward', 'source': 'pause', 'dest': 'pause'},
    {'trigger': 'backward', 'source': 'pause', 'dest': 'pause'},
    {'trigger': 'stop', 'source': 'pause', 'dest': 'stop'},
    {'trigger': 'toggle', 'source': 'stop', 'dest': 'play'}]

machine = Machine(model=model, states=states, transitions=transitions, initial='pause')

# Test
print(model.state)    # pause
model.toggle()
print(model.state)  #play
model.stop()
print(model.state)  #stop
```


