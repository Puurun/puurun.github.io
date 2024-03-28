---
title: Factory Method
date: 2024-03-28 02:50:00
categories: [Design Patterns]
tags: [design-patterns, factory]
---


# Factory
## 무엇인가? 
- 객체를 만드는 것을 목적으로 하는 클래스.
- 객체를 직접적으로 만드는 대신, Factory 를 통해 객체를 얻는다.
- Factory 객체를 이용하는 부분을 Client Code라고 부른다.


## 왜 필요할까?
- 객체를 직접적으로 만들면 각 상황에 대한 처리를 조건문 등으로 처리를 해줘야 한다.

## 좋은 점
- 객체를 얻는 방법은 다양할 수 있으므로, pool에서 객체를 얻어오는 등의 구현이 가능하다.
- Abstract Class로 구현을 하면 객체 생성을 유연하게 할 수 있다.
- SRP를 지킬 수 있다.

### 예시
- 그림을 그리는 앱을 만든다고 해보자
- 이 앱에서는 세모, 네모, 동그라미 등, 도형들을 구분해서 그릴 수 있다.

- Board 객체에서 shape를 만드는 responsibility를 분리하였다.
- 만약에 따른 방식으로 shape를 만드는 Factory가 필요하다면, Factory만 다른 것을 쓰면 된다.
- 아래의 예시에서는 두 Factory가 있다.
    - NormalShapeFactory: 단순하게 객체를 생성해서 돌려준다.
    - PoolingShapeFactory: Pooling으로 방식으로 객체를 돌려준다.
- NormalShapeFactory, PoolingShapeFactory가 각각 장단점이 있다고 하면, 상황에 따라 다른 것을 고르면 된다.
    - e.g. PoolingShapeFactory는 빠른 대신, 메모리를 지속적으로 잡아먹는다. 하드웨어에 따라 다른 것을 선택해야 할 수도 있다.

``` python
from abc import ABCMeta, abstractmethod

class Board:
    def __init__(self):
        self.shape_factory = NormalShapeFactory()
        self.shapes = []

    def enable_memory_save(self):
        self.shape_factory = PoolingShapeFactory()

    def create(self, **kwargs):
        shape = self.shape_factory.create(shape_type)
        self.shapes.append(shape)

    def render(self):
        for shape in shapes:
            shape.render()


class ShapeFactory(metaclass=ABCMeta):
    @abstractmethod
    def create(self, shape_type, **kwargs): ...

class NormalShapeFactory(ShapeFactory):
    def create(self, shape_type, **kwargs):
        if shape_type == "square":
            return Square()
        elif shape_type == "circle":
            return Circle()
        elif shape_type == "triangle":
            return Triangle()
        else:
            return None

class PoolingShapeFactory(ShapeFactory):
    def create(self, shape_type, **kwargs):
        # Some kind of pooling mechanism to get objects



```


