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
`test/integration/default/check_pkg.rb` | script needed by kitchen to check if `nginx` is installed.
`.kitchen.yml` | configuration file for `kitchen`.
`Gemfile` | used for ruby dependencies.

### How to use this repository. 
- Install `virtualbox` by following this [instructions](https://www.virtualbox.org/wiki/Downloads).
- Install `vagrant` by following this [instructions](https://www.vagrantup.com/docs/installation/).
- Clone the repository to your local computer: `git clone git@github.com:nikcbg/docker_nginx.git`.
- Go to the cloned repo on your computer: `cd docker_nginx`.
- After that execute the commands in the table below.

Command execution                    | Command outcome
------------------------------------ | --------------------------------------------------------------
`vagrant up` | to power up the xenial VM.
`vagrant ssh` | to log in to the xenial VM.

- You need to be logged into your VM (`vagrant ssh`) to be able to build the `docker` image  with `packer` and run `kitchen` tests.
- Execute `packer -v` to make sure `packer` is installed and check its version, the output will display the following:

```
1.3.2
```

- Execute `docker -v` to see make sure `packer` is isntalled and check its version, the output will display the following:

```
Docker version 17.03.2-ce, build f5ec1e2
```

- After you login to the VM execute `cd /vagrant` to work in the `vagrant` directory.

### Creating and configuring the `docker` image.
- Execute `packer validate template.json` to validate the template.
- Execute `packer build template.json` to start building the `docker` image, successful build output will display the following:
```
Build 'docker' finished.

==> Builds finished. The artifacts of successful builds are:
--> docker: Imported Docker image: sha256:3c16e873e8e57727da17d55f35642d6f4428e2f9bacc3b9b72f97f5150f39301
--> docker: Imported Docker image: nginx:0.1
```
-Once the image is ready you need to set up your testing environment. The testing environment have to be set up on the Ubuntu-xenial VM where you build the `docker` image.

### Setting up `ruby` testing environment on Ubuntu 16.04 instructions:

- Execute `sudo apt update` to update the packages on your Ubuntu VM.
- Execute `sudo apt-get install autoconf bison build-essential libssl-dev libyaml-dev libreadline6-dev zlib1g-dev libncurses5-dev libffi-dev libgdbm3 libgdbm-dev` to install `ruby` dependencies.
- Execute `git clone https://github.com/rbenv/rbenv.git ~/.rbenv` to clone `rbenv` repo. 
- Execute `echo 'export PATH="$HOME/.rbenv/bin:$PATH"' >> ~/.bashrc` to change your `~/.bashrc` file to use `ruby` command line utility
- Execute `echo 'eval "$(rbenv init -)"' >> ~/.bashrc` so `rbenv` loads automatically.
- Execute `source ~/.bashrc` to reload `bash` profile.
- Execute `type rbenv` command to verify that `rbenv` is set up properly, the output will display the following:

```
rbenv is a function
rbenv () 
{ 
    typeset command;
    command="$1";
    if [ "$#" -gt 0 ]; then
        shift;
    fi;
    case "$command" in 
        rehash | shell)
            eval `rbenv "sh-$command" "$@"`
        ;;
        *)
            command rbenv "$command" "$@"
        ;;
    esac
}
```
- Next execute the commands in the table below:

Command execution                    | Command outcome
------------------------------------ | --------------------------------------------------------------
`rbenv install 2.3.1` | to install `ruby 2.3.1` version.
`rbenv local 2.3.1` | to set the default version of `ruby` to your local directory.
`rbenv -v` |to make sure `ruby` is installed and you have the correct version.
`gem install bundler` | to install `gem` which is package manager for `ruby`.

- After this we should have our testing environment set up and ready for testing. 

### Commands needed to test with `kitchen`.

Command execution                    | Command outcome
------------------------------------ | --------------------------------------------------------------
`bundle exec kitchen list` | to list `kitchen` instances.
`bundle exec kitchen converge` | to create `kitchen` environment.
`bundle exec kitchen verify` | command to execute `kitchen` test.
`bundle exec kitchen destroy` | to destroy `kitchen` environment.
`bundle exec kitchen test` | to automatically build, test and destroy `kitchen` environment.

- If the command/s complete successfully the output will display the following:

```
  System Package nginx
     ✔  should be installed

Test Summary: 1 successful, 0 failures, 0 skipped
       Finished verifying <default-ubuntu> (0m0.48s).
-----> Kitchen is finished. (0m3.07s)
```

### TO DO:
- Check if `nginx` server is installed and running. 
