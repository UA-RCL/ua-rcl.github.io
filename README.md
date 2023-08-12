
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

Firstly, update the information in the ```research/index.md``` if necessary. Then, update the information in the ```projects/<name>``` folder.

### New Project

Create a new project information section in ```research/index.md``` following the current format. Then, generate a project in ```projects/``` folder trying to follow the design of the other projects. Then, add the newly generated website to ```_data/projects.yaml``` file.

## Team Member Updates

### Existing Member 

Navigate to ```_members``` page and change the information in the corresponding markdown file. Just change the role of the student after graduation to ```graduate```.

### New Member 

Create a new member under ```_members/``` and enter necessary information. Role parameter groups members into either current or graduate students. Upload profile picture for a new student under ```images/profiles/``` folder.

## Blog Updates

To add a new blog post, add a new markdown file to ```_posts/``` folder following the format. For modifying an existing post, just edit the corresponding blog post in ```_posts/```.

_Built with [Lab Website Template](https://greene-lab.gitbook.io/lab-website-template-docs)_

