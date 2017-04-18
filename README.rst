This docker image is meant to be used to generate an allthethings.json file from Mozilla's
Release Engineering Buildbot set up. Visit https://wiki.mozilla.org/ReleaseEngineering/How_To/allthethings.json to
know more about the file.

Generate allthethings.json
--------------------------

If you just want to generate allthethings.json locally run the following:

.. code-block:: bash

   docker pull armenzg/releng_buildbot_docker
   docker run --name allthethings --rm -i -t releng_buildbot_docker bash
   # This will generate an allthethings.json file; it will take few minutes
   /braindump/community/generate_allthethings_json.sh
   # On another tab (once the script is done)
   docker cp allthethings:/root/.mozilla/releng/repos/buildbot-configs/allthethings.json .

Hack allthethings.json
----------------------

If you want to modify how allthethings.json is generated you can do so like this:

.. code-block:: bash

   # Generate the image like this
   docker build -t releng_buildbot_docker .
   # Start a container and connect to it
   docker run --name allthethings --rm -i -t releng_buildbot_docker bash
   # Running this will check out all related repositories and set up the virtualenv
   /braindump/community/generate_allthethings_json.sh
   # All the repositories involved are checked out under ~/.mozilla/releng/repos
   # Get to the configs repository
   cd ~/.mozilla/releng/repos/buildbot-configs
   # Activate the virtualenv
   source ../../venv/bin/activate
   # Install your favourite editor. I recommend vim
   apt-get install -y vim
   # Make changes to the repositories you want and run the script
   ~/.mozilla/releng/repos/braindump/buildbot-related/dump_allthethings.sh
   # You will find the newly generated file under /root/.mozilla/releng/repos/buildbot-configs/allthethings.json
