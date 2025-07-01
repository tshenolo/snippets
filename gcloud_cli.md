# Google Cloud CLI (gcloud) Cheatsheet

*   **Purpose**: Command-line interface for managing Google Cloud Platform (GCP) resources.
*   **Installation**: Google Cloud SDK.
*   **Initialization & Authentication**: `gcloud init` (sets up project, account, default region/zone), `gcloud auth login`.
*   **Core Syntax**: `gcloud <component> <group> <command> --flags`.
*   **Common Components and Commands**:
    *   Configuration: `gcloud config set project <project_id>`, `gcloud config set compute/zone <zone>`, `gcloud config list`.
    *   Compute Engine (VMs):
        *   `gcloud compute instances create my-vm --machine-type e2-medium --image-family debian-11 --image-project debian-cloud --zone us-central1-a`
        *   `gcloud compute instances list`, `gcloud compute instances describe my-vm`, `gcloud compute instances start/stop/delete my-vm`.
        *   `gcloud compute ssh my-vm`.
    *   Cloud Storage (Buckets & Objects):
        *   `gsutil mb gs://my-bucket` (gsutil is part of gcloud SDK for storage).
        *   `gsutil cp myfile.txt gs://my-bucket/`
        *   `gsutil ls gs://my-bucket/`
    *   Google Kubernetes Engine (GKE):
        *   `gcloud container clusters create my-cluster --num-nodes 3 --zone us-central1-a`
        *   `gcloud container clusters get-credentials my-cluster --zone us-central1-a` (configures kubectl).
    *   App Engine: `gcloud app deploy app.yaml`, `gcloud app browse`.
    *   Cloud SQL: `gcloud sql instances create my-instance --database-version MYSQL_8_0 --region us-central1`.
    *   Deployment Manager: `gcloud deployment-manager deployments create my-deployment --config my-config.yaml`.
*   **Flags**: `--project`, `--zone`, `--region`, specific options for each command.
*   **Output Formats**: `--format=json` (default is often YAML-like or text), `yaml`, `text`, `csv`, `table`.
*   **Filtering and Formatting Output**: `--filter` (expression), `--format="value(name)"`.
*   **Scripting**: Use in shell scripts.
*   **Service Accounts**: For non-interactive authentication.
