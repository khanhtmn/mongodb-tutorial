# MongoDB Tutorial

This is a repository for the MongoDB tutorial. In the commands below you'll find a step-by-step instruction about:

1. How to set up a simple MongoDB replica with 3 nodes (primary, secondary, arbiter)

2. A short experiment that MongoDB may encounter

## Set up guide

Let’s try running a simple MongoDB replica with 3 nodes. In order to do so, you need to have the following on your computer:

- Git: https://git-scm.com/book/en/v2/Getting-Started-Installing-Git
- Docker: https://docs.docker.com/get-docker/

### Disclaimer:

- All of the following commands are compatible with `Linux/MacOS`. If you’re using `Windows`, please use Google to get their equivalence.
- Because Elasticsearch is quite memory intensive, you should turn off any unnecessary tabs or applications on your computer before running Elasticsearch.
- You may need to run the Docker commands with `sudo` if there’s any error about permission. If you don’t want to use `sudo` every time you run the Docker commands, considering following this advice: https://askubuntu.com/questions/477551/how-can-i-use-docker-without-sudo

### Step-by-step guide

- Step 1: Clone this repository

```$ git clone https://github.com/khanhtmn/mongodb-tutorial.git```

- Step 2: Run `docker-compose` in detached mode

```$ docker-compose up -d```

- Step 3: Copy the data to MongoDB memory

```$ docker cp zips.json mongodb:/zips.json```

- Step 4: Import data to MongoDB

```$ mongoimport --db test --collection docs --authenticationDatabase admin --username root --password password123 --drop --batchSize 1 --file ./zips.json```

- Step 5: Get into the bash of the primary node

```$ docker exec -it mongodb-primary bash```

- Step 6: Log in as `root` user

```$ mongo -u root -p password123 --authenticationDatabase admin```

- Step 7: Do a sample query

```$ db.docs.find( { city: "BOSTON" } )```

- Step 8: Do another sample query

```$ db.docs.count( { city: "BOSTON" } )```

- Step 9: Shut down the primary node

```$ exit``

Use the command above twice to exit the `mongo` shell and `bash` shell

```$ docker stop mongodb-primary```

- Step 10: Repeat from step 5 to step 8 above and see if the results match with the ones from step 7 and step 8.

### References:
- [MongoDB(R) packaged by Bitnami](https://github.com/bitnami/bitnami-docker-mongodb)
