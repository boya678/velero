# instalar el cli de velero https://velero.io/docs/v1.3.0/velero-install/
#instalar velero en el cluster con el cluster en el contexto de kubectl
velero install --provider azure --bucket STORORAGEACCOUNTCONTAINERNAME --secret-file ARCHIVOLLAVES --backup-location-config STORAGERESOURCEGROUP,storageAccount=STORORAGEACCOUNTNAME --plugins velero/velero-plugin-for-microsoft-azure:latest
#crear un schedule con el CLI, este hace backup de todo menos del los namespace de systema, todos los dias a las 00:00 UTC
velero schedule update day --schedule "*0 0 * * *"
#o utilizar un manifest propio 
kubectl apply -f schedule.yaml
#con el cluster en el contexto de kubectl ejecutar la restauración NOMBREDELBACKUP= es el nombre de la carpeta que se genera en el container del storoge account
velero restore create --from-backup NOMBREDELBACKUP
