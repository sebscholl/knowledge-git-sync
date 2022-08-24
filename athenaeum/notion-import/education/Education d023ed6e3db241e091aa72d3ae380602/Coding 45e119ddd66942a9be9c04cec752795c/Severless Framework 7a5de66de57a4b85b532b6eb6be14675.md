# Severless Framework

Last Edited: December 19, 2019 11:43 PM

Commands

Invoke Function

$ sls invoke -f FUNCTION_NAME

Invoke Function w/ Logs

$ sls invoke -f FUNCTION_NAME -l

Invoke Function Locally

$ sls invoke local -f FUNCTION_NAME

Fix File Permission Issue For Handler (PY2.7)

$ chmod 644 HANDLER_FILE_PATH

Deploy Stack

$ sls deploy -v

Deploy Specific Function

$ sls deploy function -f FUNCTION_NAME

View Function Logs

$ sls logs -f FUNCTION_NAME

Trail Function Logs

$ sls logs -f FUNCTION_NAME -t

Destroy Stack

$ sls remove

# **Config**

In serverless.yml file, the templating engine will use first defined value in comma separated list.

=> ${opt:stage, self:provider.stage}