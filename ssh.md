pull files from remote host using rsync over a specific shell

    rsync -rvz -e 'ssh -p PORT_NUMBER -i PATH_TO_KEY' USER@HOST:PATH_TO_FILE_OR_DIR

