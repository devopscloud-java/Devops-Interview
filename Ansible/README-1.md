🧩 Ansible Concepts for DevOps Engineer — Interview Guide

🚀 What is Ansible?

Ansible is an open-source automation tool used for:

Configuration management

Application deployment

Infrastructure orchestration

It is agentless (uses SSH for communication).

Written in Python and uses YAML for playbooks.

⚙️ Core Components

🗂️ 1. Inventory

A list of managed nodes where Ansible runs tasks.

Default: /etc/ansible/hosts

Supports static and dynamic inventories.

[webservers]

192.168.1.10

192.168.1.11

🔧 2. Modules

Building blocks of Ansible.

Used to perform specific operations (install package, copy file, start service, etc.).

Example modules: apt, yum, copy, file, service.

<pre>- name: Install NGINX
  apt:
    name: nginx
    state: present</pre>

📜 3. Playbooks

YAML files defining automation tasks.

Contain plays → each play runs tasks on specified hosts.
<pre>
- name: Install and start NGINX
  hosts: webservers
  tasks:
    - name: Install NGINX
      apt:
        name: nginx
        state: present

    - name: Start NGINX
      service:
        name: nginx
        state: started
</pre>
🧱 4. Tasks

Individual actions performed by Ansible using modules.

🔁 5. Handlers

Used to perform actions only when notified (e.g., restart service after config change).
<pre>
tasks:
  - name: Copy config file
    copy:
      src: nginx.conf
      dest: /etc/nginx/nginx.conf
    notify: Restart nginx

handlers:
  - name: Restart nginx
    service:
      name: nginx
      state: restarted
</pre>
🧮 6. Variables

Make playbooks dynamic and reusable.

Defined in playbooks, inventory, or separate files.

<pre>vars:
  package_name: nginx</pre>

🧩 7. Templates

Use Jinja2 templates (.j2 files) to generate dynamic configuration files.

server_name {{ server_name }};

🗃️ 8. Roles

Structure to organize playbooks into reusable units.

Directory structure:

<pre>roles/
  myrole/
    tasks/
    handlers/
    templates/
    vars/
    defaults/</pre>


Create a role:

ansible-galaxy init myrole

🧾 9. Facts

Automatically gathered system information (OS, IP, memory, etc.).

Display using:

ansible all -m setup

⚖️ 10. Conditionals

Run tasks based on conditions.
<pre>
- name: Install on Ubuntu
  apt:
    name: nginx
  when: ansible_os_family == "Debian"
</pre>
🔄 11. Loops

Repeat a task multiple times.
<pre>
- name: Install multiple packages
  apt:
    name: "{{ item }}"
    state: present
  loop:
    - git
    - curl
    - vim
</pre>
🏷️ 12. Tags

Execute specific parts of a playbook.
<pre>
- name: Install NGINX
  apt:
    name: nginx
  tags: install

</pre>
Run:

ansible-playbook playbook.yml --tags "install"

🔐 13. Vault

Encrypt sensitive files (passwords, tokens, etc.).

ansible-vault create secrets.yml
ansible-vault encrypt file.yml
ansible-vault decrypt file.yml

⚠️ 14. Error Handling

Use ignore_errors or block/rescue/always blocks.
<pre>
- block:
    - name: Task that might fail
      command: /bin/false
  rescue:
    - name: Handle failure
      debug:
        msg: "Task failed, continuing..."
</pre>
☁️ Advanced / DevOps-Focused Concepts
🌐 15. Dynamic Inventory

Integrate with cloud providers (AWS, Azure, GCP) to fetch hosts dynamically.

📦 16. Ansible Galaxy

Public repository for roles.

ansible-galaxy install geerlingguy.nginx

🖥️ 17. Ansible Tower / AWX

Web UI & API for enterprise automation.

Provides RBAC, scheduling, and centralized logs.

🔄 18. Ansible Pull

Reverse of push model – nodes pull configuration from a central repo.

⚙️ 19. CI/CD Integration

Ansible is commonly used in:

Jenkins pipelines

GitLab CI/CD

GitHub Actions

For deployment, provisioning, and configuration.

💡 Common Interview Questions

What is Ansible and how is it different from Puppet or Chef?

What are Playbooks and Roles in Ansible?

How does Ansible ensure idempotency?

What are Handlers and when are they triggered?

What is Ansible Vault used for?

Explain Ansible’s inventory types.

How do you manage multiple environments (dev, staging, prod)?

How do you use Ansible in CI/CD pipelines?

How can you debug Ansible playbooks?

What’s the difference between command, shell, and script modules?
