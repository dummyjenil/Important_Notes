```python
from  setuptools  import  find_packages, setup

  

setup(

name='dash2html',

packages=find_packages(),

version='1.0.2',

description='Convert Plotly Dash App To Static HTML File',

author='Jenil sheth',

author_email="shethjeniljigneshbhai@gmail.com",

install_requires=["flask","dash","requests"],

long_description=open('README.md').read(),

long_description_content_type="text/markdown",

)
```
---
```bash
python setup.py sdist bdist_wheel
```
```bash
twine upload dist/*
```
