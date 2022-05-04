
1. deploy the workflow
```
gcloud workflows deploy --source=./redis_export.yaml --location=us-central1 --service-account=cliu201-sa@cliu201.iam.gserviceaccount.com schedule_redis_export
```

2. (optional) test the workflow mannually
```
gcloud workflows run schedule_redis_export
```

3. create the cloud schedule to trige the workflow(hourly)
```
gcloud scheduler jobs create http redis_backup \
--schedule="0 * * * * " \
--uri="https://workflowexecutions.googleapis.com/v1/projects/cliu201/locations/us-central1/workflows/schedule_redis_export/executions" \
--message-body="{\"argument\": \"{}\"}" \
--time-zone="Asia/Shanghai" \
--oauth-service-account-email="cliu201-sa@cliu201.iam.gserviceaccount.com"
```
