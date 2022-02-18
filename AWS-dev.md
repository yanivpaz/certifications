# cname vs alias
## name
* cost money 
* only for non root domain
* points to any hostname


## alias
* free
* native health check 
* points to root or non root domain 


# code commit triggers
## SNS/Lambda
* delete branch
* push to branch
* notify external build system 
* code analsys

## cloudwatch events
* trigger for pull request 
* comment
* cloudwatch event toles goes into sns  
