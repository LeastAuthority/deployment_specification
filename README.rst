What is this?
-------------

The deployment specification repository is a canonical history of deployment configurations.  Its 
purposes are:

(1) To provide a canonical reference by which one can see what parameter set was used to
attempt the launch of a particular server.

(2) To provide a convenient format which one can use to specify what kind of server shall be
launched.

(3) ?

How do I use it?
----------------

The interface for this repository is:

``deployment_tool_or_script absolute_path_to_this_repository git_reference_to_a_commit``

The deployment specification consists of a set of files, each file contains a json formatted
reference to a git repository and a specific commit therein.  

The intent is that a deployment tool, perhaps invoked with a git "push-hook", reads those files and 
executes some combination of copying the indicated data and/or using the indicated data to specify 
how the deployment shall occur.

How is it used to deploy a Least Authority Infrastructure Server?
-----------------------------------------------------------------

There are 3 repositories specified by files within deployment_specification in this use-case.
They are:

(1) nonsecret_config: The repository containing parameters necessary to launch an EC2.
AND
(2) source_code: The repository containing the leastauthority.com code base.
(3) secret_config: The secret_config repository which contains Least Authority AWS credentials.

Within the repository referenced by "(1)", is the nonsecret_config file, a json encoded key-value map (dict) which 
leastauthority.com/deploy_infrastructure_server.py parses in order to learn parameters necessary
for the deployment.

Within the repositories referenced by "(2)" and "(3)" are code bases that will be copied to the
new EC2 once it is launched.

In all 3 cases the file in deployment_specification unambiguously indicates a specific commit within
some other repository.  These 3 references are then bound together in a single commit within the
deployment specification repository.
