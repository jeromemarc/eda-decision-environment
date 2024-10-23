# EDA Decision Environment (DE) for Red Hat Insights

This repository aims to create a Decision Environment container image utilizing the `ansible-rulebook` tool. The resulting image is intended for use in Event-Driven Ansible (EDA) automation. It integrates Red Hat Insights collections and includes the main dependencies for executing Ansible rulebooks.

A build of this DE image is available on [quay.io/jeromemarc/de-insights-eda](quay.io/jeromemarc/de-insights-eda)

## Container Image

The container image is based on the `registry.access.redhat.com/ubi9-minimal` base image and includes the following components:

- Java 17
- Python 3.11
- GCC (GNU Compiler Collection)
- Ansible
- Ansible Collections:
  - ansible.eda
  - community.general
  - redhatinsights.eda
  - redhat.insights_eda
  - servicenow.itsm
- Python packages:
  - ansible-rulebook
  - asyncio
  - aiokafka
  - aiohttp
  - aiosignal
  - asyncio_mqtt

## Build instructions:

1. **Configure your credentials to Red Hat Automation Hub**:

   Visit https://console.redhat.com/ansible/automation-hub/token and generate an Offline Token for Red Hat Automation Hub

   Edit ansible.cfg file and replace the `token` value under `[galaxy_server.automation_hub]`

1. **Build the container image**:

   Run the following command from the extracted repository:

   ```bash
   ansible-builder build -t eda-decision-environment -f de-builder.yml
   ```

2. **Push the container image**

   To push the container image to a remote repository, tag and push the image:

   ```bash
   podman login <REGISTRY_HOST>
   podman tag eda-decision-environment <REGISTRY_HOST>/<YOUR_USERNAME>/eda-decision-environment
   podman push <REGISTRY_HOST>/<YOUR_USERNAME>/eda-decision-environment
   ```

Once uploaded, you can use your new Decision Environement container in Event-Driven Ansible.
