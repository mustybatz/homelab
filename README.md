# 🏡 HomeLab | Kubernetes Adventures at Home

Welcome to my **HomeLab** repository! This is where all the magic happens—my Kubernetes home cluster configuration and documentation. If you’re curious about the details of what I’m up to, check out my [blog](https://bash.ghost.io/) for in-depth guides, experiments, and lessons learned. 🚀

The purpose of my HomeLab is to:
- 🔧 **Learn Kubernetes** by getting hands-on with real hardware and software setups.
- 🧪 **Experiment with Proof of Concept (PoC) projects**, testing ideas in a controlled environment.
- 🎉 **Deploy self-hosted apps** for fun and personal use.
- 🛡️ **Improve home network security** while exposing some services to the internet.
- 🕵️ **Practice disaster recovery, uptime management, and backups**—skills that directly relate to my role as a Site Reliability Engineer.

---

## ✨ GitOps: Version Control Meets Cluster Management
This repo also contains my **GitOps** configuration with **FluxCD** to keep my cluster in sync. This setup allows me to automate deployments and manage:
- 📈 Monitoring
- 🏡 Self-hosted apps
- ⚙️ Cluster configurations and more!

---

## ⚙️ Cluster Provisioning
Currently, my cluster consists of:
- 💻 Machines running **Ubuntu Server**
- ⚡ K3s installed on top using **Ansible**

If you’re interested in the Ansible configuration, you can find it [here](https://github.com/mustybatz/homelab-provisioning). 🚀

---

## 💻 Hardware Specs
Here’s the breakdown of my home cluster’s hardware setup:

### Main Workstation 🖥️
- **HP Z900**
  - 2x Intel Xeon X5650 processors (12 cores total)
  - 12 GiB of RAM

### Mini-PC Nodes 🖱️
- **Intel Core i5 (8th gen, 6 cores)**
- 16 GiB of RAM
- 256 GB of storage

### Total Cluster Resources:
- 🧠 **60 GiB RAM**
- 🖥️ **30 CPU cores**

This setup strikes a perfect balance between cost, performance, and energy efficiency, enabling me to explore Kubernetes while staying within a reasonable budget.

---

## 🚀 Applications Deployed
Here’s a shortlist of the apps and tools running in my cluster:
- 📊 **Prometheus** and **Grafana**: Monitoring and visualization.
- 🔗 **FluxCD**: GitOps automation for deployments.
- 📚 **Librum**: Self-hosted e-book reader with AI features.
- 🌐 **Pi-Hole**: Network-wide ad-blocking.
- 📝 **Ghost**: My blog publishing platform.
- 🛠️ **Cert-manager**: SSL/TLS certificate automation.
- 🗂️ **Linkding**: Self-hosted bookmark manager.
- 🛡️ **External-dns**: Automated DNS record updates.
- 💾 **MySQL/MariaDB**: Databases for application backends.

This lineup is just the beginning—there’s always more to explore! 🔭

---

## 📖 Learn More
For detailed write-ups, including how I:
- Set up **Ansible** for automating the cluster configuration 🤖
- Bootstraped **FluxCD** for GitOps workflows 🔄
- Deployed and tested applications in my cluster 🧪

...check out my blog: [bash.ghost.io](https://bash.ghost.io/). ✍️

---

## 🌈 Future Plans
- 🔄 Add high availability (HA) to the control plane.
- 🏗️ Experiment with new apps and architectures.
- 🛠️ Migrate from SQLite to etcd for K3s.
- 📦 Automate backups and disaster recovery.

Stay tuned for updates, and feel free to explore, fork, or contribute to this repo. Let’s build something awesome together! 🤝

---

## 🌐 Follow Along
- Blog: [bash.ghost.io](https://bash.ghost.io/) 🖋️
- Repo: [GitHub](https://github.com/mustybatz/homelab) 🧑‍💻

Enjoy exploring my Kubernetes journey! 🚢
