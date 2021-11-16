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

- Step 2: `cd` to the repository

```$ cd mongodb-tutorial```

- Step 3: Run `docker-compose` in detached mode

```$ docker-compose up -d```

- Step 4: Copy the data to MongoDB memory

```$ docker cp zips.json mongodb-primary:/zips.json```

- Step 5: Get into the `bash` shell of the primary node

```$ docker exec -it mongodb-primary bash```

- Step 6: Import data to MongoDB

```$ mongoimport --db test --collection docs --authenticationDatabase admin --username root --password password123 --drop --batchSize 1 --file ./zips.json```

- Step 7: Log in as `root` user. Now we are in the `mongo` shell

```$ mongo -u root -p password123 --authenticationDatabase admin```

- Step 8: Check the status of the replica

``` rs.status()```

- Step 9: Check the members of the replica

```rs.status.members()```

- Step 10: Do a sample query

```$ db.docs.find( { city: "BOSTON" } )```

- Step 11: Do another sample query

```$ db.docs.count( { city: "BOSTON" } )```

- Step 12: Exit the `mongo` shell and `bash` shell

```
$ exit
$ exit
``` 

**Note**: Use the command above **twice** to exit both the `mongo` shell and `bash` shell

- Step 13: Shut down the primary node

```$ docker stop mongodb-primary```

- Step 14: Get into the `bash` shell of the secondary node

```$ docker exec -it mongodb-secondary bash```

- Step 15: Repeat from `step 7` to `step 11` above and compare the results with the previous run

- Step 16: Shut down the replica

Again, exit the shell twice

```
$ exit
$ exit
$ docker-compose down
```

### References:
- [MongoDB(R) packaged by Bitnami](https://github.com/bitnami/bitnami-docker-mongodb)
