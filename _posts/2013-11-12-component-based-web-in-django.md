---
layout: single
title: Component based web in Django
tags: [django, web, component]
---
## Goal
- Fast product development and iteration
- Code reusable and readability
- Easy for testing
- component organise code and enable reusable(self contained for rendering)
- No magic - use workflow to introduce this

## Component
With in a defined component, fetch all the data it needed, then output html

- Abstraction for components
- Rendering HTML
- Fetching data
- Self-contained(components can be replaced and dropped anywhere)

```python
class SideBar(WebNode):
    template = 'test.html'
  
    def __init__(self, param1, param2)
        self.param1 = param1
        self.param2 = param2
        ...
 
    def render(self):
        ...
        return ctx      
```

- performance have some influence, depends on particle size(like function calls)

## Interactive between Front-End and Back-End

### New developing flow
Product design -\> (FrontEnd and BackEnd programing at the same time) -\> integration

- Back-End: prepare data with raw template, not ui required
- Front-End: use demo data to generate ui and implement interactive design

### Data interface
- variable in template (mock works prefect, have a talk before dev)
- ajax (need to design the format(code, message, data))
- mention: validation of params

## MVC - Decoupling
- components(read only) as `V` \> models
- controllers(read & write) \> models
- http for context

This will make views and templates into pieces and looks not that huge.

# An implementation for this idea
[https://github.com/iamsk/django-webnodes][1]

[1]:	https://github.com/iamsk/django-webnodes