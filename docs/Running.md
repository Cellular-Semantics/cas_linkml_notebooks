## How to run notebooks

To run the notebooks, please follow the given steps:

1- Create a virtual environment:

```
python3 -m venv venv
source venv/bin/activate

pip install ipykernel
python3 -m ipykernel install --user --name=venv
```

2- Install and run Jupyter notebook:

```
pip install notebook
jupyter notebook
```
