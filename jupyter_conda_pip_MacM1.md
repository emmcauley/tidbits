**Steps to making Jupyter notebook, conda, and pip to work together on new Apple M1/silicon hardware**

**Set up Rosetta**

1. I followed [these instructions](https://osxdaily.com/2020/11/18/how-run-homebrew-x86-terminal-apple-silicon-mac/). Verify success by typing `arch` into terminal (original terminal result: arm64; Rosetta terminal result: i386)

**Tell package managers which architecture to use**

2. Tell conda which architecture to use (I used these [this link](https://github.com/conda-forge/miniforge/issues/165) and [this link](https://stackoverflow.com/questions/65415996/how-to-specify-the-architecture-or-platform-for-a-new-conda-environment-apple)
for inspiration:
`CONDA_SUBDIR=osx-64 conda create -n <name> python`   # create a new environment called rosetta with intel packages.
`conda activate rosetta`
`conda env config vars set CONDA_SUBDIR=osx-64`  # make sure that conda commands in this environment use intel packages
`conda deactivate <name>`
`conda activate <name>`
`echo "CONDA_SUBDIR: $CONDA_SUBDIR"`

3. If applicable, tell pip which architecture to use (I used [this link](https://stackoverflow.com/questions/64252434/architecture-not-supported-error-when-installing-nltk-with-pip-on-mac) for inspiration: 
`ARCHFLAGS="-arch x86_64" pip install -r ~/requirements.txt`
*in this case my requirements.txt was restricted to specific package versions and so this command failed. Because I did not need to be stringent, I ended up doing: `ARCHFLAGS="-arch x86_64" pip install <package1> <package2>` and that worked. I was then able to install jupyter notebook as normal.
