## **Maintenance Repo for IT Ops — Overview**

This repo will house Ansible playbooks, inventories, roles, and automation workflows for common maintenance tasks such as:

* Restarting services
* Cleaning disk space
* Applying patches
* Backups & restore
* VM resizing
* Log rotation
* Service health checks
* Running scheduled compliance checks
* Enabling/disabling access (e.g., for users, ports)
* Cloud infrastructure cleanup

---

## **Folder Structure**

```bash
itops-maintenance/
├── README.md
├── inventories/
│   ├── prod/
│   │   └── inventory.yaml
│   └── staging/
│       └── inventory.yaml
├── group_vars/
│   └── all.yaml
├── host_vars/
│   └── vm01.yaml
├── playbooks/
│   ├── cleanup_disk.yaml
│   ├── restart_services.yaml
│   ├── patch_system.yaml
│   └── resize_vm.yaml
├── roles/
│   ├── cleanup/
│   │   ├── tasks/
│   │   └── defaults/
│   └── patching/
│       ├── tasks/
│       └── defaults/
├── vars/
│   └── common_vars.yaml
├── files/
│   └── scripts/
├── templates/
│   └── config.j2
├── ci/
│   ├── github-actions.yaml (or GitLab/others)
├── requirements.yml
└── ansible.cfg
```

---

## 🛠️ **Key Maintenance Playbooks to Include**

Each in `playbooks/` folder:

* `cleanup_disk.yaml`: Remove temp files, unused packages, old logs
* `patch_system.yaml`: Apply OS updates with optional reboots
* `restart_services.yaml`: Restart services like nginx, systemd units
* `health_check.yaml`: Validate system/service health
* `backup_data.yaml`: Backup files/db using rsync or snapshot
* `user_access.yaml`: Manage user/group access (add/remove/disable)
* `resize_vm.yaml`: Change cloud VM size (using Terraform or cloud modules)
* `rotate_logs.yaml`: Compress/move/delete old logs
* `tagging.yaml`: Enforce metadata tagging on cloud resources
* `drift_check.yaml`: Compare actual vs desired config (using Terraform or custom scripts)

---

## 🔄 **Automation Trigger Options**

Choose based on your environment:

| Platform       | How to Trigger Maintenance Tasks               |
| -------------- | ---------------------------------------------- |
| AWX/Tower      | Schedule jobs with credentials & inventory     |
| GitHub Actions | Trigger on PR/commit or manually               |
| GitLab CI/CD   | Use scheduled pipelines                        |
| Jenkins        | Use Ansible plugin or shell step               |
| Azure DevOps   | YAML pipelines with SSH/Azure login            |
| Cron job       | Run ansible-playbook via cron or systemd timer |
| Event-driven   | Use Webhook or EventBridge (AWS) + Lambda      |

---

---

## 🧩 **Best Practices**

| Area                | Recommendation                                                          |
| ------------------- | ----------------------------------------------------------------------- |
| 🔐 Secrets          | Use Ansible Vault or external secret manager (AWS SSM, Azure Key Vault) |
| 💬 Logging          | Use `ansible.builtin.debug` and `callback_plugins` for clean output     |
| 🔁 Idempotency      | Ensure playbooks can run multiple times without side effects            |
| 🧪 Testing          | Test in a staging environment using Molecule or CI/CD dry runs          |
| 🗃️ Inventory       | Use dynamic inventory plugins (Terraform, Azure, AWS, etc.)             |
| 🚧 Failure Strategy | Use `rescue:` and `block:` to handle errors gracefully                  |
| 📦 Reusability      | Parameterize tasks/roles with variables for reusability                 |
| 🚨 Alerts           | Integrate with Slack, Teams, email on failure                           |
| 📜 Docs             | Include README for each playbook describing intent, usage, variables    |


