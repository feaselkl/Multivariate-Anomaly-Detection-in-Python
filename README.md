# Implementing Multivariate Anomaly Detection in Python

This is the repository for my talk entitled Implementing Multivariate Anomaly Detection in Python.

## The Shape of the Solution

For learning purposes, I have split the multivariate outlier detection process into three files.  There's no "real-world" reason to do this but it does make it easier to see the differences as we extend an ensemble.

`multivariate1` covers the Connectivity-Based Outlier Factor (COF) technique.

`multivariate2` covers COF and Local Correlation Integral (LOCI).

`multivariate3` is the final product, covering COF, LOCI, and Copula-Based Outlier Detection (COPOD).

## Running the Code

If you are running things locally, make sure you install the necessary requirements in `requirements.txt`:

```python
pip install --no-cache-dir --upgrade -r requirements.txt
```

Then, kick off the API process with the following command from the `code\src\` folder:

```python
uvicorn app.main:app --host 0.0.0.0 --port 80
```

Note that you may need to run the following command instead:

```python
python -m uvicorn app.main:app --host 0.0.0.0 --port 80
```

If you want to use a Docker-based solution, you should not need to modify the `Dockerfile` at all.  If you are proficient with Docker, you may also wish to build one image based on the completed code and tag it separately:

```python
docker build -t anomalydetector_complete .
```

Then, when building your own version of the detector, tag it like so:

```python
docker build -t anomalydetector .
```

This will allow you to compare how your service behaves compared to the final version.

You can kick off the container by running the following command:

```bash
docker run --name anomalydetector -p 80:80 anomalydetector
```

## Running Tests

All of the integration and unit tests we use in this book are included in the `\code\test` folder.

### Unit Tests

All of the unit tests for this book are located in `code\test\` and have names starting with `test_`.  If you wish to run the unit tests, ensure that you have the PyTest library installed--which you will if you installed all packages in `requirements.txt`--and run the following command:  `pytest test_{file to run}`.  For example:

```python
pytest test_multivariate1.py
```

Note that this does **not** require that you have the API running, as these are unit tests.  It does require you to be in the `\code\test` folder and that relevant code be in `\code\src\app\`.

### Postman Integration Tests

The [Postman](https://www.postman.com/) application will allow you to run all of the integration tests, which you can find in `code\test\postman_integration_tests\`.  Import the collection in the Postman app by selecting the "Import" button and choosing the appropriate file to import all integration tests.  Note that there are no environment settings for these tests and they assume that you are running the API on port 80.

## Streamlit Dashboard

The Streamlit dashboard is located in `\code\src\web\` and you can kick it off by running the following command:

```python
streamlit run site.py
```

Note that you may need to run the following command instead:

```python
python -m streamlit run site.py
```
