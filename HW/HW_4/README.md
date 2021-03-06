## Part 1

The solution is present in part_1/ folder.

```bash
cd part_1/first && docker build -t first .    # Build the first container
cd ../second && docker build -t second .      # Build the second container
docker run -d --name first first              # Run the first containre
docker run -t -i --link first:file_io second curl file_io:9001    # Run second container in linked mode to first container to get o/p
```

![part 1 demo](http://i.imgur.com/ewDeI3b.gif)

## Part 2

Instruction for running the 4 containers:

1. Create 2 separate Digital ocean droplets. Enable private networking between them so that they can have passwordless ssh.
2. Install docker and docker-compose
3. One first instance, run `docker-compose up` inside the `part_2/first_vm/` directory.
4. One second droplet, edit the ip address inside `part_2/second_vm/docker-compose.yml` to poin the ip address of first droplet.
5. run `docker-compose up -d` inside the `part_2/second_vm/` directory.
6. Make rest call to localhost:7379 in order to communicate to redis.

![part ii demo](http://i.imgur.com/rxtev9L.gif)

## Part 3
- Initialization of bare repos:
```bash
# Initialize bare metal repos blue and green
cd ~
mkdir /home/nirmesh/semester_3/deploy/blue.git
mkdir /home/nirmesh/semester_3/deploy/green.git
cd blue.git && git init --bare
cd green.git && git init --bare

# Define remote of App
cd ~/App
git remote add blue file:///home/nirmesh/semester_3/deploy/blue.git
git remote add green file:///home/nirmesh/semester_3/deploy/green.git
```
- Copy the hooks to appropriate repos, an name them appropriately.
- Once all this is done, on each commit, the new docker image `my_app` will be created with latest code in repo and will be pushed to `localhost:5000/my_app:latest`.
- On each push to either blue.git or green.git, the respective repositories will download the latest image from localhost:5000 and run them with respective names.

The three git hooks required are given in part_3/ folder

![Imgur](http://i.imgur.com/SrIIRnr.gif)










