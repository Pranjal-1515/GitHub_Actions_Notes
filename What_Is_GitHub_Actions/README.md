# GitHub Actions
GitHub Actions is a powerful automation tool integrated into GitHub that allows you to create workflows for your software development projects. With GitHub Actions, 
you can automate tasks like continuous integration and continuous deployment (CI/CD), testing, and other repetitive tasks directly in your GitHub repository.

## Automation Platform
For purposes of the end user, GitHub Actions is a way to create and execute automa‐
ted workflows tied to GitHub events. Most commonly, you might think of this in the
context of CI/CD. As an example, you make a change via a pull request, and GitHub
kicks off a continuous delivery pipeline. Prior to GitHub Actions, you would have
needed some external tool or process to respond to a notification from GitHub that
the pull request happened and then to process it. And the automation that happened
after the pull request and initial notification would have been implemented via that
external tool. <br>
With Actions, you now have the means to create this automation within a context
managed by, and within, GitHub. You can define the what, when, and how for auto‐
mated responses to events such as pushes or pull requests. For example, when a push
happens in a branch of your repository, automatically grab the latest code and
attempt to build it. If a pull request happens for a different branch, automatically
build and test the code. If that results in a failure, update a GitHub issue. If there’s not
a failure, automatically proceed with putting out a new release.

## Framework
Taking an automation platform from a jumbled collection of mechanisms to an
organized and consumable process requires imposing structure and flow. Without
them, you simply have a collection of tools. With them, you can assemble truly useful
automation to accomplish whatever set of tasks needs to be done. <br>
For Actions, this framework is composed of a core set of related components in Git‐
Hub. These components can be put together to execute simple or complex automa‐
tion in an understandable and predictable way. And this automation is stored in the
repository as code.

## Runners
Runners are the physical or virtual computers or containers where the code for a
workflow is executed. They can be systems provided and hosted by GitHub (and run
within their control), or they can be instances you set up, host, and control. In either
case, the systems are configured to understand how to interact with the GitHub
Actions framework. This mean they can interact with GitHub to access workflows
and predefined actions, execute steps, and report outcomes.
runs-on: ubuntu-latest

## Jobs
Jobs aggregate steps and define which runner to execute them on. An individual job is
usually targeted towards accomplishing one particular goal of the overall workflow.
An example could be a workflow that implements a CI/CD pipeline with separate
jobs for building, testing, and packaging.

## Workflow
A workflow is like a pipeline. At a high level, it first defines the types of inputs
(events) that it will respond to and under what conditions it will respond to them.
This is what we talked about in the earlier section on events. The response, if the
events and conditions match, is to then execute the series of jobs in the workflow,
which, in turn, execute the steps for each job. <br> <br>
The overall flow is like a continuous integration process in that it responds to a par‐
ticular kind of change and kicks off an automated sequence of work. The next listing
shows an example of a simple workflow for processing Go programs built on the pre‐
vious definitions: <br>
![image](https://github.com/user-attachments/assets/8660ad46-9400-47a4-8ab4-12d9d97790b0)

Note that this workflow is written in YAML format. I’ll break down what’s happening
in this file, line by line: <br>
Line 1: The workflow file is assigned a name. <br>
Line 3: This is the on identifier discussed in the section on events. <br>
Lines 4–6: This workflow is triggered when a push operation is done to the branch
main in this GitHub repository. <br>
Line 8: This starts the jobs portion of the workflow. <br>
Line 9: There is one job in this workflow, named build. <br>
Line 10: This job will be executed on a runner system, hosted by GitHub, provisioned
with a standard ubuntu operating system image. <br>
Line 11: This starts the series of steps for this job. <br>
Line 12: The first step is done via pulling in a predefined action. Note the way this is
referenced. actions/checkout@v3 refers to the relative path after github.com, so this
really says it is going to run/use the action defined at github.com/actions/checkout.
Also notice that this is the only line in this step—no parameters need to be passed to
this action because it assumes it is checking out the source from this repository since
it is in this repository. <br>
Line 13: The hyphen at the start of this line indicates this is the start of a second step.
This line is giving the new step a name. <br>
Line 14: The same step is pulling in another predefined action to set up the Go envi‐
ronment. <br>
Lines 15–16: The setup-go action needs a parameter—the version of Go to use. The
parameter is passed as an input to the action via a with clause. <br>
Line 17: This is another step, one that simply runs a command as indicated by the run
keyword. The command is to execute the go run command on an example file in the
repository. <br>
