# docker_nginx

### Purpose of the repository 
- The repository creates Ubuntu-xenial box and `docker` image with `nginx` installed.

#### List of files in the repository

File name                            | File description 
------------------------------------ | --------------------------------------------------------------
`scripts/provision.sh` | script that installs Ubuntu-xenial.
`.gitignore` | which files and directories to ignore in the repository.
`Vagrantfile` | file with sript that isntalls `docker` and `packer` on the Ubuntu-xenial VM.
`template.json` | template with code for `packer` tool to create `docker` image and install `nginx`.

### How to use this repository. 
- Install `virtualbox` by following this [instructions](https://www.virtualbox.org/wiki/Downloads).
- Install `vagrant` by following this [instructions](https://www.vagrantup.com/docs/installation/).
- Clone the repository to your local computer: `git clone git@github.com:nikcbg/docker_nginx.git`.
- Go to the cloned repo on your computer: `cd docker_nginx`.
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
- You need to be logged into your VM (`vagrant ssh`) to be able to build the `docker` image  with `packer` and run `kitchen` tests.
- After you login to the VM execute `cd /vagrant` to work in the `vagrant` directory.

### Creating and configuring the `docker` image.
- Execute `packer validate template.json` to validate the template.
- Execute `packer build template.json` to start building the `docker` image. 


### TO DO:
- Check if `nginx` server is installed and running. 
