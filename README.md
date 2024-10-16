# Kubernetes Cluster installation with Ansible

This Ansible project automates the installation and configuration of a Kubernetes cluster across multiple machines. The playbook and tasks included will set up the control plane (master node) and worker nodes, generate necessary tokens for joining the cluster, and ensure that all configurations are properly applied.

## Table of Contents

- [Project Structure](#project-structure)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Variables](#variables)
- [Usage](#usage)
- [Example](#example)
- [Troubleshooting](#troubleshooting)
- [Contributions](#contributions)
- [License](#license)

## Project Structure

```bash
├── group_vars/
│── ├── k8s_prod/vars.yml         # Variables specific to the Kubernetes production environment
│── hosts/
│   ├── hosts_prod       # Production hosts inventory
├── tasks/
│   ├── generate_join_token.yml  # Task to generate join token for worker nodes
│   ├── install_kube_master.yml  # Task to install and configure Kubernetes control plane (master)
│   ├── install_kube.yml         # Common task to install Kubernetes on nodes
│   ├── join_cluster.yml         # Task to make worker nodes join the cluster
├── ansible.cfg         # Ansible configuration file
├── playbook.yml        # Main playbook to launch Kubernetes cluster setup
└── README.md           # Project documentation
```

## Features

- **Automated Control Plane Installation**: Automatically sets up Kubernetes master nodes, initializing the control plane.
- **Worker Node Setup**: Worker nodes are automatically configured and join the cluster using the generated token.
- **Token Generation**: A unique join token is created to securely add worker nodes to the cluster.
- **Scalable & Customizable**: Easily customizable for different environments by editing the `vars.yml` and `hosts_prod` files.

## Requirements

- **Ansible**: Make sure Ansible is installed and configured.

## Installation

1. Clone the repository to your control machine (the machine running Ansible):

   ```bash
   git clone <repository_url>
   cd <project_directory>
   ```

2. Modify the `hosts_prod` file under `hosts/` to reflect your infrastructure's IP addresses or hostnames.

3. Update the `vars.yml` in the `k8s_prod/` folder with the necessary configuration settings (e.g., network ranges, Kubernetes versions).

4. Run the playbook to install Kubernetes and configure the cluster:

   ```bash
   ansible-playbook -u user -i group_vars/hosts_prod playbook.yml
   ```

## Variables

The variables are defined in `vars.yml`, including:

- **Kubernetes version**
- **Pod network CIDR**
- **Service network CIDR**

Feel free to adjust these based on your cluster's requirements.

## Usage

1. Ensure all nodes are correctly listed in the `hosts_prod` file and variables are configured.
2. Run the playbook as described above.
3. The master node will be installed, and worker nodes will automatically join the cluster using the generated token.

## Example

Here’s an example command to launch the playbook:

```bash
ansible-playbook -u user -i group_vars/hosts_prod playbook.yml
```

The playbook will:

- Configure all nodes for Kubernetes installation
- Install Docker and Kubernetes on all nodes
- Configure the control plane on the master
- Generate a token and have the workers join the cluster

## Troubleshooting

- Ensure that the managed nodes are accessible via SSH.
- Check that the hostnames/IPs listed in the inventory file (`hosts_prod`) are correct.

## Contributions

Contributions are welcome! Feel free to submit a pull request or open an issue for feature suggestions or bug reports.

## License

This project is licensed under the MIT License. See the `LICENSE` file for more information.
