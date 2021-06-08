# Save docker volumes with Restic

Thanks to https://github.com/djmaze/resticker/

Configure HOST_DESTINATION_BACKUP and BACKUP_CRON variable in .env  
Make sure you want to backup the folder */var/lib/docker/volumes*     
Start : docker-compose up -d

To run a command : either open a console in portainer or  
`docker exec [CONTAINER_ID] [COMMAND]`

## Commands :

- list backup :  `restic -r rest:https://backupuser:PASSWORD4@rBACKUP_URL snapshots`

- find a specific volume, ex: `restic -r rest:https://backupuser:PASSWORD4@rBACKUP_URLfind docker_es_elasticsearch`


- Trigger a backup manually :  `restic backup /mnt/volumes`


## Restore a volume example : 

- Stop the container for which you want to restore a volume
- Delete the content of the volume repository. This step is necessary to properly restore an elasticsearch volume. Ex : `sudo rm -r /var/lib/docker/volumes/docker_es_elasticsearch`

`restic -r  rest:https://backupuser:PASSWORD4@rBACKUP_URL restore $ID --target / --include docker_es_elasticsearch`


  -  here volume name is *docker_es_elasticsearch* and *$ID* a specific snapshot id or "latest"
  -  *--target /* because the absolute path is used when restoring. "/mnt/test" if you ant to try it first
  -  Replace `https://backupuser:PASSWORD4@rBACKUP_URL` with the Rest server url


