# Readme
I built this sample page mainly with python, html, pyscript, and bootstrap.

I also trained 2 other AI models - Xgboost, and Lightboost, with optimization by tunning number of iterations, and max depth, but as at the time of deployment, pyscirpt seems still not supporting Xgboost and LightGBM libraries, so I am forced to drop them. 

In this webapp, I employed 2 simpler models which are Logistic Regression and Gradient Boost.

The LR model is straight from default; while the GB model is optimised as GradientBoostingClassifier(n_estimators=100, max_depth=4).
