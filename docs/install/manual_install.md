# Manual Installation

If you don't want to use Docker, or if you want to contribute to server development, you can also install the server directly. We use a virtual environment for the installation, so it will not mess up your regular Python install.

The installation instructions below are targeted towards OSX and \*nix shells such as bash. If you want to use Windows, we recomend using a POSIX-compliant shell such as [gitbash](https://openhatch.org/missions/windows-setup/install-git-bash) which provides similarly rich commands. If you really want to use the Command Prompt, most commands should work although you may need to convert `/` -> `\` to make the commands work.

## Installation
---------------------
### Install
Server installation is as simple as cloning the github repository.

- If you do not plan to make changes to the code, clone the master repository:
  ```
  $ git clone https://github.com/e-mission/e-mission-server.git
  ```

- If you might make changes or develop new features, fork (https://help.github.com/articles/fork-a-repo/) and clone your fork:
  ```
  $ git clone https://github.com/<username>/e-mission-server.git
  ```

### Update ###
- If you are working off the master repository:
  ```
  $ git pull origin master
  ```

- When working off your fork, you will need to sync your fork with the main repository (https://help.github.com/articles/syncing-a-fork/) and then pull from your fork (as above).


## Dependencies:
-------------------
### Database:
1. Install [Mongodb](http://www.mongodb.org/), version 3.4
  2. **Windows**: *mongodb* appears as a service on Windows devices and starts automatically on reboot
  3. **MacOS**: It is recommended to use *homebrew* to install mongodb. Follow these instruction on how to do so here: https://docs.mongodb.com/v3.4/tutorial/install-mongodb-on-ubuntu/
  4. **Ubuntu**: http://docs.mongodb.org/manual/tutorial/install-mongodb-on-ubuntu/

2. Start mongodb on the default port:

     `$ mongod`

### Python distribution
We will use the [Anaconda](https://store.continuum.io/cshop/anaconda/) distribution of Python that is optimized for scientific computing. Anaconda available for a variety of platforms and includes Python's scientific computing libraries (numpy/scipy/scikit-learn) along with
native implementations for performance. Using Anaconda avoids native library inconsistencies between versions.

The distribution also includes its own version of pip and a separate environment management tool called *conda*.

The distribution also includes an environment management tool called 'conda'. We will set up a separate `emission`
environment within anaconda to avoid conflicts with other applications.

- Install the Anaconda distribution (https://www.anaconda.com/download). Any installer should be fine--setting up the `emission` environment will automatically choose the correct version of Python. Since all required packages will be installed using this environment, if you are comfortable with the command line, you can also download the minimalist `miniconda` installer: https://conda.io/miniconda.html
  
- Setup the `emission` environment.

  ```
  $ source setup/setup.sh
  ```
  
  - If you want to use an iPython notebook, use `$ source setup/setup_notebook.sh` instead.
  - If you want to use a less optimized version that uses less disk space, use `$ source setup/setup_nomkl.sh` instead. Note that this has not been extensively tested.

- Verify that you are in the right environment. Your prompt should start with
  `(emission)` and `emission` should be starred in the environment list.

  ```
  (emission) ...$ conda env list
  # conda environments:
  #
  aws                      /..../anaconda/envs/aws
  emission              *  /..../anaconda/envs/emission
  firebase                 /..../anaconda/envs/firebase
  py27                     /..../anaconda/envs/py27
  py36                     /..../anaconda/envs/py36
  xbos                     /..../anaconda/envs/xbos
  root                     /..../anaconda
  ```
  
- If you have already setup the environment and just need to switch to it, you can use `source activate emission` to enable to the `emission` environment. To switch out of the `emission` environment, or to manipulate it in other ways, read the *conda* documentation on environments https://docs.conda.io/projects/conda/en/latest/user-guide/tasks/manage-environments.html. 

	> Depending on the version of conda that you have installed, you may use `conda activate` or `source activate`

- Remember to re-run the setup script every time you pull from the main repository as the dependencies may have changed.

  ```
  $ source setup/setup.sh
  ```

- When you are done working with *e-mission*, you can cleanup the environment and delete the entire directory.

  ```
  $ source setup/teardown.sh
  $ cd ..
  $ rm -rf e-mission-server
  ```

### Javascript Dependencies

Note: These are required only if the user needs a web interface for the server. Otherwise, these can be skipped.

Tip: Run "bower install" instead if you are prompted password for 'https://github.com' after running "bower update".

    $ cd webapp
    $ bower update

## Run
---------
1. On MacOS, first start the database (note: mongodb installs as a service on Windows and will start automatically on reboot).

        $ mongod
        2018-05-23T11:06:07.576-0700 I CONTROL  [initandlisten] MongoDB starting : pid=60899 port=27017 dbpath=/data/db 64-bit ...
        2018-05-23T11:06:07.576-0700 I CONTROL  [initandlisten] db version v3.6.2
        ...
        2018-05-23T11:06:08.420-0700 I FTDC     [initandlisten] Initializing full-time diagnostic data capture with directory '/data/db/diagnostic.data'

2. **Optional** Copy configuration files.
   The files in `conf` can be used to customize the app with custom authentication options or enable external features such as place lookup and the game integration. Look at the samples in `conf/*`, copy them over and modify as necessary - e.g.
  ```
  $ find conf -name \*.sample
  # For the location -> name reverse lookup. Client will lookup if not populated.
  $ cp conf/net/ext_service/nominatim.json.sample conf/net/ext_service/nominatim.json
  ```

3. Start the server
  ```
  $ ./e-mission-py.bash emission/net/api/cfc_webapp.py
  storage not configured, falling back to sample, default configuration
  Connecting to database URL localhost
  analysis.debug.conf.json not configured, falling back to sample, default configuration
  Finished configuring logging for <RootLogger root (WARNING)>
  Replaced json_dumps in plugin with the one from bson
  Changing bt.json_loads from <function <lambda> at 0x10f5fdb70> to <function loads at 0x1104b6ae8>
  Running with HTTPS turned OFF - use a reverse proxy on production
  Bottle v0.13-dev server starting up (using CherootServer())...
  Listening on http://0.0.0.0:8080/
  Hit Ctrl-C to quit.
  ```

4. Test your connection to the server
    - Using a web browser, go to [http://localhost:8080](http://localhost:8080)
    - Using Safari in the iOS emulator, go to [http://localhost:8080](http://localhost:8080)
    - Using Chrome in the Android emulator:
        - Change `server.host` in `conf/net/api/webserver.conf` to [0.0.0.0](0.0.0.0)
        - Go to the special IP for the current host in the Android emulator - [10.0.2.2](https://developer.android.com/tools/devices/emulator.html#networkaddresses)

