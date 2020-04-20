# Relationship between weather and influenza incidents
<!-- TABLE OF CONTENTS -->
## Table of Contents

* [About the Project](#about-the-project)
  * [Built With](#built-with)
* [Getting Started](#getting-started)
  * [JupyterLab](#jupyterlab)
  * [Jupyter Notebook](#jupyternotebook)
* [Usage](#usage)
* [Roadmap](#roadmap)
* [Contributing](#contributing)
* [License](#license)
* [Contact](#contact)
* [Acknowledgements](#acknowledgements)

<!-- ABOUT THE PROJECT -->
## About The Project
The goal of this experiment was to model the relationship between weather observations and the prevalence of new influenza infections. It included reading, preparing and transforming data. Subsequently, these data were visualized and used for building a prediction model - we tried to predict influenza infections based on weather conditions.

### Built With
This section should list any major frameworks that you built your project using. Leave any add-ons/plugins for the acknowledgements section. Here are a few examples.
* [Jupyter](https://jupyter.org)

## Getting Started

### JupyterLab

#### Installation
JupyterLab can be installed using `conda` or `pip`. For more detailed instructions, consult the [installation guide](https://jupyterlab.readthedocs.io/en/stable/getting_started/installation.html).

##### conda
If you use conda, you can install it with:

```console
conda install -c conda-forge jupyterlab
```
##### pip
If you use pip, you can install it with:

```console
pip install jupyterlab
```

If installing using `pip install --user`, you must add the user-level `bin` directory to your `PATH` environment variable in order to launch `jupyter lab`.



### Jupyter Notebook

Prerequisite: **Python**
While Jupyter runs code in many programming languages, Python is a requirement (Python 3.3 or greater, or Python 2.7) for installing the JupyterLab or the classic Jupyter Notebook.

#### Installation

##### conda
We recommend installing Python and Jupyter using the conda package manager. The miniconda distribution includes a minimal Python and conda installation.

Then you can install the notebook with:

```console
conda install -c conda-forge notebook
```
##### pip
If you use pip, you can install it with:

```console
pip install notebook
```
To run the notebook, run the following command at the Terminal (Mac/Linux) or Command Prompt (Windows):
```console
jupyter notebook
```
See [Running the Notebook](https://jupyter.readthedocs.io/en/latest/running.html#running) for more details.

## Usage

```python
target_column = ['weekly_infections']
predictors = list(set(list(data_merged.columns))-set(target_column))
data_merged[predictors] = stats.zscore(data_merged[predictors])
#data_merged.describe()

X = data_merged[predictors].values
y = data_merged[target_column].values

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.1, random_state=20)
#print(X_train.shape); print(X_test.shape)

####Support vector regression
#
svr = SVR(kernel = 'rbf', C=10000, gamma='auto', epsilon = 100)
svr.fit(X_train, y_train.ravel()) 
pred_train_svr= svr.predict(X_train)

pred_test_svr= svr.predict(X_test)
print("RMSE of testing data for SVR:\t",np.sqrt(mean_squared_error(y_test,pred_test_svr))) 
print("R2 of testing data  for SVR:\t",r2_score(y_test, pred_test_svr))

pred_final_data_svr = svr.predict(data_merged_predict[predictors])
print("Train:\n", pred_train_svr)
print("\nTest:\n", pred_test_svr)
print("\nFinal prediction:\n", pred_final_data_svr)
```





<!-- CONTRIBUTING -->
## Contributing

Contributions are what make the open source community such an amazing place to be learn, inspire, and create. Any contributions you make are **greatly appreciated**.

1. Fork the Project
2. Create your Feature Branch
```console
git checkout -b feature/AmazingFeature
```
3. Commit your Changes
``console
git commit -m 'Add some AmazingFeature'
```
4. Push to the Branch
``console
git push origin feature/AmazingFeature
```
5. Open a Pull Request
