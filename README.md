# docker_nginx

### Purpose of the repository 
- The repository creates Ubuntu-xenial box and `docker` image with `nginx` installed.

#### List of files in the repository

File name                            | File description 
------------------------------------ | --------------------------------------------------------------
`scripts/provision.sh` | script that installs Ubuntu-xenial.
`.gitignore` | which files and directories to ignore in the repository.
`Vagrantfile` | file with sript that isntalls `docker` and `packer` on the Ubuntu-xenial VM.

### How to use this repository. 
- Install `virtualbox` by following this [instructions](https://www.virtualbox.org/wiki/Downloads).
- Install `vagrant` by following this [instructions](https://www.vagrantup.com/docs/installation/).

- Clone the repository to your local computer: `git clone git@github.com:nikcbg/xenial_docker.git`.
- Go to the cloned repo on your computer: `cd xenial_docker`.
- After that execute the commands in the table below.

Command execution                    | Command outcome
------------------------------------ | --------------------------------------------------------------
`vagrant box list` | to see the list of `vagrant` boxes.
`vagrant init xenial` | to create Vagrantfile if one doesn't already exist.  
`vagrant up` | to power up the xenial VM.
`vagrant ssh` | to log in to the xenial VM.

- Execute `packer -v` to see if `packer` is installed and its version, the output will display the following:

```
1.3.2
```

- Execute `docker -v` to see if `packer` is isntalled and its version, the output will display the following:

```
Docker version 17.03.2-ce, build f5ec1e2
```


### Commands needed to test with `kitchen`.

Command execution                    | Command outcome
------------------------------------ | --------------------------------------------------------------
`bundle exec kitchen list` | to list `kitchen` instances.
`bundle exec kitchen converge` | to create `kitchen` environment.
`bundle exec kitchen verify` | command to execute `kitchen` test.
`bundle exec kitchen destroy` | to destroy `kitchen` environment.
`bundle exec kitchen test` | to automatically build, test and destroy `kitchen` environment.

### TO DO:
- Check if `nginx` server is installed and running. 
