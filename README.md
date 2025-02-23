# dijaga-patroni-replication
PostgreSQL High Availability setup using Patroni with streaming replication.  This repository contains configuration files and setup guides for managing  a highly available PostgreSQL cluster using Patroni.

Dijaga Patroni Replication Setup

This project sets up a High Availability (HA) PostgreSQL cluster using Patroni, with support for replication. The setup includes configuration files and detailed instructions on how to deploy a PostgreSQL cluster with Patroni on a local machine or server.

Overview

This repository contains the configuration and setup files to deploy a Patroni-managed PostgreSQL High Availability cluster. The main components of the setup are:
- **Patroni**: Orchestrates PostgreSQL for high availability.
- **etcd**: Stores cluster state and configuration.
- **PostgreSQL**: The relational database managed by Patroni.

The setup includes two nodes:
- **Node 1**: Acts as the **Leader**.
- **Node 2**: Acts as the **Replica**.

Prerequisites

Before setting up the cluster, make sure you have the following installed:
- **PostgreSQL** (version 14 or above)
- **Patroni** (used for high availability)
- **etcd** (key-value store for cluster state)
- **Python 3.x** (for Patroni and necessary dependencies)
- **Systemd** for managing the services

Setup Instructions

1. Clone the Repository

Clone this repository to your server or virtual machine.

```bash
git clone https://github.com/Setya78/dijaga-patroni-replication.git
cd dijaga-patroni-replication


2. Configuration Files
There are two main configuration files in this repository:

patroni.yml: Main Patroni configuration file for Node 1.
patroni-node2.yml: Configuration file for Node 2.
You may need to modify the configurations according to your system, especially paths and addresses for etcd and PostgreSQL data directories.

3. Set Up PostgreSQL Directories
Ensure the directories for PostgreSQL are set up correctly and owned by the postgres user. For example:

bash

sudo mkdir -p /var/lib/postgresql/14/main
sudo chown -R postgres:postgres /var/lib/postgresql/14/main
sudo chmod -R 700 /var/lib/postgresql/14/main

4. Start Patroni
Node 1:
To start Node 1, run the following command:

bash

sudo -u postgres patroni /etc/patroni.yml

Node 2:
For Node 2, run the same command using its specific configuration file:

bash

sudo -u postgres patroni /etc/patroni-node2.yml

5. Verify the Cluster Status
After starting both nodes, you can check the status of the Patroni cluster by running:

bash

patronictl -c /etc/patroni.yml list

This will show you the cluster status, including the role of each node (Leader/Replica) and whether they are running correctly.

6. PostgreSQL Connection
You can connect to the PostgreSQL database on each node using psql:

For Node 1 (Leader):
bash

psql -h localhost -U postgres -p 5432

For Node 2 (Replica):
bash

psql -h localhost -U postgres -p 5433

Note that the replica is set up for read-only access.

Usage
Failover Test: Simulate a failover by stopping the Patroni service on Node 1. Node 2 should automatically become the new Leader.

Replication Check: Ensure that data written to the Leader node is replicated to the Replica node by inserting data into Node 1 and verifying it on Node 2.

Troubleshooting
If you encounter any issues, check the logs for detailed error messages:

bash

journalctl -u patroni

Ensure that PostgreSQL and Patroni are both running on the correct ports and that the network configuration is correct.
