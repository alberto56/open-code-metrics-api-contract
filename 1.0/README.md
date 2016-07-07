The provider is located via an URL such as:

$USER@$SERVER:$PATH

The client can obtain metrics for a project $PROJECT (where $PROJECT is a git repo), and $REQUESTID is a universally unique id, and $BRANCH, $HASH, and $SUBFOLDER are optional by doing the following:

    * ssh $USER@$SERVER "cd $PATH && ./api-contract/open-code-metrics/1.0/get-metrics.sh $PROJECT $REQUESTID [$BRANCH] [$HASH] [$SUBFOLDER]"
    * you will be able to check on the progress of your request for 72 hours by typing
    * ssh $USER@$SERVER "cat /tmp/$REQUESTID/info.txt"

The /tmp/$REQUESTID/info.txt file shall contain:

    Request id: <the request id>
    Created: YYYY-MM-DD
    Repo: <the git repo>
    Hash: <the hash>
    Branch: <the git branch>
    Subfolder: <the subfolder>
    Status: received|queue|processing|done
    Metrics: /path/to/metrics/folder

(Created date is in UTC timezone.)
(Metrics folder will not necessarily be set before the status is "done".)
(Hash, Branch, and Subfolder are optional.)

Once the status is "done", you can find CSV files in the /path/to/metrics/folder:

    * scp -r $USER@$SERVER:/path/to/metrics/folder/*csv

longest-function.csv will contain:

  name,lloc,file,start
