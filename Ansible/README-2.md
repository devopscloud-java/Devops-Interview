🧩 Basic to Intermediate Scenario Questions
1. Inventory Management

Scenario:
You have 50 EC2 instances across dev, staging, and production environments. You want to manage all using a single inventory file.
Question:
How will you organize your Ansible inventory to handle environment-specific variables and playbooks?

✅ Expected Answer:

Use group variables (e.g., group_vars/dev.yml, group_vars/prod.yml).

Maintain separate host groups in the inventory file.

Use ansible-playbook -i inventory site.yml --limit dev to target specific environments.

2. Idempotency

Scenario:
You run a playbook multiple times, but a service restarts every time even though nothing changed.
Question:
How will you fix this issue?

✅ Expected Answer:

Use when conditions or creates/removes arguments.

Check for idempotent tasks — use Ansible modules instead of shell commands.

For example, instead of shell: systemctl restart, use service: module with state: restarted or reloaded properly.

3. Variable Precedence

Scenario:
A variable defined in group_vars/all.yml is being overridden unexpectedly.
Question:
How will you debug variable precedence and determine which variable is being used?

✅ Expected Answer:

Use ansible-inventory --graph or ansible -m debug -a "var=variable_name" host

Understand Ansible variable precedence order (extra vars > task vars > play vars > host/group vars > defaults).

4. Role Reusability

Scenario:
You have to install and configure Apache across multiple projects.
Question:
How will you design a reusable role that can be shared across teams?

✅ Expected Answer:

Create a role structure with defaults, vars, templates, and tasks.

Use role_name in multiple playbooks.

Use variables for version and configuration paths to keep it dynamic.

5. Dynamic Inventory

Scenario:
Your infrastructure is on AWS and new instances are created automatically via Terraform.
Question:
How will Ansible automatically detect and manage new EC2 instances?

✅ Expected Answer:

Use dynamic inventory plugins like aws_ec2.yml.

Configure credentials and filters to automatically fetch EC2 IPs.

Run playbook:

ansible-playbook -i aws_ec2.yml site.yml

⚙️ Advanced Real-World Scenarios
6. Zero-Downtime Deployment

Scenario:
You need to update a web application without downtime.
Question:
How will you achieve this using Ansible?

✅ Expected Answer:

Use rolling updates with serial deployment:

serial: 1


Load balance traffic with ELB/NGINX, remove one node at a time, deploy, and re-add it.

Use health checks before moving to the next node.

7. Secret Management

Scenario:
You need to store database passwords securely in playbooks.
Question:
How will you handle this in Ansible?

✅ Expected Answer:

Use Ansible Vault to encrypt variables:

ansible-vault encrypt secrets.yml


Reference them in playbooks via vars_files.

Use --ask-vault-pass or Vault IDs for multiple vaults.

8. Error Handling

Scenario:
If one of the tasks fails on a host, you don’t want the entire playbook to stop.
Question:
How can you continue execution and handle the error?

✅ Expected Answer:

Use:

ignore_errors: yes


or

block:
  - name: risky task
    command: ...
rescue:
  - debug: msg="Task failed, continuing..."

9. Conditional Execution

Scenario:
You need to install Nginx only if the OS is Ubuntu.
Question:
How can you achieve this conditionally?

✅ Expected Answer:

"- name: Install Nginx
  apt:
    name: nginx
    state: present
  when: ansible_os_family == "Debian""

10. CI/CD Integration

Scenario:
You want to trigger Ansible playbooks automatically from Jenkins after a successful build.
Question:
How will you integrate Jenkins and Ansible?

✅ Expected Answer:

Use Jenkins Ansible plugin or shell step:

ansible-playbook -i inventory deploy.yml


Pass build artifacts or variables via extra-vars:

ansible-playbook deploy.yml -e "version=${BUILD_NUMBER}"

11. Performance Optimization

Scenario:
Your playbook takes too long to execute across 100 nodes.
Question:
How will you speed it up?

✅ Expected Answer:

Increase forks in ansible.cfg: forks = 50

Use async + poll for parallel tasks.

Limit facts gathering with gather_facts: no.

Use tags to run selective tasks.

12. Troubleshooting SSH Connectivity

Scenario:
One host in your inventory fails with SSH timeout.
Question:
What steps will you take to troubleshoot?

✅ Expected Answer:

Check SSH key and permissions.

Run:

ansible all -m ping -vvv


Verify /etc/ansible/hosts and connectivity manually with ssh.

13. File Synchronization

Scenario:
You need to sync application logs from multiple servers to a central location.
Question:
How will you do it with Ansible?

✅ Expected Answer:

Use synchronize module (rsync wrapper):

"- name: Sync logs
  synchronize:
    src: /var/log/app/
    dest: /central/logs/{{ inventory_hostname }}/
    mode: pull"

14. Rolling Restart

Scenario:
You need to restart Tomcat servers in a rolling fashion without downtime.
Question:
What’s your approach?

✅ Expected Answer:

Use:

"serial: 1
tasks:
  - name: Restart tomcat
    service:
      name: tomcat
      state: restarted"

15. Debugging

Scenario:
A variable value is not as expected inside a template.
Question:
How will you debug it?

✅ Expected Answer:

Use:

- debug: var=variable_name
- Add -vvv flag for verbose output.

-Use Jinja2 filters in templates to inspect ({{ var | to_nice_json }}).
