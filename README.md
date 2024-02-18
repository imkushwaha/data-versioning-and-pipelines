# DVC Pipelines

### ML projects consist of multiple stages

- Data collection
- Data processing
- Feature extraction
- Training
- Evaluation
- ..........

### DVC Pipelines make it easy to run stages of an ML pipeline. But how?

- DVC pipelines run a sequence of steps in a smart way, which makes iterating on your project faster.
- DVC automatically determines which parts of a project need to be run.
- It uses something called Directed Acyclic Graph (DAG).
- We can create nodes of DAG and also specify input and output dependencies as well as parameter dependencies of our pipeline.
- DVC automatically determines which parts of a project needs to be run and it caches run and the results to avoid unnecessary reruns.
- 

### What we are going to do?

- We are going to build simple pipeline that consists of a number of steps.
- The first step is going to be to prepare the data
- In second step, we are going to extract some features.
- Next we are going to train our model,
- And lastly we are going to evaluate our model.

### Let's Creates some files

```bash
touch prepare_data.py make_features.py train.py evaluate.py
```

- check the demo code from the repository.

```bash
touch params.yaml
```
- This params name is special to DVC pipelines and when we use a yaml file called params, 
- DVC knows that this file exists and it can read parameters from this yaml file.
- We can also specify a different names for our yaml configuration file,
- However, in that case, while we are running DVC pipelines, we need to specify the file name.

- This yaml configuration file will hold everything we need to run our pipeline.