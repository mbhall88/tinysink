# tinysink
Synchronise Nanopore reads with a server.

This is a script for synchronising any `.fast5` or `.fastq` files being produced from a Nanopore experiment. Can be run during the sequencing, in which case it will sync new files as they are produced, or after the fact.

If you want to synchronise something other than the above listed file types feel free to change the code to your desire.

An example of how to run:

```sh
./tinysink -s <local_dir_to_data> -d <destination_dir_on_server> -u <username> -n <servername> 
```

To cancel, you just need to press `Ctrl-c` twice within 3 seconds. If you only press it once, nothing will happen.

If the destination directory on the server does not exist, it will be created for you.

Also, if there are connection issues with the server, such as internet dropouts etc. the script will go to sleep for 3 minutes before trying again. You can change this time is you like by changing the variable `WAIT_BETWEEN_SINK` at the top of the script.

**Note**: This script will **not** delete the files from the computer you are running it on - it just copies them. If you want them to be deleted after they are moved to the server you can add the `--remove-source-files` argument to the `rsync` command in the script. Alternatively you can just delete them yourself after the experiment is done (recommended). We tend to keep a back up of the data from these runs on a different server (cold storage). 
