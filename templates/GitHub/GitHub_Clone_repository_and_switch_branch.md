<a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/GitHub/GitHub_Clone_repository_and_switch_branch.ipynb" target="_parent"><img src="https://naasai-public.s3.eu-west-3.amazonaws.com/open_in_naas.svg"/></a><br><br><a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=&template=template-request.md&title=Tool+-+Action+of+the+notebook+">Template request</a> | <a href="https://github.com/jupyter-naas/awesome-notebooks/issues/new?assignees=&labels=bug&template=bug_report.md&title=GitHub+-+Clone+repository+and+switch+branch:+Error+short+description">Bug report</a> | <a href="https://app.naas.ai/user-redirect/naas/downloader?url=https://raw.githubusercontent.com/jupyter-naas/awesome-notebooks/master/Naas/Naas_Start_data_product.ipynb" target="_parent">Generate Data Product</a>

**Tags:** #github #clone #repository #branch #switch #git

**Author:** [Florent Ravenel](https://www.linkedin.com/in/florent-ravenel/)

**Description:** This notebook explains how to clone a repository from GitHub and switch to a specific branch.

**References:**
- [GitHub Documentation - Cloning a repository](https://docs.github.com/en/github/creating-cloning-and-archiving-repositories/cloning-a-repository)

## Input

### Import libraries


```python
import os
```

### Setup Variables
- `repo_url`: URL of the repository to clone
- `branch_name`: Name of the branch to switch to
- `output_dir`: Output directory to clone repo. If None, we will create a folder with the name of the branch


```python
# Inputs
repo_url = "https://github.com/jupyter-naas/awesome-notebooks"
branch_name = "1743-github-clone-repository-and-switch-branch"

# Outputs
output_dir = None
```

## Model

### Clone repository
Clone the repository from the given URL and create a local copy of it.


```python
def clone_branch(repo_url, output_dir, branch_name):
    # Get GitHub owner and repo name
    owner = repo_url.split("https://github.com/")[-1].split("/")[0]
    repo_name = repo_url.split("/")[-1]
    
    # Add repo name with .git extension
    if not repo_name.endswith(".git"):
        repo_name = f"{repo_name}.git"
    repo = f"{owner}/{repo_name}"
        
    # Init output dir
    if not output_dir:
        output_dir = branch_name
    
    # Create output directoy
    if not os.path.exists(output_dir):
        os.makedirs(output_dir)
        
    # GitHub Action
    !cd '{output_dir}'
    !git clone git@github.com:'{repo}' '{output_dir}'
    print(f"✅ GitHub repo cloned: {output_dir}")
    return output_dir
    
output_dir = clone_branch(repo_url, output_dir, branch_name)
```

## Output

### Switch branch
Change the current branch to the given branch name.


```python
def switch_branch(output_dir, branch_name):
    # GitHub action
    !cd '{output_dir}' && git checkout '{branch_name}'
    print(f"✅ Switched to branch '{branch_name}'")

switch_branch(output_dir, branch_name)
```

 

 
