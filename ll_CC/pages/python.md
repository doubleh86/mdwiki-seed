# Python

## MAC OS X python3.6 설치

1. Homebrew 설치
	- $ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

2. brew install python3 실행	

## python 웹 서버 실행 

```
python3.6 -m http.server ( python 3.x )

python -m SimpleHTTPServer ( python 2.x )

```

## matplotlib docker 실행 시 png로 이미지 저장

```python

import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt

... do something ...

plt.savefig('./name.png')

```

## matplotlib 와 psutil을 이용한 그래프 그리기 예제 

```python

"""
    Script Version: v0.1
    Author: DoubleH

    Matplotlib 를 이용한 그래프 그리기
    아직 간단한 선 그리는 것만 가능하다

"""
import matplotlib.pyplot as plt
import matplotlib.animation as animation
import time
from collections import deque

import numpy as np
from monitoring.utils.SystemInfo import SystemInfo as sys_info


class ProcessGraph(object):
    """
    matplotlib를 이용하여 그래프를 그리기 위한 클래스
    """

    def __init__(self, x_label="X", y_label="Y", x_limit=None, y_limit=None, figure_number=1):
        self.x_label = x_label
        self.y_label = y_label
        self.x_limit = x_limit
        self.y_limit = y_limit
        self.plt = plt
        self.fig = plt.figure()
        self.figure_number = figure_number
        self.animation = None

        if figure_number < 2:
            self._init_plot()

    def _init_plot(self):
        """
        그래프가 하나일 경우 초기화를 한다
        :return:
        """
        if self.x_limit is not None:
            self.plt.xlim(self.x_limit)

        if self.y_limit is not None:
            self.plt.ylim(self.y_limit)

        self.plt.xlabel(self.x_label)
        self.plt.ylabel(self.y_label)

    def _set_data(self, x_data, y_data):
        """
        데이터를 초기화 한다
        :param x_data:
        :param y_data:
        :return:
        """
        self.plt.plot(x_data, y_data)

    def add_subplots(self, x_data, y_data, row=1, col=1, number=1, **kwargs):
        """
        서브 그래프를 그린다
        :param x_data: x 축 데이터
        :param y_data: y 축 데이터
        :param row: 그려질 행
        :param col: 그려질 열
        :param number: 몇 번 subplot에 그릴 것인가
        :param kwargs: x_limit, y_limit (x, y 축 최대 값) tuple ex) x_limit=(0, 100), y_limit=(0, 100)
        :return:
        """
        ax = self.fig.add_subplot(row, col, number)

        if 'x_limit' in kwargs:
            ax.set_xlim(kwargs['x_limit'])

        if 'y_limit' in kwargs:
            ax.set_ylim(kwargs['y_limit'])

        ax.plot(x_data, y_data)

    def show_graphs(self):
        """
        그래프를 그린다
        :return:
        """
        self.plt.show()

    def show_one_graph(self, x_data, y_data):
        """
        하나의 그래프만 그리기 위해 사용
        :param x_data:
        :param y_data:
        :return:
        """
        if self.figure_number > 1:
            raise Exception('Figure Count : ' + str(self.figure_number))
        self._set_data(x_data, y_data)
        self.show_graphs()

    def save_one_graph_image_file(self, x_data, y_data, file_name=None, file_extension='png'):
        """
        하나의 그래프를 이미지로 저장한다
        :param x_data:
        :param y_data:
        :param file_name:
        :param file_extension:
        :return:
        """
        if not file_name:
            file_name = str(time.time())
        self._set_data(x_data, y_data)
        self.plt.savefig(file_name + '.' + file_extension)

    def cpu_real_time_graph(self):
        ax = plt.axes(xlim=(0, 200), ylim=(0, 100))
        line, = ax.plot([], [])
        line.set_data([], [])

        y_data = deque([-1] * 400)
        x_data = deque([np.linspace(200, 0, num=400)])

        def wrapper(i):
            y_data.pop()
            y_data.appendleft(sys_info.get_cpu_usage(None, False))
            line.set_data(x_data, y_data)
            return line,

        self.animation = animation.FuncAnimation(self.fig, wrapper, frames=200, interval=100, blit=True)

    def memory_usage_real_time_graph(self):
        ax = plt.axes(xlim=(0, 200), ylim=(0, 100))
        line, = ax.plot([], [])
        line.set_data([], [])

        y_data = deque([-1] * 400)
        x_data = deque([np.linspace(200, 0, num=400)])

        def wrapper(i):
            y_data.pop()
            memory_info = sys_info.get_memory_info()
            y_data.appendleft(memory_info.percent)
            line.set_data(x_data, y_data)
            return line,

        self.animation = animation.FuncAnimation(self.fig, wrapper, frames=200, interval=100, blit=True)


```

## psutil 을 이용한 시스템 정보 가져오는 방법

```python

"""
    utils.SystemInfo

    시스템 정보를 가져오기 위해 psutil 라이브러리를 사용하여 SystemInfo class를 작성
"""

import psutil
from collections import namedtuple


class SystemInfo(object):
    """
    SystemInfo 정보를 가져오기 위한 psutil library wrapping class
    """
    @classmethod
    def get_core_count(cls):
        """
        CPU의 코어 개수를 가져온다
        :return: [물리 CPU, 논리 CPU]
        """
        return [psutil.cpu_count(), psutil.cpu_count(logical=False)]

    @classmethod
    def get_cpu_usage(cls, interval=1, percpu=True):
        """

        :param interval: CPU 사용량 체크 시간
        :param percpu: 전체 CPU or 각각의 CPU 사용량을 가져 올건지에 대한 True / False flag ( True 면 각각의 CPU 의 상태를 가져온다
        :return: CPU 사용량 ex) 10.0 or [ 10.0, 2.0, 3.0, 12.0 ]
        """
        return psutil.cpu_percent(interval=interval, percpu=percpu)

    @classmethod
    def get_memory_info(cls):
        """
        시스템의 메모리 정보를 가져온다
        :return: Memory namedtuple ( total : 전체 물리 메모리
                                     Percent : 메모리 사용량
                                     AVAILABLE : 사용 가능한 메모리
                                     USED : 사용 중인 메모리
        """
        Memory = namedtuple('Memory', 'total percent available used')
        total = SystemInfo.byte_to_gigabyte(psutil.virtual_memory().total)
        percent = psutil.virtual_memory().percent
        used = SystemInfo.byte_to_gigabyte(psutil.virtual_memory().used)
        free = SystemInfo.byte_to_gigabyte(psutil.virtual_memory().available)

        return Memory(total, percent, free, used)

    @classmethod
    def byte_to_gigabyte(cls, byte_value):
        """
        byte value to gigabyte value helper method
        (1024 ^ 3) or byte >> 30
        :param byte_value: 기가바이트로 변경할 바이트
        :return:
        """

        return float("{0:.2f}".format(byte_value / (1024 ** 3)))


```

## Python Websocket Server / Unity WebGL Client

- Server <-> Client 패킷 전송을 위해 Python Server 에선 string 데이터를 bytes로 변환하여 보내야한다. 

```python

await websocket.send(str.encode(greeting))

```

- WebSocket library 

```
	https://github.com/crossbario/autobahn-python
	https://pawelmhm.github.io/python/websockets/2016/01/02/playing-with-websockets.html
```

## Python Type hinting

```python
# https://www.python.org/dev/peps/pep-0526/

from typing import Dict, List

class MyClass(object):
	def __init__(self):
		
		self.myDict # type: Dict[str, int]
		
		self.myDict2: Dict[str, User] = {}
		
		self.myList # type: List[int]

```

## Python backend - C# list json 사용 시 유의사항

- python 에서 str(list) 를 사용하여 문자열 데이터를 assign한 후 json 문자열로 변환 하면 문자열이 "{'data': 'test'}" 이런식으로 " ' " 가 붙는다. C# 클라이언트의 경우 " ' " 문자열로 인식을 못하여 json을 object 시키지 못한다. object에 list 데이터를 그대로 넣고 ujson.dumps()를 하면 {"data": "test"} 이런식으로 문자열이 만들어 진다. ( 아래 예제는 ujson package를 사용 함. )

```python
	class jsonConvertObject(object):
		def __init__(self, list_data: List[str]):
			self.data = list_data

		def convert_to_json_string(object):
			return ujson.dumps(self)

```

## Python namedTuple로 객체 만들기

namedtuple('Object Name', 'variable_1 variabel_2 ... ')

```python
Memory = namedtuple('Memory', 'total percent available used')
memory = Memory(100, 20, 30, 40)

print(memory.total)
```

## Python 3항 연산

```
방법 1 and or 사용:
    (Condition) and (Condition True) or (Condition False)

    이 방법을 사용하였을 경우 아래와 같은 경우 0이 False를 의미 하기 때문에 원하는 결과가 나오지 않는다.

    a = 10
    b = 10
    result = a == b and a-b or a+b    # 결과는 a+b = 20 ???????


방법 2 if else 사용:
    (Condition True) if (Condition) else (Condition False)
```


## Abstract class
```python
from abc import *

class AbstractClass(metaclass=ABCMeta):
    def __init__(self):
        pass

    @abstractmethod
    def abstract_method(self):
        pass

```
## Pylint install

- pip install ( python 3.x ) 

```
    $ pip3.6 install pylint
```

- pycharm setting 

```
    https://stackoverflow.com/questions/38134086/how-to-run-pylint-with-pycharm
```

## 기본 문법들
 - list
 -1- https://codeburst.io/python-basics-6-lists-and-list-manipulation-a56be62b1f95

## Python command pattern

- https://github.com/doubleh86/Design-Patterns-in-Python/blob/master/command.py

## 참고 사이트

- 튜토리얼
https://github.com/golbin/TensorFlow-Tutorials

- Memory 최적화
http://tech.oyster.com/save-ram-with-python-slots/

- 파이썬 기본 문법

