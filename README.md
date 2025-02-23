# dijaga-patroni-replication
PostgreSQL High Availability setup using Patroni with streaming replication.  This repository contains configuration files and setup guides for managing  a highly available PostgreSQL cluster using Patroni.

# Dijaga Patroni Replication Setup

This project sets up a High Availability (HA) PostgreSQL cluster using Patroni, with support for replication. The setup includes configuration files and detailed instructions on how to deploy a PostgreSQL cluster with Patroni on a local machine or server.

## Overview

This repository contains the configuration and setup files to deploy a Patroni-managed PostgreSQL High Availability cluster. The main components of the setup are:
- **Patroni**: Orchestrates PostgreSQL for high availability.
- **etcd**: Stores cluster state and configuration.
- **PostgreSQL**: The relational database managed by Patroni.

The setup includes two nodes:
- **Node 1**: Acts as the **Leader**.
- **Node 2**: Acts as the **Replica**.

### Prerequisites

Before setting up the cluster, make sure you have the following installed:
- **PostgreSQL** (version 14 or above)
- **Patroni** (used for high availability)
- **etcd** (key-value store for cluster state)
- **Python 3.x** (for Patroni and necessary dependencies)
- **Systemd** for managing the services

## Setup Instructions

### 1. Clone the Repository

Clone this repository to your server or virtual machine.

```bash
git clone https://github.com/Setya78/dijaga-patroni-replication.git
cd dijaga-patroni-replication
