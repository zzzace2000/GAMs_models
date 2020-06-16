# Generalized additive models used in the paper "How Interpretable and Trustworthy are GAMs?"

This repo is a simplified version designed to use the GAM models with your own datasets.
In this repo, we provide the following GAMs implementation in python:
1. XGB (xgboost with depth 1 and visualized as a GAM)
2. Spline (both pygam package and R mgcv package)
3. Fused Lasso Additive Model (FLAM)
4. Logistic Regression

To fully reproduce the paper's result, please see the repo https://github.com/zzzace2000/GAMs

## Install

We use the following python packages:
```
 pip install pandas scikit-learn numpy seaborn xgboost interpret rpy2 pygam
```

We also use the R packages to run the R spline and FLAM models. To install:
1. If you already have R installed, go into the R console and run
```
install.packages('mgcv')
install.packages('flam')
```

2. If you do not have R installed and are using conda environment, you can do:
```
conda install -c r r r-mgcv
```
Then install flam inside R console (run ``` R() ```):
```
install.packages('flam')
```

## Usages

The main usages are similar to scikit-learn models:
```
from arch import MyXGBClassifier, MyBaggingClassifier
xgb = MyXGBClassifier(max_depth=1)

# And do a bagging 20 times
xgb = MyBaggingClassifier(base_estimator=xgb, n_estimators=20)
xgb.fit(X, y)

df = xgb.get_GAM_plot_dataframe()
df.head()
```

The dataframe would have all the shape plots details and feature importances. Then you can visualize by:
```
from vis_utils import vis_main_effects

fig, axes = vis_main_effects({
    'XGB': xgb.get_GAM_plot_dataframe(),
})
```

See the main.ipynb for how to use.

## Citations

If you find the code useful, please cite:
```
@article{chang2020interpretable,
  title={How Interpretable and Trustworthy are GAMs?},
  author={Chang, Chun-Hao and Tan, Sarah and Lengerich, Ben and Goldenberg, Anna and Caruana, Rich},
  journal={arXiv preprint arXiv:2006.06466},
  year={2020}
}
```
