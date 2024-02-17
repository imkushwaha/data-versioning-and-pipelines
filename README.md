# Data Versioning Control

- DVC also uses git to verison the information of our data

### Intialize an empty git repository in data directory

```bash
git init
```

### Intialize dvc

```bash
dvc init
```

### I will version the images present in images folder

```bash
dvc add ./images
```

### Now, to tarck the changes with git, run

```bash
git add images.dvc .gitignore
```

### After that we need to commit our changes

```bash
git commit -m <commit message>
```

- DVC add moved the data to the projects cache and linked it back to the workspace tree.
- hash value of the images, get added.
- to check cache, we can run:
  
```bash
tree .dvc/cache
```

- since these images won't be stored on Git because DVC automatically added these images into gitignore file.
- Now we need to store these images somewhere else, because as we see DVC only keeps the information.
- Then later on, DVC keeps track of these images for us.
- It is just data versioning like git, which keeps information about the changes in our dataset.
- The next step is to store and share the this data.
- As we used to store our code that is tracked by Git, we need a storage for our data which is tracked by DVC.

- There are multiples options for this:
- It can be local storage in our machine.
- It can be google drive, AWS S3 bucket.
- It can be Azure Blob Storage or it can be Google Cloud Storage and so on.

- Here we will store our images in Google Drive!!

### How can we specify a storage for DVC

```bash
dvc remote add -d <name-of-the-storage> <storage-uri>
```

### Now push the data we have here into our remote storage

- Please install dvc[gdrive]

```bash
pip install "dvc[gdrive]" 
```

```bash
dvc push
```
- Provide required authentication.


### Now let's remove the cache (we saw here DVC stored the images) to see how we can retrieve the images we are storing in our remote storage

```bash
rm -rf .dvc/cache
```

- Also remove our images folder from here because DVC is tracking it right now

```bash
rm -rf ./images
```

- Now to pull the images, just run

```bash
dvc pull
```

- Since DVC knows everything about our data, where we are storing it, the names of them and so on.
- DVC knows everything necessary to pull this data back here


### Now let's say we want to make some changes into our dataset

- Let's see we add one new image and train our model with these new images.
- The one image which we just add into our images dir is not tracked by DVC because we just added them.

- Let's check DVC status

```bash
dvc status
```

- Here we can see that images folder is modified
- Now we need to update our DVC in order to track this new image

```bash
dvc add ./images
```
- now next we can run

```bash
git add images.dvc
```

- now we need to do commit

```bash
git commit -m <commit-message>
```

- And lastly, i need to push new images into my remote repository

```bash
dvc push
```

### Here we are using DVC and it's very easy for us to go back to first version of our data.

- DVC only keeps track of the information of the files and it stores everything inside <folder-name>.dvc
- Here in this case, images.dvc
- We can use git commit hash id to go to other version of data
- To get the hash id of git commit, we can run


```bash
git log
```

- After copying the hash id of git commit, we can run:

```bash
git checkout <git-commit-hash-d>
```

- remove .dvc/cache and images directory and run

```bash
git pull
```

- There is also a better way to handle switching between different versions of our data using DVC.
- It will be much simpler than this.
- Actually we can use just YAML file ans we will have a version key and we will specify the version which we need.
- And everything will be done for us automatically.
- We won't need to worry about this checkout and going back to some previous commit and so on.