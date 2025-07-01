# Google Cloud CLI (gcloud) Cheatsheet

The Google Cloud CLI (`gcloud`) is a set of tools to create and manage Google Cloud resources. It includes `gcloud`, `gsutil` (for Cloud Storage), and `bq` (for BigQuery).

## Installation and Setup

*   **Install Google Cloud SDK**: Follow the official documentation for your OS: [https://cloud.google.com/sdk/docs/install](https://cloud.google.com/sdk/docs/install)
*   **Initialize `gcloud`**: This sets up your configuration, authenticates your user account, and sets default project, region, and zone.
    ```bash
    gcloud init
    ```
*   **Authenticate User Account** (if not done via `gcloud init` or for additional accounts):
    ```bash
    gcloud auth login
    ```
*   **Authenticate with a Service Account** (for automation, e.g., on a server):
    ```bash
    gcloud auth activate-service-account --key-file=/path/to/service-account-key.json
    # To list authenticated accounts:
    # gcloud auth list
    ```
*   **List Configurations**:
    ```bash
    gcloud config configurations list
    ```
*   **Activate a Configuration**:
    ```bash
    gcloud config configurations activate <CONFIG_NAME>
    ```
*   **Set Default Project**:
    ```bash
    gcloud config set project <PROJECT_ID>
    ```
*   **Set Default Region and Zone** (for Compute Engine):
    ```bash
    gcloud config set compute/region <REGION> # e.g., us-central1
    gcloud config set compute/zone <ZONE>     # e.g., us-central1-a
    ```
*   **View Current Configuration**:
    ```bash
    gcloud config list
    # gcloud config list project # Show current project
    ```
*   **Get Help**:
    ```bash
    gcloud --help
    gcloud <component> --help # e.g., gcloud compute --help
    gcloud <component> <group> --help # e.g., gcloud compute instances --help
    gcloud <component> <group> <command> --help # e.g., gcloud compute instances create --help
    ```
*   **Update gcloud CLI components**:
    ```bash
    gcloud components update
    # List installed components:
    # gcloud components list
    ```

## Projects

*   **List Projects** your account has access to:
    ```bash
    gcloud projects list
    ```
*   **Describe a Project**:
    ```bash
    gcloud projects describe <PROJECT_ID>
    ```

## Compute Engine (Virtual Machines)

*   **List VM Instances**:
    ```bash
    gcloud compute instances list
    # Filter by zone:
    # gcloud compute instances list --zones us-central1-a,us-west1-b
    ```
*   **Create a VM Instance**:
    ```bash
    gcloud compute instances create <INSTANCE_NAME> \
        --machine-type <MACHINE_TYPE> \
        --image-family <IMAGE_FAMILY> \
        --image-project <IMAGE_PROJECT> \
        --boot-disk-size <SIZE_GB> \
        --zone <ZONE> \
        --tags http-server,https-server \
        --metadata startup-script="sudo apt-get update && sudo apt-get install -y nginx"
    # Example:
    # gcloud compute instances create my-vm-1 --machine-type e2-medium --image-family debian-11 --image-project debian-cloud --zone us-central1-a
    # Example with preemptible VM:
    # gcloud compute instances create my-preempt-vm --machine-type n1-standard-1 --preemptible --maintenance-policy TERMINATE
    ```
    *   Common machine types: `e2-micro`, `e2-small`, `e2-medium`, `n1-standard-1`, `n2-standard-2`, etc.
    *   Common image families: `debian-11`, `ubuntu-2004-lts`, `centos-7`, `rhel-8`, `windows-2019`.
    *   Common image projects: `debian-cloud`, `ubuntu-os-cloud`, `centos-cloud`, `rhel-cloud`, `windows-cloud`.
*   **Show Details of a VM Instance**:
    ```bash
    gcloud compute instances describe <INSTANCE_NAME> --zone <ZONE>
    ```
*   **Start a VM Instance**:
    ```bash
    gcloud compute instances start <INSTANCE_NAME> --zone <ZONE>
    ```
*   **Stop a VM Instance**:
    ```bash
    gcloud compute instances stop <INSTANCE_NAME> --zone <ZONE>
    ```
*   **Reset a VM Instance** (similar to power cycling):
    ```bash
    gcloud compute instances reset <INSTANCE_NAME> --zone <ZONE>
    ```
*   **Delete a VM Instance**:
    ```bash
    gcloud compute instances delete <INSTANCE_NAME> --zone <ZONE> --quiet # --quiet to skip confirmation
    ```
*   **SSH into a VM Instance**: `gcloud` handles key generation and transfer if needed.
    ```bash
    gcloud compute ssh <INSTANCE_NAME> --zone <ZONE>
    # SSH as a different user:
    # gcloud compute ssh <USERNAME>@<INSTANCE_NAME> --zone <ZONE>
    ```
*   **Copy Files to/from a VM Instance**: Uses `scp` semantics.
    *   Local to VM:
        ```bash
        gcloud compute scp /local/path/to/file <INSTANCE_NAME>:/remote/path/ --zone <ZONE>
        ```
    *   VM to Local:
        ```bash
        gcloud compute scp <INSTANCE_NAME>:/remote/path/to/file /local/path/ --zone <ZONE>
        ```
    *   Recursively (`--recurse`):
        ```bash
        gcloud compute scp --recurse /local/dir <INSTANCE_NAME>:/remote/dir --zone <ZONE>
        ```
*   **Add/Remove Tags on a VM**:
    ```bash
    gcloud compute instances add-tags <INSTANCE_NAME> --tags new-tag,another-tag --zone <ZONE>
    gcloud compute instances remove-tags <INSTANCE_NAME> --tags old-tag --zone <ZONE>
    ```
*   **Set Machine Type (Resize VM)**: VM must be stopped.
    ```bash
    gcloud compute instances set-machine-type <INSTANCE_NAME> --machine-type <NEW_MACHINE_TYPE> --zone <ZONE>
    ```
*   **Manage Disks**:
    *   List disks: `gcloud compute disks list`
    *   Create a disk: `gcloud compute disks create <DISK_NAME> --size <SIZE_GB> --type <DISK_TYPE> --zone <ZONE>` (e.g., `pd-standard`, `pd-ssd`)
    *   Attach a disk: `gcloud compute instances attach-disk <INSTANCE_NAME> --disk <DISK_NAME> --zone <ZONE>`
    *   Detach a disk: `gcloud compute instances detach-disk <INSTANCE_NAME> --disk <DISK_NAME> --zone <ZONE>`

## Cloud Storage (Buckets and Objects - using `gsutil`)

`gsutil` is the command-line tool for Cloud Storage. It's part of the Google Cloud SDK.

*   **Create a Bucket**: Bucket names must be globally unique.
    ```bash
    gsutil mb -p <PROJECT_ID> -c <STORAGE_CLASS> -l <LOCATION> gs://<BUCKET_NAME>/
    # Example:
    # gsutil mb -p my-gcp-project -c STANDARD -l US-CENTRAL1 gs://my-unique-app-bucket/
    ```
    *   Storage classes: `STANDARD`, `NEARLINE`, `COLDLINE`, `ARCHIVE`.
    *   Locations: e.g., `US-CENTRAL1`, `EUROPE-WEST1`, `ASIA-EAST1` (region) or `US` (multi-region).
*   **List Buckets**:
    ```bash
    gsutil ls -p <PROJECT_ID>
    ```
*   **List Contents of a Bucket**:
    ```bash
    gsutil ls gs://<BUCKET_NAME>/
    # List recursively:
    # gsutil ls -r gs://<BUCKET_NAME>/
    ```
*   **Upload Files/Directories**:
    *   Upload a single file:
        ```bash
        gsutil cp /local/path/to/file.txt gs://<BUCKET_NAME>/
        # Upload and rename:
        # gsutil cp /local/path/to/file.txt gs://<BUCKET_NAME>/new-filename.txt
        ```
    *   Upload a directory recursively (`-r`):
        ```bash
        gsutil cp -r /local/path/to/directory gs://<BUCKET_NAME>/
        ```
    *   Synchronize a directory (`rsync`): More efficient for repeated uploads, only copies changed/new files.
        ```bash
        gsutil rsync -r /local/path/to/directory gs://<BUCKET_NAME>/target-directory
        # Use -d to delete files in destination that are not in source
        # gsutil rsync -d -r /local/dir gs://<BUCKET_NAME>/target-dir
        ```
*   **Download Files/Directories**:
    *   Download a single file:
        ```bash
        gsutil cp gs://<BUCKET_NAME>/object-name.txt /local/path/
        ```
    *   Download a directory recursively:
        ```bash
        gsutil cp -r gs://<BUCKET_NAME>/source-directory /local/path/
        ```
*   **Delete Objects**:
    ```bash
    gsutil rm gs://<BUCKET_NAME>/object-name.txt
    # Delete all objects in a "folder":
    # gsutil rm -r gs://<BUCKET_NAME>/folder/*
    ```
*   **Delete a Bucket** (must be empty first, unless `-r` is used cautiously):
    ```bash
    # gsutil rm -r gs://<BUCKET_NAME>/ # Deletes all objects
    # gsutil rb gs://<BUCKET_NAME>/     # Deletes empty bucket
    # To delete a bucket and all its contents (use with extreme care):
    # gsutil rm -r gs://<BUCKET_NAME>/
    ```
*   **Set Object ACLs (Access Control)**:
    ```bash
    gsutil acl ch -u AllUsers:R gs://<BUCKET_NAME>/public-object.jpg # Make object publicly readable
    gsutil acl ch -g <GROUP_EMAIL>:W gs://<BUCKET_NAME>/object.txt # Grant write to a group
    # For fine-grained access, prefer IAM permissions on buckets.
    ```
*   **Set Bucket Default Object ACLs**:
    ```bash
    gsutil defacl ch -u AllUsers:R gs://<BUCKET_NAME> # New objects will be public by default
    ```
*   **Make Object Publicly Readable (simpler way)**:
    ```bash
    gsutil iam ch allUsers:objectViewer gs://<BUCKET_NAME>/public-file.txt
    # For entire bucket (all objects become public):
    # gsutil iam ch allUsers:objectViewer gs://<BUCKET_NAME>
    ```
*   **Generate Signed URLs** (time-limited access to private objects):
    ```bash
    gsutil signurl -d 10m /path/to/service-account-key.json gs://<BUCKET_NAME>/private-object.zip
    # -d 10m: Duration 10 minutes
    ```

## Google Kubernetes Engine (GKE)

*   **Create a GKE Cluster**:
    ```bash
    gcloud container clusters create <CLUSTER_NAME> \
        --num-nodes <NUMBER_OF_NODES_PER_ZONE> \
        --machine-type <MACHINE_TYPE> \
        --zone <ZONE> # Or --region <REGION> for regional clusters
    # Example:
    # gcloud container clusters create my-gke-cluster --num-nodes 2 --machine-type e2-medium --zone us-central1-a
    # Example Autopilot cluster:
    # gcloud container clusters create-auto my-autopilot-cluster --region us-central1
    ```
*   **List GKE Clusters**:
    ```bash
    gcloud container clusters list
    ```
*   **Get Credentials for a Cluster** (configures `kubectl`):
    ```bash
    gcloud container clusters get-credentials <CLUSTER_NAME> --zone <ZONE> # Or --region <REGION>
    # After this, you can use kubectl commands
    # kubectl get nodes
    # kubectl get pods --all-namespaces
    ```
*   **Describe a GKE Cluster**:
    ```bash
    gcloud container clusters describe <CLUSTER_NAME> --zone <ZONE>
    ```
*   **Resize a GKE Cluster's Node Pool**:
    ```bash
    gcloud container clusters resize <CLUSTER_NAME> \
        --node-pool <NODE_POOL_NAME> \
        --num-nodes <NEW_NODE_COUNT> \
        --zone <ZONE>
    # Example:
    # gcloud container clusters resize my-gke-cluster --node-pool default-pool --num-nodes 3 --zone us-central1-a
    ```
*   **Upgrade a GKE Cluster's Master or Nodes**:
    *   Get available versions: `gcloud container get-server-config --zone <ZONE>`
    ```bash
    # Upgrade master:
    gcloud container clusters upgrade <CLUSTER_NAME> --master --cluster-version <NEW_VERSION> --zone <ZONE>
    # Upgrade nodes in a node pool:
    gcloud container clusters upgrade <CLUSTER_NAME> --node-pool <NODE_POOL_NAME> --cluster-version <NEW_VERSION> --zone <ZONE>
    ```
*   **Delete a GKE Cluster**:
    ```bash
    gcloud container clusters delete <CLUSTER_NAME> --zone <ZONE> --quiet
    ```

## App Engine

*   **Deploy an App Engine Application** (from directory with `app.yaml`):
    ```bash
    gcloud app deploy app.yaml [--project <PROJECT_ID>] [--version <VERSION_ID>] [--quiet]
    # Example (Node.js):
    # gcloud app deploy
    ```
*   **List App Engine Services**:
    ```bash
    gcloud app services list
    ```
*   **List App Engine Versions for a Service**:
    ```bash
    gcloud app versions list --service <SERVICE_NAME>
    ```
*   **Browse an App Engine Service**:
    ```bash
    gcloud app browse [--service <SERVICE_NAME>] [--version <VERSION_ID>]
    ```
*   **Stream App Engine Logs**:
    ```bash
    gcloud app logs tail -s default # For default service
    # gcloud app logs read # Read logs
    ```
*   **Set Traffic Splitting between Versions**:
    ```bash
    gcloud app services set-traffic <SERVICE_NAME> --splits <VERSION1>=<WEIGHT1>,<VERSION2>=<WEIGHT2>
    # Example:
    # gcloud app services set-traffic default --splits v1=0.8,v2=0.2
    ```

## Cloud SQL (Managed MySQL, PostgreSQL, SQL Server)

*   **List Cloud SQL Instances**:
    ```bash
    gcloud sql instances list
    ```
*   **Create a Cloud SQL Instance (e.g., MySQL)**:
    ```bash
    gcloud sql instances create <INSTANCE_NAME> \
        --database-version MYSQL_8_0 \
        --tier db-f1-micro \
        --region <REGION> \
        --root-password <ROOT_PASSWORD> # Prompts if not provided
    # Example for PostgreSQL:
    # gcloud sql instances create my-pg-instance --database-version POSTGRES_13 --cpu=2 --memory=4GB --region us-central1
    ```
*   **Describe a Cloud SQL Instance**:
    ```bash
    gcloud sql instances describe <INSTANCE_NAME>
    ```
*   **Connect to a Cloud SQL Instance using Cloud SQL Proxy**:
    1.  Install Cloud SQL Auth Proxy: [https://cloud.google.com/sql/docs/mysql/sql-proxy](https://cloud.google.com/sql/docs/mysql/sql-proxy)
    2.  Start the proxy:
        ```bash
        ./cloud_sql_proxy -instances=<PROJECT_ID>:<REGION>:<INSTANCE_NAME>=tcp:3306
        # Example: ./cloud_sql_proxy -instances=my-project:us-central1:my-mysql-instance=tcp:3306
        ```
    3.  Connect using local MySQL client:
        ```bash
        mysql -u root -p --host 127.0.0.1 --port 3306
        ```
*   **Set Root Password**:
    ```bash
    gcloud sql users set-password root --host % --instance <INSTANCE_NAME> --password <NEW_PASSWORD> # Prompts if not provided
    ```
*   **Create a Database within an Instance**:
    ```bash
    gcloud sql databases create <DATABASE_NAME> --instance <INSTANCE_NAME>
    ```

## Output Formatting and Filtering

*   **Output Formats (`--format`)**:
    *   `default` (YAML-like for complex, text for simple)
    *   `json`
    *   `yaml`
    *   `text` (key: value)
    *   `csv`
    *   `table` (human-readable table)
    *   `value(<key>)` (extracts a single value)
    ```bash
    gcloud compute instances list --format="table(name, zone, status)"
    gcloud projects list --format="value(projectId)"
    ```
*   **Filtering Output (`--filter`)**: Uses a Lisp-like expression syntax.
    ```bash
    gcloud compute instances list --filter="zone:(us-central1-a OR us-central1-b) AND status:RUNNING"
    gcloud projects list --filter="name ~ ^my-project-" # Regex match on name
    ```

This provides a comprehensive set of commands for `gcloud_cli.md`. Next will be `curl_wget.md`.The `gcloud_cli.md` cheatsheet has been updated with detailed command examples for managing various Google Cloud services like Compute Engine, Cloud Storage (gsutil), GKE, App Engine, and Cloud SQL. It also includes notes on output formatting and filtering.

Next, I will enhance `curl_wget.md` with more specific examples and common use cases for both `curl` and `wget`.
