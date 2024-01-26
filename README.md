
# UA-RCL's Website

Visit **[ua-rcl.github.io](https://ua-rcl.github.io)** 🚀

Following the below instructions should be enough to make modifications. Everyting is generated automatically after making below changes.

## Main and Sub Page Updates

Go to following files to update each pages information:

```
main:     index.md
research: research/index.md
team:     team/index.md
blog:     blog/index.md
contact:  contact/index.md
```

## Project Updates

### Existing Project

Update the information in the ```projects/<name>``` folder.

### New Project

Generate a project in ```projects/``` folder trying to follow the design of the other projects. Then, add the newly generated website to ```_data/projects.yaml``` file.

## Team Member Updates

### Existing Member 

Navigate to ```_members``` page and change the information in the corresponding markdown file. Just change the role of the student after graduation to ```graduate```.

### New Member 

Create a new member under ```_members/``` and enter necessary information. Role parameter groups members into either current or graduate students. Upload profile picture for a new student under ```images/profiles/``` folder.

## Blog Updates

To add a new blog post, add a new markdown file to ```_posts/``` folder following the format. For modifying an existing post, just edit the corresponding blog post in ```_posts/```.

_Built with [Lab Website Template](https://greene-lab.gitbook.io/lab-website-template-docs)_


## Test changes with Docker

It is recommended to use the provided Docker configuration with this repo to start a local server, and test out how the changes reflect on the webpage, before pushing to github. Follow the steps below:
1. Download and install docker for your OS distribution. ([Docker Install Page](https://docs.docker.com/engine/install/)).
2. In the current repository directory, run `sudo bash .docker/run.sh`. This step sets up the docker and launches a server.
3. Once the docker sets up the server, user will get notification such as the following-

    <img src="./images/readme_scrsht_1.png" alt="scrsht" width="400">

4. Open the server address (`http://localhost:4000`) in the browser to view the webpage, and review the changes.

Any changes made in the sources while the server is running, prompts the docker to regenerate the website, which may take a few minutes to reflect in the browser.
