<p align="center">
  <img width="300" src="./docs/images/vec-nap-logo-standard.svg#gh-light-mode-only">
</p>
<p align="center">
  <img width="300" src="./docs/images/vec-nap-logo-invertiert.svg#gh-dark-mode-only">
</p>

# NAP - ML docker container scripts
Boilerplates to setup docker containers with GPU support on single/multiuser servers with minimal effort.<br>
The containers run in an unprivileged mode. Therefore all apt packages should be installed in advance as defined in
the setup section.

## Usage
1. select the boilerplate you want to build on (currently only pytorch)
2. in the dockerfile
    - change the UID and GID to your IDs on the host machine to prevent privilege errors
3. in the compose file
    - required:
        - change the UID and GID to your IDs on the host machine to prevent privilege errors
        - change the port in the docker compose to the port you want to expose
    - optionally
        - adjust shared memory (`shm_size`)
        - add deploy section with/without restrictions to enable GPU usage in the container
4. If you need any specific python/apt packages add those to `/pytorch/setup/{requirements/apt_packages}.txt`
    - these will be automatically installed during the container build
    - python packages can be installed during container runtime, apt packages cannot
5. run the container
    - run `docker-compose up` to build the container and run it
    - if you made changes to `/pytorch/setup/{requirements/apt_packages}.txt` after the initial `docker-compose up`
      run `docker-compose build` to apply those and the run `docker-compose up` to start the container again