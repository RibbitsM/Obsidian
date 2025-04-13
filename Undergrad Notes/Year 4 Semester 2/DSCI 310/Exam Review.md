- We can save long strings of bash commands that we regularly run to a bash.sh file
- This lets us run these commands by just running bash bash.sh
- Make sure that when you are calling a script, if you just type bash then it will only work in the current working directory
- However, if you call a script using its relative or absolute path, you can run that script in your working directory even if the script was run from another directory
- The same process works in R, except the file will be called script.R instead of bash.sh
- To run a .R file, just type Rscript and then the file name

**YML and Github Actions**

- The name of a github actions script is not the actual file name, but whatever is assigned to the name variable within the file
- For the on: section, you have a couple different options
- The first is workflow_dispatch, which lets you manually trigger it
- Another common option is push, which triggers whenever something is pushed
- You can add the variable branches to push to specify which branches you want to trigger this action when pushed to
- Another option is to trigger only when a certain file is changed called paths
- It goes even further, we can set a scheduled time each week for an action to be run
- The next section to talk about is jobs
- This is where you write what you want the action to do
- An action can have multiple jobs, and they all need names
- You'll have to specify the operating system you want it to run on (usually ubuntu-latest), and what action you want to take for that job
- The actions will be put under the steps variable, and we can use preset actions like actions/checkout@v4 which just checks out your repository

**Exam**

- Final exam is being hosted on Github, make sure you remember to push regularly or else your progress will not be saved
- Graded on the timestamp of your commits, anything pushed after the exam doesn't count
- Part 1 is just multiple choice questions, mostly softballs
- Part 2 is split into five main components
- First part is just testing knowledge of basic bash commands
- Second part is related to Git and Github, basically pushing pulling, making branches and solving merge conflicts, may also include pull requests
- Basically any reference material you want is allowed, just can't use collaborative documents
- Third part is creating and running scripts, fourth part is creating and building docker images
- Final part is creating Github Actions