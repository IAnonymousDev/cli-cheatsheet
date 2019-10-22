# CLI cheat sheet
A collection of cli commands for Shell / PowerShell users
## AWS
### CloudWatch
<pre>
<code><b>aws events list-rules --query 'Rules[].Name'</b></code>

# lists AWS CloudWatch event rules.
</pre>
<pre>
<code><b>aws logs describe-log-streams `
	--log-group-name /aws/lambda/log-group `
	--order-by LastEventTime `
	--descending</b></code>

# lists the log streams and filter results by log group name
</pre>
<pre>
<code><b>aws logs get-log-events `
	--log-group-name /ecs/ecs-task-definition `
	--log-stream-name ecs/ecs-container-definition/</b></code>

# lists all events under a stream
</pre>
<pre>
<code><b>aws cloudwatch get-dashboard `
	--dashboard-name &lt;dashboard-name&gt;" `
	--output text </b></code>

# displays the details of the specified dashboard
# returns the results in text format instead of JSON
</pre>
<pre>
<code><b>aws cloudwatch list-metrics --namespace &lt;"metric-namespace"&gt;</b></code>

# lists the specified metrics filtered by namespace
</pre>

### CloudFormation
<pre>
<code><b>aws cloudformation delete-stack --stack-name &lt;stack-name&gt;</b></code>

# deletes the specified cloudformation stack
</pre>
<pre>
<code><b>aws cloudformation list-stacks `
	--stack-status-filter UPDATE_COMPLETE `
	--query 'StackSummaries[?StackName==`&lt;stack-name&gt;`].StackId'</b></code>

# lists all stacks under UPDATE_COMPLETE status and
# filter the results by StackName
</pre>
<pre>
<code><b>aws cloudformation delete-stack --stack-name &lt;stack-name&gt;</b></code>

# deletes the specified stack
</pre>

### Configure
<pre>
<code><b>$Env:AWS_PROFILE="&lt;aws-profile-name&gt;"</b></code>

# sets AWS_PROFILE environment variable on Windows.
</pre>
<pre>
<code><b>echo $Env:AWS_PROFILE</b></code>

# outputs the value of AWS_PROFILE environment variable on Windows
# use this to confirm environment variable has been set
</pre>
<pre>
<code><b>Remove-Item env:AWS_PROFILE</b></code>

# removes AWS_PROFILE environment variable from the current session on Windows
</pre>
<pre>
<code><b>export AWS_PROFILE=&lt;aws-profile-name&gt;</b></code>

# sets AWS_PROFILE environment variable on Linux, macOS, or Unix.
</pre>
<pre>
<code><b>aws configure list</b></code>

# outputs the value of AWS_PROFILE environment variable on Linux, macOS, or Unix
# use this to confirm environment variable has been set
</pre>

### DynamoDB
<pre>
<code><b>aws dynamodb create-table `
	--table-name &lt;table-name&gt; `
	--attribute-definitions AttributeName=Id,AttributeType=N `
	--key-schema AttributeName=Id,KeyType=HASH `
	--provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 `
	--endpoint-url http://localhost:8000</b></code>

# creates a new table
</pre>
<pre>
<code><b>aws dynamodb create-table `
	--table-name &lt;table-name&gt; `
	--attribute-definitions AttributeName=Id,AttributeType=N AttributeName=IsActive,AttributeType=S `
	--key-schema AttributeName=Id,KeyType=HASH `
	--provisioned-throughput ReadCapacityUnits=5,WriteCapacityUnits=5 `
	--global-secondary-indexes IndexName=IsActive_Index,KeySchema=["{AttributeName=IsActive,KeyType=HASH}"],Projection="{ProjectionType=INCLUDE,NonKeyAttributes=["Name"]}",ProvisionedThroughput="{ReadCapacityUnits=10,WriteCapacityUnits=10}" `
	--endpoint-url http://localhost:8000</b></code>

# creates a new table along with a global secondary index
</pre>
<pre>
<code><b>aws dynamodb batch-write-item `
	--request-items file://&lt;json-file-path&gt; `
	--endpoint-url http://localhost:8000</b></code>

# reads one or more items from json file and writes them to the table.
</pre>
<pre>
<code><b>aws dynamodb put-item `
	--table-name &lt;table-name&gt; `
	--item file://&lt;json-file-path&gt; `
	--return-consumed-capacity TOTAL `
	--endpoint-url http://localhost:8000</b></code>

# creates a new item, or replaces an old item with a new item if another item with the same primary key already exists.
</pre>
<pre>
<code><b>aws dynamodb list-tables --endpoint-url http://localhost:8000</b></code>

# returns an array of table names associated with the current account and endpoint
</pre>
<pre>
<code><b>aws dynamodb describe-table `
	--table-name &lt;table-name&gt; `
	--endpoint-url http://localhost:8000</b></code>

# returns information about the table, including the current status of the table, when it was created, the primary key schema, and any indexes on the table.
</pre>
<pre>
<code><b>aws dynamodb delete-table `
	--table-name &lt;table-name&gt; `
	--endpoint-url http://localhost:8000</b></code>


# deletes a table and all of its items
</pre>
<pre>
<code><b>aws dynamodb scan `
	--table-name &lt;table-name&gt; `
	--endpoint-url http://localhost:8000</b></code>

# returns all rows from the table associated with the current endpoint
</pre>

### Lambda
<pre>
<code><b>aws lambda list-functions --query 'Functions[].FunctionName'</b></code>

# list Lambda functions and return their function names
# --query parameter accepts strings that are compliant with the JMESPath specification.
</pre>
<pre>
<code><b>aws lambda list-functions --profile &lt;aws-profile-name&gt;</b></code>

# returns the list of lambda functions along with their environment variables
</pre>

### ECR
<pre>
<code><b>aws ecr create-repository --repository-name &lt;repository-name&gt;</b></code>

# creates an ecr repository
</pre>
<pre>
<code><b>aws ecr get-login --no-include-email</b></code>

# returns a docker login command along with a token
</pre>
<pre>
<code><b>aws ecr describe-repositories --repository-name &lt;repository-name&gt;</b></code>

# describes the specified image repositories in a registry
</pre>

### ECS
<pre>
<code><b>aws ecs list-tasks `
	--cluster &lt;cluster-name&gt; `
	--desired-status RUNNING</b></code>

# returns a list of tasks for the specified cluster 
# and under specified status
</pre>
<pre>
<code><b>aws ecs describe-tasks `
	--tasks &lt;task-id | task-arn&gt; `
	--cluster &lt;short-name | full-arn&gt;</b></code>

# describes a specified task or tasks in the specified cluster
</pre>

### RDS
<pre>
<code><b>aws rds describe-db-instances --db-instance-identifier &lt;db-identifier&gt;</b></code>

# Returns information about provisioned RDS instances
</pre>

### S3
<pre>
<code><b>aws s3api head-bucket --bucket &lt;bucket-name&gt;</b></code>

# determines if a bucket exists and we have permission to access it
</pre>
<pre>
<code><b>aws s3api get-bucket-encryption --bucket &lt;bucket-name&gt;</b></code>

# returns the server-side encryption configuration of a bucket.
</pre>
<pre>
<code><b>aws s3 cp s3://&lt;bucket-name&gt;/sample-video.mp4 c:\sample-video.mp4</b></code>

# copies a local file or S3 object to another location locally or in S3.
</pre>
<pre>
<code><b>aws s3 ls &lt;bucket-name&gt;</b></code>

# lists S3 objects and common prefixes under a prefix or all S3 buckets
</pre>
<pre>
<code><b>aws s3 rm s3://&lt;bucket-name&gt; --recursive</b></code>

#  removes all objects from the specified bucket without specifying a prefix
</pre>

### Secrets Manager
<pre>
<code><b>aws secretsmanager list-secrets `
	--query 'SecretList[?Name==`&lt;secret-name&gt;`].Name'</b></code>

# lists all the secrets that are stored by Secrets Manager in the AWS account 
# and returns the Name property of the one with the name <i>secret-name</i>
</pre>

### Step Functions
<pre>
<code><b>aws stepfunctions list-executions `
	--state-machine-arn &lt;state-machine-arn&gt; `
	--query 'executions[0]'</b></code>

# lists the executions of a state machine
</pre>
<pre>
<code><b>aws stepfunctions get-execution-history `
	--execution-arn &lt;execution-arn&gt;</b></code>

# returns the history of the specified execution as a list of events
</pre>
<pre>
<code><b>aws cognito-idp list-user-pools `
	--max-results 20 `
	--query 'UserPools[?Name==`&lt;user-pool-name&gt;`].Id' `
	--profile &lt;&gt;</b></code>

# lists the names of user pools associated with specified AWS profile
</pre>
<pre>
<code><b>aws cognito-idp delete-user-pool --user-pool-id=&lt;user-pool-id&gt;</b></code>

# deletes the specified AWS Cognito user pool
</pre>
<pre>
<code><b>aws cognito-idp list-users --user-pool-id &lt;lists users under a pool&gt;</b></code>

# lists users in the specified AWS Cognito user pool
</pre>

## AWS Lambda Tools
<pre>
<code><b>dotnet lambda package ` 
	--configuration Release `
	--output-package ./file.zip `
	--framework netcoreapp2.1</b></code>

# creates package file for the specified configuration
</pre>

## Docker
<pre>
<code><b>docker build --no-cache -f ./Dockerfile -t my-media/dotnet:2.1-sdk ./</b></code>

# builds a docker image from docker file and tag the image
</pre>
<pre>
<code><b>docker build ` 
	--build-arg awsAccessKeyId=value `
	--build-arg awsSecretKey=value `
	--build-arg region=value `
	--no-cache `
	-f ./Dockerfile ./</b></code>

# passes arguments to docker build command. 
# NOTE: trailing backtick <code>'</code> in PowerShell allows splitting up a command over multiple lines. 
# Replace backtick with backslash <code>\</code> if using shell.
</pre>
<pre>
<code><b>docker run -t &lt;image-id&gt;|&lt;repository-name&gt;</b></code>

# runs a docker container from an image id or repository name
</pre>
<pre>
<code><b>docker run -i -t &lt;image-id&gt;</b></code>

# helps get inside the docker container by image id
</pre>
<pre>
<code><b>docker run -i -t --entrypoint='bash' &lt;image-id&gt;</b></code>

# starts a container and stops at bash
</pre>
<pre>
<code><b>
docker run `
	-e AWS_ACCESS_KEY_ID=value `
	-e AWS_SECRET_KEY=value `
	-it `
	&lt;image-id&gt;
</b></code>
# starts a container and sets environment variables
</pre>
<pre>
<code><b>docker images -f “dangling=true” -q </b></code>

# shows all the dangling images (untagged images)
</pre>
<pre>
<code><b>docker image prune</b></code>

# deletes any unused or dangling images 
# a dangling image is the one that is not tagged and not referenced by any container
</pre>
<pre>
<code><b>docker ps</b></code>

# lists all running containers
</pre>
<pre>
<code><b>docker ps -a</b></code>

# lists all containers including stopped/exited ones
</pre>
<pre>
<code><b>docker stop $(docker ps -a -q)</b></code>

# stops all docker containers
</pre>
<pre>
<code><b>docker start &lt;container-id&gt;</b></code>

# starts a stopped container
</pre>
<pre>
<code><b>docker rm -f &lt;container-id&gt;</b></code>

# stops the container if running and removes it
</pre>
<pre>
<code><b>docker rm $(docker ps -a -q)</b></code>

# removes all stopped containers
</pre>
<pre>
<code><b>docker exec -it &lt;container-id&gt; bash</b></code>

# helps get into a running container
</pre>
<pre>
<code><b>docker tag &lt;image-id&gt; xxxxxxxxxxxx.dkr.ecr.ap-southeast-2.amazonaws.com/xx-xxxxx/dotnet:2.1-sdk</b></code>

# tags a local docker image
</pre>
<pre>
<code><b>docker push xxxxxxxxxxxx.dkr.ecr.ap-southeast-2.amazonaws.com/xx-xxxxx/dotnet</b></code>

# pushes the docker image tagged in the above command
</pre>
<pre>
<code><b>docker cp &lt;container-id&gt;:/tmp/workdir/file.mp4 ./file.mp4</b></code>

# copies the file from a running or stopped docker container to host
</pre>
<pre>
<code><b>docker cp ./file.mp4 &lt;container-id&gt;:/tmp/workdir/file.mp4</b></code>

# copies file from host machine into a folder on running docker container
</pre>
<pre>
<code><b>Ctrl+p, Ctrl+q</b></code>

# detaches user from docker container but will keep the container running in daemon mode
</pre>
<pre>
<code><b>docker pull xxxxxxxxxxxx.dkr.ecr.ap-southeast-2.amazonaws.com/ffmpeg-container:12</b></code>

# pulls an image from aws ecr by repository uri
</pre>

## Git
<pre>
<code><b>git add -f {file-path}</b></code>

# stages files before committing
</pre>
<pre>
<code><b>git add -A</b></code>

# stages all changes
</pre>
<pre>
<code><b>git add .</b></code>

# stages additions and modifications, but not deletions
</pre>
<pre>
<code><b>git add -u</b></code>

# stages modifications and deletions, but not additions
</pre>
<pre>
<code><b>git branch --list</b></code>

# to list all branches in the current repo
</pre>
<pre>
<code><b>git branch -d task/task-99-description</b></code>

# deletes the local branch
</pre>
<pre>
<code><b>git branch</b></code>

# lists branches (the asterisk denotes the current branch)
</pre>
<pre>
<code><b>git config mergetool.kdiff3.path="C:/Program Files/KDiff3/kdiff3.exe"</b></code>

# configures kdiff3 as the default merge tool 
</pre>
<pre>
<code><b>git config --list</b></code>

# shows git configuration including configured diff and merge tools
</pre>
<pre>
<code><b>git commit --amend</b></code>

# edits a message of the last commit
</pre>
<pre>
<code><b>git commit -m "my message"</b></code>

# commits changes with a message
</pre>
<pre>
<code><b>git checkout develop</b></code>

# switches to develop branch
</pre>
<pre>
<code><b>git checkout -b task/task-99-description develop</b></code>

# creates a new branch off develop and switches to it
</pre>
<pre>
<code><b>git checkout -- .</b></code>

# discards all unstaged files in the current working directory
</pre>
<pre>
<code><b>git checkout -- src/myfile.txt</b></code>

# discards changes to a file
</pre>
<pre>
<code><b>git clean -n</b></code>

# prints out the list of files which will be removed
</pre>
<pre>
<code><b>git clean -f</b></code>

# deletes untracked files from the repository
</pre>
<pre>
<code><b>git diff --stat --cached origin/task/task-99/description</b></code>

# compares the differences against remote branch
</pre>
<pre>
<code><b>git fetch --prune origin</b></code>

# fetches all branches that exist in the origin
# --prune = deletes the remote tracking references
</pre>
<pre>
<code><b>git pull origin develop</b></code>

# pulls latest from origin/develop branch
</pre>
<pre>
<code><b>git log --pretty=%P -n 1 &lt;commit-number&gt;</b></code>

# finds the parent of a commit by commit id
</pre>
<pre>
<code><b>git merge develop</b></code>

# merges develop branch into the current branch
</pre>
<pre>
<code><b>git push -u origin &lt;local-branch&gt;</b></code>

# pushes local-branch to origin and adds tracking reference
</pre>
<pre>
<code><b>git push --dry-run</b></code>

# shows what is about to be pushed
</pre>
<pre>
<code><b>1. git rebase --interactive &lt;xxxxxxxx^&gt;
2. git commit --amend (change pick to edit in the line whose commit being modified)
3. git rebase --continue</b></code>

# allows to change the message of a commit which is not the very latest
# xxxxxxxx^ = number of the commit being edited
</pre>
<pre>
<code><b>git status</b></code>

# shows the working tree status
</pre>
<pre>
<code><b>git stash list</b></code>

# lists the stash entries that we currently have
</pre>
<pre>
<code><b>git stash push -m "task-99-description"</b></code>

# stashes the working copy
</pre>
<pre>
<code><b>git stash apply stash@{0}</b></code>

# applies the specific stash by stash name
</pre>
<pre>
<code><b>git reset --hard HEAD</b></code>

# let's you start over the merge if you screwed it up
</pre>
<pre>
<code><b>git reset --hard &lt;your commit hash key&gt;
</b></code>

# let's you reset your repo back a specified commit
# use git log to get the hash key of your desired commit
</pre>

## JavaScript
<pre>
<code><b>yarn prettier --write .\file.js</b></code>

# formats a file using prettier node module
</pre>

## Linux
<pre>
<code><b>id -u &lt;user-name&gt;</b></code>

# gets the id of the user by username
</pre>
<pre>
<code><b>find . -iname "*msbuild*"</b></code>

# starts a case-insensitive (-i) search for keyword msbuild 
# in current directory and all directories inside it
</pre>
<pre>
<code><b>cut -d: -f1 /etc/passwd</b></code>

# lists all local users 
</pre>
<pre>
<code><b>adduser &lt;user-name&gt;</b></code>

# creates a new user
</pre>
<pre>
<code><b>su -c "/usr/share/dotnet/dotnet-sonarscanner end" \
	-s /bin/sh &lt;user-name&gt;</b></code>

# runs dotnet-sonarscanner utility as another user
</pre>
<pre>
<code><b>apt-get install ttf-mscorefonts-installer -y</b></code>

# installs ttf-mscorefonts-installer
# -y = automatic yes to prompts
</pre>
<pre>
<code><b>curl `
	-X GET "http://captive.apple.com/" `
	-H "Origin: https://subdomain.mydomain.com" `
	-H "accept: application/json"</b></code>

# helps test CORS
</pre>

## Serverless
<pre>
<code><b>yarn sls deploy `
	--aws-profile &lt;aws-profile-name&gt; `
	--stage dev `
	--region ap-southeast-2
	--verbose</b></code>

# deploys the serverless application to specified region and stage
</pre>
<pre>
<code><b>yarn sls remove `
	--stage dev `
	--region ap-southeast-2 `
	--verbose</b></code>

# removes the deployed service, defined in your current working directory
</pre>

## Windows
<pre>
<code><b>1. netstat -ano | findstr :3000</b>
<b>2. taskkill /pid &lt;process-id&gt; /F</b></code>

# finds the id of the process listening on the specified port and kills it
# /F forcefully terminates the process
</pre>
